# API242DLF

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API242DLF

---

## API概述

查询 **业务伙伴(其他)** 。

|功能类型|处理类型|
|:--|:--|
|查询业务数据|同步|

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**querybpartnerother**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|bpartner_IsActive|String|1||查询对象业务伙伴的有效。格式为Y/N。|
|bpGroup_Name|string|60||查询对象业务伙伴组的名称。|
|location_IsActive|String|1||查询对象地址的有效。格式为Y/N。|

JSON格式样例
```
{
    "requestId": "API242DL-0000-0000-0000-000000000001",
    "requestTime": "2021-11-30 12:30:00",
    "bpartner_IsActive": "Y",
    "bpGroup_Name": "主体公司",
    "location_IsActive": "Y"
}
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

* 有数据时返回如下JSON数据

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|bpartnerList|list||✓|业务伙伴列表|
|&nbsp; &nbsp; org_Value|string|40|✓|组织的编码|
|&nbsp; &nbsp; org_Name|string|60|✓|组织的名称|
|&nbsp; &nbsp; isCustomer|string|1|✓|是否客户。格式为Y。|
|&nbsp; &nbsp; isVendor|string|1|✓|是否供应商。格式为Y。|
|&nbsp; &nbsp; bpartner_IsActive|string|1|✓|业务伙伴的有效。格式为Y/N。|
|&nbsp; &nbsp; value|string|40|✓|业务伙伴的编码|
|&nbsp; &nbsp; name|string|60|✓|业务伙伴的名称|
|&nbsp; &nbsp; shortName|string|60|✓|业务伙伴的简称|
|&nbsp; &nbsp; bpGroup_Name|string|60|✓|业务伙伴组的名称|
|&nbsp; &nbsp; description|string|255||附注|
|&nbsp; &nbsp; locationList|list|||地址列表|
|&nbsp; &nbsp; &nbsp; &nbsp; location_Name|string|60||地址的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; location_ReferenceNo|string|40||地址的参考号|
|&nbsp; &nbsp; &nbsp; &nbsp; localocation_IsActivetor_Text|string|60||地址的有效。格式为Y/N。|
|&nbsp; &nbsp; &nbsp; &nbsp; location_Country_Name|string|60||地址的国家的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; location_Region_Name|string|60||地址的省份的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; location_City_Name|string|60||地址的城市的名称|
|&nbsp; &nbsp; &nbsp; &nbsp; address1|string|60||地址1|
|&nbsp; &nbsp; &nbsp; &nbsp; address2|string|60||地址2|
|&nbsp; &nbsp; &nbsp; &nbsp; postal|string|10||邮编|
|&nbsp; &nbsp; &nbsp; &nbsp; contact_Name|string|60||联系人|
|&nbsp; &nbsp; &nbsp; &nbsp; phone|string|60||电话|
|&nbsp; &nbsp; &nbsp; &nbsp; fax|string|60||传真|
|&nbsp; &nbsp; &nbsp; &nbsp; isShipTo|string|1||是否收发货地址。格式为Y/N。|
|&nbsp; &nbsp; &nbsp; &nbsp; isBillTo|string|1||是否开票地址。格式为Y/N。|
|&nbsp; &nbsp; &nbsp; &nbsp; location_Description|string|255||地址的附注|
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 处理成功|

JSON格式样例
```
{
    "bpartnerList": [
        {
            "org_Value": "0",
            "org_Name": "*",
            "isCustomer": "Y",
            "isVendor": "Y",
            "bpartner_IsActive": "Y",
            "value": "D01",
            "name": "HugeVision-SCM Demo",
            "shortName": "HVS Demo",
            "bpGroup_Name": "主体公司",
            "description": "附注",
            "locationList": [
                {
                    "location_Name": "地址名称",
                    "location_ReferenceNo": "M00001",
                    "localocation_IsActivetor_Text": "Y",
                    "location_Country_Name": "中国",
                    "location_Region_Name": "上海市",
                    "location_City_Name": "浦东新区",
                    "address1": "地址1",
                    "address2": "地址2",
                    "postal": "200000",
                    "contact_Name": "联系人",
                    "fax": "021-0000-0001",
                    "phone": "021-0000-0002",
                    "isShipTo": "Y",
                    "isBillTo": "Y",
                    "location_Description": "地址附注"
                }
            ]
        }
    ],
    "requestId": "API242DL-0000-0000-0000-000000000001",
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
    "requestId": "API242DL-0000-0000-0000-000000000001",
    "requestResult": "1",                                                              /*1: 成功*/
    "responseTime": "2021-11-30 12:00:30",
    "errorMsg": "No Data!"
}
```
