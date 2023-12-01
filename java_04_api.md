## 常用API：
###  Math类：    
<img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E4%BA%91%E9%A1%B6%E7%AC%94%E8%AE%B0/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-10-25%20211840.png">

###  System类：
> 时间原点：1970年1月1日8点<p></p>
> 1s==1000ms(毫秒)==1000000nm(纳秒)
```java
System.exit(0);//当我们需要把整个程序都结束的时候就调用该方法
long num = System.currentTimeMillis();//从时间原点到现在所经历的总的毫秒数（单位是毫秒）
System.arraycopy(arr1,0,arr2,0,10);//参数一：要拷贝的数据模板；参数二：从数据源中第几个索引开始拷贝；参数三：要拷贝到哪个数组中；参数四：目的地数组的索引；参数五：拷贝的个数
//如果两个数组都是基本数据类型，则应该前后一致；如果是引用数据类型，则拷贝地址值 ，父类可以拷贝子类的元素
```

### Runtime类：
只能有一个对象，通过这个对象查看当 前jvm的运行环境
```java
Runtime r = Runtime.getRuntime();//获取对象
r.exit(0);//停止JVM
r.availableProcessors();//获得cpu线程数
r.maxMemory();//获得总内存大小
r.freeMemory();//剩余内存的大小
r.exec("shutdown -a");//执行cmd命令
//后面加-s：1分钟后关机。-s -t 指定关机时间。-a:取消关机。-r:关机并重启。
```

### 顶级父类Object,objects:
object中没有成员变量，所以只有***空参构造***
* 一些成员方法：
```java
Object obj = new Object();
Student s1 = new Student();
Student s2 = new Student();
obj.toString();//对象变成字符串(想看属性值，重写toString方法)
s1.equals(s2);//比较两个对象的地址值（重写方法去比较对象内部的属性值）
s1.clone();//必须重写方法,然后调用父类中的clone方法，（浅克隆，只克隆值（地址值，值不开辟新空间））
//深克隆就重写clone方法
//gson
Objects.equals(s1,s1);//返回布尔值，使用s1或s2的类型的equals方法判断（地址值）
Objects.isNUll(s1);//判断s1是否为空，返回布尔值
//重写了就比较属性值
```
> 重写方法：alt+F12+一直next+finish  打开源码：ctrl+b



### BigInteger类：
```java
public BigInteger(int num,Random rnd);//随机大整数（0~2的num次方-1）
public BigInteger(String val);//获取指定大整数
public BigInteger(String val,int radix);//获取指定进制大整数
//常见的成员方法就是加减乘除比大小
```
https://www.bilibili.com/video/BV17F411T7Ao?p=161&vd_source=e784791125f15902299642a7c0e039d8




### BigDecima类：
对于小数的精确运算
https://www.bilibili.com/video/BV17F411T7Ao?p=162&vd_source=e784791125f15902299642a7c0e039d8


### 正则表达式：
帮助文档里搜：Pattern
***先分开写，再从左到右合到一起（直接合，有的要用分组）***
```java
"agyuhdfawbdasioy".matches("对应正则表达式");
(?i)x//大写或者小写的x
| //或者 -------使用逻辑运算符一定要加括号
```
<img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-01%20210321.png">

> 预定义字符：两个\

<img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-01%20211419.png">

> X是任意内容


### 爬虫：
```java
import java.util.regex.Matcher
import java.util.regex.Pattern
String str = "java8yangjingtingsbchewyjava7";//对应字符串
Person p = Person.compile("java\\d{0,2}");//用Person锁定正则规则，创建Person的对象
Matcher m = p.matcher(str);//调用matcher文本匹配器来在str中复合规则p的小串
boolean b = m.find();//从头开始找符合的子串返回布尔值（底层返回索引值）
String s1 = m.group();//group底层来调用find方法来返回串的左索引以及右索引+1;再在底层调用subString(起始索引，结束索引)进行截取;相当于group() = find()+subString();必须先find()函数
System.ou.println(s1);
```
demo:
<img src="https://200307yjt.oss-cn-beijing.aliyuncs.com/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-02%20200536.png">



* #### 条件爬取：
对于符合规则的字符串选择性爬取
```java
import java.util.regex.Matcher
import java.util.regex.Pattern
String str = "java经过了多次的迭代从原来的Java6和Java7变成了现在的Java9和前些年的java8";//对应字符串,现在我只爬java8 java7 java9里面的java
String regex = "((?i)Java)(?=8|7|9|6))";//改变条件，只爬前面的java（忽略j的大小写），后面问号代表前面的字符串，=后面连上的8或7或9------------等于号是核心    代表只要前面的爬取，后面是筛选条件    换成冒号则代表忽略条件整体为判断规则   换成感叹号则代表筛整体且没有后面的数字的串
String regex1 = "((?i)Java)(?:8|7|9|6))";
String regex2 = "((?i)Java)(?!8|7|9|6))";
Pattern p = Pattern.compile(regex);
Matcher m = p.matcher(str);
while(m.find()){
  System.out.println(m.gruop());
}
//regex:Java Java Java java
//regex1:Java6 Java7 Java9 java8
//regex2:java 
```

* #### 贪婪爬取：
> 在爬取数据的时候尽可能的多爬取数据<p></p>
例如：<p></p>
***非贪婪***：在爬取时尽可能的少爬取数据<p></p>
子串：abbbbbbbbbbbbbbbbbbbbb<p></p>
**正则**：贪婪：`ab+`非贪婪：`ab+?`
* 贪婪爬取：abbbbbbbbbbbbbbbbbbbbb
* 非贪婪爬取：ab


* #### 字符串替换：
```java
String s = "杨镜廷";
String result = s.replaceAll("正则表达式","替换成的那个字符串");//替换对应表达式符合的字符串
String []arr = s.split("正则表达式");//按照符合这则表达式字符串所在位置分割剩余字符串
```

* #### 捕获分组：
> 一般分组只看左括号的位置是否靠左优先
```java
adgcda    bxyhsnb    1bsbxu1    &byxbyquz&
String regex = "(.).+\\1";//第一组加括号且为任意字符，\\1表示最后一组与第一组相同
aaa123aaa   bbbbsyguxbwybbbb   111nsha111   rrxnsiarr
//要求一致：用分组
String regex = "((.)\\2*).+\\1";//就是将连续一样的aaa中第一个a看做第一组
"(?:) (?!) (?=)"//这样再开头写这个不占用组号      非捕获分组
"\\1"//正则表达式内部使用   "$1"//正则表达式外部使用，表示使用正则表达式的第一组
```






### Stream流：