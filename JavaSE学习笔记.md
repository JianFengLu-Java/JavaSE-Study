# 01->String类

[TOC]

------

### String类中的常用方法（也可以参考API文档）

- char charAt(int index):返回索引处的char值。

  ```JAva
  String a = "abc";
  char c = a.charAt(2);//返回值类型为char；
  System.out.println(c);//c
  ```

- int length():获取字符串的长度。

  ```Java
  String a = "abc";
  int i = a.length();
  System.out.println(i);//3
  ```

- boolean isEmpty():判断字符串是否是空字符串，如果length()为0，就是空字符串。

  ```Java
  String a = "";
  System.out.println(a.isEmpty());//true
  ```

- boolean equals(String s):判断两个字符串是否相等。

  ```Java
  String a = "123";
  String b = "123";
  System.out.println(a.equals(b));//true
  ```

- boolean equalsIsIgnoreCase(String s1):判断两个字符串是否相等，忽略大小写。

  ```Java
  String bigWord = "ABC";
  String littleWord = "abc";
  System.out.println(bigWord.equalsIsIgnoreCase(littleWord));//true
  ```

- boolean contains(CharSequence s):判断字符串中是否包含某个子字符串。

  ```
  String a = "123456";
  String b = ""234;
  System.out.println(a.contains(b));//true
  ```


------

# 基本数据类型&包装类

| 基本数据类型 |      对应包装类       |
| :----------: | :-------------------: |
|    `byte`    |   `java.lang.Byte`    |
|    `char`    | `java.lang.Character` |
|    `int`     |  `java.lang.Integer`  |
|   `short`    |   `java.lang.Short`   |
|    `long`    |   `java.lang.Long`    |
|   `float`    |   `java.lang.Float`   |
|   `double`   |  `java.lang.Double`   |
|  `boolean`   |  `java.lang.Boolean`  |

**包装类属于引用类型，为了方便开发**

- 如果在调用的方法里传的参数是Object类型的对象，则没有办法传入参数了，所以现在需要将数据包装成Object类型

- ```java
  public class IntegerTest01{
    public static void main(String[] args){
      //定义要传的值
      int value = 10;
      MyInteger integer = new MyInteger(value);
      method(integer);
    }
    
    public void method(Object obj){	
      //这里的参数是Object类型，但是我要将int数据传进来，该怎么做呢？
    	//将int基本类型数据包装成Object类，再传进来～
      //然后将Object类对象向下转型成MyInteger对象
      MyInteger myInteger = (MyInteger)obj;
      //再调用getValue()方法
      System.out.pringln(myInteger.getValue());
    }
  }
  ```

  ```java
  public class MyInteger{
    //这个类是默认集成所有类的老祖宗：Object基类的。
    //所以这个int值传进来以后，它就被包装成一个Object类的对象了。
    private final int value;
    public MyInteger(int value){
      this.value = value;
    }
    //提供set、get方法访问成员变量
    public int getValue(){
      return value;
    }
    
    public void setValue(int value){
      this.value = value;
    }
  }
  ```

- 包装类的实现原理⬆️

### 装箱与拆箱

#### 拆箱(unboxing)

- Byte、Short、Integer、Long...等六个数字型包装类都继承了Number类

- 因此这些类中都有以下方法

  | Method                   |
  | ------------------------ |
  | byteValue()-> `byte`     |
  | shortValue()-> `short`   |
  | intValue()-> `int`       |
  | longValue()-> `long`     |
  | floatValue()-> `float`   |
  | doubleValue()-> `double` |

  这些方法的作用是将**包装类型数据**转换成**基本类型数据**，调用以上六个方法中任何一个都叫<u>*‘拆箱’*</u>

- Boolean的拆箱方法是：booleanValue()
- Charaction的拆箱方法是：charValue()

### 枚举类型

### UUID

- 工具类java.util.UUID
- UUID是一种软件构建标准，用来生成具有唯一性的ID
- UUID具有以下特点：
  - UUID可以在分布式系统中生成唯一标识符，避免因主键冲突等造成的问题带来的麻烦。
  - UUID具有足够的唯一性，重复的概率相当低，UUID使用的是128位数字
  - UUID在生成时不依赖任何中央控制器或者数据库服务器，可以在本地方便快捷的生成唯一标识符
  - UUID生成后可以被许多其他的编程语言支持，并方便的转化为字符串的形式表示，适用于多种应用场景。
  - 在Java开发中，UUID的作用非常广泛，可以用于生成数据表主键，场景标识符、链路追踪、缓存key等
- 使用：
  - 生成UUID: static UUID randomUUID();
  - 将UUID转换为字符串:  String toString();

### 集合

#### 集合的概念

- 什么是集合？
  - 集合是一种容器，用来组织管理数据的，非常重要。
  - Java的集合框架对应的这一套类库，就是对各种数据结构的实现。
  - 每一个集合类底层采取的数据结构不同。
  - 不用程序员去实现底层数据结构，通过Java集合的类库，直接用就可以了。

- 默认情况下，如果不使用泛型的话，集合可以储存任何类型的引用，只要是Object的子类都可以储存。
- Java集合框架下的类都在`java.util`包下
- Java集合框架分为两部分：
  - Collection结构：元素以单个形式储存
  - Map结构：元素以键值对的形式储存

#### Collection继承结构

##### 示意图：

<img src="/Users/lujianfeng/Library/Application Support/typora-user-images/image-20250103110405157.png" alt="image-20250103110405157" style="zoom:50%;" />

##### Collection接口的通用方法：

| 序号 | 返回类型  |         方法         |                  作用                  |
| ---- | :-------: | :------------------: | :------------------------------------: |
| 1    | `boolean` |       add(E e)       |            向集合中添加元素            |
| 2    |   `int`   |        size()        |              获取元素个数              |
| 3    | `boolean` | addAll(Collection c) | 将参数集合中的元素全部加入到当前集合中 |
| 4    | `boolean` |  contains(Object o)  |        判断集合中是否包含对象o         |
| 5    | `boolean` |   remove(Object o)   |           从集合中删除对象o            |
| 6    |  `void`   |       clear()        |                清空集合                |
| 7    | `boolean` |      isEmpty()       |        判断集合中的元素是否为0         |
| 8    | `Object`  |      toArray()       |          将集合转换成一堆数组          |

##### Collection的遍历/迭代（集合的通用遍历方式）

- 第一步：获取当前集合依赖的迭代器对象Iterator

  ```java
  Iterator it = collection.iterator();
  ```

- 第二步：编写循环，循环条件是，当前光标指向的位置是否存在元素

  ```java
  while(it.hasNext()){//hasNext的返回值是布尔类型，表示如果在当前光标下有元素存在就返回true。
  
  }
  ```

- 第三步：如果存在，将元素返回，然后将光标下移动一位

  ```java
  Object o = it.next();
  ```

  
