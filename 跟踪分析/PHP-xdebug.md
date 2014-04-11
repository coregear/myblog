## 使用XDebug和WinCacheGrind发现php性能瓶颈

### 介绍：

使用apache的module方式启动php后只有一个httpd主进程，这时如果php程序出现问题，例如连接数据库或者抓取web内容等动作，或者反复执行某些消耗cpu的语句等情况就会导致整个httpd进程卡住。发生这种情况后本来如果没有程序员配合就非常难查出问题，但使用下面的方法运维还是有办法独立判断出问题所在的（对付喜欢扯皮的程序员最管用了）。

大致结构如下：

![](http://i.imgur.com/GYJKeqf.png)

### 安装：
1. 下载PHP的XDebug扩展，网址：http://xdebug.org/
1. 编译安装：
```bash
wget http://xdebug.org/files/xdebug-2.2.3.tgz
tar -xzf xdebug-2.2.3.tgz
cd xdebug-2.2.3
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config --enable-xdebug
make
cp modules/xdebug.so /usr/local/php/lib/php/extensions/no-debug-zts-20090626/
```
1. 修改php配置：
注意此处分为**zend_extension**和**zend_extension_ts**注意区分一下(注意你的php是不是thread safe版的)
```bash
vi /usr/local/webserver/php/lib/php.ini
zend_extension="/usr/local/webserver/php/lib/php/extensions/no-debug-zts-20090626/xdebug.so"
xdebug.profiler_enable=on
xdebug.trace_output_dir="/tmp/xdebug"
xdebug.profiler_output_dir="/tmp/xdebug"
xdebug.profiler_output_name="cachegrind.out"
```
1. 添加目录权限，**重启apache**：
```bash
mkdir -p /tmp/xdebug
chmod 777 /tmp/xdebug
/usr/local/apache/bin/apachectl -k restart
```

### 分析：
1. 从服务器的/tmp/xdebug路径下载生成的性能日志
1. 打开WinCacheGrind分析

### 实例：

看到php:curl_exec占用了很多时间，进一步分析，找到调用该方法的文件
查看该文件中的占用时间的方法，发现是curl的url占用时间过长，改为内网IP后故障解决

![](http://i.imgur.com/axGjbyu.png)

![](http://i.imgur.com/UqUcFLm.png)