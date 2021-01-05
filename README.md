# 数据结构与算法入门笔记

标签 ：数据结构与算法习笔记

---------

##为什么要学习数据结构和算法以及做这个笔记的初衷
1.备战一线大厂，现在一线大厂数据结构基础和学历一样重要，都是一块敲门砖，缺一不可呀。
2.为以后工作打基础，以后肯定不想一直做curd，既然选择了这一行就得往高处走，能不能走的远走的高数据结构和算法基础还是很重要的。
3.学了很久的东西都是会忘的，虽然说学过一次了忘了再学是很快的但是找资源教程重新学习也是需要时间的，因此感觉有自己学过的一份笔记浏览一遍复习才是最快的，所以才有了这份笔记。
4.在做这份笔记的时候有时候会遇到一些其他的知识点，比如java的基础什么的也会在上面补充上
5.做这份笔记以后也是有可能对其他人有帮助的。

##题目一、判断一个数是否为2的n次方：
如2、4、8是2的n次方6、10等不是（阿里面试题）
###初级分析思路
```java
//当一个数可以分解成n个2相乘的时候就符合
//本示例程序1除外
boolean function(int n){
    while(n>=1){
        if(n % 2 == 0){ //当不等于0是就判断为不是2的n次方
            n = n/2;    
        }else{
            return false;
        }
    }
    return true;
}
```
###高级分析思路
利用二进制的位运算符号来解决
分析各2的n次方的数的二进制
n | 二进制|n&(n-1)|二进制结果
--|---|---|----
1 | 0001|0001&0000|0001
2 | 0010|0010&0001|0011
3 | 0011|0011&0010|0010
4 | 0100|0100&0011|0000
5 | 0101|0101&0100|0100
6 | 0110|0110&0101|0100
7 | 0111|0111&0110|0110
8 | 1000|1000&0111|0000
分析结论得出2的n次方的数只有第一位是1其余为0
因此对其小一位数进行按位与运算如果为真即为2的n次方
因此转化为代码
```java
if(n&(n-1)==0)//即为2的n次方
```
###复习按位运算符和逻辑运算符（基于java）
####按位运算符运算结果是一个数也可是一个Boolean类型值
运算符|结果|
---|---
&|按位与，同一二进制两数同时为1则结果为1，其余结果为0
\||按位或，同一二进制两数同时为0结果为0，其余结果为1
^|按位异或，同一二进制位两数不同时结果为1，其余为0
同时位运算符还有>>(右移)、>>>(无符号右移)、<<(左移)、~(一元非)等，以后补充
#####按位运算符示例
如：8&7和8|7的结果即他们的二进制进心按位运算
```  
  1000     1000
& 0111   | 0111
-------  -------
  0000     1111
```
####逻辑运算符运算结果是Boolean类型值
逻辑运算符|运算结果
----|----
&|与(AND)
\||或(OR)
^|异或(XOR)
\|\||短路或(short-circuit OR)当操作数1为真是无论第二个操作数为什么都为真
&&|短路与(short-circuit AND)当操作数1为假时无论第二个操作数为什么都为假
补充：短路与和短路或在进行判断时当第一个有可能会不执行操作数2的代码
因此可以提高代码执行的效率，但是当操作数2的代码必须执行时不适用
##算法的五个特征
有穷性、确定性、可行性、有输入、有输出
##算法的设计原则
正确性、可读性、健壮性、高效率低存储：内存+cpu
##评价算法的重要指标
###时间复杂度
几种常见的复杂度主要有
常数级：O(1)
```java
    int a = 1;                  //O(1)
    for(int i = 0;i < 3;i++){   //运行4次最后一次判断i是否等3
        a=a+1;                  //运行3但不是O(3)时间复杂度O(1)来代表
    }
```
对数级：O(logn)
```java
int n = 1000;//n是未知的，如果是已知的则为O(1)
for(int i = 0;i < n;i++){
    i=i*2;  //求运行多少次结束
            //i的值2，4，6，8-->2^0、2^1、2^2、2^x等
            //我们这里要求2^x = n -> x = log2n->常数忽略->logn
}
```
补充：二分查找也是O(logn)因为它每次减少一半
线性级：O(n)
```java
int n = 100;
int a = 0;
for(int i = 0;i < n;i++){
    a = a +1;               //因为n是未知的且n与运行次数成正相关则为O(n)
}
```
指数级：O(n<sup>2</sup>)
```java
int n = 100;
int k = 100;
for(int i = 0;i < n; i++){
    for(int j = 0;j < k;j++){
        int a = a+1;        //这里应该是O(n^2)
    }
}
```
分析冒泡排序算法的时间复杂度
```java
void fun(int[] n){
        for(int i = 0;i < n.length-1;i++){
            for(int k = i; k < n.length-i-1;k++){
                if(n[k]>n[k+1]){//加个=就是不稳定的
                    int a = 0;
                    a = n[k];
                    n[k] = n[k+1];
                    n[k+1] = a;
                }
            }
        }
    }
```
分析：
第一个for循环的次数是n
第二个for循环的次数是变化的
k=0 运行n-1次
k=1 运行n-2次
.............
k=i 运行1次 
最终有等差数列得n*(n-1)/2->O(n<sup>2</sup>)->只取最高阶的即可

还有O(nlogn)、O(logn)、O(n!)等

###空间复杂度
是对一个算法在运行过程中临时占用存储空间大小的量度也是判断一个算法好坏的一个度量，但是我刚觉重要程度没有时间复杂度高

# 数据结构与算法-数组
---------

##题目：给定一个5g大小的含有全国人民年龄的数据，在一台2核2G的电脑应该如何取得各个年龄人数有多少？（曾经阿里校招题）
要求：不得使用现成的数据结构如Map
思路一：将数据分成小部分，利用分布式的方法来解决
缺点：有点太复杂，杀鸡焉用宰牛刀
思路二：排序算法
解析：好像不能解决问题，排序最高算法效率O(nlogn)内存不够，排不出来
思路三：设置一个数组大小为180，每一个下标代表年龄存储这个年龄段的人数，对数据进行一行一行的读取，读取到的数据属于哪个区间哪个区间就+1
代码实现
```java
import java.io.*;
public class ageMain {
    public static void main(String[] args) throws IOException {
        String str = "";
        String filePath = "E:\\MyFile\\learn\\java\\IDEA\\test\\src\\age.txt";
        InputStreamReader inputStream = new InputStreamReader(new FileInputStream(filePath),"utf-8");
        long startTime = System.currentTimeMillis();
        BufferedReader bufferedReader = new BufferedReader(inputStream);
        int count = 0;//数据的条数
        int data[] = new int[200];
        //按行循环遍历文件，将读到的年龄当作数据的下标，让此下标的数据值+1
        while ((str = bufferedReader.readLine())!=null){
            int age = Integer.valueOf(str);
            data[age]++;
            count++;
        }
        for(int i = 0;i < data.length;i++){
            System.out.println(i+":"+data[i]);
        }
        System.out.println("总数据量大小为"+count+"条");
        System.out.println("花费时间为"+(System.currentTimeMillis() - startTime)+"mm");
    }
}
```
```
测试结果
...
总数据量大小为2430
花费时间为25mm
```
####对此分析：
1.时间复杂度为O(n),核心部分为while循环部分，运行时间和数据量成线性关系
2.为什么要用数组作为最后存储结果的数据结构而不用列表和其他的

###数组的定义：
数组（Array）是有序的元素序列。若将有限个类型相同的变量的集合命名，那么这个名称为数组名。
###数组的特点
1.数组是相同数据类型的元素的集合。
2.数组中的各元素的存储是有先后顺序的，它们在内存（物理内存中的连续）中按照这个先后顺序连续存放在一起。
3.数组元素用整个数组的名字和它自己在数组中的顺序位置来表示。例如，a[0]表示名字为a的数组中的第一个元素，a[1]代表数组a的第二个元素，以此类推。
4.**查询快**，因为可以根据下标**随机访问**。
5.**增删慢**，因为在增删的时候可能会重新生成空间而且需要移动元素

###图例：
物理地址|0x001|0x002|0x003|0x004|0x005|0x006
----|----|
数组|a[0]|a[1]|a[2]|a[3]|a[4]|a[5]
###表现形式
```java
int[] a = new int[5];//大小为5的数组类型为int，没有赋值的时候默认初始为0
int[] b = {1,2,3};//大小为3，类型为int，存储为1，2，3
int[][] c = new int[2][2];//二行二列的二维数组
int[][] d = {{1,2},{3,4}};//二行二列的二维数组且已经赋值
for (int i : a) {
    System.out.println(i);
}
```
输出结果
```
0
0
0
0
0
```
###ArrayList数组简单的实现形式(入门级别，不是太规范)
```java

public class ArrayListMain{
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList(5);
        arrayList.add(1);
        arrayList.add(2);
        arrayList.add(3);
        arrayList.print();
        System.out.println(arrayList.get(0));
        arrayList.delete(1);
        arrayList.print();
        arrayList.insert(0,10);
        arrayList.print();
    }
}
class ArrayList {
    private int size;
    private int index;
    private int[] data;

    public ArrayList(int size){
        this.size = size;
        data = new int[size];
        index = 0;
    }

    /**
     * 添加函数
     * @param num 要添加的数据
     * 时间复杂度O(1)
     */
    public void add(int num){
        data[index] = num;
        index++;
    }

    /**
     * 插入函数
     * @param loc 要插入的下标
     * @param num 要插入的数据
     * 时间复杂度O(n)
     */
    public void insert(int loc,int num){
        //将插入位置元素之后的元素一次往后移动
        if(index<size) {
            for (int i = index-1; i > loc; i--) {
                data[i+1] = data[i];
            }
            data[loc] = num;
        }else {
            //进行数组扩增，一般是当数组容量达到0.75的时候进行size*2扩增
            //这里暂时不写
        }
    }

    /**
     * 取值函数
     * @param loc 取值的下标
     * @return 返取到的值，取不到返回0；
     * 时间复杂度O(1)
     */
    public int get(int loc){
        if(loc<size){
            return data[loc];
        }else{
            return 0;
        }
    }

    /**
     * 删除函数
     * @param loc 删除数据的下标
     * 时间复杂度O(n)
     */
    public void delete(int loc){
        if(loc < index){
            for(int i = loc; i < index;i++){
                data[i] = data[i+1];
            }
            data[index]=0;//最后一位赋值为0就代表删除
        }
        index--;
    }

    /**
     * 输出函数
     * 时间复杂度O(1)
     */
    public void print(){
        for(int i = 0; i < index;i++){
            System.out.println(i+":"+data[i]);
        }
    }
}
```
运行结果
```
0:1
1:2
2:3
1
0:1
1:3
0:10
1:3
```
###ArrayList和数组：
1.ArrayList实际上就是对数组进行了封装，将一些操作变得简单一些，而且增加了扩容机制，当然缺点就是在某些情况比直接操作数组效率低一些
2.在jvm虚拟集中数据因为是new出来的所以存在**堆内存**里面，而占内存里面存放局部变量等
3.堆栈的区别：栈的速度更快，栈数据的内存可以共享，主要存一些基本的数据类型，由此特性分析以下问题
```java
int a = 3;//首先在栈中创建a变量，其次再去栈中寻找是否存在3，如果不存在就创建3            //如果存在3这个数值就用a直接指向3
int b = 3;//首先创建一个变量b，在栈中寻找到了3就直接引用，就是根据栈数据内存可           //以共享的特性
```
####经典面试题：jvm栈堆机制；
```java
//例题一：
String str1 = "abc";
String str2 = "abc";
System.out.println(str1 == str2);
/*判断这个输出结果
答案：true
解析：首先==判断的是内存地址，根据上面讲的原理，当创建str2的时候发现栈内存里面有"abc"这个值便会让str2直接指向这个值的内存空间，因此str1和str2的地址是一样的*/
//例题二：
String str1 = "abc";
String str2 = "abc";
str1 = "bcd";
System.out.println(str1+","+str2);
System.out.pringln(str1==str2);
/*
答案：bcd,abc false
解析：虽然str1一开始和str2指向的内存地址是一样的，但是后来str1重新赋值就相当于str1重新指向的新的地址，而str2原来指向的地址不变，因此最后输出fasle
*/
//例题三：
String str1 = new String("abc");
String str2 = "abc";
System.out.println(str1 == str2);
/*
答案：false
解析：因为str1是用的new来创建的对象，所以它一定会开辟新的地址而且在堆中，str2是普通赋值操作因此"abc"是存储在栈中所以他们内存地址不相等
*/
//例题四：
String str1 = "ja";
String str2 = "va";
String str3 = "java";
String str4 = str1 + str2;
System.out.println(str4 == str3);
System.out.println(str4.equals(str3));
/*
答案：false true
解析：这里是因为"+"操作符底层进行了重载，会调用stringBuild方法来new新的字符串
而equals方法在字符串中已经被重写所以比较的是内容
*/

```
####如何选用
1.当不知道要存数据的大小的时候尽量选用ArrayList，因为涉及到扩容，如果自己写扩容机制的话容易出错
当
2.当数据量已经确定了的时候可以选择数组，因为直接操作数组的效率会更高
####为什么数组的下标从0开始
因为数据是存在物理地址连续的空间中，而物理地址只需要加上数组下标就可以直接找到此数组下标的真实物理地址从而直接取到值，而如果从1开始的话便会需要-1因此产生了多余的运算效率低

#数据结构与算法-链表
---------
链表的定义：链表是将一组零散的内存块串联在一起，我们把内存穿起来的内存块成为节点每个链表节点存储数据之外，还需要存储下一个节点的内存地址
*省略图*
##单链表
**定义**：
每个结点的构成：元素(数据元素的映象) + 指针(指示后继元素存储位置)，元素就是存储数据的存储单元，指针就是连接每个结点的地址数据。
**代码实现**
```java
public class MyLinkListMain{
    public static void main(String[] args) {
        MyLinkList myLinkList = new MyLinkList();
        myLinkList.insertHead(1);
        myLinkList.insertHead(2);
        myLinkList.insertHead(3);
        System.out.println("初始数组");
        myLinkList.print();
        System.out.println("第二位置插入0");
        myLinkList.insertMid(1,0);
        myLinkList.print();
        System.out.println("尾插法5");
        myLinkList.insertTall(5);
        myLinkList.print();
        System.out.println("删除3位置元素");
        myLinkList.delete(2);
        myLinkList.print();
    }
}
class MyLinkList {
    int size = 0;
    private LinkNode head;

    /**
     * 头插法
     * @param data 插入的数据
     */
    public void insertHead(int data){
        LinkNode node = new LinkNode(data);
        node.next = head;
        head = node;
        size++;
    }

    /**
     * 插入到链表中间的函数
     * @param loc 插入位置
     * @param data 插入的数据
     */
    public void insertMid(int loc,int data){
        LinkNode node = new LinkNode(data);
        if(loc == 0){//表示插入在头部
            insertHead(data);
        }else
        {
            LinkNode p = head;
            for(int i = 0 ; i < loc-1;i++){
                p = p.next;
            }
            node.next = p.next;
            p.next = node;
        }
        size++;
    }

    /**
     * 尾插法函数
     * @param data 尾插要插入的数据
     */
    public void insertTall(int data){
        LinkNode node = new LinkNode(data);
        LinkNode p = head;
        for(int i = 0;i <size-1;i++){
            p = p.next;
        }
        p.next = node;
        size++;
    }

    /**
     * 删除
     * @param loc 删除的下标
     */
    public void delete(int loc){
        LinkNode p = head;
        for(int i = 0;i < loc-1;i++){
            p = p.next;
        }
        p.next = p.next.next;
        size--;
    }

    /**
     * 获取值
     * @param loc 值得下标
     * @return 返回要获取得值
     */
    public int get(int loc){
        LinkNode p = head;
        for(int i = 0;i < loc-1;i++){
            p = p.next;
        }
        return p.next.data;
    }

    /**
     * 输出整个链表
     */
    public void print(){
        LinkNode p = head;
        for(int i = 0;i < size;i++){
            System.out.println(p.data);
            p = p.next;
        }
        System.out.println("数组的大小为："+size);
    }

}
class LinkNode{
    int data;
    LinkNode next;
    public LinkNode(int data){
        this.data = data;
    }
}
```
输出结果
```
初始数组
3
2
1
数组的大小为：3
第二位置插入0
3
0
2
1
数组的大小为：4
尾插法5
3
0
2
1
5
数组的大小为：5
删除3位置元素
3
0
1
5
数组的大小为：4

```
###【经典面试题-反转链表】
题目描述：
输入一个链表，反转链表后，输出新链表的表头。
示例1
输入
```
{1,2,3}
```
返回值
```
{3,2,1}
```
答案：
```
public class Solution {
    public ListNode ReverseList(ListNode head) {
        if(head == null){
            return null;
        }
        if(head.next == null){
            return head;
        }
        ListNode p = head;
        ListNode p1 = null;
        ListNode p2 = null;
        //head.next = null;
        p1 = head.next;
        p2 = head.next.next;//临时存储
        while(p2 != null){
            p1.next = head;
            head = p1;
            p1 = p2;
            p2 = p1.next;
        }
        p1.next = head;
        p.next = null;
        return p1;
    }
}
```
##双链表
**定义**：
双向链表也叫双链表，是链表的一种，它的每个数据结点中都有两个指针，分别指向直接后继和直接前驱。
**代码实现**
```java
public class DoubleLinkLIst {
    public static void main(String[] args) {
        MyDoubleLinkList myDoubleLinkList = new MyDoubleLinkList();
        myDoubleLinkList.insertHead(1);
        myDoubleLinkList.insertHead(2);
        myDoubleLinkList.insertHead(3);
        myDoubleLinkList.print();
        myDoubleLinkList.delete(2);
        System.out.println("删除2位置之后");
        myDoubleLinkList.print();
    }
}
class MyDoubleLinkList{
    DoubleLinkNode head = null;
    DoubleLinkNode tail = null;
    int size = 0;

    public void insertHead(int data){
        DoubleLinkNode node = new DoubleLinkNode(data);
        if(head == null){
            tail = node;
        }else {
            node.next = head;
            head.pre = node;
        }
        head = node;
        size++;
    }
    public void delete(int loc){
        DoubleLinkNode p = head;
        for(int i = 0;i < loc - 2;i++){
            //找到要删除元素的前一个节点
            p = p.next;
        }
        p.next = p.next.next;
        p.next.pre = p;
        size--;
    }
    public void print(){
        DoubleLinkNode p = head;
        for(int i = 0;i < size;i++){
            System.out.println(p.data);
            p = p.next;
        }
    }

}
class DoubleLinkNode{
    int data;
    DoubleLinkNode pre;
    DoubleLinkNode next;
    public DoubleLinkNode(int data){
        this.data = data;
    }
}
```
```
3
2
1
删除2位置之后
3
1
```
###【经典算法题】LRU缓存淘汰算法
1.什么是 LRU 算法
就是一种缓存淘汰策略。

计算机的缓存容量有限，如果缓存满了就要删除一些内容，给新内容腾位置。但问题是，删除哪些内容呢？我们肯定希望删掉哪些没什么用的缓存，而把有用的数据继续留在缓存里，方便之后继续使用。那么，什么样的数据，我们判定为「有用的」的数据呢？

LRU 缓存淘汰算法就是一种常用策略。LRU 的全称是 Least Recently Used，也就是说我们认为最近使用过的数据应该是是「有用的」，很久都没用过的数据应该是无用的，内存满了就优先删那些很久没用过的数据。（摘自知乎）
2.LRU算法的简单实现思路
```
(1)用一个双向链表来保存要插入的数据
(2)待插入的节点，在插入之前在双向链表里面进行查找是否有这个节点
    如果有这个节点就删除出插入头部
    如果这个节点不存在就判断空间是否足够
        如果空间足够就直接插入头部
        如果空间不足就删除尾部节点后再插入头部
```
##循环链表
**定义**：
循环链表是另一种形式的链式存贮结构。它的特点是表中最后一个结点的指针域指向头结点，整个链表形成一个环。
###【经典算法题】约瑟夫问题
   约瑟夫环问题的原来描述为，设有编号为1，2，……，n的n(n>0)个人围成一个圈，从第1个人开始报数，报到m时停止报数，报m的人出圈，再从他的下一个人起重新报数，报到m时停止报数，报m的出圈，……，如此下去，直到所有人全部出圈为止。当任意给定n和m后，设计算法求n个人出圈的次序
   
##循环双链表
**定义**：
在双链表的基础上它的表中最后一个结点的指针域指向头结点，整个链表形成一个环。

###数组和链表的对比
时间复杂度|数组|链表
---|---
插入删除|O(n)|O(1)
随机访问|O(1)|O(n)
**重要区别**
1.数组简单易用，在实现上又是连续的物理空间，可以借助cpu的缓存机制，预读数组中的数据提高访问效率
2.链表在物理内存中并不是连续存储的因此没办法预读效率并不高
3.数组的缺点是大小固定，一经声明就要占据整个内存空间，如果声明空间过大，系统没有足够的内存就有可能导致内存不足
4.数组有时候需要动态扩容机制的存在，而动态扩容需要重新开辟一块更大的物理空间将原有数据拷贝进去，因此需要更大的物理空间和更多的时间
5.链表本身没有空间限制只要有足够的内存就可以一直存储下去。

#数据结构与算法-栈
---------
定义：
栈作为一种数据结构，是一种只能在一端进行插入和删除操作的特殊线性表。它按照先进后出的原则存储数据，先进入的数据被压入栈底，最后的数据在栈顶，需要读数据的时候从栈顶开始弹出数据（最后一个数据被第一个读出来）。栈具有记忆作用，对栈的插入与删除操作中，不需要改变栈底指针。
##【经典面试题】括号匹配
1.如何设计一个括号匹配算法，给你一个含有括号的字符串判断括号是否都能匹配，假定只有"()","{}","[]"这三种括号
如：
```
{{{[()]}}}匹配
{{{{([(])}}}不匹配
{[}]不匹配
```
**初级思路**
1.利用栈的原理，从左到右遍历括号
2.遍历到第一个括号时判断栈为空，然后将括号字符放入栈内
3.遍历到第二个括号时判断栈不为空，然后将栈内的括号与将要放入的括号进行匹配
4.如果匹配的上就将栈内的括号出栈继续遍历第三个括号字符依次类推，
5.如果栈最后里面没有元素则判断为括号都匹配，如果剩余元素则不匹配
**代码实现**
```java
import java.util.Stack;
/**
 * 括号匹配问题
 */
public class SolutionMain {
    public static void main(String[] args) {
        String str1 = "{()[]}";
        String str2 = "{([)]}";
        System.out.println(judge(str1)?"str1为匹配括号串":"str1为不匹配");
        System.out.println(judge(str2)?"str2为匹配括号串":"str2为不匹配");
    }

    /**
     * 判断所有的字符是否为括号匹配
     * @param str 要做匹配括号的字符串
     * @return true 为匹配
     */
    public static boolean judge(String str){
        Stack s = new Stack();//利用java.util.Stack提供的栈
        for(int i = 0;i < str.length();i++){
            if(s.empty()){
                s.push(str.charAt(i));
            }else {
                //如果栈顶字符和将要入栈字符匹配则出栈
                char a = (char)s.get(s.size()-1);
                if(judgeTwo((char)s.get(s.size()-1), (char) str.charAt(i))){
                    s.pop();
                }else {
                    s.push(str.charAt(i));
                }
            }
        }

        return s.isEmpty();
    }

    /**
     * 判断两个字符是否匹配
     * @param c1 一定为栈内的字符
     * @param c2 将要入栈的字符
     * @return true 为匹配
     */
    public static boolean judgeTwo(char c1,char c2){
        if(c1 == '(' && c2 == ')') return true;
        if(c1 == '{' && c2 == '}') return true;
        if(c1 == '[' && c2 == ']') return true;
        return false;
    }
}
```
输出结果
```
str1为匹配括号串
str2为不匹配
```
##【经典面试题】如何设计一个浏览器的前进后退功能
解答:利用两个栈分别为A，B，A里面存后退的内容，B里面存前进的内容，当前进时当前内容进A栈，显示新内容，当后退时当前内容进B栈，A出栈显示，当点开新页面时需要清除B栈内容。
##【经典栈应用】如何设计一个加减乘除的四则运算、
【难度系数⭐⭐⭐⭐⭐】
###【题目描述:】
```
用户输入一个包含 + , - , * , / , ( , )的四则运算表达式字符串计算其值
```
###【数据组织:】
表达式采用字符串的形式如：
```java
str = "1+2*(4+2)"
```
###【设计运算算法：】
```
1.将字符串表达时转换为后缀表达式
2.将后缀表达式进行计算求值
```
###【什么是**后缀表达式**，**前缀表达式**，**中缀表达式**】
####1.中缀表达式：
在算数表达式中，运算符位于两个操作符中间的成为**中缀表达式**。例如：1+2*3。中缀表达式是最常用的一种表达形式，我们日常生活中都是用的中缀表达式。对于中缀表达式我们一般采用"先乘除，后加减，先算括号内，再算括号外，越在前面的越优先执行"的运算规则。
####2.前缀表达式
同样在算数表达式中，如果运算符号在操作数的前面，成为**前缀表达式**，如"1+2*3"的前缀表达式为"+1*23"，这里不过多解释
####3.后缀表达式
运算符在操作数后面的称为后缀表达式又称为逆波兰表达式，在后缀表达式中已经考虑了运算符的优先级没有括号而且越放在前面的运算符越优先执行，如"1+2*3"的后缀表达式为"123*+"
#####如何将算数中缀表达式转换为后缀表达式
简单来说在一个中缀表达式转为后缀表达式的时候操作数的顺序是不会改变的，但运算符的次序可能会发生改变，根据优先运算的运算符在前面的原则放置。
#####简单的转换步骤
为了能够初步的了解到如何进行中缀表达式到后缀表达式的转换，我们先假定操作数为10以内的正整数。
以str = "1+2*3"为例
```
1.首先定义一个栈称为stack，用来临时存放运算符
2.定义一个String类型的变量postexp，用来存放转换为后缀表达式的结果
3.对要转换为后缀表达式的中缀表达式str进行逐个字符遍历
4.当遍历到操作数"1"的时候将"1"存入变量postexp后面
5.当遍历到运算符"+"的时候此时判断栈为空直接将"+"入栈stack
6.当遍历到操作数"2"的时候将"2"存入变量postexp后面
7.当遍历到运算符"*"的时候，此时判断栈不为空且将栈内元素"+"和将要入栈的"*"比较，发现"*"的运算级别高，因此将"*"直接入栈（如果将要入栈的运算级别比栈内元素运算级别低就依次将栈顶出栈放入postexp直到遇到将要入栈的运算级别比栈内元素运算级别高的时候直接入栈）
8.当遍历到操作数"3"的时候将"3"放入postexp后面
9.当没有可遍历的数据的时候将栈内元素依次出栈放在postexp的后面
10.最后postexp就是后缀表达是的结果postexp="123*+"
```
#####将后缀表达式转换为最终的结果
还是以上面刚转换为后缀表达式的结果为例
```
postexp = "123*+"
1.首先定义一个栈stack
2.遍历postexp中的字符如果遇到操作数就进栈，此时stack内元素为123
3.当遇到运算符"*"的时候就出栈两次，分别为a（第一次出栈），b（第二次出栈）进行运算c=a*b;然后将c进栈
4.当遍历到"+"运算符的时候进行出栈两次a，b进行c = a + b；
5.最后结果就是c
```
####表达式求值的最终代码展示
在对如何进行中缀表达式如何转化后缀表达式到转为最终结果有了初步认识之后我们就可以直接通过直接读代码来学习如何进行完整的求职过程
```java
import java.util.Stack;

public class BasicCalculatorMain {
    public static void main(String[] args) {
        String str1 = "1+2+3";
        System.out.println(str1+"-->"+trans(str1)+"-->"+calculatePostExp(trans(str1)));
        String str2 = "10+2*3";
        System.out.println(str2+"-->"+trans(str2)+"-->"+calculatePostExp(trans(str2)));
        String str3 = "(1+2)*3";
        System.out.println(str3+"-->"+trans(str3)+"-->"+calculatePostExp(trans(str3)));
        String str4 = "(1+2)/(3-4)";
        System.out.println(str4+"-->"+trans(str4)+"-->"+calculatePostExp(trans(str4)));

    }

    /**
     * 根据中缀表达式求得后缀表达式
     * @param midStr 要求的中缀表达式
     * @return 返回后缀表达式
     */
    public static String trans(String midStr){
        Stack<Character> stack = new Stack<>();//定义存放运算符的栈stack
        String postExp = "";//定义存放最后结果的字符串
        for(int i = 0;i < midStr.length();){//定义循环遍历字符串
            //事先定义好tempChar，为了不让后面一直调用charAt函数提高效率
            char tempChar = midStr.charAt(i);
            switch (tempChar){
                case '(':
                    //如果是左括号就入栈
                    stack.push(tempChar);
                    i++;
                    break;
                case ')':
                    //如果是右括号将栈内"("以前的元素出栈放入postExp中
                    while (stack.get(stack.size()-1) != '('){
                        postExp += stack.pop();
                    }
                    stack.pop();//将无用的'('出栈
                    i++;
                    break;
                case '+':
                case '-':
                    // 当遇到”+"和“-”运算符时
                    // 准备入栈，并且和已经在栈里的对比是否优先运算
                    // 只要是在"("以前的都比"+"运算符优先级别高因此"+"应该放到最里面
                    while (!stack.isEmpty()){   //对栈进行循环遍历
                        if(stack.get(stack.size()-1)!='('){//如果栈顶元素不等于"("
                            postExp += stack.pop();//出栈放入postExp
                        }else {
                            break;
                        }
                    }
                    stack.push(tempChar);//将当前“+”或“-”入栈
                    i++;
                    break;
                case '*':
                case '/':
                    //当遇到乘除时
                     while(!stack.isEmpty()){//当栈不为空时循环
                         if(stack.get(stack.size()-1)=='*'
                                 || stack.get(stack.size()-1) == '/'){//如果栈顶元素为"*"或者"/"
                             postExp += stack.pop();//由于先进栈的"*"或"/"是优先运算的因此让它们出栈放入postExp中
                         }else {
                             break;
                         }
                     }
                     stack.push(tempChar);//进栈当前元素
                    i++;
                    break;
                default:
                    // 当以上都没选择到时一定为数字格式，就放入postExp字符串中
                    while(i<midStr.length() && Character.isDigit(midStr.charAt(i))) {
                        postExp += midStr.charAt(i);
                        i++;
                    }
                    postExp += "#";//用#来分割数字，防止混淆
            }
        }
        //此时中缀表达式已经循环完毕，需要对栈进行清空
        while (!stack.isEmpty()){
            postExp += stack.pop();
        }
        return postExp;
    }
    public static int calculatePostExp(String postExp){
        Stack<Integer> stack =new Stack<>();//定义操作数栈，用来存放操作数
        for(int i = 0;i < postExp.length();){
            char tempChar = postExp.charAt(i);
            int numA = 0;
            int numB = 0;
            int numC = 0;
            switch (tempChar){
                case '+':
                    //当遇到"+"时从栈中弹出前两个数分别为 numA和numB执行numC = numB+numA
                    numA = stack.pop();
                    numB = stack.pop();
                    numC = numB + numA;
                    stack.push(numC);
                    i++;
                    break;
                case '-':
                    numA = stack.pop();
                    numB = stack.pop();
                    numC = numB - numA;
                    stack.push(numC);
                    i++;
                    break;
                case '*':
                    numA = stack.pop();
                    numB = stack.pop();
                    numC = numB * numA;
                    stack.push(numC);
                    i++;
                    break;
                case '/':
                    numA = stack.pop();
                    numB = stack.pop();
                    if(numA!=0){
                        numC = numB / numA;
                    }else{
                        System.out.println("除0错误");
                        break;
                    }
                    stack.push(numC);
                    i++;
                    break;
                default:
                    //当遇到数字时
                    int num = 0;//定义中间遍历num
                    while (Character.isDigit(postExp.charAt(i))){
                        //https://www.cnblogs.com/daleyzou/p/9510334.html如何转化char-->int
                        num += num*10+Integer.parseInt(String.valueOf(postExp.charAt(i)));//字符强制转为int再将#以前的转为整数
                        i++;
                    }
                    //转化后的存入stack
                    stack.push(num);
                    i++;
                    break;
            }
        }
        return stack.pop();
    }
}


```
输出结果
```
1+2+3-->1#2#+3#+-->6
10+2*3-->10#2#3#*+-->17
(1+2)*3-->1#2#+3#*-->9
(1+2)/(3-4)-->1#2#+3#4#-/-->-3
```

##为什么要使用栈这种数据结构
因为在某些场景中就需要栈这种具有限制的数据结构，如果用数据和链表来进行替代栈的话虽然能够实现栈相关的功能，但是它们暴露出了了太多的接口可供操作从而增加了不安全性
##栈的分类
1.数组类型的栈，通常以数组头为栈底，

2.链表类型的栈，通常以链表头为栈定，方便数据的增加删除
他们最大的区别就是扩容机制，链表可以随意扩容，但是容易出现栈溢出，因此一般使用数组类型的栈，使用之前定义好容量，一般不扩容

##栈的代码实现
```java
public class StackMain {
    public static void main(String[] args) {
        ArrayStack<Integer> arrayStack = new ArrayStack<>(2);
        arrayStack.push(1);
        arrayStack.push(2);
        arrayStack.push(3);//扩容之后
        System.out.println(arrayStack.pop());
        System.out.println(arrayStack.pop());
        System.out.println(arrayStack.pop());
        
    }
}
class ArrayStack<T> {
    int size = 0;//栈的大小，默认为0
    T[] data = (T[])new Object[16];//注意不能new T[16]
    //构造函数
    public ArrayStack(int size){
        this.size = size;
        data = (T[]) new Object[size];
    }

    /**
     * 入栈函数
     * @param newData 入栈的参数
     */
    public void push(T newData){
        //当栈已经满的时候
        if(size == this.data.length){
            reSize(size * 2);//2倍扩容
        }
        data[size] = newData;
        size++;
    }

    /**
     * 出栈函数
     * @return 返回出栈的元素
     */
    public T pop(){
        //当栈内元素为空的时候返回空
        if(isEmpty()){
            return null;
        }
        T temp = data[size-1];
        size--;
        return temp;//size--先用再减

    }

    /**
     * 判断栈是否为空
     * @return true 为空
     */
    public boolean isEmpty(){
        return (size == 0);//size == 0的时候代表为空
    }

    /**
     * 扩容函数
     * @param newSize 扩容后的大小
     */
    public void reSize(int newSize){
        T[] temp = (T[]) new Object[newSize];
        for(int i = 0;i < size; i++){
            temp[i] = data[i];
        }
        data = temp;
    }
}
```
```
3
2
1
```
#数据结构与算法-队列
---------
##队列的定义
队列是一种特殊的线性表，特殊之处在于它只允许在表的前端（front）进行删除操作，而在表的后端（rear）进行插入操作，和栈一样，队列是一种操作受限制的线性表。进行插入操作的端称为队尾，进行删除操作的端称为队头。队列中没有元素时，称为空队列。
队列的数据元素又称为队列元素。在队列中插入一个队列元素称为入队，从队列中删除一个队列元素称为出队。因为队列只允许在一端插入，在另一端删除，所以只有最早进入队列的元素才能最先从队列中删除，故队列又称为先进先出（FIFO—first in first out）线性表。（百度百科）
##队列的特点
1.线性表如数组或者链表

##队列的分类
1.顺序队列（只能在一端插入数据和删除数据）
2.环形队列（可以在两端分别插入数据和删除数据）
##队列的基本操作
1.入队（将数据插入队列的尾部）
2.出队（将队列从头部取出)
##对列的用途
队列和栈一样，是一种操作受限的数据结构，作为一种基础的数据结构它的用途也是非常广泛的如循环队列、阻塞队列、并发队列。它在偏系统的底层，框架，中间件的开发中有着重要的作用。
##顺序队列(数组)代码实现
```java
public class QueueMain {
    public static void main(String[] args) {
        ArrayQueue a = new ArrayQueue(2);
        a.push(1);
        a.pop();
        a.push(2);
        a.push(3);
        a.push(4);
        System.out.println(a.pop());
        System.out.println(a.pop());

    }
}
class ArrayQueue{
    private int[] data;//存放数据的数组
    private int head = 0;//头指针
    private int tail = 0;//尾指针
    private int size = 0;

    /**
     * 构造函数
     * @param size 队列的大小
     */
    public ArrayQueue(int size){
        data = new int[size];
    }

    /**
     * 入队列
     * @param num
     */
    public void push(int num){
        //判断队列是否可以前移
        if(tail == data.length){
            if(head==0){
                //说明队列已经满了没有办法移动
                System.out.println("队列已经满了");
                return;
            }
            //进行队列数据的前移
            for(int i =0;i< tail-head;i++){
                data[i] = data[head];
                head++;
            }
            tail = tail - head + 1;
            head=0;
        }
        //添加数据
        data[tail] = num;
        tail++;
        size++;
    }

    /**
     * 出队列函数
     * @return 返回队头元素
     */
    public int pop(){
        //如果为空返回-1;
        if(isEmpty()){
            return -1;
        }
        int re = data[head];
        head++;
        size--;
        return re;
    }

    /**
     * 判断队列是否为空
     * @return true：空
     */
    public boolean isEmpty(){
        boolean b = false;
        //当队头 == 队尾的时候队列为空
        if(tail == head){
            b = true;
        }
        return b;
    }

}
```
输出结果
```
2
3
队列已经满了
```
##循环队列(数组)代码实现
```java
import org.w3c.dom.CDATASection;

public class CircleArrayQueueMain {
    public static void main(String[] args) {
        //这里虽然设置的大小为2，由于为了判断队列满所以会留有一个空间不存
        CircleArrayQueue c = new CircleArrayQueue(4);
        c.push(1);
        c.pop();
        c.push(2);
        c.push(3);
        c.push(4);
        c.push(5);
        System.out.println(c.pop());
        System.out.println(c.pop());
        System.out.println(c.pop());
    }
}
class CircleArrayQueue{
    private int[] data;//存数据的数组
    private int head = 0;//头指针
    private int tail = 0;//尾指针
    private int size = 0;//数组已存数据的多少
    private int n;//数组的大小
    public CircleArrayQueue(int n){
        data = new int[n];
        this.n = n;
    }
    public void push(int num){
        //判断队列是否满了两种方法1.size==n;2.(tail + 1)%n == head;
        if((tail+1)%n == head){//重点：其实此时数组还留有一个空间，队头指针在队尾指针下一位时,队列为满
            System.out.println("队列已经满了");
            return;
        }
        data[tail] = num;
        //假设n=2;当tail=0时(tail+1)%n=1;
        //       当tail=1时(tail+1)%n=0;依次类推，这便是循环队列的精华
        tail = (tail+1)%n;
    }
    public int pop(){
        if(isEmpty()){
            //如果为空返回-1
            return -1;
        }
        int re = data[head];
        head = (head+1)%n;
        return re;
    }

    private boolean isEmpty() {
        if(tail == head){
            return true;
        }
        return false;
    }

}
```
输出结果
```
队列已经满了
2
3
4
```
##优先队列
普通的队列是一种先进先出的数据结构，元素在队列尾追加，而从队列头删除。在优先队列中，元素被赋予优先级。当访问元素时，具有最高优先级的元素最先删除。优先队列具有最高级先出 （first in, largest out）的行为特征。通常采用堆数据结构来实现。
（后面补充）
##阻塞队列
阻塞队列（BlockingQueue）是一个支持两个附加操作的队列。这两个附加的操作支持阻塞的插入和移除方法

1.支持阻塞的插入方法：意思是当队列满时，队列会阻塞插入元素的线程，直到队列不满
2.支持阻塞的移除方法：意思是在队列为空时，获取元素的线程会等待队列变为非空

阻塞队列常用于生产者和消费者的场景，生产者是向队列里添加元素的线程，消费者是从队列里取元素的线程。阻塞队列就是生产者用来存放元素、消费者用来获取元素的容器。
（摘自https://www.jianshu.com/p/32665a52eba1）
##线程池的思考
当线程池里面的任务满的时候，此时又来一个线程，线程池如何处理，具体有哪些策略，这些策略又是如何实现的
处理策略：
1.排队：阻塞队列，有空闲的时候再拿
2.不处理直接抛弃

#算法思想(递归&分治&回溯)
##递归
思考：
1.微信分销有一个返利系统，比如B是A的下线，C是B的下线，因此当C买东西B和A会拿到提成，当B买东西，A会拿到提成
2.斐波那契数列
1，1，2，3，5，8
求解第n个斐波那契数为多少
###斐波那契的代码实现
```java
public class FibonacciMain {
    public static void main(String[] args) {
        System.out.println(fib(1));
        System.out.println(fib(2));
        System.out.println(fib(3));
        System.out.println(fib(4));
    }
    public static int fib(int n){
        int result;//定义返回结果result
        //首先定义结束条件
        //当n==1时，返回值为1
        if (n == 1) {
            return 1;
        }else if(n == 2){//当n==2时返回1
            return 1;
        }
        //最后结果就为上一个数加上上一个数分别表示为fib(n-1)和fib(n-2)
        result = fib(n-1)+fib(n-2);
        return result;
    }
}
```
输出结果
```
1
1
2
3
```
###优化以上代码
因为递归的时间复杂度为O(2<sup>n</sup>)太高了，每一个递归都可以改写成不使用递归的for循环的他的时间复杂度为O(n);
```java
public static int forFib(int n){
        int result = 0;
        int a = 1;
        int b = 1;
        if(n<=2){
            return 1;
        }
        for(int i = 0;i < n-2;i++){
            result = a + b;
            a = b;
            b = result;
        }
        return result;
    }
```
3.n！
未测试代码
```java
public static int fun(){
    int result = 0;
    if(n == 1){
        return 1;
    }
    result = n*f(n-1);
}
```
###深入分析递归为什么效率低
递归会进行很多重复的计算，比如计算f(4)f(3)之后再计算f(5)，因为f(5)=f(4)+f(3)虽然前面计算过f(4)但是这里还会重复计算一遍导致效率低。
###为什么递归效率低还要有递归呢？
递归效率低是函数调用的开销导致的。在一个函数调用之前需要做许多工作，比如准备函数内局部变量使用的空间、搞定函数的参数等等，这些事情每次调用函数都需要做，因此会产生额外开销导致递归效率偏低，所以逻辑上开销一致时递归的额外开销会多一些当然了，通过有意识的组织代码的写法可以把某些递归写成尾递归，尾递归可以进行特殊的优化所以效率会比普通的递归高一些，也不会因为递归太多导致栈溢出遍历树还不用递归的话，那么人肉写一个栈+深度优先遍历或者人肉队列+广度优先遍历，再辅以黑魔法给栈或者队列提速，应该会比递归快一些，加速幅度和语言和写法相关，但在大多数情况下我觉得是得不偿失的，花了很大精力很可能效率提升不明显(摘自知乎)
###如何优化递归
1.使用非递归
2.通过缓存机制将计算过的数据存储起来
```java
 public static int fib(int n){
    int result;
    int[] data = new int[10];//假设n最大为9；
    if (n <= 1) {
        return 1;
    }
    //用数组来做缓存
    if(data[n]>0){
        return data[n];
    }
    result = fib(n-1)+fib(n-2);
    data[n] = result;
    return result;
}
```
3.使用尾递归
什么是尾递归：
尾递归就是调用函数一定出现在末尾，没有其他操作了，因为我们编译器在编译代码的时候，如果发现函数末尾已经没有任何操作了，就不会创建新的栈，而且覆盖到前面去。
####尾递归计算n!
```java
public class TailFacMain {
    public static void main(String[] args) {
        System.out.println(tailFac(5,1));
    }
    //尾递归，以n!为例子
    public static int tailFac(int n,int res){
        if(n<=1){
            return res;
        }
        return tailFac(n-1,n*res);
    }
}
```
####尾递归计算斐波那契
public class TailFibMain {
    public static void main(String[] args) {
        System.out.println(TailFib(3,1,1));
    }
```java
    /**
     * 尾递归求斐波那契
     * @param n 求第几位,最后调用参数是n-1,是因为从最大开始，每次递归都减少1，
     *          一直到循环结束，其中求得的值通过参数以某种方式传递下去
     * @param pre 相当于f(n-1)的值
     * @param res 相当于f(n-1)+f(n-2)的值
     *            ps:这里很难想，降n取3的时候思考一下
     * @return 结果
     */
    public static int TailFib(int n,int pre,int res){
        if(n <= 2){
            return res;
        }
        return TailFib(n-1,res,pre+res);
    }
}

```
输出结果
```
2
```
##回溯算法

回溯算法实际上一个类似枚举的搜索尝试过程，主要是在搜索尝试过程中寻找问题的解，当发现已不满足求解条件时，就“回溯”返回，尝试别的路径。回溯法是一种选优搜索法，按选优条件向前搜索，以达到目标。但当探索到某一步时，发现原先选择并不优或达不到目标，就退回一步重新选择，这种走不通就退回再走的技术为回溯法，而满足回溯条件的某个状态的点称为“回溯点”。许多复杂的，规模较大的问题都可以使用回溯法，有“通用解题方法”的美称。(百度百科)

##枚举
是列出某些有穷序列集的所有成员的程序

##分治
在计算机科学中，分治法是一种很重要的算法。字面上的解释是“分而治之”，就是把一个复杂的问题分成两个或更多的相同或相似的子问题，再把子问题分成更小的子问题……直到最后子问题可以简单的直接求解，原问题的解即子问题的解的合并。这个技巧是很多高效算法的基础，如排序算法(快速排序，归并排序)，傅立叶变换(快速傅立叶变换)

#算法思想之排序-插入&希尔&归并
##一般的排序算法

###选择排序
选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理是：第一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，然后再从剩余的未排序元素中寻找到最小（大）元素，然后放到已排序的序列的末尾。以此类推，直到全部待排序的数据元素的个数为零。选择排序是不稳定的排序方法。
```java
public class SelectionSortMain {
    public static void main(String[] args) {
        int[] data = {5,4,3,2,1};
        selectionSort(data);
        for (int datum : data) {
            System.out.println(datum);
        }
    }
    public static void selectionSort(int[] data){
        for(int i = 0;i < data.length;i++){
            for(int j = i+1;j < data.length;j++){
                if(data[i]>data[j]){
                    int t = data[i];
                    data[i] = data[j];
                    data[j] = t;
                }
            }
        }
    }
}
```
###冒泡排序
冒泡排序（Bubble Sort），是一种计算机科学领域的较简单的排序算法。它重复地走访过要排序的元素列，依次比较两个相邻的元素，如果顺序（如从大到小、首字母从Z到A）错误就把他们交换过来。走访元素的工作是重复地进行直到没有相邻元素需要交换，也就是说该元素列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端（升序或降序排列），就如同碳酸饮料中二氧化碳的气泡最终会上浮到顶端一样，故名“冒泡排序”。（百度百科）
####实现代码
```java
public class BubbleSortMain {
    public static void main(String[] args) {
        int[] n ={10,3,4,5,6};
        bubbleSort(n);
        for (int i : n) {
            System.out.println(i);
        }
    }
    //冒泡排序每次都会将最大的，第二大的，...放到最后面
    static void bubbleSort(int[] n){
        for(int i = 0;i < n.length-1;i++){//最后一个不需要冒泡
            for(int k = 0; k < n.length-i-1;k++){//
                if(n[k]>n[k+1]){
                    int a = 0;
                    a = n[k];
                    n[k] = n[k+1];
                    n[k+1] = a;
                }
            }
        }
    }
}

```
####冒泡排序如何优化
尽快推出
###快速排序


###桶排序
###堆排序（数论里讲）
###基数排序
###插入排序
一般也被称为直接插入排序。对于少量元素的排序，它是一个有效的算法。插入排序是一种最简单的排序方法，它的基本思想是将一个记录插入到已经排好序的有序表中，从而一个新的、记录数增1的有序表。在其实现过程使用双层循环，外层循环对除了第一个元素之外的所有元素，内层循环对当前元素前面有序表进行待插入位置查找，并进行移动（百度百科）
####类比扑克：
插入排序的工作方式像许多人排序一手扑克牌。开始时，我们的左手为空并且桌子上的牌面向下。然后，我们每次从桌子上拿走一张牌并将它插入左手中正确的位置。为了找到一张牌的正确位置，我们从右到左将它与已在手中的每张牌进行比较。拿在左手上的牌总是排序好的，原来这些牌是桌子上牌堆中顶部的牌
####基本算法思想
```
1.将一个数组已排序段和未排序段，初始化已排序段只有一个元素
2.从未排序段去除一个元素插入到已排序段，并保证已排序段时有序的
3.重复执行以上操作，知道排序完成。
```
####思考用什么数据结构来实现

####实现代码
```java
public class InsertionSortMain {
    public static void main(String[] args) {
        int[] data = {9,8,7,6,5};
        insertionSort(data);
        for (int i : data) {
            System.out.println(i);
        }
    }
    public static void insertionSort(int[] data){
        //这里采用的思想是将这个数组分为两部分，
        //第一个循环就是第一部分，从1开始代表左边只有一个数
        int n = data.length;
        for(int i = 1; i < n; i++){
            int temp = data[i];//因为a[i]这个位置会被顶替掉，因此要拿出来
            for(int j = i-1;j >= 0;j--){
                if(temp<data[j]){//如果temp<data[j]
                    //将前面元素后移
                    data[j+1] = data[j];
                }else {
                    //直接插入
                    data[j+1] = temp;//这里应该是data[j+1]
                    break;//已经插入，打破内层循环
                }
                //这里代表是当没有数可以与它相比较的时候插入到最前面
                data[j] = temp;
            }
        }
    }
}
```
####时间复杂度判断
普通的时候或者最坏的时候时间复杂度：O(n<sup>2</sup>)
最好的情况为O(n)，当数组为有序的时候
####如何优化
分段：当break执行的次数越多执行的效率越高，这是后希尔排序就出现了
###希尔排序
####基本思想
希尔排序(Shell's Sort)是插入排序的一种又称“缩小增量排序”（Diminishing Increment Sort），是直接插入排序算法的一种更高效的改进版本。希尔排序是非稳定排序算法。该方法因 D.L.Shell 于 1959 年提出而得名。
希尔排序是把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至 1 文件为一组，终止。
###归并排序（二路归并）
归并排序（Merge Sort）是建立在归并操作上的一种有效，稳定的排序算法，该算法是采用分治法（Divide andConquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。
####实现代码
```java
public class MergeSortMain {
    public static void main(String[] args) {
        int[] data = {7,6,5,4,3,2,1};
        mergeSort(data,0, data.length-1);
        for (int datum : data) {
            System.out.println(datum);
        }
    }
    public static void mergeSort(int[] data,int left,int right) {
        //递归的终止条件
        if (left < right) {
            //首先将数组用递归的方式进行分开
            int mid = (left + right) / 2;
            mergeSort(data, left, mid);
            mergeSort(data, mid + 1, right);
            //将分开的进行合并
            merge(data, left, mid, right);
        }
    }
    private static void merge(int[]data,int left,int mid,int right) {
        int[] temp = new int[data.length];//定义一个空的数组用来接收排好序的数据，数据量大的时候每次都开一个数组，所以要放到外面！
        int point1 = left;//指向左边数组的第一个数
        int point2 = mid+1;//指向右边数组的第一个数
        int loc = left;//指向temp已经存入数据的最后一位
            while(point1<=mid && point2<=right){
            //如果point1的值小就将point1的值赋值给temp
            if(data[point1]<data[point2]){
                temp[loc] = data[point1];
                point1++;
                loc++;
            }
            //如果point2的值小就将point2的值赋值给temp
            if(data[point1]>data[point2]){
                temp[loc] = data[point2];
                point2++;
                loc++;
            }
        }
        //最后左边数组或右边数组会有值没有被放入temp
        //当左边数组最后一个值没有
        while(point1<=mid){
            temp[loc] = data[point1];
            point1++;
            loc++;
        }
        while(point2<=right){
            temp[loc] = data[point2];
            point2++;
            loc++;
        }
        //最后将temp放回data
        for(int i = left;i <= right;i++){
            data[i] = temp[i];
        }
    }
}

```
###计数排序
当数据量很大，并且可以确定在一个范围内，且可以不关注稳定性的情况下是可以采用计数排序的
例如：有一组200万的成绩数据，数据范围在0-100之间。因此可以参考上面统计年龄的思想，用数组下标来存储成绩，下标所在值来存储个数，然后对这个数组进行遍历便可以得到排序结果

插入->希尔->归并 和 选择->冒泡->快速是递进关系所以放在一起

##我们从哪些方面来判断一个算法的好坏
1.时间复杂度
2.空间复杂度
3.比较次数&交换次数
为什么有了时间复杂度和空间复杂度来判断算法的好坏还要有比较和交换次数？
因为交换和比较的次数都是需要花时间的，可以更准确的计算算法使用的时间
4.稳定性
是指同样的数据，相对位置不变
比如:1、2(1)、3、2(2)
排序:1、2(1)、2(2)、3 和1、2(2)、2(1)、3这两个2的位置不一样，前面的更稳定
稳定排序有什么意义？应用在哪里？
电商订单里的排序：首先按照金额从小到大排序，金额相同的按照下单时间排序，从订单中心过来的订单已经按照时间排序好了，当你再用金额再次排序的时候，相同金额的订单排在一起但是他们的时间顺序应该不变才可以。
##各种排序对比
排序名称|时间复杂度|是否稳定|额外空间开销|
--|--
插入排序|O(n<sup>2</sup>)|稳定|O(1)|
冒泡排序|O(n<sup>2</sup>)|稳定|O(1)|
选择排序|O(n<sup>2</sup>)|不稳定|O(1)|
希尔排序|O(n<sup>2</sup>)|不稳定|O(1)|
归并排序|O(nlogn)|稳定|O(n)|
快速排序|O(nlogn)|不稳定|O(1)|
##各种排序怎么选择
1.分析稳定性
2.分析数据量
数据量小的时候优先选择插入排序，比如50个
3.分析空间，归并排序会有额外的空间
综上所诉：没有一个全能的排序算法，都是要根据情况分析的，如果你不会分析就选择归并或者快排

#算法思想-(贪心算法&动态规划)
##思考
1.某天公司领导需要你拍一个会议室的时间表，有N个同等级的会议，需要在同一个会议室里面开会，给你各个会议的开始结束时间，应该怎么排。
2.某天你中了一个奖可以清空购物车里面5000元的东西，只能买一件，不能找零，应该怎么买
加入你购物车有4000,3000,2000元的东西需要购买，因此你选择3000+2000可以最大化利益

##贪心算法
贪心算法又叫贪婪算法，它在求解某个问题的时候总能做出最大化的利益。
也就是说它只顾眼前，不顾大局，所以他是局部最优解。特点是通过局部最优推出全局最优
思考题1
0-9
8-10
10-12
8-20
思路：首先按照结束时间排序，让第一个先去开会，只要开始时间少于上场结束时间的就可以接着开
###贪心算法的思想
一定会有一个排序。其中哈夫曼编码，贪心算法，压缩算法，最短路径等都是贪心算法的思想
贪心算法不是对所有的问题都能得到最优解，关键是贪心策略的选择，选择贪心算法应该是具有无后效性，也就是说某个状态的改变不会影响以后的状态，只与当前状态有关。

##动态规划-背包问题(面试常见)
一小偷去商店偷东西，背包容量为50kg，现在有以下物品，请问怎么拿才能得到最大价值
物品|重量|价值|性价比
---|---
物品1|10kg|60元|60/10=6|
物品2|20kg|100元|100/20=50|
物品3|40kg|120元|120/40=30|
性价比最高排序，贪心策略可以拿到60+100=160的商品
很显然这是不对的，不过有时候贪心算法是可以解决的，但是只能解决一部分因此这就是贪心可动态规划的一部分，但是贪心能不能完全解决很难证明，只能多举例子。

但是如果不用贪心应该怎么解决
我们还可以用枚举的方法，排列组合出所有的情况，在符合条件的情况下找出最大价值的情况，不过很显然当超过10中物品的情况下是有很大计算量的，因此超过10的情况是很难解决出来的


（动态规划暂时放弃）
#数据结构与算法-树论基础&二叉树
在树形结构中重要的术语：
1.节点：树里面的元素
2.父子关系：节点相连的的两个节点之间的关系
3.子树：当节点大于1时，其余的节点分为互不相交的集合称为子树
4.度：一个节点用于子树的数量成为度
5.叶子几点：度为0的节点
6.孩子：节点的子树的根称为孩子节点
7.双亲：和孩子节点对应
8.兄弟：同一双亲节点
9.森林：由N个互不相交的树构成森林
##二叉树的遍历
重要口诀：根节点输出
1.前序遍历：根左右
2.中序遍历：左根右
3.后序遍历：左右根
4.层次遍历：


