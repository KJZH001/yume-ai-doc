# API统一格式
> 这里讲的是大部分服务的接口格式，不包括一些特殊的接口，比如登录接口和GPT接口，这些接口的格式会在各自的文档中说明。

## 基准路由
```https://ai.moeworld.tech/api/service/```

您在`概述`页面中看到的路由都是用于此基准路由之上的，例如`通用人脸检测`的子路由为`/image/general/human/face/det`

那么您的请求地址就应该是这样的：`https://ai.moeworld.tech/api/service/image/general/human/face/det`

## 请求方式
所有的接口都是使用`POST`请求，请求的`Content-Type`为`application/form`

## 请求参数
对于这些视觉图像分析的接口而言，请求的参数都是一样的

总共有两个参数，分别是`apikey`和`image`，其中`apikey`是您的API密钥，`image`是您要分析的图片

ApiKey您可以在控制台的仪表盘中找到它，注意不要将它泄露给任何人，包括站点管理员，因为管理员不会向您索要您的个人API密钥