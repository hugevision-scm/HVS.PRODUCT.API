# API210COF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API210COF

---

## API概述

创建 **Sellout** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|同步|

**系统异常结后，还得调用API210NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importdealerselloutorder_co_f**
  
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
|&nbsp; &nbsp; doctype_Name|string|60||单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 销售订单-Sellout|
|&nbsp; &nbsp; dateOrdered|date|10||订单日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; bpartner_Value|string|40|条件|业务伙伴的编码。编码或名称为必填。|
|&nbsp; &nbsp; bpartner_Name|string|60|条件|业务伙伴的名称。编码或名称为必填。|
|&nbsp; &nbsp; priceList_Text|string|60||价格表的名称。不填写时取得业务伙伴的价格表。|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Value|string|40|条件|产品的编码。编码或名称为必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Name|string|60|条件|产品的名称。编码或名称为必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; qty|bigdecimal|16,6|✓|数量。允许正负数。不允许为0。|
|&nbsp; &nbsp; &nbsp; &nbsp; price|bigdecimal|16,6||单价。必须大于等于0。不填写时取得价格表维护的价格。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||单据行的附注|

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
|&nbsp; &nbsp; taxExcludedAmtTotal|bigdecimal|16,2||HVS的不含税总额(原币)|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20|✓|外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; lineResult|string|1|✓|单据行处理结果<br>&nbsp; 1:成功<br>&nbsp; 9:失败|
|&nbsp; &nbsp; &nbsp; &nbsp; lineErrorMsg|string|2000||单据行报错消息。单据行处理结果为**失败**时设定。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineNoHVS|string|10||HVS的单据行号。单据处理结果为**成功**时设定。|
|&nbsp; &nbsp; &nbsp; &nbsp; priceActual|bigdecimal|16,2||HVS的单价(原币)|
|&nbsp; &nbsp; &nbsp; &nbsp; taxExcludedAmt|bigdecimal|16,2||HVS的不含税金额(原币)|
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
            "docNo": "SOC2021110001",
            "docResult": "1",                                                          /*1: 成功*/
            "docErrorMsg": "",
            "docNoHVS": "2111SOC0001",
            "docStatus": "AP",
            "taxExcludedAmtTotal": "2000",
            "lineList": [
                {
                    "lineId": "1",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": "10",
                    "priceActual": "10",
                    "taxExcludedAmt": "1000"
                },
                {
                    "lineId": "2",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": "20",
                    "priceActual": "10",
                    "taxExcludedAmt": "1000"
                }
            ]
        }
    ],
    "requestId": "API210CO-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "处理成功",
    "targetRequestId": "API210CO-0000-0000-0000-000000000001",
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
    "requestId": "API210CO-0000-0000-0000-000000000001",
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
    "requestId": "API210CO-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-30\"",
    "targetRequestId": "API210CO-0000-0000-0000-000000000001",
    "targetRequestStatus": "1",
    "targetRequestResult": "6",
    "targetRequestErrorMsg ": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-30\""
}
```
