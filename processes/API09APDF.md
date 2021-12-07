# API09ADPF

##### [文档首页](index.md)>[HugeVision-SCM API开发手册向导页](../api.md)

---

## API概述

查询待处理发货单信息，查询后发货单的物流回执状态为**处理中**。

|功能类型|处理类型|
|:--|:--|
|查询业务数据|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**exportshipment_pd**
  
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
|doctype_Name|string|60||检索条件。发货单的单据类型的名称。|
|documentNo|string|20||检索条件。发货单的单据号。|
|poReference|string|20||检索条件。发货单的外部单据号。|
|documentNo_Order|string|20||检索条件。订单的单据号。|
|poReference_Order|string|20||检索条件。订单的外部单据号。|
|bpartner_Value|string|40||检索条件。业务伙伴的编码。|
|bpartner_Name|string|60||检索条件。业务伙伴的名称。|
|warehouse_Value|string|40||检索条件。仓库的编码。|
|warehouse_Name|string|60||检索条件。仓库的名称。|
|warehouse_ReferenceNo|string|40||检索条件。仓库的参考号。|
|movementDate|date|10||检索条件。交付日期From。格式为yyyy-MM-dd。|
|movementDateTo|date|10||检索条件。交付日期To。格式为yyyy-MM-dd。|

JSON格式样例(有条件)
```
{
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestTime": "2021-11-24 12:00:00",
    "org_Value" : "D01",
    "org_Name" : "HugeVision-SCM Demo",
    "doctype_Name" : "发货单-信用",
    "documentNo" : "2110DOC8003",
    "poReference" : "DOC0001",
    "documentNo_Order" : "2110SOC8002",
    "poReference_Order" : "SOC0001",
    "bpartner_Value" : "CD01NB50",
    "bpartner_Name" : "D01信用客户50名称",
    "warehouse_Value" : "00",
    "warehouse_Name" : "D01仓库A",
    "warehouse_ReferenceNo" : "WH1",
    "movementDate" : "2021-11-24",
    "movementDateTo" : "2021-11-24"
}
```

JSON格式样例(无条件)
```
{
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestTime": "2021-11-24 12:00:00"
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
|&nbsp; &nbsp; documentNo|string|30|✓|发货单的单据号|
|&nbsp; &nbsp; poReference|string|20||发货单的外部单据号|
|&nbsp; &nbsp; documentNo_Order|string|30|✓|订单的单据号|
|&nbsp; &nbsp; poReference_Order|string|20||订单的外部单据号|
|&nbsp; &nbsp; movementDate|date|10|✓|交付日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; warehouse_Value|string|40|✓|仓库的编码|
|&nbsp; &nbsp; warehouse_Name|string|60|✓|仓库的名称|
|&nbsp; &nbsp; warehouse_ReferenceNo|string|40||仓库的参考号|
|&nbsp; &nbsp; bpartner_Value|string|40|✓|业务伙伴的编码|
|&nbsp; &nbsp; bpartner_Name|string|60|✓|业务伙伴的名称|
|&nbsp; &nbsp; bpartnerLocation_Name|string|60||收货地址的名称|
|&nbsp; &nbsp; bpartnerLocation_ReferenceNo|string|40||收货地址的参考号|
|&nbsp; &nbsp; country_Name|string|60|✓|收货地址的国家|
|&nbsp; &nbsp; region_Name|string|60|✓|收货地址的省份|
|&nbsp; &nbsp; city_Name|string|60|✓|收货地址的城市|
|&nbsp; &nbsp; address1|string|60|✓|收货地址的地址1|
|&nbsp; &nbsp; address2|string|60||收货地址的地址2|
|&nbsp; &nbsp; postal|string|10||收货地址的邮编|
|&nbsp; &nbsp; contact_Name|string|60|✓|收货地址的联系人|
|&nbsp; &nbsp; phone|string|60|✓|收货地址的电话|
|&nbsp; &nbsp; description|string|255||发货单的附注|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; line|string|10|✓|发货单行的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Value|string|40|✓|库位的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Name|string|60|✓|库位的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Value|string|40|✓|产品的编码|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Name|string|255|✓|产品的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; upc|string|30||产品的UPC/EAN|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||发货单行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; movementQty|bigdecimal|16,6|✓|发货数量|
|&nbsp; &nbsp; &nbsp; &nbsp; uom_Name|string|60|✓|计量单位的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; attrList|list||✓|产品属性的列表|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; lot|string|40||批号。保质期管理产品时有值。|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10||生产日期。保质期管理产品时有值。格式为yyyy-MM-dd|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; invStatus_Text|string|60|✓|库存状态的名称<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; attrMovementQty|bigdecimal|16,6|✓|产品属性级别的发货数量|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; attrDescription|string|255||产品属性的附注|
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
            "documentNo": "2110DOC8004",
            "poReference": "",
            "documentNo_Order": "2110SOC8002",
            "poReference_Order": "",
            "movementDate": "2021-10-25",
            "warehouse_Value": "00",
            "warehouse_Name": "D01仓库A",
            "warehouse_ReferenceNo": "",
            "bpartner_Value": "CD01NB50",
            "bpartner_Name": "D01信用客户50名称",
            "bpartnerLocation_Name": "CD01NB50自提地址",
            "bpartnerLocation_ReferenceNo": "",
            "country_Name": "中国",
            "region_Name": "上海市",
            "city_Name": "浦东新区",
            "address1": "CD01NB50自提地址1",
            "address2": "CD01NB50开票地址2",
            "postal": "CD01NB50",
            "contact_Name": "CD01NB50开票地址联系人",
            "phone": "CD01NB50开票地址电话",
            "description": "",
            "lineList": [
                {
                    "line": "10",
                    "locator_Value": "0001",
                    "locator_Name": "D01仓库A正品库位",
                    "product_Value": "SD01B09",
                    "product_Name": "D01食品酒饮09X",
                    "upc": "4940010100009",
                    "lineDescription": "",
                    "movementQty": "1",
                    "uom_Name": "个",
                    "attrList": [
                        {
                            "lot": "20210323",
                            "dateProduction": "2021-01-06",
                            "invStatus_Text": "正常",
                            "attrMovementQty": "1.0",
                            "attrDescription": ""
                        }
                    ]
                }
            ]
        }
    ],
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-24 14:57:43",
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
    "requestId": "431e38b8-b67f-4eb8-ba15-173b3495f67c",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-24 14:54:39",
    "errorMsg": "No Data!"
}
```
