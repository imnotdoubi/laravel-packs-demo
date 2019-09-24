# laravel-packs-demo
laravel开发、本地测试、发布自己的 Composer扩展包示例

## 安装
```
$ composer require yht/demo
```
### 使用

```php

use Yht\Demo\Demo;

$demo = new Demo();

$demo->index();//输入结果：云海天测试发布 


```
## 创建过程

### 扩展包开发过程


```php
1、首先创建一个新的 Laravel 
composer create-project laravel/laravel laradmin -vvv

2、接下来在此项目中，创建目录 packages/{your_name}/{your_package_name}

yht/demo (vendor/name) 为我们要发布的 Laravel 包，yht 对应为 username，demo 对应为 项目名
跟目录下面创建packages/yht/demo  这3个文件夹
然后demo 下创建src目录 src 这里就是我们放置代码的地方
mkdir src

3、demo 文件夹下执行 composer init   
这里type一般选择project/library，license一般选择MIT协议

4、修改demo文件夹下composer.json  
   "autoload": {
            "psr-4": {
                "Yht\\Demo\\": "src/"
            }
        },
    "autoload-dev": {
            "psr-4": {
                "Yht\\Demo\\Tests\\": "tests/"
       },
5、在 yht/demo 下的 src 目录创建 DemoServiceProvider.php 文件和 Demo.php ：
		DemoServiceProvider.php 文件内容
		<?php
		namespace Yht\Demo;

		use Illuminate\Support\ServiceProvider;

		class DemoServiceProvider extends ServiceProvider
		{
		    public function boot()
		    {
		        //
		    }

		    public function register()
		    {
		        $this->app->singleton('demo', function () {
		            return new Demo;
		        });
		    }
		}

		Demo.php内容
		<?php

		namespace Yht\Demo;

		class Demo
		{
		    public function index()
		    {
		        echo '云海天测试发布' . "\n";
		    }
		}


6、修改 根目录项目下的 composer.json 文件：

		"autoload": {
		        "psr-4": {
		            "Yht\\Demo\\": "packages/yht/demo/src/"
		        },
		    },

7、修改confing/app.php 添加

	Yht\Demo\DemoServiceProvider::class,

8、执行 composer dumpautoload

9、web.php 中修改一下（本地测试）//http://127.0.0.1/   出现：云海天测试发布 说明本地成功
	Route::get('/', function () {
	    app('demo')->index();
	});

```

### 扩展包发布

1.	创建 github.com 帐号 2.	创建 github.com 工程  3.	创建 packagist.org 帐号

```php
1、将文件夹demo 下的所有文件发布到github上

2 访问 Packagist 官网，登录后，点击右上角Submit按钮，进入发布向导
记录下 GitHub 版本库的地址，注意是 HTTPS

3、发布成功后版本默认是  composer require yht/demo:dev-master

```

### 验证包安装


```php
composer require yht/demo dev-master

use Yht\Demo\Demo;

$demo = new Demo();

$demo->index();
//出现：云海天测试发布   恭喜你成功！
```