# API140COB

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API140COB

---

## API概述

创建 **移库单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|异步|

**此API调用后，还得调用API140NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importinventorymove_co_b**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式，与API140COF相同

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; org_Text|string|60||组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60|✓|单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 移库单<br>&nbsp; 移库单-确认|
|&nbsp; &nbsp; movementDate|date|10||移库日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; dateAcct|date|10||记账日期。格式为yyyy-MM-dd。不填写时取得移库日期。|
|&nbsp; &nbsp; shipDate|date|10||出库日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; dateReceived|date|10||入库日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; warehouse_Text|string|60|✓|移出仓库的编码/名称/编码_名称。|
|&nbsp; &nbsp; shipper_Text|string|60||移出仓库物流公司的编码/名称/编码_名称。不填写时取得移出仓库的物流公司。|
|&nbsp; &nbsp; deliveryViaRule_Text|string|60||发货方式的名称。<br>可填写发货方式如下。<br>&nbsp; 配送<br>&nbsp; 自提|
|&nbsp; &nbsp; warehouseTo_Text|string|60|✓|移入仓库的编码/名称/编码_名称。|
|&nbsp; &nbsp; shipperTo_Text|string|60||移入仓库物流公司的编码/名称/编码_名称。不填写时取得移入仓库的物流公司。|
|&nbsp; &nbsp; country_Name|string|60||国家的名称。不填写时取得移入仓库的国家。|
|&nbsp; &nbsp; region_Name|string|60||省份的名称。不填写时取得移入仓库的省份。|
|&nbsp; &nbsp; city_Name|string|60||城市的名称。不填写时取得移入仓库的城市。|
|&nbsp; &nbsp; address1|string|60||地址1。不填写时取得移入仓库的地址1。|
|&nbsp; &nbsp; address2|string|60||不填写时取得移入仓库的地址2。|
|&nbsp; &nbsp; contact_Name|string|60||联系人的名称。不填写时取得移入仓库的联系人。|
|&nbsp; &nbsp; phone|string|60||电话。不填写时取得移入仓库的电话。|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Text|string|60|✓|移出库位的编码/名称/编码_名称。|
|&nbsp; &nbsp; &nbsp; &nbsp; locatorTo_Text|string|60|✓|移入库位的编码/名称/编码_名称。|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Text|string|40|✓|产品的编码/名称/编码_名称。|
|&nbsp; &nbsp; &nbsp; &nbsp; lot|string|40|条件|批号。批号管理产品时必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10|条件|生产日期。保质期管理产品时必填。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; &nbsp; &nbsp; invStatus_Name|string|60|条件|库存状态的名称。库存状态管理产品时必填。<br>可填写如下库存状态。<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||单据行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; movementQty|bigdecimal|16,6|✓|移动数量。必须大于0。|

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
|requestId|string|36|✓|Request的ID|
|requestResult|string|1|✓|请求结果<br>&nbsp; 1:成功|
|responseTime|timestamp|19|✓|响应时间。格式为yyyy-MM-dd hh24:mi:ss。|
|errorMsg|string|255|✓|处理消息<br>&nbsp; 异步处理提交成功|

JSON格式样例(导入成功)
```
{
    "requestId": "API140CO-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "异步处理提交成功"
}
```
