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

