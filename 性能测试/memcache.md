## memcache性能测试脚本

shell测试命令：

	time echo "stats" |nc 10.70.63.155 11211

完成时间应该小于0.01秒
php测试代码：
```php
<?php
$mem=new Memcache();
$mem->addServer ("10.70.63.155",11211,false,1,100);
$start=microtime(true);
$str= str_repeat ("a",1024);//1k数据
for($i=0;$i<10000;$i++){
   $mem->set("test_$i",$str,0,30);
   $mem->get("test_$i");
}
echo microtime(true)-$start;
?>
```
完成时间应该在10-15秒
