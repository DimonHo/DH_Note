docker pull elasticsearch ##下载elasticsearch镜像  
docker run -p 9100:9100 -p 9200:9200 -p 9300:9300 --name es1 -d elasticsearch ##启动elasticsearch容器  
docker exec -it es1 /bin/bash ##进入elasticsearch容器  
apt-get update ##elasticsearch的docker image是基于debian制作的，里面除了java，像vim，git这些都没有的，所以首先需要安装这些工具  
apt-get install vim -y  
apt-get install git -y  
wget https://nodejs.org/dist/v6.11.0/node-v6.11.0-linux-x64.tar.xz  
tar -xvf node-v6.11.0-linux-x64.tar.xz  
mv node-v6.11.0-linux-x64.tar.xz node  
vim /etc/profile   
```config
export NODE_HOME=/opt/node
export PATH=$PATH:$NODE_HOME/bin
```  
source /etc/profile

cd /usr/share/elasticsearch/plugins/
git clone git://github.com/mobz/elasticsearch-head.git
cd elasticsearch-head
npm install -g cnpm --registry=https://registry.npm.taobao.org
npm install grunt --save
