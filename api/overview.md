# 算法一览
| 算法名称               | 算法类型   | 路由                              | 备注                         |
|-----------------------|------------|----------------------------------|------------------------------|
| 通用人脸检测           | 检测       | /image/general/human/face/det    |                              |
| 通用人体检测           | 检测       | /image/general/human/person/det  |                              |
| 轻量级通用人体关键点   | 关键点     | /image/general/human/person/pose |                              |
| 通用人体行为-玩手机   | 检测       | /image/general/human/person/hold_phone |                          |

## 备注
路由是一个比较重要的概念，它是用来区分不同算法的

比如`/image/general/human/face/det`，这个路由就是用来区分通用人脸检测算法的，它的意思是`/image`是图片算法，`/general`是通用算法，`/human`是人体算法，`/face`是人脸算法，`/det`是检测算法。

同时在api请求中你也会用到它们，具体请参见下一小节(开发说明)[api/developDesc.md]

# 介绍
## 通用模型
### [人脸检测](api/general/human/face/det)
这里是一点介绍
- 特性
- 2
- 3
### [人体检测](api/general/human/person/det)
### [轻量人体关键点](api/general/human/person/pose)
### 行为检测
### [玩手机](api/general/human/person/hold_phone)
