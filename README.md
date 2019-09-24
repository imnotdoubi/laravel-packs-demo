# laravel-packs-demo
laravel开发、本地测试、发布自己的 Composer扩展包示例

## 安装

使用 Composer 安装:

```
$ composer require yht/demo
```
### 使用

```php

use Yht\Demo\Demo;

$demo = new Demo();

$demo->index();//输入结果：云海天测试发布 


```