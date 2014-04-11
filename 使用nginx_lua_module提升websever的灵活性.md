## 使用nginx_lua_module提升websever的灵活性 ##

### 安装：###

1. 安装lua-jit
1. 下载ngx_devel_kit
1. 下载lua-nginx-module
1. 指定参数编译安装nginx

```bash
cd /usr/src
wget http://luajit.org/download/LuaJIT-2.0.2.tar.gz
tar zxvf LuaJIT-2.0.2.tar.gz
cd LuaJIT-2.0.2
make
make install PREFIX=/home/myself/lj2
cd ..

wget https://github.com/simpl/ngx_devel_kit/archive/v0.2.19.tar.gz
wget https://github.com/chaoslawful/lua-nginx-module/archive/v0.9.4.tar.gz
tar zxvf v0.2.19.tar.gz
tar zxvf v0.9.4.tar.gz

export LUAJIT_LIB=/usr/local/luajit/lib
export LUAJIT_INC=/usr/local/luajit/include/luajit-2.0

./configure --prefix=/usr/local/nginx --add-module=/usr/src/ngx_devel_kit-0.2.19 --add-module=/usr/src/lua-nginx-module-0.9.4
make -j2
make install
```



### 使用：###

lua语法：http://coolshell.cn/articles/10739.html

nginx教程：http://openresty.org/download/agentzh-nginx-tutorials-zhcn.html

测试：
http://10.70.56.146/test.com:8008/statuses/public_timeline.json?source=88882523327593

实例：http://www.cnblogs.com/wenbiao/p/3227998.html

手册：http://17173ops.com/2013/11/01/17173-ngx-lua-manual.shtml
