随着公司系统越来越多，各个系统各自为政显然不太专业，单点登录的需求应运而生。
CAS框架能够满足我们的需求。

## 生成SSL证书，导入到服务器
首先使用keytool工具生成证书，wdrsa是我的证书名称，你可以自定义，f:/key/wdrsa是证书文件的路径，先要保证`f:/key`路径已存在。
>keytool.exe -genkey -alias wdrsa -keyalg RSA -keystore f:/key/wdrsa  

接下来把证书导出来。
>keytool -export -file f:/key/wdrsa.crt -alias wdrsa -keystore f:/key/wdrsa  

然后把证书导入到服务器
>keytool -import -keystore "d:\Program Files\Java\jdk1.8.0_91\jre\lib\security\cacerts" -file f:\key\wdrsa.crt -alias wdrsa  
这里需要输入密码，这个不是指你在上面设置的密码，而是固定的写法：
>changeit  


## 问题总结
- **运行访问`http://localhost:8080/cas`登录，无法保持登录状态？**
1. 修改`/cas-server-webapp/src/main/webapp/WEB-INF/deployerConfigContext.xml`文件，找到id="proxyAuthenticationHandler"的代码片段，添加`p:requireSecure="false"`属性：
```
<bean id="proxyAuthenticationHandler"
  class="org.jasig.cas.authentication.handler.support.HttpBasedServiceCredentialsAuthenticationHandler"
  p:httpClient-ref="supportsTrustStoreSslSocketFactoryHttpClient"
  p:requireSecure="false" />
```
2. 修改`/cas-server-webapp/src/main/webapp/WEB-INF/spring-configuration/ticketGrantingTicketCookieGenerator.xml`文件，找到id="ticketGrantingTicketCookieGenerator"的代码片段，将p:cookieSecure="true"修改为p:cookieSecure="false"：
```
<bean id="ticketGrantingTicketCookieGenerator" class="org.jasig.cas.web.support.CookieRetrievingCookieGenerator"
  c:casCookieValueManager-ref="cookieValueManager"
  p:cookieSecure="false"
  p:cookieMaxAge="-1"
  p:cookieName="TGC"
  p:cookiePath=""/>
```
3. 修改`/cas-server-webapp/src/main/webapp/WEB-INF/spring-configuration/warnCookieGenerator.xml`文件，找到id="warnCookieGenerator"代码片段，将p:cookieSecure="true"修改为p:cookieSecure="false"：
```
<bean id="warnCookieGenerator" class="org.jasig.cas.web.support.CookieRetrievingCookieGenerator"
  p:cookieSecure="false"
  p:cookieMaxAge="-1"
  p:cookieName="CASPRIVACY"
  p:cookiePath=""/>
```
4. 重启应用，重新登录，发现已经可以支持http登录保持，End！
