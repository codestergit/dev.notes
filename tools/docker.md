# docker

##资料
> https://github.com/yeasy/docker_practice
> https://github.com/widuu/chinese_docker

##容器的组成
容器= cgroup+namespace+rootfs+ 容器引擎（用户态工具）
其中各项的功能分别为：   
·Cgroup： 资源控制。  
·Namespace： 访问隔离。  
·rootfs： 文件系统隔离。  
·容器引擎： 生命周期控制。  

##Dockerfile
Dockerfile的第一条有效信息(注释除外)必须是基础镜像信息, 维护者信息紧随其后。

##启动
```
docker-machine start default
docker-machine env default
eval $(docker-machine env default)
```

