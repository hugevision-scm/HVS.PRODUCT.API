# API120COB

##### [文档首页](../index.md)>[HugeVision-SCM API开发手册向导页](../api.md)>API120COB

---

## API概述

创建 **付款单** 并单据操作提交。

|功能类型|处理类型|
|:--|:--|
|创建业务数据|异步|

**此API调用后，还得调用API120NNF查询处理结果。**

##  Request

 ```POST```  https://*{ HVS的URL }*/api/v1/processes/**importappayment_co_b**
  
###  Request Header

请参考API共通

###  Request Body

做成如下JSON格式，与API120COF相同

|名称|类型|长度|必填项|附注|
|:--|:--|:--|:--|:--|
|requestId|string|36|✓|每次处理唯一的ID|
|requestTime|timestamp|19|✓|请求时间。格式为yyyy-MM-dd hh24:mi:ss。|
|docList|list||✓|单据列表|
|&nbsp; &nbsp; docNo|string|20|✓|外部系统的单据号|
|&nbsp; &nbsp; org_Text|string|60||组织的编码/名称/编码_名称。不填写时取得登录用户组织。|
|&nbsp; &nbsp; doctype_Name|string|60||单据类型的名称。<br>可填写如下单据类型<br>&nbsp; 付款单|
|&nbsp; &nbsp; isPrepayment|string|1||是否预付。只允许为Y。|
|&nbsp; &nbsp; bankTrnNo|string|60||银行流水号|
|&nbsp; &nbsp; dateAcct|date|10||记账日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; bpartner_Value|string|40|条件|业务伙伴的编码。编码或名称为必填。|
|&nbsp; &nbsp; bpartner_Name|string|60|条件|业务伙伴的名称。编码或名称为必填。|
|&nbsp; &nbsp; dateTrx|date|10||申请日期。格式为yyyy-MM-dd。不填写时取得当前日期。|
|&nbsp; &nbsp; datePlanPay|date|10||希望支付日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; dateActualPay|date|10||实际支付日期。格式为yyyy-MM-dd。|
|&nbsp; &nbsp; bankAccount_Text|string|60|条件|银行账户的编码/名称。如果货币有多个银行账户时必填。|
|&nbsp; &nbsp; customerAccountNo|string|20||对方账户的账号。|
|&nbsp; &nbsp; customerBankName|string|60||对方银行的名称。|
|&nbsp; &nbsp; currency_Text|string|3|✓|货币的编码。<br>可填写货币在实体使用条件里维护。|
|&nbsp; &nbsp; settlementRate|bigdecimal|16,10||结算汇率。不填写时取得申请日期当天的汇率。|
|&nbsp; &nbsp; payAmt|bigdecimal|16,6|✓|支付金额(原币)。不允许为0。|
|&nbsp; &nbsp; description|string|255||单据的附注|

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
