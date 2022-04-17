---
title: "使用couqi-TTS从文字生成语音"
# author: 
tags:
  - TTS
date: '2022-04-17'
ShowToc: true
draft: false
---
描述了如何开箱即用的使用TTS框架进行文本转语音
<!--more-->

---

# 前置知识

- TTS(架构知识)
- Git

# 1 安装(使用Git)

对于需要后续进行模型训练的目的来说, 官方推荐使用Git的方式进行安装

进入项目地址https://github.com/coqui-ai/TTS找到Git链接后 `git clone` 到想要安装的文件夹

之后再使用 `pip` 进行安装(在TTS文件夹中, 路径下看见 `[setup.py](http://setup.py)` 就对了)

```bash
git clone https://github.com/coqui-ai/TTS
pip install -e .[all,dev,notebooks,tf]  # Select the relevant extras
```

安装会有点久

# 2 使用现有模型进行语音合成

首先可以键入

```bash
tts --list_models
```

进行现有模型的查看(包括TTS模型和Vocoder模型, 一般是成对的, 也需要成对使用, 也有的模型没有Vocoder, 那么它的效果可能会差一点, 但也能用)

然后输入以下的命令生成语音, `--model_name` 和`--vocoder_name` 就是上面列出的那些模型, 选择需要的填入就行了

```bash
tts --text "YOUR_TEXT" --model_name "MODEL_NAME" --vocoder_name "VOCODER_NAME"
```

如果当前使用的模型不存在, 会直接进行下载模型, 会持续相当长的一段时间, 且没有进度提示, 耐心.

结束后会生成 `.wav` 文件在当前的路径下, 语音最短似乎是六秒钟.

# 参考

1. [https://github.com/coqui-ai/TTS](https://github.com/coqui-ai/TTS)
2. [https://tts.readthedocs.io/en/latest/training_a_model.html](https://tts.readthedocs.io/en/latest/training_a_model.html)
3. [https://tts.readthedocs.io/en/latest/formatting_your_dataset.html#formatting-your-dataset](https://tts.readthedocs.io/en/latest/formatting_your_dataset.html#formatting-your-dataset)
4. [https://github.com/coqui-ai/TTS/wiki/What-makes-a-good-TTS-dataset](https://github.com/coqui-ai/TTS/wiki/What-makes-a-good-TTS-dataset)
5. [https://tts.readthedocs.io/en/latest/faq.html](https://tts.readthedocs.io/en/latest/faq.html)
6. [https://tts.readthedocs.io/en/latest/finetuning.html](https://tts.readthedocs.io/en/latest/finetuning.html)
7.