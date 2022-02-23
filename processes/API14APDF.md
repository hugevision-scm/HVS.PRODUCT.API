# API14APDF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API14APDF

---

## API概述

查询移出待处理移库单信息，查询后移库单的物流回执状态(移出)为**处理中**。

|功能类型|处理类型|
|:--|:--|
|查询业务数据|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**exportinventorymovefrom_pd**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID。重复也不报错。|
|requestTime|timestamp|19|✓|请求时间|
|org_Value|string|40||检索条件。组织的编码。|
|org_Name|string|60||检索条件。组织的名称。|
|doctype_Name|string|60||检索条件。移库单的单据类型的名称。|
|documentNo|string|20||检索条件。移库单的单据号。|
|poReference|string|20||检索条件。移库单的外部单据号。|
|warehouse_Value|string|40||检索条件。移出仓库的编码。|
|warehouse_Name|string|60||检索条件。移出仓库的名称。|
|warehouse_ReferenceNo|string|40||检索条件。移出仓库的参考号。|
|movementDate|date|10||检索条件。移库日期From。格式为yyyy-MM-dd。|
|movementDate_to|date|10||检索条件。移库日期To。格式为yyyy-MM-dd。|

JSON格式样例(有条件)
```
{
    "requestId": "API14APD-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:00:00",
    "org_Value" : "D01",
    "org_Name" : "HugeVision-SCM Demo",
    "doctype_Name" : "移库单",
    "documentNo" : "2111ST0001",
    "poReference" : "DOC0001",
    "warehouse_Value" : "00",
    "warehouse_Name" : "D01B2C仓库",
    "warehouse_ReferenceNo" : "B2C",
    "movementDate" : "2021-11-01",
    "movementDate_to" : "2021-11-30"
}
```

JSON格式样例(无条件)
```
{
    "requestId": "API14APD-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:00:00"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 有数据时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; org_Value|string|40|✓|组织的编码|
|&nbsp; &nbsp; org_Name|string|60|✓|组织的名称|
|&nbsp; &nbsp; documentNo|string|30|✓|移库单的单据号|
|&nbsp; &nbsp; poReference|string|20||移库单的外部单据号|
|&nbsp; &nbsp; movementDate|date|10|✓|移库日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; warehouse_Value|string|40|✓|移出仓库的编码|
|&nbsp; &nbsp; warehouse_Name|string|60|✓|移出仓库的名称|
|&nbsp; &nbsp; warehouse_ReferenceNo|string|40||移出仓库的参考号|
|&nbsp; &nbsp; warehouseTo_Value|string|40|✓|移入仓库的编码|
|&nbsp; &nbsp; warehouseTo_Name|string|60|✓|移入仓库的名称|
|&nbsp; &nbsp; warehouseTo_ReferenceNo|string|40||移入仓库的参考号|
|&nbsp; &nbsp; country_Name|string|60|✓|收货地址的国家|
|&nbsp; &nbsp; region_Name|string|60|✓|收货地址的省份|
|&nbsp; &nbsp; city_Name|string|60|✓|收货地址的城市|
|&nbsp; &nbsp; address1|string|60|✓|收货地址的地址1|
|&nbsp; &nbsp; address2|string|60||收货地址的地址2|
|&nbsp; &nbsp; contact_Name|string|60|✓|收货地址的联系人|
|&nbsp; &nbsp; phone|string|60|✓|收货地址的电话|
|&nbsp; &nbsp; description|string|255||移库单的附注|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; line|string|10|✓|移库单行的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Value|string|40|✓|移出库位的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Name|string|60|✓|移出库位的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; locatorTo_Value|string|40|✓|移入库位的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; locatorTo_Name|string|60|✓|移入库位的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Value|string|40|✓|产品的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Name|string|60|✓|产品的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; upc|string|30||产品的UPC/EAN|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||移库单行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; lot|string|40||批号。批号管理产品时有值。|
|&nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10||生产日期。保质期管理产品时有值。格式为yyyy-MM-dd|
|&nbsp; &nbsp; &nbsp; &nbsp; invStatus_Text|string|60||库存状态的名称。库存状态管理产品时有值。<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; movementQty|bigdecimal|16,6|✓|移库数量|
|&nbsp; &nbsp; &nbsp; &nbsp; uom_Name|string|60|✓|单位的名称|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理成功|

JSON格式样例
```
{
    "docList": [
        {
            "org_Value": "D01",
            "org_Name": "HugeVision-SCM Demo",
            "documentNo": "2111ST0001",
            "poReference": "DOC0001",
            "movementDate": "2021-11-30",
            "warehouse_Value": "00",
            "warehouse_Name": "D01B2C仓库",
            "warehouse_ReferenceNo": "B2C",
            "warehouseTo_Value": "02",
            "warehouseTo_Name": "D01B2B仓库",
            "warehouseTo_ReferenceNo": "B2B",
            "country_Name": "中国",
            "region_Name": "上海市",
            "city_Name": "浦东新区",
            "address1": "D01B2B仓库地址1",
            "address2": "D01B2B仓库地址2",
            "contact_Name": "D01B2B仓库联系人",
            "phone": "D01B2B仓库电话",
            "description": "附注",
            "lineList": [
                {
                    "line": "10",
                    "locator_Value": "0001",
                    "locator_Name": "D01B2C仓库常规库位",
                    "locatorTo_Value": "0201",
                    "locatorTo_Name": "D01B2B仓库常规库位",
                    "product_Value": "SD01B09",
                    "product_Name": "D01食品酒饮09",
                    "upc": "4940010100009",
                    "lineDescription": "行附注",
                    "lot": "202101",
                    "dateProduction": "2021-01-01",
                    "invStatus_Text": "正常",
                    "movementQty": "100",
                    "uom_Name": "个"
                }
            ]
        }
    ],
    "requestId": "API14APD-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:00",
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
    "requestId": "API14APD-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "No Data!"
}
```
