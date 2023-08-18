# 大语言模型
这篇文档主要会介绍关于大语言模型的通用接口的一些基本用法


## 模型介绍
目前主要包含两大类型模型，分别为来自Openai的GPT和清华大学国产的ChatGLM

GPT当前主要支持ChatGPT(GPT-3.5)，使用自部署的聚合后端接口对接Azure Openai认知服务

ChatGLM使用的是ChatGLM6B的int4量化模式运行，效果目前不如ChatGPT，但是完全自行部署，具有更好的安全性和隐私性

## 接口定义
以ChatGPT为例，你可以在[这里](https://ai.moeworld.tech/chat/gpt)查看接口的大致定义和在线调试