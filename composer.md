## 写一个属于自己的composer包
* 前面我们已经介绍了依赖包管理工具的便利，许许多多的先辈在开源工具的时候往往都会上传到`github`或者制作成`composer`包。
* 如果传到github，可以解决下载问题，但是与其他包的依赖关系却得不到自动处理，一般用于开源整个项目。
* composer包则适合在需要与其他依赖包配合的情况下使用。
####那么我们下面就来写一个自己的composer包吧，首先我们创建一个空的目录，并且运行以下命令初始化一个空白的composer包
```
composer init
```
* 需要输入包名
```
This command will guide you through creating your composer.json config.`
Package name (<vendor>/<name>) :
```
* 需要输入描述
* 需要输入最低稳定版本
````
Minimum Stability []:
该选项有可选值：stable, RC, beta, alpha, dev 一般填dev
````
* 需要输入开源协议
````
License []:
根据自己情况填写，我们填Apache
````

* 设置包需要依赖的其他环境或者包
````
Define your dependencies.
Would you like to define your dependencies (require) interactively [yes]?
如果需要设置依赖环境或者其他包 则输入yes回车，会让你搜索，我们这里给包设置php版本必须大于5.6，所以搜索php。

Enter the version constraint to require (or leave blank to use the latest version):
输入最低要求版本号 >=5.6.0
````

* 如果需要设置多个环境要求，则重复搜索填写即可，如果不需要了，则在Search for a package:不填写内容，直接回车即可

* 接下来设置依赖包
````
Would you like to define your dev dependencies (require-dev) interactively [yes]?
我们不需要 直接回车回车。
````
````
{
"name": "yancoo.cn/test",
"description": "This is a test package,form yancoo.cn,author is siam.",
"type": "l",
"require": {
"php": ">=5.6.0"
},
"license": "Apache",
"authors": [
{
"name": "宣言",
"email": "59419979@qq.com"
}
],
"minimum-stability": "dev"
}
Do you confirm generation [yes]?
````
确认信息，yes 回车 初始化完成

````
Do you confirm generation [yes]? yes
Would you like to install dependencies now [yes]? yes
````

````
{
    "name": "bailun/test",
    "description": "nonono",
    "type": "1",
    "require": {
        "php": ">=5.6.0"
    },
    "autoload": {
        "classmap": [
        ],
        "files": [
        ],
        "psr-4": {
            "Siam\\": "src/siam"
        }
    },
    "license": "apache",
    "authors": [
        {
            "name": "Berlain",
            "email": "522957318@qq.com"
        }
    ],
    "minimum-stability": "dev"
}
````
* 这里的路径需要根据你自己的来定，也可以参考以上写法即可。

* 写完之后需要运行一下命令行`composer dump-autoload`更新composer的命名空间与文件夹映射关系。
* 上一步骤非常重要 漏了就不正常执行了。
* 然后我们创建`src`文件夹，再创建`siam`文件夹，在里面创建`Test.php`文件
* 写上命名空间 Siam; 根据psr-4规范，类名要与文件名相同。

````
<?php
//Test.php文件
namespace Siam;
class Test
{
    function test()
    {
        echo "Form Test -> test()";
    }
}
````
* 再在最外层写下index.php测试文件，正确做法是创建demo文件夹 然后再写测试文件。
````
<?php
require "vendor/autoload.php";
$Test = new Siam\Test();
$Test->test();
````
* 可以根据你自己的想法来写类，只需要注意命名空间的层级与文件夹层级相同，类名与文件名相同即可自动加载。
## 上传composer包
