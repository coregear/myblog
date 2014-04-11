## http_load web性能测试

### 安装：

```bash
http://www.acme.com/software/http_load/http_load-12mar2006.tar.gz
make && make install
```

### 使用：

+ 测试脚本：

```bash
P="1 2 4 8 16 32 64 128 256 512 1024 2048 4096 8192"
S=10
U=url

for p in $P
do
        echo -n "$p|"
        ./http_load -s $S -p $p $U 2> /dev/null |grep "/sec\|bad" |tr -t "\n" "|"
        echo
done
```

+ 测试场景：虚拟机 2*E5-2650 4G nginx+lua

结果：

![](http://i.imgur.com/gDuupLU.png)

+ 测试场景：虚拟机 2*E5-2650 4G nginx 静态文件

结果：

![](http://i.imgur.com/OiZqF0a.png)

+ 测试场景：虚拟机 2*E5-2650 4G nginx+PHP

结果：

![](http://i.imgur.com/Jwun3bT.png)
