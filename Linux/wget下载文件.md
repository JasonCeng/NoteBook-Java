# wget下载文件
从有数字规律的网址抓取网页并保存在当前目录。假设网址为 http://test/0.xml， 其中这个数字可以递增到100。
```shell
for((i=0;i<100;++i));
do  
  wget http://test/$i.xml;
done
```
