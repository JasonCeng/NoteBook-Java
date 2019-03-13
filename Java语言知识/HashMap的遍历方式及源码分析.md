# HashMap的遍历方式及源码分析

## 1.Map的遍历方式
（1）for each map.keySet(),再调用get获取
```java
Map<String, String> map = new HashMap<String, String>();
for(String key : map.keySet()) {
  map.get(key);
}
```
