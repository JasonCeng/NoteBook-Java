# String之equals()方法
```Java
/**
     * Compares this string to the specified object.  The result is {@code
     * true} if and only if the argument is not {@code null} and is a {@code
     * String} object that represents the same sequence of characters as this
     * object.
     *
     * 译：将给定的String与指定的对象进行比较。结果是{@code true}当且仅当参数不
     * 是{@code null}且是{@code String}对象时，它表示与此对象相同的字符序列。
     *
     * @param  anObject
     *         The object to compare this {@code String} against
     *         要将此{@code String}与之进行比较的对象
     *
     * @return  {@code true} if the given object represents a {@code String}
     *          equivalent to this string, {@code false} otherwise
     *          {@code true}如果给定对象表示与此字符串等效的{@code String}，
     *          否则为{@code false}    
     *
     * @see  #compareTo(String)
     * @see  #equalsIgnoreCase(String)
     */
    public boolean equals(Object anObject) {
      /**
      * == 表示比较两个对象的首地址
      * 如果当前对象（this）的首地址与给定对象（anObject）的首地址相同
      * 则return true;
      */
        if (this == anObject) {
            return true;
        }
        /**
        * 1.首先判断给定对象（anObject）是否为String类型
        *       如果是则进行下一步操作，否则返回false
        * 2.先将anObject赋值给局部变量String类型的anotherString
        *   并记录当前字符串对象（this）的长度n
        * 3.然后判断n与anotherString长度是否相同
        *      如果相同则进行下一步操作，否则结束该if块return false;
        * 4.将当前字符串对象（this）的值与anotherString的值分别存储到char
        * 类型数组v1、v2中
        * 5.定义一个游标i，用于判断v1、v2中各个值是否相同
        * 6.遍历判断v1、v2各个元素是否相等，只要有一个元素不相等，就return false
        *      通过n控制while循环，通过i++遍历数组V1、V2
        */
        if (anObject instanceof String) { // 1
            String anotherString = (String)anObject;  // 2
            int n = value.length;
            if (n == anotherString.value.length) { // 3
                char v1[] = value; // 4
                char v2[] = anotherString.value;
                int i = 0; // 5
                while (n-- != 0) { // 6
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```
