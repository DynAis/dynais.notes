---
title: "Colab自动挂机代码"
# author: 
tags:
  - Python
date: '2022-04-16'
ShowToc: true
draft: false
---

防Colab踢你下线😢

<!--more-->

---

## 代码

复制输入网页控制台

```jsx
function ClickConnect(){
console.log("Working"); 
document.querySelector("colab-toolbar-button#connect").click() 
}
setInterval(ClickConnect,60000)
```

## 参考

1. [https://www.cnblogs.com/clemente/p/12395195.html](https://www.cnblogs.com/clemente/p/12395195.html)