# API230DLF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API230DLF

---

## API概述

查询 **库存明细** 。

|功能类型|处理类型|
|:--|:--|
|查询业务数据|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**querystock**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|rpt010_GroupLevel|string|2|✓|查询对象汇总级别。<br>可填写汇总级别如下。<br>&nbsp; 10:按产品汇总<br>&nbsp; 20:按批次汇总|
|org_Value|string|40|✓|查询对象组织的编码|
|warehouse_Value|string|40||查询对象仓库的编码|
|warehouse_Name|string|60||查询对象仓库的名称|
|locator_Value|string|40||查询对象库位的编码|
|locator_Name|string|60||查询对象库位的名称|
|productCategoryL1_Value|string|40||查询对象产品类别(第一级)的编码|
|productCategoryL1_Name|string|60||查询对象产品类别(第一级)的名称|
|productCategory_Value|string|40||查询对象产品类别的编码|
|productCategory_Name|string|60||查询对象产品类别的名称|
|product_Value|string|40||查询对象产品的编码|
|product_Name|string|60||查询对象产品的名称|
|lot|string|40||查询对象批号|
|dateProduction|date|10||查询对象生产日期From|
|dateProductionTo|date|10||查询对象生产日期To|
|guaranteeDate|date|10||查询对象保质期From|
|guaranteeDateTo|date|10||查询对象保质期To|
|validityStatus_Name|string|60||查询对象效期状态的名称。<br>可填写的效期状态如下。<br>&nbsp; 良好<br>&nbsp; 1/3效期<br>&nbsp; 1/2效期<br>&nbsp; 2/3效期<br>&nbsp; 过期|
|invStatus_Name|string|60||查询对象库存状态的名称。<br>可填写的库存状态如下。<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|

JSON格式样例
```
{
    "requestId": "API230DL-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:30:00",
    "rpt010_GroupLevel": "20",
    "org_Value": D01",
    "warehouse_Value": "00",
    "warehouse_Name": "D01B2C仓库",
    "locator_Value": "0001",
    "locator_Name": "D01B2C仓库常规库位",
    "productCategoryL1_Value": "40",
    "productCategoryL1_Name": "食品酒饮",
    "productCategory_Value": "400101",
    "productCategory_Name": "食品酒饮0101",
    "product_Value": "SD01B01",
    "product_Name": "D01食品酒饮01",
    "lot": "202101",
    "dateProduction": "2021-01-01",
    "dateProductionTo": "2021-12-31",
    "guaranteeDate": "2021-01-01",
    "guaranteeDateTo": "2021-12-31",
    "validityStatus_Name": "良好",
    "invStatus_Name": "正常"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 有数据时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|stockList|list||✓|库存列表|
|&nbsp; &nbsp; groupLevel|string|2|✓|汇总级别。<br>检索条件的汇总级别。<br>&nbsp; 10:按产品汇总<br>&nbsp; 20:按批次汇总|
|&nbsp; &nbsp; org_Value|string|40|✓|组织的编码|
|&nbsp; &nbsp; org_Name|string|60|✓|组织的名称|
|&nbsp; &nbsp; warehouse_Value|string|40|✓|仓库的编码|
|&nbsp; &nbsp; warehouse_Name|string|60|✓|仓库的名称|
|&nbsp; &nbsp; locator_Value|string|40|✓|库位的编码|
|&nbsp; &nbsp; locator_Name|string|60|✓|库位的名称|
|&nbsp; &nbsp; productCategoryL1_Value|string|40|✓|产品类别(第一级)的编码|
|&nbsp; &nbsp; productCategoryL1_Name|string|60|✓|产品类别(第一级)的名称|
|&nbsp; &nbsp; productCategory_Value|string|40|✓|产品类别的编码|
|&nbsp; &nbsp; productCategory_Name|string|60|✓|产品类别的名称|
|&nbsp; &nbsp; product_Value|string|40|✓|产品的编码|
|&nbsp; &nbsp; product_Name|string|60|✓|产品的名称|
|&nbsp; &nbsp; lot|string|40||批号|
|&nbsp; &nbsp; dateProduction|date|10||生产日期From|
|&nbsp; &nbsp; guaranteeDate|date|10||保质期From|
|&nbsp; &nbsp; validityStatus_Name|string|60||效期状态的名称。<br>&nbsp; 良好<br>&nbsp; 1/3效期<br>&nbsp; 1/2效期<br>&nbsp; 2/3效期<br>&nbsp; 过期|
|&nbsp; &nbsp; invStatus_Name|string|60||库存状态的名称。<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; qtyOnHand|bigdecimal|16,6|✓|在手数量|
|&nbsp; &nbsp; qtyAvailable|bigdecimal|16,6|✓|可用数量|
|&nbsp; &nbsp; qtyReserved|bigdecimal|16,6|✓|占用数量|
|&nbsp; &nbsp; amtOnHand|bigdecimal|16,6||在手金额|
|&nbsp; &nbsp; moveInQty|bigdecimal|16,6||移入数量。开放移库单的入库数量。|
|&nbsp; &nbsp; moveOutQty|bigdecimal|16,6||移出数量。开放移库单的出库数量。|
|invStatus_Name|string|60||库存状态的名称。<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理成功|

JSON格式样例
```
{
    "stockList": [
        {
            "groupLevel": "20",
            "org_Value": "D01",
            "org_Name": "HugeVision-SCM Demo",
            "warehouse_Value": "00",
            "warehouse_Name": "D01B2C仓库",
            "locator_Value": "0001",
            "locator_Name": "D01B2C仓库常规库位",
            "productCategoryL1_Value": "40",
            "productCategoryL1_Name": "食品酒饮",
            "productCategory_Value": "400101",
            "productCategory_Name": "食品酒饮0101",
            "product_Value": "SD01B01",
            "product_Name": "D01食品酒饮01",
            "lot": "202101",
            "dateProduction": "2021-01-01",
            "guaranteeDate": "2021-12-31",
            "validityStatus_Name": "良好",
            "invStatus_Name": "正常",
            "qtyOnHand": "1000",
            "qtyAvailable": "900",
            "qtyReserved": "100",
            "amtOnHand": "10000",
            "moveInQty": "50",
            "moveOutQty": "60",
        }
    ],
    "requestId": "API230DL-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:30:00",
    "errorMsg": "处理成功"
}
```

* 无对象数据时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; No Data!|

JSON格式样例
```
{
    "requestId": "API230DL-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:30",
    "errorMsg": "No Data!"
}
```
