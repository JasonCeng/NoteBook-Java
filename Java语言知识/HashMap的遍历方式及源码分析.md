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
## 2.HashMap五种遍历方式的性能测试及对比
以下是性能测试代码，会输出不同数量级大小的ArrayList和LinkedList各种遍历方式所花费的时间。
```java

```

## 3.HashMap源码分析
### （1）JDK7中的HashMap
HashMap底层维护一个数组，数组中的每一项都是一个Entry
```Java
transient Entry<k,v>[] table;
```
我们向HashMap中放置的对象实际上是存储在该数组当中。
而Map中的key，value则以Entry的形式存放在数组中。
```Java
static class Entery<K,V> implements Map.Entry<K,V> {
  final K key;
  V value;
  Entry<K,V> next;
  int hash;
}
```
