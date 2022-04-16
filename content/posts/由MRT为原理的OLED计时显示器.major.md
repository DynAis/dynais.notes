---
title: 由MRT为原理的OLED计时显示器
tags:
  - 单片机
categories:
  - 项目
  - nxp-smart-car
thumbnailImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725003554.png
thumbnailImagePosition:
coverImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: 432b5708
date: 2019-12-08 00:00:00
---



## 遇到的问题

1. #### OLED无法点亮

   困扰了很久的问题，最后发现是硬件上出了毛病，使用飞线或者杜邦线会导致连接不稳定

   

2. #### OLED屏幕显示闪烁

   可能是因为屏幕刷新不够快，尝试保持一个高刷新率即可

   

3. #### OLED屏幕数字重叠

   使用uint16时调用现有函数显示数字会有5位的空位（0占位）在设定的坐标之前，注意防止显示内容重叠

   

4. #### 中断计时时间不准确（很慢）

   原因是在中断中加入了函数

   ```
   mrt_clean(MRT_CH0);
   ```

   本来是我认为防止数据溢出而使用的，最后发现会使每次中断的速度大大降低，导致计时不准确，并且去掉这个函数数据好像也不会溢出...
   
   <!-- more -->

---------------------------



### 工程目标

1. 了解MRT的使用方法
2. 了解OLED的工作协议和引脚定义
3. 了解IIC的工作原理
4. 结合MET和OLED制作计时器
5. 使用按钮控制调节计时器的几个工作状态



### 问题解决思路

查阅底层函数了解使用方法，结合OLED的数据手册了解OLED的使用方法，查阅IIC的时序，通过一步步调试减少错误，也便于即时修改。



### 待解决问题

1. 如何初始化，打开，调用和关闭MRT
2. IIC协议如何工作
3. 如何开启MRT的计时中断操作
4. OLED的数据引脚如何发送命令
5. 如何把MRT的反馈显示到OLED上
6. 如何通过按钮控制计时器状态



### 实行（可能）流程

1. 通过底层函数观察如何使用MRT
2. 通过网上资料或数据手册了解IIC如何工作
3. 通过底层函数观察如何使用OLED
4. 通过简单的程序让OLED显示字符
5. 编写计时函数
6. 编写按钮函数
7. 封装程序



------



### Lösungen

1. **如何操作MRT**

   ```c++
   /*********************************************************************************************************************
    * COPYRIGHT NOTICE
    * Copyright (c) 2018,逐飞科技
    * All rights reserved.
    * 技术讨论QQ群：179029047
    *
    * 以下所有内容版权均属逐飞科技所有，未经允许不得用于商业用途，
    * 欢迎各位使用并传播本程序，修改内容时必须保留逐飞科技的版权声明。
    *
    * @file       		MRT(多速率定时器)
    * @company	   		成都逐飞科技有限公司
    * @author     		逐飞科技(QQ3184284598)
    * @version    		查看LPC546XX_config.h文件内版本宏定义
    * @Software 		IAR 7.8 or MDK 5.24a
    * @Target core		LPC54606J512BD100
    * @Taobao   		https://seekfree.taobao.com/
    * @date       		2018-11-21
    ********************************************************************************************************************/
   
   
   #include "LPC546XX_mrt.h"
   
   
   //-------------------------------------------------------------------------------------------------------------------
   //  @brief      MRT周期中断模式初始化
   //  @param      mrtchx      MRT通道号
   //  @param      time        周期中断时间
   //  @return     void
   //  Sample usage:           mrt_pit_init(MRT_CH0,1000);         //无需用户调用 请使用H文件内的宏定义
   //-------------------------------------------------------------------------------------------------------------------
   void mrt_pit_init(MRTNUM_enum mrtchx, uint32 time)
   {
       SYSCON->AHBCLKCTRLSET[1] = SYSCON_AHBCLKCTRL_MRT_MASK;      //打开MRT时钟
       SYSCON->PRESETCTRLCLR[1] = SYSCON_PRESETCTRL_MRT_RST_MASK;  //清除MRT复位时钟
       
       ASSERT(time <= MRT_CHANNEL_TIMER_VALUE_MASK);//断言
       
       MRT0->CHANNEL[mrtchx].CTRL = MRT_CHANNEL_CTRL_INTEN_MASK | MRT_CHANNEL_CTRL_MODE(0);//PIT模式 打开中断
       MRT0->CHANNEL[mrtchx].INTVAL = time;        //设置间隔时间 定时器停止后载入时间 并启动定时器
       enable_irq(MRT0_IRQn);     				    //开启RIT中断
       //set_irq_priority(MRT0_IRQn,0);//设置优先级 越低优先级越高
   }
   
   
   
   //-------------------------------------------------------------------------------------------------------------------
   //  @brief      MRT延时函数
   //  @param      mrtchx      MRT通道号
   //  @param      time        周期中断时间
   //  @return     void
   //  Sample usage:           mrt_delay(MRT_CH0,1000);            //无需用户调用 请使用H文件内的宏定义
   //-------------------------------------------------------------------------------------------------------------------
   void mrt_delay(MRTNUM_enum mrtchx, uint32 time)
   {
       SYSCON->AHBCLKCTRLSET[1] = SYSCON_AHBCLKCTRL_MRT_MASK;      //打开MRT时钟
       SYSCON->PRESETCTRLCLR[1] = SYSCON_PRESETCTRL_MRT_RST_MASK;  //清除MRT复位时钟
       
       ASSERT(time <= MRT_CHANNEL_TIMER_VALUE_MASK);//断言
   
       MRT0->CHANNEL[mrtchx].CTRL = MRT_CHANNEL_CTRL_MODE(1);      //一次中断模式模式
   
       MRT0->CHANNEL[mrtchx].INTVAL = time | MRT_CHANNEL_INTVAL_LOAD_MASK;        //设置间隔时间 立即载入时间 并启动定时器
       while(!MRT_FLAG_READ(mrtchx));              //等待时间到
       MRT_FLAG_CLR(mrtchx);                       //清除标志位
   }
   
   
   
   //-------------------------------------------------------------------------------------------------------------------
   //  @brief      MRT开始计时
   //  @param      mrtchx      MRT通道号
   //  @param      time        周期中断时间
   //  @return     void
   //  Sample usage:           mrt_start(MRT_CH0);            
   //-------------------------------------------------------------------------------------------------------------------
   void mrt_start(MRTNUM_enum mrtchx)
   {
       SYSCON->AHBCLKCTRLSET[1] = SYSCON_AHBCLKCTRL_MRT_MASK;      //打开MRT时钟
       SYSCON->PRESETCTRLCLR[1] = SYSCON_PRESETCTRL_MRT_RST_MASK;  //清除MRT复位时钟
       
       MRT0->CHANNEL[mrtchx].CTRL = MRT_CHANNEL_CTRL_MODE(1);      //一次中断模式模式
       MRT0->CHANNEL[mrtchx].INTVAL = MRT_CHANNEL_INTVAL_IVALUE_MASK | MRT_CHANNEL_INTVAL_LOAD_MASK;//设置间隔时间 立即载入时间 并启动定时器
   }
   
   //-------------------------------------------------------------------------------------------------------------------
   //  @brief      MRT获取计时时间
   //  @param      mrtchx      MRT通道号
   //  @return     void
   //  Sample usage:           uint32 time = mrt_get(MRT_CH0);     //无需用户调用 请使用H文件内的宏定义
   //-------------------------------------------------------------------------------------------------------------------
   uint32 mrt_get(MRTNUM_enum mrtchx)
   {
       return (MRT_CHANNEL_INTVAL_IVALUE_MASK - MRT0->CHANNEL[mrtchx].TIMER); //如果返回的是0，则计时已经超出
   }
   
   
   //-------------------------------------------------------------------------------------------------------------------
   //  @brief      MRT计时清除
   //  @param      mrtchx      MRT通道号
   //  @return     void
   //  Sample usage:           清除计时并重新启动
   //-------------------------------------------------------------------------------------------------------------------
   void mrt_clean(MRTNUM_enum mrtchx)
   {
       MRT0->CHANNEL[mrtchx].INTVAL = MRT_CHANNEL_INTVAL_IVALUE_MASK | MRT_CHANNEL_INTVAL_LOAD_MASK;//设置间隔时间 立即载入时间 并启动定时器
   }
   
   
   
   
   
   
   ```

   

2. **如何设置延时？**

   ```c++
   //-------------------------------------------------------------------------------------------------------------------
   //  @brief      毫秒级systick延时函数
   //  @param      ms              延时多少毫秒
   //  @return     void
   //  Sample usage:               systick_delay_ms(1000);   //延时1000毫秒
   //-------------------------------------------------------------------------------------------------------------------
   void systick_delay_ms(uint32 ms)
   {
       //get_clk();//获取内核时钟便于后面设置
   	while(ms--) systick_delay(main_clk_mhz*1000);
   }
   
   ```

