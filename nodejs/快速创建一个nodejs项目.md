# 环境准备
OS： windwos平台  
1. 下载安装[nodejs](http://nodejs.cn/download/)
2. 使用npm安装express(一个基于 Node.js 平台，快速、开放、极简的 web 开发框架。)  
> `npm install express  –g`   
> `npm install express-generator -g`  ## -g表示全局安装
   
3. 创建blog项目骨架  
> `express blog` ##创建名为blog的项目  
> `cd blog`      ##进入blog目录  
> `npm install`  ##安装项目依赖   
> `set DEBUG=blog & npm start`  ##debug模式启动项目，直接npm start也是可以的，那就是非debug模式启动。  
> 访问 http://localhost:3000   

4. 使用supervisor监控代码修改，自动重启服务提高调试效率  
> ` npm -g install supervisor`  ##安装supervisor  
> `supervisor .\bin\www`  ##代替npm start命令启动应用  
