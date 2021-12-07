
# HugeVision-SCM API


HugeVision-SCM API是赋能连接与协同的开放接口<br>
服务使用方的其他系统(后称"外部系统")可以使用API接口与HugeVision-SCM平台进行数据交互和业务协同<br>
<br>

<span id="说明文档构成"></span>

---
## **说明文档构成**

[API调用说明](#API调用说明)<br>
[API功能说明](#API功能说明)<br>
[API接口列表](#API接口列表)<br>


<span id="API调用说明"></span>

## **API调用说明**

接口需使用HTTPS协议、JSON数据格式、UTF8编码


![](images/API_CallStep.png)<br>

**Step1 协同平台注册**<br>
在HugeVision-SCM中注册协同平台，获得系统名、系统密码<br>
在HugeVision-SCM中注册协同平台用户，获得实体、组织、角色<br>

**Step2 验证身份并获取Token**<br>
使用Step1中注册的系统名、用户名、系统密码进行登录认证，取得事先配置的实体、组织、角色以获取令牌<br>
※令牌为JWT-JSON Web Token(RFC7591)认证令牌<br>
※具体请参考[TOKEN获取](tokens/Tokens.md)

**Step3 缓存和刷新Token**<br>
开发者需要缓存Token，用于后续接口的调用<br>
※Token不可以返回外部系统前台，需要保存在后台，所有访问API的请求需由后台发起<br>
※不能频繁调用TOKEN获取接口，否则会受到频率拦截<br>

**Step4 调用具体的业务API**<br>
使用缓存的Token调用具体业务API，具体请参考[API接口列表](#API接口列表])<br>
※Token的有效时长为60分钟，当Token失效或过期时，需要重新获取
<br>

---
<span id="API功能说明"></span>

## **API功能说明**


**功能类型**<br>
---
API的功能类型有——<br>
1、查询业务数据<br>
查询业务数据，可以同时更新接口字段的状态
2、创建业务数据<br>
创建业务单据，同时执行单据操作-完成处理<br>
3、查询异步处理结果<br>
查询创建业务数据的处理结果，一般用于异步处理<br>


**处理类型**
---
F:同步处理<br>
API调用后，同时完成API请求导入及所有后续处理，处理完成后返回处理结果<br>
※所有功能类型均可支持同步处理<br>
<br>
B:异步处理<br>
API调用后，只执行API请求导入，导入成功即返回"异步处理提交成功"的消息<br>
每30分钟一次执行计划任务处理上述API请求，处理完成后保留异步处理结果待查<br>
外部系统需另行调用各业务的**查询异步处理结果API**，查看异步处理结果<br>
※仅创建业务数据功能类型的API支持异步处理<br>
<br>

**API接口方式图**
---
### 查询业务数据
(仅支持同步处理)<br>
![](images/API_DataQuery.png)<br>

### 创建业务数据(同步)
![](images/API_DocCreate-F.png)<br>

### 创建业务数据(异步)
![](images/API_DocCreate-B.png)<br>

### 查询异步处理结果
(仅支持同步处理)<br>
![](images/API_ResultQuery.png)<br>

---
<span id="API接口列表"></span>

## **业务API具体说明**
---
**业务API列表(点击说明文档可跳转到具体说明页面)**

|功能Code|功能类型|处理类型|概述|具体说明
|:--|:---|:--|:----|:--|
|-|认证并获取Token|同步|认证并获取Token|[TOKEN获取](tokens/Tokens.md)
|API09APDF|查询业务数据|同步|查询待处理发货单信息|[API09APDF](processes/API09APDF.md)
|API170COF|创建业务数据|同步|创建库存调整单|[API170COF](processes/API09APDF.md)
|API170COB|创建业务数据|异步|创建库存调整单|[API170COB](processes/API170COB.md)
|API170NNF|查询异步处理结果|同步|查询库存调整单的异步处理结果|[API170NNF](processes/API170NNF.md)
