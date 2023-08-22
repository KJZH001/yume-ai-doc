# 大语言模型聚合接口
这个接口允许你通过修改不同的参数，来实现调用我们所有支持的模型

和我们的私有的`MoeChat`协议接口不同，这个接口保持了和`Openai`官方接口的一致性

你可以在[这里](https://beta.openai.com/docs/api-reference/completions/create)查看官方的接口定义

或者，你也可以在[这里](https://openai.apifox.cn/api-67883981)查看国内镜像版本的**中文**文档

## 接口地址
```url
https://api.moeworld.top/api/openai/index.php?web=true&
```
这是完整的接口地址，你可以直接使用它

同时，你可能也已经在`在线面板`的使用文档中看到了这个地址，没错，它们是一样的

## 接口参数
因为使用方法和官方的接口一致，所以这里不再赘述

如果需要，你可以去查阅官方的文档，或者你只是想快速调用的话，也可去`大语言模型/概述`一节去查看我们对于使用方法的大致说明

这里我们只讲一些需要注意的地方，以及不同之处

### 基本地址
```url
https://api.moeworld.top/api/openai/index.php
```
这一部分是最基本的地址，你可以直接使用它，也可以在后面加上参数

但是请注意，不要去掉index.php，否则将会容易导致出现一些意外的问题

### 可选参数
```url
?web=true&
```
正如你所见的，它是一个GET参数，你可以在后面加上它，也可以不加

如果你不加，那么你将会得到一个JSON格式的回复，这个回复将会是一个标准的Openai接口回复

如果添加了web=true，那么你会得到一个仅包含文本的回复，这个回复将会是一个纯文本

对应的是Openai接口回复中的`choices`字段的`message`字段的`content`字段的值

也就是GPT或者其他的模型返回给用户可被理解的文本

这么说可能有点抽象，下面我们来看一下具体的例子

```json
{
    "id": "chatcmpl-7oqoflxUbLGTN6rWApmbCMjPX9Hzj",
    "object": "chat.completion",
    "created": 1692353781,
    "model": "gpt-35-turbo",
    "choices": [
        {
            "index": 0,
            "finish_reason": "stop",
            "message": {
                "role": "assistant",
                "content": "你好啊！有需要我帮忙的吗？"
            }
        }
    ],
    "usage": {
        "completion_tokens": 16,
        "prompt_tokens": 11,
        "total_tokens": 27
    }
}
```
以这段标准的Openai接口回复的json为例

如果提交的get参数中，web=true，那么你将会得到这样的回复

```text
你好啊！有需要我帮忙的吗？
```

是的，只有这一句话，这就是我们所说的纯文本回复，也就是返回给用户可被理解的文本

#### 这个参数的其他部分有什么用呢？
`?`的作用不必多说，是为了让服务器知道从这里开始就是参数了

`&`的作用是让调用接口的一方可以随意往url后面添加路径，而不必担心会出现问题

毕竟有些程序你无法控制它会往url后面添加什么参数

举个例子，实际调用的时候可能你的路径会变成这样

```url
https://api.moeworld.top/api/openai/index.php?web=true&/v1/chat/completions
```
