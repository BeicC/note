* 为什么需要Docker？
和springboot相似，Docker将应用程序和其所依赖的环境打成一个整体，部署在服务器上
<img src="docker.png" width=600px>
* `docker pull`:下载镜像
```bash
sudo docker pull mysql:5.7
```
* 查看镜像(images):`sudo docker images`
* 查看docker正在运行的容器
`docker ps`
* `run`
    * `docker run -d --name nginx01 -p 3344:80 nginx`
    docker run 启动image
    -d ： 后台运行
    --name ： 起个名字，如果不写，默认为image名
    -p 3344：80: 端口映射，将本地(vmware虚拟机)的3344端口与nginx01(小Linux)的80端口绑定； 只要访问vmware的3344端口，就可以访问到ngnix
    nginx：想要启动的image名字
* docker重启mysql
`docker restart mysql`
* 进入小Linux
`docker exec -it  mysql /bin/bash`