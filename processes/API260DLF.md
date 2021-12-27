# API260DLF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API260DLF

---

## API概述

查询 **盘点单** 。

|功能类型|处理类型|
|:--|:--|
|查询业务数据|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**queryphysicalinventory**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|documentNo|string|20|✓|查询对象盘点单的单号。|
|locator_Value|string|40||检索条件。库位的编码。|
|locator_Name|string|60||检索条件。库位的名称。|
|productCategoryL1_Value|string|40||检索条件。产品类别(第一级)的编码。|
|productCategoryL1_Name|string|60||检索条件。产品类别(第一级)的名称。|
|product_Value|string|40||检索条件。产品的编码。|
|product_Name|string|60||检索条件。产品的名称。|

JSON格式样例
```
{
    "requestId": "API260DL-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:30:00",
    "documentNo": "2111SC0001",
    "locator_Value": "0001",
    "locator_Name": "D01B2C仓库常规库位",
    "productCategoryL1_Value": "40",
    "productCategoryL1_Name": "食品酒饮",
    "product_Value": "SD01B01",
    "product_Name": "D01食品酒饮01"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 有数据时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|docList|list||✓|盘点单列表|
|&nbsp; &nbsp; org_Value|string|40|✓|组织的编码|
|&nbsp; &nbsp; org_Name|string|60|✓|组织的名称|
|&nbsp; &nbsp; doctype_Name|string|60|✓|单据类型的名称|
|&nbsp; &nbsp; docStatus_Name|string|60|✓|单据状态的名称|
|&nbsp; &nbsp; documentNo|string|20|✓|盘点单的单据号。|
|&nbsp; &nbsp; inventoryDate|date|10|✓|盘点日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; warehouse_Value|string|40|✓|仓库的编码|
|&nbsp; &nbsp; warehouse_Name|string|60|✓|仓库的名称|
|&nbsp; &nbsp; shipper_Name|string|60|✓|物流公司的名称|
|&nbsp; &nbsp; description|string|255||附注|
|&nbsp; &nbsp; lineList|list|||盘点单行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; line|string|10|✓|盘点单行的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Value|string|40|✓|库位的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Name|string|60|✓|库位的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; productCategoryL1_Value|string|40|✓|产品类别(第一级)的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; productCategoryL1_Name|string|60|✓|产品类别(第一级)的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; productCategory_Value|string|40|✓|产品类别的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; productCategory_Name|string|60|✓|产品类别的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Value|string|40|✓|产品的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Name|string|60|✓|产品的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; uom_Name|string|60|✓|单位的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; lot|string|40||批号|
|&nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10||生产日期|
|&nbsp; &nbsp; &nbsp; &nbsp; invStatus_Name|string|60||库存状态<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; qtyBook|bigdecimal|16,6|✓|账存数量|
|&nbsp; &nbsp; &nbsp; &nbsp; qtyCount|bigdecimal|16,6|✓|盘点数量|
|&nbsp; &nbsp; &nbsp; &nbsp; differenceQty|bigdecimal|16,6|✓|差异数量|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||盘点单行的附注|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理成功|

JSON格式样例
```
{
    "docList": [
        {
            "org_Value": "0",
            "org_Name": "*",
            "doctype_Name": "盘点单",
            "docStatus_Name": "草稿",
            "documentNo": "2111SC0001",
            "inventoryDate": "2021-11-30",
            "warehouse_Value": "00",
            "warehouse_Name": "D01B2C仓库",
            "shipper_Name": "D01仓储物流公司01名称",
            "description": "附注",
            "lineList": [
                {
                    "line": "10",
                    "locator_Value": "0001",
                    "locator_Name": "D01B2C仓库常规库位",
                    "productCategory_Value": "400101",
                    "productCategory_Name": "食品酒饮0101",
                    "productCategoryL1_Value": "40",
                    "productCategoryL1_Name": "食品酒饮",
                    "product_Value": "SD01B01",
                    "product_Name": "D01食品酒饮01",
                    "uom_Name": "个",
                    "lot": "202101",
                    "dateProduction": "2021-01-01",
                    "invStatus_Name": "正常",
                    "qtyBook": "2000.00",
                    "qtyCount": "1980.00",
                    "differenceQty": "20.00",
                    "lineDescription": "行附注"
                }
            ]
        }
    ],
    "requestId": "API260DL-0000-0000-0000-000000000001",
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
    "requestId": "API260DL-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:30",
    "errorMsg": "No Data!"
}
```
