# tp-session-on-redis-to-share
a easy way to share session data between sub-domain sites in thinkphp
## 目的:

本例主要用来解决同一主域名下不同子域名(服务器)之间的session共享问题。比如说`www.mydomain.com`和`home.mydomain.com`之间的Session共享
---
## 鸣谢:
ThinkPHP的Session的Redis驱动来自[这里](http://www.thinkphp.cn/extend/547.html), 我稍有改动.
## 使用方法：
- 将`Redis.class.php`文件复制到ThinkPHP框架根目录下的`Library\Think\Session\Driver\`目录下
- 在`config.php`文件中增加配置如下:
```php
//Redis - SESSION设置
'SESSION_AUTO_START' => true,    //是否自动开启Session
'SESSION_TYPE' => 'Redis',    //session类型
'SESSION_OPTIONS' => ['domain'=> '.mydomain.com'], //请指定您的实际主域名, 此配置以实现子域名网站间session_id共享(通过cookie)
'SESSION_PERSISTENT' => 1,        //是否长连接(对于php来说0和1都一样)
'SESSION_CACHE_TIME' => 1,        //连接超时时间(秒)
'SESSION_EXPIRE' => 3600,        //session有效期(单位:秒) 0表示永久缓存
'SESSION_PREFIX' => 'tp_sess_',        //session前缀
'SESSION_REDIS_HOST' => '127.0.0.1', //分布式Redis,默认第一个为主服务器
'SESSION_REDIS_PORT' => '6379',           //端口,如果相同只填一个,用英文逗号分隔
'SESSION_REDIS_AUTH' => '',    //Redis auth认证(密钥中不能有逗号),如果相同只填一个,用英文逗号分隔
```
## 原理
可以参考[这里](http://blog.chinaunix.net/uid-14719335-id-2787868.html)