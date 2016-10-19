# Laravel PHP Framework


## 1 开发环境

### 1.1 创建新项目

```shell
// 安装laravel installer
composer global require "laravel/installer"
// 新建项目
laravel new blog
// 项目启动，默认的为localhost:8080
php artisan serve
```


### 1.1 配置相关

* 应用的入口文件：public/index.php
* 配置文件目录：config
* 目录权限： storage 和 bootstrap/cache 需要写权限；
* Application Key: 通过Composer or the Laravel installer会自动生成key(命令php artisan key:generate)，添加这个key到.env中，如果没有就在根目录下创建此文件。
     此设置的主要目的：保证sessions and other encrypted data数据的安全。
* 其他配置：
     config/app.php 中timezone,local等配置可以根据应用情况修改；
     cache
     database
     session等

### 1.1.1 获取config/下配置信息

可以使用全局函数config来获取config目录下文件配置信息，格式为：fileName.configkey。 如果在配置文件中没有配置信息，可以在config函数中配置默认值。

```shell
$value = config('app.timezone');
```

在程序 运行的时候，也可以通过config进行配置的设置；

```shell
config(['app.timezone' => 'America/Chicago']);
```

### 1.1.2 环境参数配置

在开发环境和生产环境中，获取不同的配置信息；laravel使用了DotEnv的php库来设置不同环境的设置； 如果通过composer安装laravel的，那么.evn会在根目录下自动生成；否则需要自动生成；

**获取环境参数配置**
默认的.env中的所有的参数都是在请求进入的时候被加载到$_ENV超全局变量中。 但是，在应用中可以使用env帮助函数来获取配置文件中的信息。

```shell
// config配置中使用了，如下的配置。第二个参数为默认值
'debug' => env('APP_DEBUG', false),
```

    **注意**： .env是不允许被提交到源代码中的。 不同的开发者使用.env是不一样的。 共同的配置可以添加到.evn.example中，供组内成员参考。

**决定当前环境变量**
当前的环境是由.env中的APP_ENV变量决定的。 你可以使用门面类App的environment方法获取到此参数；

```shell
$environment = App::environment();
```

此方法可以传入参数，来对当前的环境变量是否匹配指定的值。

```shell
    if (App::environment(\'local\')) {
        // The environment is local
    }

    if (App::environment(\'local\', \'staging\')) {
        // The environment is either local OR staging...
    }
```

### 1.1.3 缓存配置

为了提高应用的响应速度，我们可以使用Artisan命令config:cache将所有的配置文件缓存到单个的文件中。
在生产环境中，我们可以执行`php artisan config:cache`命令。但是在开发环境中，不建议执行此命令，开发中配置文件变更的频率比较大。

### 1.1.4 维护模式

当应用处于维护的状态时，所有的请求都会被指向一个自定义的页面。在更新或者维护应用的时候，这样可以很简单的停止应用。在应用的中间件中，维护模式的检查是其中的一个默认组件。如果应用在维护模式下，一个MaintenceModeException异常会使用503状态抛出。

要启用维护模式，仅需要执行Artisan命令down:

```shell
php artisan down
```

在上述命令后边可以添加message和retry选项， message是用来显示自定义信息，retry用来给响应添加Retry-After Http头；

```shell
php artisan down --message='Upgrading Database' --retry=60
```

重新启用应用，执行如下命令：

```shell
php artisan up
```

维护模式响应模板在resources/views/errors/503.blade.php, 可以随意修改。
维护模式下，队列任务会停止执行；
由于维护模式是需要停止应用，因此为了更好的启动应用，可以使用Envoyer来实现不需要关闭应用的操作。

## 2 生产环境


### 2.1 配置相关