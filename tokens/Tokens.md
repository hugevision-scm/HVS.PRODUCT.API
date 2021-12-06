# Tokens
---

## API概述

此API是认证系统和用户，获取Token

以系统编号，API Key，平台用户进行认证，认证通过就返回Token

|功能类型|处理类型|
|:--|:--|
|其他|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/auth/**tokens**
 
###  Request Header

无特别描述

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|systemKey|string|40|✓|HVS协同平台配置的编码|
|uniqueCode|string|255|✓|HVS协同平台配置的识别码|
|userName|string|80|✓|HVS协同平台用户的平台用户名|

JSON格式样例
```
{
    "systemKey": "LogiSystem",
    "uniqueCode": "215295df-f978-4a43-bb89-d756dbac0330",
    "userName": "user01@LogiSystem"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 登录成功时返回如下JSON数据，可以获取token

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|token|string|518|✓|生成token结果|

JSON格式样例
```
{
    "token": "eyJraWQiOiJpZGVtcGllcmUiLCJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJSZXN0RnVsQWNjZXNzQEhWU0RlbW9TeXN0ZW0xIiwiQURfTGFuZ3VhZ2UiOiJ6aF9DTiIsIkFEX1JvbGVfSUQiOjgwMDA3MywiQURfVXNlcl9JRCI6ODAwMDU3LCJBRF9PcmdfSUQiOjEwMDAwMDEsImlzcyI6ImlkZW1waWVyZS5vcmciLCJBRF9DbGllbnRfSUQiOjEwMDAwMDMsImV4cCI6MTYzNzcyMzcxNX0.RInhiL0DqMFB4HTrEBqb27AeOgKg1LfLAxg7zhI1t_Mr3tmYUcU046Txdd-aSjZGbx9BHe8EitPmsxt00n6RFA"
}
```

* 登录失败功时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|title|string|<span>100</span>|✓|错误标题|
|status|integer|<span>3</span>|✓|错误编码|
|detail|string|<span>255</span>|✓|错误消息|

JSON格式样例
```
{
    "title": "Authenticate error",
    "status": 401,
    "detail": "Invalid User ID or Password"
}
```
