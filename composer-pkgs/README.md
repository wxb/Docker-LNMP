# composer依赖管理

Composer 不是一个包管理器。是的，它涉及 "packages" 和 "libraries"，但它在每个项目的基础上进行管理，
在你项目的某个目录中（例如 vendor）进行安装。默认情况下它不会在全局安装任何东西。因此，这仅仅是一个依赖管理。

* [composer官方文档](https://getcomposer.org/)

* [composer中文文档](http://docs.phpcomposer.com/)


# Packageist
* [Packageist官方镜像](https://packagist.org/)
* [Packageist中国镜像](http://pkg.phpcomposer.com/)

# composer-pkgs怎么用?

* composer-pkgs中的php包、类库等代码,会在docker-LNMP环境中php.ini中引入
    ```
    bitnami提供的镜像引入了这个目录
    ; UNIX: "/path1:/path2"
    include_path = ".:/opt/bitnami/php/lib/php"
    
    我们在配置php-fpm的时候只要将composer-pkgs目录挂在到对应目录下即可引入到php中
    phpfpm:
        restart: always
        image: bitnami/php-fpm:5.6.18-0
        ports:
            - "9000:9000"
        expose:
            - "9000"
        volumes:
            - $PWD/app:/app
            - $PWD/php-fpm/conf:/bitnami/php-fpm/conf
            - $PWD/logs/php-fpm:/bitnami/php-fpm/logs
            - $PWD/composer-pkgs:/opt/bitnami/php/lib/php/composer-pkgs
        links:
            - "mysql:mysql_machine"
    
    
    ```

* 在composer-pkgs中使用composer安装相关依赖
    ```
    >composer init
    >composer require  topthink/framework:^5.0
    ```
    或者根据已有`composer.json`来安装依赖
    ```
    >composer install
    ```

* 当我们需要使用的时候就可以直接在代码中这样引入, 下面举例thinkphp的入口文件

    ```php
    <?php
    // +----------------------------------------------------------------------
    // | ThinkPHP [ WE CAN DO IT JUST THINK ]
    // +----------------------------------------------------------------------
    // | Copyright (c) 2006-2016 http://thinkphp.cn All rights reserved.
    // +----------------------------------------------------------------------
    // | Licensed ( http://www.apache.org/licenses/LICENSE-2.0 )
    // +----------------------------------------------------------------------
    // | Author: liu21st <liu21st@gmail.com>
    // +----------------------------------------------------------------------
    
    // [ 应用入口文件 ]
    
    // 定义应用目录
    define('APP_PATH', __DIR__ . '/../app/');
    
    // 加载框架引导文件
    //require __DIR__ . '/../thinkphp/start.php';
    // 这里用我们已经引入到php的核心类库代替
    require 'composer-pkgs/thinkphp/start.php';  
    
    ```



