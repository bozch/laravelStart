# 目录结构

默认的laravel程序架构给开发小型或者大型的应用一个高的起点。当然你可以根据个人喜好来组织你的应用。Laravel对任何类的加载都没有做限制，只要composer能够加载类就可以。

**模型目录在哪里？**
很多开发者在开始使用laravel的时候都会对缺少model模型目录感到疑惑。但是，缺少此目录是有意这样的。 model模型对于不同的人意义不同。一些开发者把model看做业务逻辑；另一些把它看做和关系型数据交互的类。
基于此，默认的我们把Eloquent model模型放到了app目录下，也允许开发者将他们放到其他目录下。

## 根目录

### 1 app 目录
    此目录包含了所有的应用代码
### 2 bootstrap 目录
    此目录中包含了引导 框架和配置 加载的文件。还包含了cache目录，这个目录中包含了框架产生的用来进行性能优化的文件，例如路由和服务缓存文件。
### 3 config 目录
     应用配置文件都在此；
### 4 database 目录
    此目录包含了数据库迁移和种子文件，如果可以，你可以把SQLite数据库放在此处；
### 5 public 目录
    此目录包含了index.php，它接受所有进入应用的请求。 此外此目录还有图片、JavaScript和css文件目录；
### 6 resoures 目录
    此目录包含了视图文件，还有原始的、未编译的资源文件，例如Less,SAss或者JavaScript。此外所有的语言文件也在此目录下；
### 7 routes 目录
   routes目录包含了应用中所有的路由文件。默认的、laravel包含了三个路由文件：web.php, api.php和console.php;

   
### 8 storage 目录   

## 应用目录 