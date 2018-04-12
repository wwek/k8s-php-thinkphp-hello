# k8s-php-thinkphp-hello
一个PHP项目ThinkPHP框架用kubernets（k8s）部署和docker-compose部署的示例
dockerfile https://github.com/wwek/k8s-php-thinkphp-hello
docker iamges https://hub.docker.com/r/wwek/k8s-php-thinkphp-hello/

## kubernets（k8s）部署运行
```
kubectl apply -f k8s-php-thinkphp-hello.yml
kubectl get svc |grep k8s-php-thinkphp-hello
```

浏览器访问
http://k8snode:nodeport/
http://k8snode:nodeport/phpinfo.php

如果有Ingress那么把k8sphpthinkphp.com hosts解析到Ingress 的ip
然后通过 http://k8sphpthinkphp.com/  http://k8sphpthinkphp.com/phpinfo.php 访问

## docker-compose部署运行

### 直接up方式，直接pull已经build好的docker images
```
docker-compose up -d
```

### 本地build方式
```
docker-compose up -d --build
```
浏览器访问
http://127.0.0.1
http://127.0.0.1/phpinfo.php


## 特性
* 支持docker-compose部署
* 支持kubernets部署
* 以PHP框架thinkphp为例
* 多容器方式，php代码，openresty（nginx），php-fpm 3容器方式
