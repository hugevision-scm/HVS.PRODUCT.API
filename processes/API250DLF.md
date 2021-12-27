# API250DLF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API250DLF

---

## API概述

查询 **产品** 。

|功能类型|处理类型|
|:--|:--|
|查询业务数据|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**queryproduct**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|org_Value|string|40||查询对象组织的的编码。|
|product_IsActive|String|1||查询对象产品的有效。格式为Y/N。|
|productType_Name|string|60||查询对象产品类型的名称。<br>可填写产品区分如下。<br>&nbsp; 物品|
|productCategoryL1_Value|string|40||查询对象产品类别(第一级)的编码。|
|discontinued|string|1||查询对象已停产。格式为Y/N。|
|isStocked|string|1||查询对象可库存。格式为Y/N。|
|isPurchased|string|1||查询对象可采购。格式为Y/N。|
|isSold|string|1||查询对象可销售。格式为Y/N。|
|stockType_Name|string|1||查询对象产品区分。<br>可填写产品区分如下。<br>&nbsp; 普通品<br>&nbsp; 紧俏品|
|isBom|string|1||查询对象BOM。格式为Y/N。|
|isPurchasedDealer|string|1||查询对象公开发售。格式为Y/N。|

JSON格式样例
```
{
    "requestId": "API250DL-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:30:00",
    "org_Value": "D01",
    "product_IsActive": "Y",
    "productType_Name": "物品",
    "productCategoryL1_Value": "40",
    "discontinued": "N",
    "isStocked": "Y",
    "isPurchased": "Y",
    "isSold": "Y",
    "stockType_Name": "紧俏品",
    "isBom": "N",
    "isPurchasedDealer": "Y"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 有数据时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|productList|list||✓|产品列表|
|&nbsp; &nbsp; org_Value|string|40|✓|组织的编码|
|&nbsp; &nbsp; org_Name|string|60|✓|组织的名称|
|&nbsp; &nbsp; value|string|40|✓|业务伙伴的编码|
|&nbsp; &nbsp; name|string|60|✓|业务伙伴的名称|
|&nbsp; &nbsp; product_IsActive|string|1|✓|产品的有效。格式为Y/N。|
|&nbsp; &nbsp; productType_Name|string|60|✓|产品类型的简称|
|&nbsp; &nbsp; productCategory_Value|string|40|✓|产品类别的编码|
|&nbsp; &nbsp; productCategory_Name|string|60|✓|产品类别的名称|
|&nbsp; &nbsp; productCategoryL1_Value|string|40|✓|产品类别(第一级)的编码|
|&nbsp; &nbsp; productCategoryL1_Name|string|60|✓|产品类别(第一级)的名称|
|&nbsp; &nbsp; productCategoryL2_Value|string|40||产品类别(第二级)的编码|
|&nbsp; &nbsp; productCategoryL2_Name|string|60||产品类别(第二级)的名称|
|&nbsp; &nbsp; productCategoryL3_Value|string|40||产品类别(第三级)的编码|
|&nbsp; &nbsp; productCategoryL3_Name|string|60||产品类别(第三级)的名称|
|&nbsp; &nbsp; productCategoryL4_Value|string|40||产品类别(第四级)的编码|
|&nbsp; &nbsp; productCategoryL4_Name|string|60||产品类别(第四级)的名称|
|&nbsp; &nbsp; productCategoryL5_Value|string|40||产品类别(第五级)的编码|
|&nbsp; &nbsp; productCategoryL5_Name|string|60||产品类别(第五级)的名称|
|&nbsp; &nbsp; uom_Name|string|60|✓|单位的名称|
|&nbsp; &nbsp; upc|string|30||条码|
|&nbsp; &nbsp; harmonizedCode|string|30||海关编码|
|&nbsp; &nbsp; tax_Rate|string|60||税率的名称|
|&nbsp; &nbsp; poTax_Rate|string|60||税率(采购)的名称|
|&nbsp; &nbsp; vat_Rate|bigdecimal|16,2||增值税率|
|&nbsp; &nbsp; consumptionTax_Rate|bigdecimal|16,2||消费税率|
|&nbsp; &nbsp; duty_Rate|bigdecimal|16,2||关税税率|
|&nbsp; &nbsp; weight|bigdecimal|16,6||重量|
|&nbsp; &nbsp; volume|bigdecimal|16,6||体积|
|&nbsp; &nbsp; discontinued|string|1|✓|是否已停产。格式为Y/N。|
|&nbsp; &nbsp; discontinuedAt|date|10||停产日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; description|string|255||附注|
|&nbsp; &nbsp; help|string|255||备注|
|&nbsp; &nbsp; isStocked|string|1|✓|是否可库存。格式为Y/N。|
|&nbsp; &nbsp; isPurchased|string|1|✓|是否可采购。格式为Y/N。|
|&nbsp; &nbsp; isSold|string|1|✓|是否可销售。格式为Y/N。|
|&nbsp; &nbsp; stockType_Name|string|60||产品区分的名称。<br>&nbsp; 普通品<br>&nbsp; 紧俏品|
|&nbsp; &nbsp; isBom|string|1|✓|是否BOM。格式为Y/N。|
|&nbsp; &nbsp; attributeSet_Name|string|60|✓|属性集的名称。|
|&nbsp; &nbsp; guaranteeMonths|integer|3||保质期月数|
|&nbsp; &nbsp; isPurchasedDealer|string|1|✓|是否公开发售。格式为Y/N。|
|&nbsp; &nbsp; userDefField01|string|60||自定义字段01|
|&nbsp; &nbsp; userDefField02|string|60||自定义字段02|
|&nbsp; &nbsp; userDefField03|string|60||自定义字段03|
|&nbsp; &nbsp; userDefField04|string|60||自定义字段04|
|&nbsp; &nbsp; userDefField05|string|60||自定义字段05|
|&nbsp; &nbsp; userDefField06|string|60||自定义字段06|
|&nbsp; &nbsp; userDefField07|string|60||自定义字段07|
|&nbsp; &nbsp; userDefField08|string|60||自定义字段08|
|&nbsp; &nbsp; userDefField09|string|60||自定义字段09|
|&nbsp; &nbsp; userDefField10|string|60||自定义字段10|
|&nbsp; &nbsp; userDefNumField01|bigdecimal|16,6||自定义数字字段01|
|&nbsp; &nbsp; userDefNumField02|bigdecimal|16,6||自定义数字字段02|
|&nbsp; &nbsp; userDefNumField03|bigdecimal|16,6||自定义数字字段03|
|&nbsp; &nbsp; userDefNumField04|bigdecimal|16,6||自定义数字字段04|
|&nbsp; &nbsp; userDefNumField05|bigdecimal|16,6||自定义数字字段05|
|&nbsp; &nbsp; userDefNumField06|bigdecimal|16,6||自定义数字字段06|
|&nbsp; &nbsp; userDefNumField07|bigdecimal|16,6||自定义数字字段07|
|&nbsp; &nbsp; userDefNumField08|bigdecimal|16,6||自定义数字字段08|
|&nbsp; &nbsp; userDefNumField09|bigdecimal|16,6||自定义数字字段09|
|&nbsp; &nbsp; userDefNumField10|bigdecimal|16,6||自定义数字字段10|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理成功|

JSON格式样例
```
{
    "productList": [
        {
            "org_Value": "0",
            "org_Name": "*",
            "value": "SD01B01",
            "name": "D01食品酒饮01",
            "product_IsActive": "Y",
            "productType_Name": "物品",
            "productCategory_Value": "400101",
            "productCategory_Name": "食品酒饮0101",
            "productCategoryL1_Value": "40",
            "productCategoryL1_Name": "食品酒饮",
            "productCategoryL2_Value": "4001",
            "productCategoryL2_Name": "食品酒饮01",
            "productCategoryL3_Value": "400101",
            "productCategoryL3_Name": "食品酒饮0101",
            "productCategoryL4_Value": "",
            "productCategoryL4_Name": "",
            "productCategoryL5_Value": "",
            "productCategoryL5_Name": "",
            "uom_Name": "个",
            "upc": "4940010100001",
            "harmonizedCode": "123456",
            "tax_Rate": "3%销项",
            "poTax_Rate": "13%进项",
            "vat_Rate": "13.00",
            "consumptionTax_Rate": "6.50",
            "duty_Rate": "3.00",
            "weight": "26.710000000000",
            "volume": "0.498000000000",
            "discontinued": "N",
            "discontinuedAt": "",
            "description": "附注",
            "help": "备注",
            "isStocked": "Y",
            "isPurchased": "Y",
            "isSold": "Y",
            "stockType_Name": "普通品",
            "isBom": "N",
            "attributeSet_Name": "批号&保质期管理",
            "guaranteeMonths": "24",
            "isPurchasedDealer": "Y",
            "userDefField01": "自定义字段01",
            "userDefField02": "自定义字段02",
            "userDefField03": "自定义字段03",
            "userDefField04": "自定义字段04",
            "userDefField05": "自定义字段05",
            "userDefField06": "自定义字段06",
            "userDefField07": "自定义字段07",
            "userDefField08": "自定义字段08",
            "userDefField09": "自定义字段09",
            "userDefField10": "自定义字段10",
            "userDefNumField01": "1.00",
            "userDefNumField02": "2.00",
            "userDefNumField03": "3.00",
            "userDefNumField04": "4.00",
            "userDefNumField05": "5.00",
            "userDefNumField06": "6.00",
            "userDefNumField07": "7.00",
            "userDefNumField08": "8.00",
            "userDefNumField09": "9.00",
            "userDefNumField10": "10.00"
        }
    ],
    "requestId": "API250DL-0000-0000-0000-000000000001",
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
    "requestId": "API250DL-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:30",
    "errorMsg": "No Data!"
}
```
