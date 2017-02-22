# LNMP-Docker

基于Docker容器技术，配置一个可分发、快速、简单、标准、统一的LNMP开发环境。

# 长久以来的痛点

在我平时的开发中,经常会配置开发环境,对于一个开发人员来说快速流畅的配置好开发环境是必备技能,也许你越是熟悉或者精通,越能体会到配置环境本身
其实是一个体力活,重复的劳动毫无意义。

每次无论是换工作还是给新人部署开发环境都是一件费事，费时和让人烦躁的事情，各种莫名奇妙的东西，太浪费时间了。有时候同样的某个扩展可能自己在
安装的时候费了九牛二虎之力已经完成，但是当团队中有新的环境配置部署时你不得不在头疼一次,更危险的是当你的团队中的开发人员在某个版本开发过程中
需要一些新的扩展或者配置时,其他的开发者就还得将相同的工作重复一遍,并且测试环境和线上环境也得小心翼翼的再来一次。

那么如何才能做到环境的**分发**, 就是一次配置到处运行。曾是我将LNMP的开发环境以**绿色**安装的形式保存来尝试解决这种重复的体力劳动,
但是效果似乎还是不那么理想。知道我了解到**docker**


# docker
第一次知道docker,实在2016年的3月,当时看到docker的说明简直就是如沐春风啊! 简单说明一下docker-一种容器技术(虚拟化技术),有点类似与沙箱
的感觉。我们的应用不在运行在我们的系统上,而是在系统之上虚拟出来一套环境也就是容器,这个容器和我们的应用是相辅相成的。而容器本身是跨平台、
易分发、标准化、且很安全。

其实docker的logo就很有代表性:一直鲸鱼载着很多集装箱。集装箱在货运领域的革新是很明显的:制定了标准,统一了标准;走到世界的任何一个港口集装箱
都是这个尺寸,至于里面是装了什么东西,装了什么形状都不用运输的人员操心。所以,docker通过logo就在说明docker的特点。

我也只是docker使用的一个新手,关于docker相关的中文资料目前相对较少,并且docker也属于新技术,很多英文资料因为自己英语基础啃起来很费劲。
很多东西还没有搞清楚,这里简单的说一下自己理解的docker的特点:

* 标准化    
    统一的标准的应用运行容器, 当对一个应用的docker容器配置建立起且运行起以后, 这套容器就和运行浑然一体了,运行环境在哪里都是统一的,标准的。
* 易分发      
    无论在那个机器上,我们只需要将docker安装好,执行一条命令我们的环境和应用就像copy了一份一样完美运行! 不用再为环境配置而烦心。
* 简单快速
    目前无论国内还是国外基于容器技术的容器云服务公司越来越多,包括阿里云也在今年推出了容器服务。原因就是容器在现在企业应用要求快速迭代、快速
    发布时可以做到一键发布上线。做到真正意义上的持续集成（CI）和持续发布（CD）!
* 跨平台
    容器是在系统之上虚拟化出来的系统, 具有很强的跨平台性,docker目前已经支持Linux、Windows、Mac等系统
* 安全性
    容器是在真实系统上采用虚拟化技术虚拟出来的,所以和真实系统相对隔离,可以保证真实系统的安全
    
# 关于LNMP-Docker使用

## 依赖

LNMP-Docker 并不是我的创造，而只是因为一直频繁的被nginx+php的环境配置所困扰，刚好有遇到了docker，心中窃喜！终于可以将某个web应用环境以分发的形式共享给团队开发人员。并且这个环境可以保持`开发`-`测试`-`生产` 环境的一致；降低运维成本；做的CI，CD（持续集成和持续发布）

LNMP-Docker 主要都是基于 [bitnami](https://github.com/bitnami) 所释放/分享出来的相关镜像：

  * [bitnami-docker-nginx](https://github.com/bitnami/bitnami-docker-nginx)
  * [bitnami-docker-php-fpm](https://github.com/bitnami/bitnami-docker-php-fpm)
  * daocloud/wangxb/mysql - docker pull daocloud.io/wangxb/mysql:5.6
更多扩展可根据项目需要自行扩展

## 规范

LNMP-Docker 是使用 `docker-compose` 应用编排进行的，在使用执行请确认你的系统中已经安装了：`docker` 和 `docker-compose`  

  * 克隆 `$ git clone git@github.com:wxb/Docker-LNMP.git`
  * 修改名字 `$ mv Docker-LNMP {项目名} && cd {项目名}}`
  * 拉取你的项目放到workspace目录下并改名app `$ git clone git@github.com:wxb/xxx.git && mv xxx app`
  * 配置虚拟主机 `$ cp vhost-example.conf vhost.conf` 然后修改`vhost.conf`文件
  * 在需要对`php`或者`php-fpm`进行个性配置时，将`php-fpm/conf/`目录下相应`*.example`复制一份改名为：`php-fpm/conf/php.ini`和`php-fpm/conf/php-fpm.conf`进行个性配置
  * 如果有通过composer需要安装的依赖, 请将依赖安装在**composer-pkgs**文件夹中,具体说明参见[composer-pkgs](./composer-pkgs/README.md)
  * 启动环境 `docker-compose up -d`


## 说明

LNMP-Docker 只是我在了解了docker之后进行的简单尝试，使用过程中还可能会出现很多的问题，后面我会逐步完善；不过现在我已经对docker技术充满了想法，只是相关知识的缺乏还不能更好的利用；待之后努力学习，争取用号docker，提升开发-发布环境一致性。

同时，也尝试配合使用[daocloud.com](https://dashboard.daocloud.io/) 对项目进行docker形式的持续集成（CI）和持续发布（CD）。后期如果自己使用的这套构建流完善之后，我会写一篇进行详细介绍，欢迎大家使用
