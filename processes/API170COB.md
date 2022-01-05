# API170COB

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API170COB

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
|&nbsp; &nbsp; org_Text|string|60|✓|组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60|-|<br>可填写如下单据类型<br>&nbsp; 库存调整<br>&nbsp; 库存调整(代理商)<br>&nbsp; 库存调整(供应商)。<br>不填写时根据组织取得。|
|&nbsp; &nbsp; movementDate|date|10|-|调整日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; dateAcct|date|10||记账日期。格式为yyyy-MM-dd。不填写时取得调整日期。|
|&nbsp; &nbsp; warehouse_Text|string|60|✓|仓库的编码/名称/编码_名称|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Text|string|60|✓|库位的编码/名称/编码_名称|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Text|string|60|✓|产品的编码/名称/编码_名称|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||单据行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; lot|string|40||批号。保质期管理产品时必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10||生产日期。保质期管理产品时必填。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; &nbsp; &nbsp; invStatus_Text|string|60|✓|库存状态的名称<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; adjustQuantity|bigdecimal|16,6|✓|调整数量。允许正负数量。不允许为0|

JSON格式样例
```
{
    "requestId": "API0170CO-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:00:00",
    "docList": [
        {
            "docNo": "INV2021110001",
            "org_Text": "HugeVision-SCM Demo",
            "doctype_Name": "库存调整",
            "movementDate": "2021-11-30",
            "dateAcct": "2021-11-30",
            "warehouse_Text": "D01B2C仓库",
            "description": "库存调整附注",
            "lineList": [
                {
                    "lineId": "1",
                    "locator_Text": "0001_D01B2C仓库常规库位",
                    "product_Text": "SD01B02_D01食品酒饮02",
                    "lineDescription": "L01明细附注",
                    "lot": "L202111",
                    "dateProduction": "2021-11-01",
                    "invStatus_Text": "正常",
                    "adjustQuantity": "1000"
                },
                {
                    "lineId": "2",
                    "locator_Text": "0001_D01B2C仓库常规库位",
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

创建业务数据异步处理的响应格式

&nbsp;&nbsp;&nbsp;&nbsp;→&nbsp;[响应格式&样例](Response_Body_01.md)
