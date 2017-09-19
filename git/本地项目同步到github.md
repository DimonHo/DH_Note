1.在本地创建一个项目，在该目录下运行git bash
```
git init
```
2. 在github上创建一个同名项目，复制git地址。
3. remote 远程地址到本地项目
```
git remote https://github.com/DimonHo/wdMysqlTools.git
```
4. pull远程项目到本地
```
git pull origin master --allow-unrelated-histories
```
5. 提交本地文件到git
```
git add *
git commit * -m "init"
git push -u origin master
```
