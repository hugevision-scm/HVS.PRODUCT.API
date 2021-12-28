# API070COB

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API070COB

---

## API概述

创建 **收货单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|异步|

**此API调用后，还得调用API070NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importreceipt_co_b**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式，与API070COF相同

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; org_Text|string|60||组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60||单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 收货单<br>&nbsp; 收货单-进口。<br>不填写时取得订单对应的收货单单据类型。|
|&nbsp; &nbsp; movementDate|date|10||交付日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; dateAcct|date|10||记账日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; docNoOrder|string|20|✓|采购订单的单据号。|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; warehouse_Text|string|60||仓库的编码/名称。不填写时取得订单的仓库。<br>如果仓库填写并不填写物流公司时取得仓库的物流公司。|
|&nbsp; &nbsp; shipper_Text|string|60||物流公司的编码/名称。不填写时取得订单的物流公司。|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; locator_Text|string|60||库位的编码/名称/编码_名称。不填写时取得订单行的库位。|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Value|string|40|条件|产品的编码。编码或名称为必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Name|string|60|条件|产品的名称。编码或名称为必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; movementQty|bigdecimal|16,6|条件|交付数量。必须大于0。不允许为0。<br>属性列表填写时可以不填。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||单据行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; attrList|list||条件|产品属性列表。收货单要签收确认不需要填写。|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; lot|string|40|条件|批号。批号管理产品时必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; dateProduction|date|10|条件|生产日期。保质期管理产品时必填。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; invStatus_Name|string|60|条件|库存状态的名称。库存状态管理产品时必填。<br>可填写如下库存状态。<br>&nbsp; 正常<br>&nbsp; 冻结<br>&nbsp; 破损<br>&nbsp; 待定|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; attrMovementQty|bigdecimal|16,6|条件|产品属性数量。必须大于0。填写属性列表时必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; dateReceipt|date|10||入库日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; attrDescription|string|255||产品属性的附注|

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
    "requestId": "API070CO-0000-0000-0000-000000000001",
    "requestResult": "1",
    "responseTime": "2021-11-30 12:00:00",
    "errorMsg": "异步处理提交成功"
}
```
