## iftop监控与服务器交互的ip流量

观察流量用，可以细化到ip和端口，对于发现网络瓶颈有很大帮助

### 界面：

![](http://i.imgur.com/MK7Q8HP.png)

### 安装：

机器如果有epel源则直接安装即可

```bash
yum install -y iftop
```

### 使用：

使用以下命令即可进入一个类似top的界面

	iftop -i [网卡名]

快捷键：

	h		显示帮助
	p		切换端口
	P		切换暂停
	n		切换ip的dns解析
	N		切换端口dns解析