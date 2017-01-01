# LNMP-Docker

基于Docker容器技术，规范一套LNMP开发环境。

每次无论是换工作还是给新人部署开发环境都是一件费事，费时和让人烦躁的事情，各种莫名奇妙的东西，太浪费时间了。有时候同样的某个扩展可能自己
在安装的时候费了九牛二虎之力已经完成，但是当团队中有新的环境配置部署时你不得不在头疼一次，有了docker，妈妈再也不担心我们的环境了，针对
每个项目，负责人在这个基础上添加扩展之后就可以分发给团队每一个成员，就像你们在同一台机子上开发一样一样的。

# 依赖

LNMP-Docker 并不是我的创造，而只是因为一直频繁的被nginx+php的环境配置所困扰，刚好有遇到了docker，心中窃喜！终于可以将某个web应用环境以分发的形式共享给团队开发人员。并且这个环境可以保持`开发`-`测试`-`生产` 环境的一致；降低运维成本；做的CI，CD（持续集成和持续发布）

LNMP-Docker 主要都是基于 [bitnami](https://github.com/bitnami) 所释放/分享出来的相关镜像：

  * [bitnami-docker-nginx](https://github.com/bitnami/bitnami-docker-nginx)
  * [bitnami-docker-php-fpm](https://github.com/bitnami/bitnami-docker-php-fpm)
  * daocloud/wangxb/mysql - docker pull daocloud.io/wangxb/mysql:5.6
更多扩展可根据项目需要自行扩展

# 规范

LNMP-Docker 是使用 `docker-compose` 应用编排进行的，在使用执行请确认你的系统中已经安装了：`docker` 和 `docker-compose`  

  * 克隆 `$ git clone git@github.com:wxb/Docker-LNMP.git`
  * 修改名字 `$ mv Docker-LNMP {项目名} && cd {项目名}}`
  * 拉取你的项目放到workspace目录下并改名app `$ git clone git@github.com:wxb/xxx.git && mv xxx app`
  * 配置虚拟主机 `$ cp vhost-example.conf vhost.conf` 然后修改`vhost.conf`文件
  * 在需要对`php`或者`php-fpm`进行个性配置时，将`php-fpm/conf/`目录下相应`*.example`复制一份改名为：`php-fpm/conf/php.ini`和`php-fpm/conf/php-fpm.conf`进行个性配置
  * 启动环境 `docker-compose up -d`


# 说明

LNMP-Docker 只是我在了解了docker之后进行的简单尝试，使用过程中还可能会出现很多的问题，后面我会逐步完善；不过现在我已经对docker技术充满了想法，只是相关知识的缺乏还不能更好的利用；待之后努力学习，争取用号docker，提升开发-发布环境一致性。

同时，也尝试配合使用[daocloud.com](https://dashboard.daocloud.io/) 对项目进行docker形式的持续集成（CI）和持续发布（CD）。后期如果自己使用的这套构建流完善之后，我会写一篇进行详细介绍，欢迎大家使用
