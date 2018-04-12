# k8s-php-thinkphp-hello

一个以php框架thinkphp的php项目，在kubernets上采用多容器在一个Pod的部署范例

Docker镜像支持同时部署到kubernets或者docker-compose

dockerfile 和 yaml文件 https://github.com/wwek/k8s-php-thinkphp-hello

docker iamges仓库 https://hub.docker.com/r/wwek/k8s-php-thinkphp-hello/


## kubernets（k8s）部署运行
```
kubectl apply -f k8s-php-thinkphp-hello.yml
kubectl get pods |grep k8s-php-thinkphp-hello
kubectl get service |grep k8s-php-thinkphp-hello
kubectl get ingress |grep k8s-php-thinkphp-hello
```

把 k8sphpthinkphp.com hosts解析到Ingress 的ip

然后浏览器

访问  http://k8sphpthinkphp.com/ 可以看到thinkphp的欢迎页面

访问  http://k8sphpthinkphp.com/phpinfo.php 可以看到phpinfo信息

如果没有ingress请自行修改service的type为 NodePort 使用节点的ip和端口访问

## docker-compose部署运行

### 直接up方式，直接pull已经build好的docker images
```
docker-compose up -d
```

### 本地build方式
```
docker-compose up -d --build
```
浏览器
访问 http://127.0.0.1
访问 http://127.0.0.1/phpinfo.php


## 特性
* 组织的容器支持docker-compose部署
* 组织的容器支持kubernets部署
* 以php框架thinkphp为示例，演示php项目的kubernets部署
* 多容器方式（3容器）分别为：appphp（php代码）、openresty（nginx webserver），php-fpm（php的运行环境）
