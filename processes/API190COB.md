# API190COB

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API190COB

---

## API概述

创建 **采购订单(代理商)** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|异步|

**此API调用后，还得调用API190NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importdealerpurchaseorder_co_b**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式，与API190COF相同

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; org_Text|string|60||组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60||单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 采购订单-信用(代理商)<br>&nbsp; 采购订单-预付(代理商)。不填写时取得发票伙伴的账期类型对应的单据类型|
|&nbsp; &nbsp; dateOrdered|date|10||订单日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; bpartner_Value|string|40|条件|业务伙伴的编码。多主体公司交易时编码或名称为必填。|
|&nbsp; &nbsp; bpartner_Name|string|60|条件|业务伙伴的名称。多主体公司交易时编码或名称为必填。|
|&nbsp; &nbsp; billpartner_Value|string|40||发票伙伴的编码。不填写时取得组织业务伙伴。|
|&nbsp; &nbsp; billpartner_Name|string|60||发票伙伴的名称。不填写时取得组织业务伙伴。|
|&nbsp; &nbsp; location_Text|string|60|条件|收货地址的名称。多地址的情况必填。|
|&nbsp; &nbsp; priceList_Text|string|60||价格表的名称。不填写时取得业务伙伴的价格表。|
|&nbsp; &nbsp; settlementRate|bigdecimal|16,10||结算汇率。不填写时取得订单日期当天的汇率。|
|&nbsp; &nbsp; isFixedRate|string|1||固定汇率。格式为Y/N。不填写时为N。|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Value|string|40|条件|产品的编码。编码或名称为必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Name|string|60|条件|产品的名称。编码或名称为必填。|
|&nbsp; &nbsp; &nbsp; &nbsp; qty|bigdecimal|16,6|✓|数量。必须大于0。|
|&nbsp; &nbsp; &nbsp; &nbsp; uom_Name|string|60||单位的名称。不填写时取得产品的单位。|
|&nbsp; &nbsp; &nbsp; &nbsp; tax_Text|string|60||税率的名称/附注。不填写时取得产品的税率。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||单据行的附注|

JSON格式样例
```
(待补充)
```

##  Response
 
###  Response Header

无特别描述

###  Response Body

创建业务数据异步处理的响应格式

&nbsp;&nbsp;&nbsp;&nbsp;→&nbsp;[响应格式&样例](Response_Body_01.md)
