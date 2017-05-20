![](https://github.com/DimonHo/DH_Note/blob/master/git/images/logo.jpg)
## 创建版本库
### 本地版本库
> mkdir DH_Note && cd DH_Note
> git init
> git remote add origin git@github.com:DimonHo/DH_Note.git
### 克隆远程版本库
> git clone git@github.com:DimonHo/DH_Note.git  
或者  
> git clone https://github.com/DimonHo/DH_Note.git
## 基本提交流程
1. `git add files` | `git rm files` //提交变更到暂存区。
2. `git commit -m "提交说明文本"` //将暂存区提交到本地版本库分支。说明文本不能为空，否则会提示Aborting commit due to empty commit message.提交到本地版本库失败。
3. `git push -u origin master` | `git push origin master` | `git push` //提交到远程版本库中。
- 下面是截图：
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0004.png)
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0005.png)
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0006.png)
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0007.png)
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0008.png)
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0009.png)
![](https://github.com/DimonHo/DH_Note/blob/master/git/images/image0010.png)
