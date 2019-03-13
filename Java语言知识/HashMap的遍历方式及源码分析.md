# HashMap的遍历方式及源码分析

## 1.Map的遍历方式
（1）for each map.keySet(),再调用get获取
```java
Map<String, String> map = new HashMap<String, String>();
for(String key : map.keySet()) {
  map.get(key);
}
```
（2）for each map.entrySet()
```java
Map<String, String> map = new HashMap<String, String>();
for(Entry<String, String> entry : map.entrySet()) {
  entry.getKey();
  entry.getValue();
}
```
（3）显示调用map.entrySet()的集合迭代器
```java
Iterator<Map.Entry<String, String>> iterator = map.entrySet().iterator();
while(iterator.hashNext()){
  Map.Entry<String, String> entry = iterator.next();
  entry.getKey();
  entry.getValue();
}
```
（4）for each map.entrySet()，用临时变量保存map.entrySet()（第（2）种的变形）
```java
Set<Entry<String, String>> entrySet = map.entrySet();
for(Entry<String, String> entry : entrySet){
  entry.getKey();
  entry.getValue();
}
```
（5）通过map.values()遍历所有的value，但不能遍历key
```java
Map<String, String> map = new HashMap<String, String>();
for(String value : map.values()){
  return value;
}
```
