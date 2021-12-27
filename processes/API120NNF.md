# API120NNF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API120NNF

---

## API概述

查询 **付款单** 的异步处理结果 。

|功能类型|处理类型|
|:--|:--|
|查询异步处理结果|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**inquiryappayment_co**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|targetRequestId|string|36|✓|查询对象请求ID|

JSON格式样例
```
{
    "requestId": "API120NN-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:30:00",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 处理成功时返回如下JSON数据（与API120COF的Response一样格式）

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; docResult|string|1|✓|单据处理结果<br>&nbsp; 1:成功<br>&nbsp; 9:失败|
|&nbsp; &nbsp; docErrorMsg|string|2000||单据级别的报错消息。单据处理结果为**失败**时设定。|
|&nbsp; &nbsp; docNoHVS|string|20||HVS的单据号。单据处理结果为**成功**时设定。|
|&nbsp; &nbsp; docStatus|string|2||单据状态。单据处理结果为**成功**时设定。<br>&nbsp; AP:待批<br>&nbsp; CO:完成|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功<br>&nbsp; 9:失败(系统异常)|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理成功<br>&nbsp; 处理失败(请求数据数据错误导入失败)<br>&nbsp; 系统异常(请服务提供商联系)|
|targetRequestId|string|36|✓|目标请求ID，与RequestID一致|
|targetRequestStatus|string|1|✓|目标请求处理状态<br>&nbsp; 1:已处理|
|targetRequestResult|string|1|✓|目标请求处理结果<br>&nbsp; 1:成功<br>&nbsp; 7: 失败(数据错误)<br>&nbsp; 9: 失败(系统异常)|
|targetRequestErrorMsg|string|255|✓|目标请求处理消息<br>&nbsp; 处理成功<br>&nbsp; 处理失败(请求数据数据错误导入失败)<br>&nbsp; 系统异常(请服务提供商联系)|

JSON格式样例(导入成功)
```
{
    "docList": [
        {
            "docNo": "PAY2021110001",
            "docResult": "1",
            "docErrorMsg": "",
            "docNoHVS": "2111PAY0001",
            "docStatus": "AP"
        }
    ],
    "requestId": "API120NN-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:30:00",
    "errorMsg": "处理成功",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "1",
    "targetRequestResult": "1",
    "targetRequestErrorMsg ": "处理成功"
}
```

JSON格式样例(导入失败)
```
{
    "docList": [
        {
            "docNo": "PAY2021110001",
            "docResult": "9",                                                          /*9: 失败*/
            "docErrorMsg": "上传组织不存在或没有访问权限,单据类型不存在或没有访问权限,产品不存在或没有访问权限,必须填写下列字段的内容：数量,",
            "docNoHVS": "",
            "docStatus": ""
        },
        {
            "docNo": "PAY2021110002",
            "docResult": "1",                                                          /*1: 成功*/
            "docErrorMsg": "",
            "docNoHVS": "",
            "docStatus": ""
        },
        {
            "docNo": "PAY021110003",
            "docResult": "9",                                                          /*9: 失败*/
            "docErrorMsg": "产品不存在或没有访问权限,库位不存在或没有访问权限,必须填写下列字段的内容：数量,",
            "docNoHVS": "",
            "docStatus": ""
        }
    ],
    "requestId": "API120NN-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:30:00",
    "errorMsg": "处理失败(请求数据数据错误导入失败)",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "1",                                                        /*1: 已处理*/
    "targetRequestResult": "7",                                                        /*7: 失败(数据错误)*/
    "targetRequestErrorMsg ": "处理失败(请求数据数据错误导入失败)"
}
```
JSON格式样例(单据操作失败)
```
```

* 对象请求还没处理完成时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 该请求还在处理中|
|targetRequestId|string|36|✓|目标请求ID，与RequestID一致|
|targetRequestStatus|string|1|✓|目标请求处理状态<br>&nbsp; 0:未处理|
|targetRequestResult|string|1|✓|目标请求处理结果<br>&nbsp; 0: 未处理|
|targetRequestErrorMsg|string|255|✓|目标请求处理消息<br>&nbsp; 该请求还在处理中|

JSON格式样例
```
{
    "requestId": "API120NN-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:30:00",
    "errorMsg": "该请求还在处理中",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "0",
    "targetRequestResult": "0",
    "targetRequestErrorMsg ": "该请求还在处理中"
}
```

* Request Body的JSON格式错误时返回如下JSON数据（与API120COF的Response一样格式）

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理失败(请求数据格式错误解析失败) - {解析错误消息}|
|targetRequestId|string|36|✓|目标请求ID，与RequestID一致|
|targetRequestStatus|string|1|✓|目标请求处理状态<br>&nbsp; 1:已处理|
|targetRequestResult|string|1|✓|目标请求处理结果<br>&nbsp; 6: 失败(格式错误)|
|targetRequestErrorMsg|string|255|✓|目标请求处理消息<br>&nbsp; 处理失败(请求数据格式错误解析失败) - {解析错误消息}|

JSON格式样例
```
{
    "requestId": "API120NN-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:30:00",
    "errorMsg": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-30\"",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "1",
    "targetRequestResult": "6",
    "targetRequestErrorMsg ": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-30\""
}
```
