参考：http://huoding.com/2013/04/21/246


```bash
vi /etc/logrotate.d/nginx
/data/logs/nginx/*.log {
    daily
    dateext
    compress
    rotate 90
    sharedscripts
    postrotate
        kill -USR1 `cat /usr/local/nginx/logs/nginx.pid`
    endscript
}
```


- **dateext**       Archive  old versions of log files adding a daily extension like YYYYMMDD instead of simply adding a number.

- **sharedscripts**     Normally, prescript and postscript scripts are run for each log which is rotated and the absolute path tothe log file is passed as first argument to the script. That means a single script may be run multiple times for log file entries which match multiple files (such as the /var/log/news/* example).  If  sharedscripts  is  specified,  the scripts are only run once, no matter how many logs match the wildcarded pattern, and whole pattern is passed to them.  However, if none of the logs in the pattern require rotating,the  scripts  will not be run at all. This option overrides the nosharedscripts option and implies create option.

如果你等不及CRON，可以通过如下命令来手动执行：

```bash
logrotate -f /etc/logrotate.d/nginx
```

当然，正式执行前最好通过Debug选项来验证一下，这对调试也很重要：

```bash
logrotate -d -f /etc/logrotate.d/nginx
```
