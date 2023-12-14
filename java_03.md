# 内部类：
  * 内部类，写在一个类里面的类
    * 内部类可以直接访问外部类的成员对象<mark>包括私有
    * 外部类要访问内部类的成员必须创建方法***方法内部创建内部类的对象***
        > 内部类在逻辑上一定是和外部类是顺承的逻辑关系
    * 内部类的**分类**：
      * 成员内部类：写在成员位置（类中方法外）（类比成员的使用）
        * 成员内部类的使用：
          * <mark>1.正常情况</mark>可以通过点运算符先调用外部类再调用内部类。从而像单一类一样创建对象
          <img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-14%20191659.png">
          * <mark>2.若内部类被private修饰</mark>可以编写外部类的成员方法，方法将该类return出去
          <img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-14%20193027.png">
          <u>上图中左端代码即为该成员方法</u><br/>
          <u>右端代码中o是Outer的实例，调用Inner的父类Object来承接inner的类型（**private修饰**）</u><br/>
          <u>下图中，左第12行代码，```Outer.this```实际上代指一种外部类的实例（这里的this在堆的内部类空间中存储）</u>
          <img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E4%BA%91%E9%A1%B6%E7%AC%94%E8%AE%B0/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-14%20205021.png">
    * 静态内部类：
      * 用static修饰：只能访问外部类中的静态变量和静态方法，访问非静态需要创建对象
      ```java
      Outer.Inner oi = new Outer.Inner();//创建静态内部类对象的方式
      Outer.Inner.show();//调用静态内部类的静态方法
      ```
    * 局部内部类（了解）：
      * 将内部类定义在***方法里面***叫做局部内部类 
      > 无论是局部变量还是局部内部类都只能用final修饰或者不添加修饰（如：public private protected）
      * 外界无法直接使用局部内部类或局部变量（需要在方法内部创建对象）
      * 可以直接访问外部成员，也可以直接访问方法内局部变量
    * 匿名内部类：
      * 隐藏了名字的内部类，可以写在成员位置也可以在局部位置
      ```java
      new Swim(){
        @Override//关于接口方法的重写（覆盖，覆写）
        public void swim(){
          System.out.println("输出语句");
        }
      };// 实现关系  方法重写  创建对象（实质上是一个对象类型为Swim）（new ）  Swim是一个接口被该匿名类实现

      -------------------------------------------------

      //匿名类中方法的调用：

      method(

        new Swim(){
          @Override
          public void swim(){
              System.out.println("输出语句");
          }
        };


      );//在外部类内部定义方法，该方法将匿名类当做参数、
      //在外部类外面调用该方法：
      public static void method(Swim a){//公开 静态方法
          a.swim();
      }

      -------------------------------------------------

      new Swim(){
        @Override//关于接口方法的重写（覆盖，覆写）
        public void swim(){
          System.out.println("输出语句");
        }
      }.swim();//swim方法也可以这样用。

      ```
      > 匿名内部类实际上有名字例如（```外部类$1```）（字节码文件）

#  集合：
  *  集合长度可变
  *  只能存引用数据类型，基本数据类型得换成对应的包装类
  *  泛型：限定集合中存储数据的类型
### Collection类集合（单列集合）（一次添加一个数据）:
***分为List和Set两类***<p></p>
```java
Collection<String> coll = new ArrayList<>();//Collection是单列集合顶层接口，用此处多态的方式创建ArrayList集合为了好演示（且该集合实现Collection接口）
//正常创建对象就行
//对应方法：
coll.add("aaa");//会查看是否在集合中重复出现返回true或false
coll.addAll("a","b","c");
coll.clear();//清空集合
coll.remove("aaa");//删除元素
coll.contains("aaa");//底层依赖equals方法实现查找匹配,判断是否包含
coll.isEmpty();//判断是否为空
int size = coll.size();//返回该集合的长度
```

*****
* LIST(有序，可重复，有索引):（collections接口的实现类）
  * ArrayList:
```java
ArrayList<String> list =  new ArrayList<>();//创建集合（java的一种集合）一种字符串类型的集合的创建
list.add("element");//添加元素
list.remove("element");//删除元素（均返回布尔值）（参数值可以是元素也可以是下标值）
list.set(1,"removement");//替换覆盖元素
String s= list.get(1);//查询元素
list.size();//集合中的最大索引值
```
*****
* SET(无序，不重复，无索引):


### Map类集合（双列集合）（一次添加一对数据）：
> 键值对的形式存储，键不可以重复（唯一的），值可以重复，键与值一一对应（一个键值对Java中叫做Entry对象）
```java
Map<String,String> m = new HashMap<>();
m.put("key","value");//添加数据，键如果已经存在则会把原有的键值对对象覆盖，会把覆盖的值进行返回。键不存在直接添加，返回null
m.remove("key");//无返回值，直接删除该键值对
m.clear();//清空
m.containsKey("key");//返回布尔值，传入键
m.containsValue("value");//返回布尔值，传入值
m.isEmpty();//返回布尔值观察该集合是否为空
m.size();//返回长度
m.get(key值);//传入key值后会返回value值。

//对于map的for-each遍历:
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);
map.put("C", 3);
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
}
```






# 异常（程序出现的问题）：
> `java.lang.Throwable`:分为***Error***和***Exception***两类<p></p>

* ERROR（错误）: 系统级别的错误，程序员不需要管理，出现后将由SUN公司进行封装
* EXCEPTION（顶层父类）（异常）:
  * （**异常可以作为一个特殊的返回值以便知道调用者的执行情况**）
  * 运行时异常：RuntimeException本身及其子类。（编译时不处理，运行时报错）（***数组越界***）<mark>代码出错导致程序出现问题</mark>
  * 编译时异常：直接继承于Exception（处理否则代码报错运行不了）<mark>编译阶段JAVA不会运行代码只检查语法错误，提醒检查本地信息 </mark>
#### JVM 默认处理异常的方式：程序停止，红字控制台打印异常
#### 自己处理异常（捕获异常）：
```java
try{
  //可能出现异常的代码。
  System.out.println(arr[10]);//若此处出现异常，程序会在这里创建一个ArrayIndexOutOfBoundsException对象（和下面throw异常异曲同工）
  //拿着这个对象与下面小括号里面的e对比看是否可以接收--------接收不了交给JVM默认处理
  System.out.println("这句程序也就不执行了，上面直接转catch了");//多异常除外，意味着try-catch没有执行完毕
}catch(ArrayIndexOutOfBoundsException/*异常类名*/ ,e/*变量名*/){//存在父子关系的话，父类在下面，子类在上面
  //如果出现异常我该怎么办的代码
  System.out.println("索引越界");
}
```
#### 异常的常见方法：
Throwable的成员方法。<p></p>
```java
try{
  System.out.println(arr[10]);
}catch(Exception,e){
  e.printStackTrace();//打印信息，包含下面两个信息之和以及异常所在行数
  String msg = e.getMessage();//异常简短描述
  String str = e.toString();//异常的名字+信息
}
```


#### 抛出异常：
> throws throw

* ***throws***:写在方法定义处，声明,明示可能遇到的异常（RuntimeException不需要手动声明）。<p>选中ctrl+b查看源码</p>
* ***throw***：方法里面写，结束方法。
```java
throw new ArrayIndexOutOfBoundsException();//手动抛出异常，程序终止（将该异常与catch里面比较）
```

#### 自定义异常：
有时候异常没有匹配的，就得自己写
```java
public class NameFormatException extends RuntimeException{
  //自己写的：NameFormatException
  //完善构造方法alt+insert(空参+带参数构造)（带参构造参数是message报错信息（String））
}
```





# 文件：
```java
String str = "C:\\Users\\a.txt";//文件绝对路径（路径存在与否无所谓）
File f1 = new File(str);//创建File类的对象 
File f2 = new File(父串,子串);//第二种构造方法
File f2 = new File("D:\\aaa\\b.txt");//此路径假的，b.txt不存在
f1.isDirectory();
f1.isFile();
f1.exists();//是否存在
file（File类型对象）.mkdirs();//创建文件夹
src（File型对象）.createNewFile();//创建文件
f1.length();//文件大小，单位：字节（len/1024=KB;len/1024/1024=MB;len/1024/1024/1024=GB）
f1.getAbsolutePath();
f1.getPath();
f1.getName();//返回带后缀名称
f1.lastModfied();//文件最后修改时间
//创建，删除：
boolean b = f3.createNewFile();//方法返回true当且仅当文件不存在且成功创建(创建b.txt)
//父级路径不存在会报错
boolean c = f3.mkdir();//创建文件夹（只创建单级文件夹）
boolean c = f3.mkdirs();//创建文件夹（可以创建多级文件夹）
boolean v = f3.delete();//删除文件：直接删除；删除空文件夹：直接删除；删除有内容的文件夹：删除失败
```
```java
File f = new File("D:\\aaa");
File[] files = f.listFiles();//转成File类型的数组（包含隐藏文件夹）
for(File file : files){
  System.out.println(file);//输出遍历
}
```



