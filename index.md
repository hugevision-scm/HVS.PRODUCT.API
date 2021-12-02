
# 使用准备

## 获取API的systemKey&uniqueCode

请API管理角色登录HVS，维护协同平台配置。

# 用语

|用语|说明|
|:--|:--|
|功能类型|API的功能类型分为3个<br>&nbsp; &nbsp; 1:创建业务数据<br>&nbsp; &nbsp; &nbsp; &nbsp; 创建业务单据并单据操作完成<br>&nbsp; &nbsp; 2:查询异步处理结果<br>&nbsp; &nbsp; &nbsp; &nbsp; 查询创建业务数据的处理结果，一般用于异步处理<br>&nbsp; &nbsp; 3:查询业务数据<br>&nbsp; &nbsp; &nbsp; &nbsp; 查询待处理业务数据并更新状态|
|处理类型|API的处理类型分为2个<br>&nbsp; &nbsp; F:同步<br>&nbsp; &nbsp; &nbsp; &nbsp; API调用后，HVS处理完成后返回结果。所有API提供同步处理。<br>&nbsp; &nbsp; B:异步<br>&nbsp; &nbsp; &nbsp; &nbsp; API调用后马上返回"异步处理提交成功"的消息。30分钟内自动处理，处理完成后可以查询结果。仅创建业务数据API提供异步处理。|

# API共通

## Request

先获取token，然后调用业务API
  
###  Request Header

调用业务API时要设定token

|KEY|Value|
|:--|:--|
|Authorization| Bearer *{Tokens}*|

*{Tokens}*是Tokens API的返回值

###  Request Body

业务API的Request Body的共通字段

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID。重复也不报错。|
|requestTime|timestamp|19|✓|请求时间|

**大小写请正确输入！**

## Response

HVS服务器停止时，无返回Response

### Response Body

* 异常情况时返回如下JSON数据，此时HVS未接收请求

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|servlet|string|255|✓|错误代码|
|message|string|255|✓|错误消息|
|url|string|255|✓|调用时指定的URL|
|status|integer|3|✓|错误编码|


Request Headers输入的Token失效时返回如下JSON数据

```
{
    "servlet": "com.trekglobal.idempiere.rest.api.v1.ApplicationV1",
    "message": "Unauthorized",
    "url": "{调用时指定的URL}",
    "status": "401"
}
```

Request Body的JSON解析失败时返回如下JSON数据
```
{
    "servlet": "com.trekglobal.idempiere.rest.api.v1.ApplicationV1",
    "message": "Request failed.",
    "url": "{调用时指定的URL}",
    "status": "500"
}
```