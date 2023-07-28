# API统一格式
> 这里讲的是大部分服务的接口格式，不包括一些特殊的接口，比如登录接口和GPT接口，这些接口的格式会在各自的文档中说明。

## 基准路由
```https://ai.moeworld.tech/api/service/```

您在`概述`页面中看到的路由都是用于此基准路由之上的，例如`通用人脸检测`的子路由为`/image/general/human/face/det`

那么您的请求地址就应该是这样的：`https://ai.moeworld.tech/api/service/image/general/human/face/det`

## 请求方式
所有的接口都是使用`POST`请求，请求的`Content-Type`为`application/form`

## 请求参数
