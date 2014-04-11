## tcpdump抓包并使用wireshark分析

用来解决一些涉及网络通信的疑难杂症，费时间，噪音比较多，没有深厚基础不能准确定位问题，功力不到不推荐使用。如果相关软件有debug模式建议打开，配合log分析，这样效率会高很多。

### 使用：

linux自带该命令，如果无法使用yum安装即可

	tcpdump -i <interface> -s 65535 -w <some-file>

wireshark分析参考：
1. http://fangxin.blog.51cto.com/1125131/735178
1. http://vipscu.blog.163.com/blog/static/181808372201131141348134/
