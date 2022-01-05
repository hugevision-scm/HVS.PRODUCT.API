# API270COB

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API270COB

---

## API概述

创建 **询价单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|异步|

**此API调用后，还得调用API270NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importrfq_co_b**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式，与API270COF相同

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; org_Text|string|60||组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60||单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 询价单|
|&nbsp; &nbsp; dateDoc|date|10||单据日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; dateDeliveryTo|date|10|✓|希望交付日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; rfqTopic_Name|string|60|✓|询价单主题的名称|
|&nbsp; &nbsp; name|string|60|✓|询价单的名称|
|&nbsp; &nbsp; quoteType_Text|string|60||询价方式的名称。<br>可填写询价方式如下<br>&nbsp; 选择行报价<br>&nbsp; 逐行报价<br>未填写时为选择行报价|
|&nbsp; &nbsp; isQuoteAllQty_Text|string|1||是否总数报价。格式为Y/N。未填写时为N|
|&nbsp; &nbsp; currency_Text|string|3||货币的编码。未填写时为实体默认货币。|
|&nbsp; &nbsp; description|string|255||单据的附注|
|&nbsp; &nbsp; lineList|list||✓|单据行列表|
|&nbsp; &nbsp; &nbsp; &nbsp; lineId|string|20||外部系统的行号|
|&nbsp; &nbsp; &nbsp; &nbsp; product_Text|string|60|✓|产品的编码/名称/编码_名称。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineIsActive|string|1||询价单行的有效。格式为Y/N。未填写时为Y。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineDescription|string|255||询价单行的附注|
|&nbsp; &nbsp; &nbsp; &nbsp; qty|bigdecimal|16,6|✓|数量。必须大于0。|
|&nbsp; &nbsp; &nbsp; &nbsp; uom_Name|string|60||单位的名称。未填写时取得产品单位。|
|&nbsp; &nbsp; &nbsp; &nbsp; lineQtyIsActive|string|1||询价单行数量的有效。格式为Y/N。未填写时为Y。|
|&nbsp; &nbsp; &nbsp; &nbsp; benchmarkPrice|bigdecimal|16,6||基准单价。必须大于等于0。|
|&nbsp; &nbsp; &nbsp; &nbsp; isPurchaseQty|string|1||是否采购数量。格式为Y/N。未填写时为Y。|


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
