# API170COF
---

## API概述

创建 **库存调整单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|同步|

**系统异常结后，还得调用API170NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importintenaluseinventory_co_f**
  
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
|&nbsp; &nbsp; org_Text|string|60|✓|组织的编码/名称/编码_名称|
|&nbsp; &nbsp; doctype_Name|string|60|✓|固定为库存调整|
|&nbsp; &nbsp; movementDate|date|10|✓|调整日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; dateAcct|date|10||记账日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; warehouse_Text|string|60|✓|仓库的编码/名称/编码_名称|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Text|string|60|✓|库位的编码/名称/编码_名称|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Text|string|255|✓|产品的编码/名称/编码_名称|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||单据行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; lot|string|40||批号。保质期管理产品时必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10||生产日期。保质期管理产品时必填。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; &nbsp; &nbsp; invStatus_Text|string|60|✓|库存状态的名称<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; adjustQuantity|bigdecimal|16,6|✓|调整数量。允许正负数量。不允许为0|

JSON格式样例
```
{
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestTime": "2021-11-15 12:00:00",
    "docList": [
        {
            "docNo": "INV2021110001",
            "org_Text": "HugeVision-SCM Demo",
            "doctype_Name": "库存调整",
            "movementDate": "2021-11-15",
            "dateAcct": "2021-11-15",
            "warehouse_Text": "D01仓库A",
            "description": "库存调整附注",
            "lineList": [
                {
                    "lineId": "1",
                    "locator_Text": "0001_D01仓库A正品库位",
                    "product_Text": "SD01B02_D01食品酒饮02",
                    "lineDescription": "L01明细附注",
                    "lot": "L202111",
                    "dateProduction": "2021-11-01",
                    "invStatus_Text": "正常",
                    "adjustQuantity": "1000"
                },
                {
                    "lineId": "2",
                    "locator_Text": "0001_D01仓库A正品库位",
                    "product_Text": "BD01A01_D01零部件001",
                    "lineDescription": "L02明细附注",
                    "invStatus_Text": "正常",
                    "adjustQuantity": "200"
                }
            ]
        }
    ]
}
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
|&nbsp; &nbsp; docStatus|string|2||单据状态。单据处理结果为**成功**时设定。<br>&nbsp; DR:草稿<br>&nbsp; AP:待批<br>&nbsp; IP:开放<br>&nbsp; CO:完成|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20|✓|外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; lineResult|string|1|✓|单据行处理结果<br>&nbsp; 1:成功<br>&nbsp; 9:失败|
|&nbsp; &nbsp; &nbsp; &nbsp; lineErrorMsg|string|2000||单据行报错消息。单据行处理结果为**失败**时设定。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineNoHVS|string|10||HVS的单据行号。单据处理结果为**成功**时设定。|
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
            "docNo": "INV2021110001",
            "docResult": "1",                                                          /*1: 成功*/
            "docErrorMsg": "",
            "docNoHVS": "2111SA0008",
            "docStatus": "AP",
            "lineList": [
                {
                    "lineId": "1",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": "10"
                },
                {
                    "lineId": "2",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": "20"
                }
            ]
        }
    ],
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-24 11:59:10",
    "errorMsg": "处理成功",
    "targetRequestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "targetRequestStatus": "1",                                                        /*1: 已处理*/
    "targetRequestResult": "1",                                                        /*1: 成功*/
    "targetRequestErrorMsg ": "处理成功"
}
```

JSON格式样例(导入失败)
```
{
    "docList": [
        {
            "docNo": "INV2021110002",
            "docResult": "9",                                                          /*9: 失败*/
            "docErrorMsg": "上传组织不存在或没有访问权限,单据类型不存在或没有访问权限,产品不存在或没有访问权限,库存状态不存在或没有访问权限,必须填写下列字段的内容：调整数量,",
            "docNoHVS": "",
            "docStatus": "",
            "lineList": [
                {
                    "lineId": "1",
                    "lineResult": "9",                                                 /*9: 失败*/
                    "lineErrorMsg": "必须填写下列字段的内容：调整数量,库存状态不存在或没有访问权限,产品不存在或没有访问权限,",
                    "lineNoHVS": ""
                },
                {
                    "lineId": "2",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": ""
                }
            ]
        },
        {
            "docNo": "INV2021110003",
            "docResult": "1",                                                          /*1: 成功*/
            "docErrorMsg": "",
            "docNoHVS": "",
            "docStatus": "",
            "lineList": [
                {
                    "lineId": "3",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": ""
                }
            ]
        },
        {
            "docNo": "INV2021110004",
            "docResult": "9",                                                          /*9: 失败*/
            "docErrorMsg": "产品不存在或没有访问权限,库存状态不存在或没有访问权限,库位不存在或没有访问权限,必须填写下列字段的内容：调整数量,",
            "docNoHVS": "",
            "docStatus": "",
            "lineList": [
                {
                    "lineId": "4",
                    "lineResult": "9",                                                 /*9: 失败*/
                    "lineErrorMsg": "必须填写下列字段的内容：调整数量,库存状态不存在或没有访问权限,产品不存在或没有访问权限,库位不存在或没有访问权限,库位不存在或没有访问权限,",
                    "lineNoHVS": ""
                },
                {
                    "lineId": "5",
                    "lineResult": "1",                                                 /*1: 成功*/
                    "lineErrorMsg": "",
                    "lineNoHVS": ""
                }
            ]
        }
    ],
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-24 14:17:49",
    "errorMsg": "处理失败(请求数据数据错误导入失败)",
    "targetRequestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "targetRequestStatus": "1",                                                        /*1: 已处理*/
    "targetRequestResult": "7",                                                        /*7: 失败(数据错误)*/
    "targetRequestErrorMsg ": "处理失败(请求数据数据错误导入失败)"
}
```
JSON格式样例(单据操作失败)
```
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
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "6",
    "responseTime": "2021-11-24 11:57:16",
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
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "1",
    "responseTime": "2021-11-24 14:08:05",
    "errorMsg": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-15\"",
    "targetRequestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "targetRequestStatus": "1",
    "targetRequestResult": "6",
    "targetRequestErrorMsg ": "处理失败(请求数据格式错误解析失败) - Parse Error;Unparseable date: \"202X-11-15\""
}
```
