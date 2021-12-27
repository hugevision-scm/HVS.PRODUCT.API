# API120COF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API120COF

---

## API概述

创建 **付款单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|同步|

**系统异常结后，还得调用API120NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importappayment_co_f**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; org_Text|string|60||组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60||单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 付款单|
|&nbsp; &nbsp; isPrepayment|string|1||是否预付。只允许为Y。|
|&nbsp; &nbsp; bankTrnNo|string|60||银行流水号|
|&nbsp; &nbsp; dateAcct|date|10||记账日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; bpartner_Value|string|40|条件|业务伙伴的编码。编码或名称为必填。|
|&nbsp; &nbsp; bpartner_Name|string|60|条件|业务伙伴的名称。编码或名称为必填。|
|&nbsp; &nbsp; dateTrx|date|10||申请日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; datePlanPay|date|10||希望支付日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; dateActualPay|date|10||实际支付日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; bankAccount_Text|string|60|条件|银行账户的编码/名称。如果货币有多个银行账户时必填。|
|&nbsp; &nbsp; customerAccountNo|string|20||对方账户的账号。|
|&nbsp; &nbsp; customerBankName|string|60||对方银行的名称。|
|&nbsp; &nbsp; currency_Text|string|3|✓|货币的编码。<br>可填写货币在实体使用条件里维护。|
|&nbsp; &nbsp; settlementRate|bigdecimal|16,10||结算汇率。不填写时取得申请日期当天的汇率。|
|&nbsp; &nbsp; payAmt|bigdecimal|16,6|✓|支付金额(原币)。不允许为0。|
|&nbsp; &nbsp; description|string|255||单据的附注|

JSON格式样例
```
(待补充)
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 处理成功时返回如下JSON数据

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
            "docResult": "1",                                                          /*1: 成功*/
            "docErrorMsg": "",
            "docNoHVS": "2111PAY0001",
            "docStatus": "AP"
        }
    ],
    "requestId": "API120CO-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "处理成功",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "1",                                                        /*1: 已处理*/
    "targetRequestResult": "1",                                                        /*1: 成功*/
    "targetRequestErrorMsg ": "处理成功"
}
```

JSON格式样例(导入失败)
```
(待补充)
```
JSON格式样例(单据操作失败)
```
(待补充)
```
* Request Body的requestId重复时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 6:失败(格式错误)|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; RequestId重复|

JSON格式样例
```
{
    "requestId": "API120CO-0000-0000-0000-000000000001",
    "requestResult": "6",
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "RequestId重复"
}
```

* Request Body的JSON格式错误时返回如下JSON数据

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
    "requestId": "API120CO-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-30\"",
    "targetRequestId": "API120CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "1",
    "targetRequestResult": "6",
    "targetRequestErrorMsg ": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-30\""
}
```
