# PHP必知必会100点
----

>参考：[Markdown基本语法](https://www.jianshu.com/p/191d1e21f7ed)  
>前提：php 7.2

* empty()判断空值时的特例
```
<?php
$val = '0';
var_dump(empty($val)); //true

```

* display_errors()
* error_reporting(E_ALL)
* date_default_timezone_set('UTC');
* & | ~ 的含义
* << >> 的含义
* composer.json版本限定符
* xdebug_debug_zval()
* memory_get_usage()
* php中引用的含义
* php写时拷贝
* php的普通赋值和引用赋值
* static::延迟绑定
* strtotime的特殊用法
```
<?php
echo strtotime("now"), "\n";
echo strtotime("10 September 2000"), "\n";
echo strtotime("+1 day"), "\n";
echo strtotime("+1 week"), "\n";
echo strtotime("+1 week 2 days 4 hours 2 seconds"), "\n";
echo strtotime("next Thursday"), "\n";
echo strtotime("last Monday"), "\n";
```
* $_SERVER['REQUEST_TIME'] 中保存了发起该请求时刻的时间戳
* mktime()的用法
* 