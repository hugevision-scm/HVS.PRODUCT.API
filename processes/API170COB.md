# API170COB
---

## API概述

创建 **库存调整单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|异步|

**此API调用后，还得调用API170NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importintenaluseinventory_co_b**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式，与API170COF相同

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
|&nbsp; &nbsp; &nbsp; &nbsp; descriptionLine|string|255||单据行的附注|
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
                    "descriptionLine": "L01明细附注",
                    "lot": "L202111",
                    "dateProduction": "2021-11-01",
                    "invStatus_Text": "正常",
                    "adjustQuantity": "1000"
                },
                {
                    "lineId": "2",
                    "locator_Text": "0001_D01仓库A正品库位",
                    "product_Text": "BD01A01_D01零部件001",
                    "descriptionLine": "L02明细附注",
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
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 异步处理提交成功|

JSON格式样例(导入成功)
```
{
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "1",
    "responseTime": "2021-11-24 15:38:12",
    "errorMsg": "异步处理提交成功"
}
```