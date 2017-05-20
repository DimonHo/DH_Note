##事件起因
今天使用elasticsearch发现一个node节点挂掉了，然后查看进程发现有几个defunct的进程。
![](https://github.com/DimonHo/DH_Note/blob/master/linux/images/image0001.png)
简单的了解了一下，原来这是僵尸进程。

##解决过程
看看还有没有其它的僵尸进程：`ps -A|grep defunct`
![](https://github.com/DimonHo/DH_Note/blob/master/linux/images/image0002.png)
	恩，看来就只有这两个，那么该怎么杀死他们呢？如果你使用命令 `kill -9 1944` 尝试杀死ID为1944的进程，可能会没效果。要想成功杀死该进程，需要对其父进程执行kill命令。那么怎么看父进程？其实最开始用ps命令的时候我们已经看到了
![这里写图片描述](https://github.com/DimonHo/DH_Note/blob/master/linux/images/image0003.png)。
当然你也可以用`ps -ef|grep defunct|more` 这个命令来查看
![](https://github.com/DimonHo/DH_Note/blob/master/linux/images/image0004.png)
可以看到他们的父进程是1942。
杀死父进程`kill -9 1942`，再来看看`ps -A|grep defunct`，如果显示无结果，那么就搞定了！否则，你可能需要重启一下系统。

##延伸阅读
在上面，查看某进程的父进程，发现1942的进程的父进程是1，那么1是个什么进程呢？使用ps -ef| grep 1查看发现属于/sbin/init的。
在这里发现一篇介绍linux特殊进程0、1、2的文章：（http://blog.csdn.net/gatieme/article/details/51566690），想继续深入了解可以去看看。
