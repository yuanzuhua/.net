<!-- TOC -->

- [编程基础](#编程基础)
    - [数据类型](#数据类型)
        - [变量](#变量)
            - [值类型](#值类型)
            - [引用类型](#引用类型)
        - [常量](#常量)
        - [类型转换](#类型转换)
        - [装箱(boxing)、拆箱(unboxing)](#装箱boxing拆箱unboxing)
        - [结构体](#结构体)
            - [结构体和类](#结构体和类)
    - [流程控制](#流程控制)
        - [顺序](#顺序)
        - [分支](#分支)
        - [循环](#循环)
    - [数组](#数组)
        - [一维数组](#一维数组)
        - [循环](#循环-1)
        - [多维数组](#多维数组)
        - [Array](#array)
    - [方法](#方法)
        - [形参实参](#形参实参)
        - [重载](#重载)
        - [参数传递](#参数传递)
            - [值传递](#值传递)
            - [引用传递](#引用传递)
            - [输出参数](#输出参数)
            - [params](#params)
    - [数据集合DataCollection](#数据集合datacollection)
        - [ArrayList](#arraylist)
        - [Hashtable](#hashtable)
        - [排序列表SortedList](#排序列表sortedlist)
        - [堆栈Stack](#堆栈stack)
        - [队列Queue](#队列queue)
    - [泛型](#泛型)
        - [泛型使用](#泛型使用)
        - [泛型集合List<T>](#泛型集合listt)
        - [Dictionay<Tkey,Tvalue>](#dictionaytkeytvalue)

<!-- /TOC -->
<a id="markdown-编程基础" name="编程基础"></a>
# 编程基础

<a id="markdown-数据类型" name="数据类型"></a>
## 数据类型
<a id="markdown-变量" name="变量"></a>
### 变量
<a id="markdown-值类型" name="值类型"></a>
#### 值类型
原类型（Sbyte、Byte、Short、Ushort、Int、Uint、Long、Ulong、Char、Float、Double、Bool、Decimal）、枚举(enum)、结构(struct)

值型就是在栈中分配内存，在申明的同时就初始化，以确保数据不为NULL；

<a id="markdown-引用类型" name="引用类型"></a>
#### 引用类型
类、数组、接口、委托、字符串等。

引用型是在堆中分配内存，初始化为null，引用型是需要GARBAGE COLLECTION来回收内存的，值型不用，超出了作用范围，系统就会自动释放！




<a id="markdown-常量" name="常量"></a>
### 常量
**const和static readonly**


<a id="markdown-类型转换" name="类型转换"></a>
### 类型转换

<a id="markdown-装箱boxing拆箱unboxing" name="装箱boxing拆箱unboxing"></a>
### 装箱(boxing)、拆箱(unboxing)
装箱就是隐式的将一个值型转换为引用型对象。
```cs
//将i进行装箱操作
int i=0;
object obj=i;
```

拆箱就是将一个引用型对象转换成任意值型
```cs
针对上例中的obj进行拆箱
int res = (int)obj;
```

```cs
int i=0;//L1
object obj=i;//L2
Console.WriteLine(i+","+(int)obj);//L3
```
上述代码实际进行了三次装箱、一次拆箱

L2行，i装箱为obj，1次装箱；

L3行，writeline参数应该为字符串，即i又进行一次装箱，变为string引用类型，2次装箱；

L3行，(int)obj对obj对象进行拆箱转换为值类型，1次拆箱；

L3行，(int)obj的结果为值类型，控制台打印输出需要又一次的装箱为string类型，3次装箱；

频繁的装拆箱会造成性能的损耗

<a id="markdown-结构体" name="结构体"></a>
### 结构体
结构体是值类型数据结构。它使得一个单一变量可以存储各种数据类型的相关数据。struct 关键字用于创建结构体。

结构存放在栈中并按值传递，和存放在堆中的类对象相比，它们具有性能上的优势。
1. 值类型的分配优于引用类型。
2. 存放在栈中的值一离开作用域就立即被收回。不用等待垃圾回收器来完成工作。

```cs
//定义结构体
public struct Books
{
    //定义字段
    public string _field;
    
    //定义属性
    public string PropertyName { get; set;}
    
    //定义方法
    public void Say(){ }
};  
```

<a id="markdown-结构体和类" name="结构体和类"></a>
#### 结构体和类
类和结构有以下几个基本的不同点：
* 类是引用类型，结构是值类型。
* 结构不支持继承。
* 结构不能声明默认的构造函数。

以下代码体现了，结构体在参数传递时实际传递的是副本，而不是像类一样传递引用。
```cs
//定义Student类
public class Student
{
    public string Name { get; set; }
}

//定义StructStu结构体
public struct StructStu
{
    public string Name { get; set; }
}

class Program
{
    static void ResetName(StructStu stu)
    {
        stu.Name = "default";
    }

    static void ResetName(Student stu)
    {
        stu.Name = "default";
    }

    static void Main(string[] args)
    {
        Student stu1 = new Student();
        stu1.Name = "jack";

        StructStu stu2 = new StructStu();
        stu2.Name = "jack";

        ResetName(stu1);
        ResetName(stu2);

        Console.WriteLine("修改后的值：" + stu1.Name);
        Console.WriteLine("修改后的值：" + stu2.Name);
    }
}
```

和引用类型相比，结构越复杂，复制造成的性能开销越大。因此，结构应该只用来表示小的数据结构。


<a id="markdown-流程控制" name="流程控制"></a>
## 流程控制
<a id="markdown-顺序" name="顺序"></a>
### 顺序
程序渐进的流程，一条语句一条语句地逐条推进，按预先设置好的步骤来完成功能

<a id="markdown-分支" name="分支"></a>
### 分支
if...else...

<a id="markdown-循环" name="循环"></a>
### 循环
- do{}while()
- while(true){}
- for(){}

跳出循环：

break
continue
return


<a id="markdown-数组" name="数组"></a>
## 数组
数组是一个存储相同类型元素的固定大小的顺序集合。数组是用来存储数据的集合，通常认为数组是一个同一类型变量的集合。
数组中某个指定的元素是通过索引来访问的。所有的数组都是由连续的内存位置组成的。最低的地址对应第一个元素，最高的地址对应最后一个元素。
这也是为什么在初始化数组的时候就需要指定数组的大小。

<a id="markdown-一维数组" name="一维数组"></a>
### 一维数组
在内存中是顺序连续存储的，所以它的索引速度非常快，赋值与修改元素也很简单。数组也是一个引用类型，初始化需要使用new关键字。

```cs
//使用字面值
int[] array = { 1, 2, 3, 4, 5 };
//使用new操作符
int[] array = new int[5];
//两者结合
int[] array = new int[] { 1, 2, 3, 4, 5 };
```

<a id="markdown-循环-1" name="循环-1"></a>
### 循环
```cs
//索引遍历（for循环）
for (int i = 0; i < array.Length; i++){..array[i]..}

/*
只读遍历
foreach 是自动迭代的，不需要事先获取数组的长度，但是只能读数据而不能写数据
只有实现了 IEnumerable 接口的类才能使用 foreach
*/
foreach (int data in array){..data..}
foreach (var data in array){..data..}

//示例
int[] array = { 1, 2, 3, 4, 5 };
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(i);
}
foreach (int item in array)
{
    Console.WriteLine(item);
}
```

<a id="markdown-多维数组" name="多维数组"></a>
### 多维数组
多维数组最简单的形式是二维数组。一个二维数组，在本质上，是一个一维数组的列表。

一个二维数组可以被认为是一个带有 x 行和 y 列的表格。下面是一个二维数组，包含 3 行和 4 列：

![](../assets/Programming/two_dimensional_arrays.jpg)

规则数组，即每行的元素个数都是相同的
```cs
//int[,]这样声明的二维数组，需要通过相同索引器进行访问：array1[1,1]
int[,] array1 = { { 1, 2, 3, 4 }, { 4, 5, 6, 7 }, { 8, 9, 10, 11 } };
int[,] array2 = new int[3, 4];
int[,] array3 = new int[,] { { 1, 2, 3, 4 }, { 4, 5, 6, 7 }, { 8, 9, 10, 11 } };

//循环遍历
foreach (int item in array1)
{
    Console.Write(item + "\t");
}
Console.WriteLine();
```

锯齿数组，即不规则数组
```cs
//锯齿数组，同样可以使用for和foreach进行遍历，通过索引器访问 array[1][1]
int[][] array = new int[3][] { new int[] { 1, 2, 3, 4 }, new int[] { 5, 6, 7 }, new int[] { 8, 9 } };
int[][] array = new int[][] { new int[] { 1, 2 }, new int[] { 1, 2, 3 }, new int[] { } };

//循环遍历
foreach (int[] item in array)
{
    foreach (int v in item)
    {
        Console.Write(v + "\t");
    }
    Console.WriteLine();
}
```

<a id="markdown-array" name="array"></a>
### Array
Array类是一个抽象类，无法实例化该类。主要作为基类进行扩展，实际使用中很少直接使用Array类。

但可以通过它的一些静态方法来进行数组的创建、遍历、拷贝、排序等操作，下面给出部分示例：
```cs
/*
以下两种初始化的方式是等效的
*/
string[] arr = { "a", "b", "c" };

Array arr = Array.CreateInstance(typeof(string), 3);
arr.SetValue("a", 0);
arr.SetValue("b", 1);
arr.SetValue("c", 2);
```

<a id="markdown-方法" name="方法"></a>
## 方法
一个方法是把一些相关的语句组织在一起，用来执行一个任务的语句块。每一个 C# 程序至少有一个带有 Main 方法的类。

定义方法：
```cs
/*
<Access Specifier> 访问修饰符
<Return Type> 返回类型
<Method Name> 方法名
Parameter List 形参列表
*/
<Access Specifier> <Return Type> <Method Name>(Parameter List)
{
   Method Body
}
```

调用方法：`MethodName(<parameter>);`

<a id="markdown-形参实参" name="形参实参"></a>
### 形参实参
```cs
//方法的定义，返回类型int，方法名Add，形参列表：int a, int b
int Add(int a, int b)
{
    return a + b;
}

//方法的调用，传入实参 1和2
int sum = Add(1, 2);
```

<a id="markdown-重载" name="重载"></a>
### 重载
```cs
public int Calculate(int x, int y) {......}
public double Calculate(double x, double y) {......}
```
特点（两必须一可以）
1. 方法名必须相同
2. 参数列表必须不相同
3. 返回值类型可以不相同

<a id="markdown-参数传递" name="参数传递"></a>
### 参数传递
当调用带有参数的方法时，您需要向方法传递参数。在 C# 中，有三种向方法传递参数的方式：

方式 | 描述
---|---
值参数 | 这种方式复制参数的实际值给函数的形式参数，实参和形参使用的是两个不同内存中的值。在这种情况下，当形参的值发生改变时，不会影响实参的值，从而保证了实参数据的安全。
引用参数 | 这种方式复制参数的内存位置的引用给形式参数。这意味着，当形参的值发生改变时，同时也改变实参的值。
输出参数 | 这种方式可以返回多个值。

<a id="markdown-值传递" name="值传递"></a>
#### 值传递
值参数，实际在传递时发生了拷贝，即方法调用时实际改变你的是变量的副本。如下例所示：
```cs
static void Swap(int x, int y)
{
    int temp = x;
    x = y;
    y = temp;
}

static void Main(string[] args)
{
    int a = 1;
    int b = 2;
    Swap(a, b);
    Console.WriteLine("交换后：{0}\t{1}", a, b);
}
```

<a id="markdown-引用传递" name="引用传递"></a>
#### 引用传递
引用参数是一个对变量的内存位置的引用。当按引用传递参数时，与值参数不同的是，它不会为这些参数创建一个新的存储位置。
引用参数表示与提供给方法的实际参数具有相同的内存位置。

下面案例中的类Student是一个引用类型，在参数传递时并未发生拷贝，传递的是地址，所以在方法内的改变也会影响到对象本身。
```cs
public class Student
{
    public string Name { get; set; }
}

class Program
{
    static void ResetStudent(Student stu)
    {
        stu.Name = "default name";
    }

    static void Main(string[] args)
    {
        Student stu = new Student();
        stu.Name = "jack";
        ResetStudent(stu);
        Console.WriteLine(stu.Name);
    }
}
```

针对上例中的交换方法Swap难道没有办法进行引用传递吗？即传递是变量本身，而非值的副本。

当然，我们可以使用ref关键字来声明参数是引用传递，需要特别注意方法声明和调用处都需要添加ref关键字，ref是reference的简写。如下示例：
```cs
static void Swap(ref int x, ref int y)
{
    int temp = x;
    x = y;
    y = temp;
}

static void Main(string[] args)
{
    int a = 1;
    int b = 2;
    Swap(ref a, ref b);
    Console.WriteLine("交换后：{0}\t{1}", a, b);
}
```

<a id="markdown-输出参数" name="输出参数"></a>
#### 输出参数
return 语句可用于只从函数中返回一个值。但是，可以使用 输出参数 来从函数中返回两个值。
输出参数会把方法输出的数据赋给自己，其他方面与引用参数相似。
```cs
static void AddValue(out int val)
{
    //模拟返回值，通过out关键字，可以返回多个值
    val = 5;
}

static void Main(string[] args)
{
    int res;
    AddValue(out res);
}
```

<a id="markdown-params" name="params"></a>
#### params
有时，当声明一个方法时，您不能确定要传递给函数作为参数的参数数目。
在使用数组作为形参时，C# 提供了 params 关键字，使调用数组为形参的方法时，既可以传递数组实参，也可以传递一组数组元素。

params 的使用格式为：`public 返回类型 方法名称( params 类型名称[] 数组名称 )`
```cs
static int GetSum(params int[] arr)
{
    int sum = 0;
    foreach (int i in arr)
    {
        sum += i;
    }
    return sum;
}

static void Main(string[] args)
{
    int sum = GetSum(1, 2, 3, 4, 5);
    Console.WriteLine("总和是： {0}", sum);
}
```
需要注意的是：
1. 带 params 关键字的参数类型必须是一维数组，不能使用在多维数组上；
2. 不允许和 ref、out 同时使用；
3. 带 params 关键字的参数必须是最后一个参数，并且在方法声明中只允许一个 params 关键字。
4. 不能仅使用 params 来使用重载方法。
5. 没有 params 关键字的方法的优先级高于带有params关键字的方法的优先级

<a id="markdown-数据集合datacollection" name="数据集合datacollection"></a>
## 数据集合DataCollection

<a id="markdown-arraylist" name="arraylist"></a>
### ArrayList
在System.Collections命名空间下，同时继承了IList接口。

ArrayList对象的大小可按照其中存储的数据进行动态增减，所以在声明ArrayList对象时并不需要指定它的长度。

但是由于ArrayList会把插入其中的所有数据当作为object类型来处理，在存储或检索值类型时会发生装箱和拆箱操作，带来很大的性能耗损。

另外，ArrayList没有泛型的实现，也就是ArrayList不是类型安全的，在我们使用ArrayList处理数据时，很可能会报类型不匹配的错误。

因为ArrayList存在不安全类型与装箱拆箱的缺点，所以出现了泛型的概念。
```cs
//没有类型的约束，数值、字符串、布尔值均可以作为元素
ArrayList arrList = new ArrayList();
arrList.Add(1);//装箱 int->object
arrList.Add("abc");//装箱 string->object
arrList.Add(true);//装箱 bool->object
```

<a id="markdown-hashtable" name="hashtable"></a>
### Hashtable
Hashtable也并非类型安全的，用于处理和表现类似key-value的键值对，其中key通常可用来快速查找，同时key是区分大小写；

value用于存储对应于key的值。Hashtable中key-value键值对均为object类型，所以Hashtable可以支持任何类型的key-value键值对.

```cs
Hashtable ht = new Hashtable();
ht.Add(0, 1);
ht.Add("key", "name");
ht.Add(1.23, true);

//添加一个keyvalue键值对：
ht.Add(key,value);

//移除某个keyvalue键值对：
ht.Remove(key);

//移除所有元素：           
ht.Clear(); 

// 判断是否包含特定键key：
ht.Contains(key);
```

什么情况下应该使用Hashtable：
1. 某些数据会被高频率查询
2. 数据量大
3. 查询字段包含字符串类型
4. 数据类型不唯一

<a id="markdown-排序列表sortedlist" name="排序列表sortedlist"></a>
### 排序列表SortedList
SortedList 类代表了一系列按照键来排序的键/值对，这些键值对可以通过键和索引来访问。

排序列表是数组和哈希表的组合。它包含一个可使用键或索引访问各项的列表。
如果您使用索引访问各项，则它是一个动态数组（ArrayList）；
如果您使用键访问各项，则它是一个哈希表（Hashtable）。
集合中的各项总是按键值排序。

```cs
//需要添加 using System.Collections;
SortedList sl = new SortedList();
sl.Add("002", "钱二");
sl.Add("001", "赵一");
sl.Add("003", "孙三");
sl.Add("004", "李四");

//通过key值进行访问
Console.WriteLine(sl["001"]);

//虽然添加时并未排序，但遍历时会按照key进行排序
foreach (var item in sl.Keys)
{
    Console.WriteLine("遍历：" + sl[item]);
}
```

<a id="markdown-堆栈stack" name="堆栈stack"></a>
### 堆栈Stack
堆栈（Stack）代表了一个后进先出LIFO的对象集合。当您需要对各项进行后进先出的访问时，则使用堆栈。
当您在列表中添加一项，称为推入元素，当您从列表中移除一项时，称为弹出元素。

* Count：返回栈中所包含的元素个数
* Clear：删除所有的项
* Peek：返回一个处于调用栈顶端的对象的引用，但不删除它。
* Pop：返回并删除顶端的对象
* Push：向栈中添加指定的对象

```cs
//需要添加 using System.Collections;
Stack st = new Stack();
st.Push(1);
st.Push("abc");
st.Push(true);
st.Push(new object());

Console.WriteLine("长度：" + st.Count);

Console.WriteLine(st.Peek());
Console.WriteLine("长度：" + st.Count);

Console.WriteLine(st.Pop());
Console.WriteLine("长度：" + st.Count);
```

<a id="markdown-队列queue" name="队列queue"></a>
### 队列Queue
队列（Queue）代表了一个先进先出的对象集合。
当您需要对各项进行先进先出的访问时，则使用队列。
当您在列表中添加一项，称为入队，当您从列表中移除一项时，称为出队。类似排队的效果。

```cs
//需要添加 using System.Collections;
Queue qu = new Queue();
qu.Enqueue("赵一");
qu.Enqueue("钱二");
qu.Enqueue("孙三");
qu.Enqueue("李四");

foreach (var item in qu)
{
    Console.WriteLine("入队后：" + item);
}
qu.Dequeue();
foreach (var item in qu)
{
    Console.WriteLine("出队：" + item);
}
```

<a id="markdown-泛型" name="泛型"></a>
## 泛型
泛型可以定义类型安全的数据结构，而无须使用实际的数据类型。有助于最大限度地重用代码、保护类型的安全以及提高性能。
泛型（Generic）允许您延迟编写类或方法中的编程元素的数据类型的规范，直到实际在程序中使用它的时候。
换句话说，泛型允许您编写一个可以与任何数据类型一起工作的类或方法。

您可以通过数据类型的替代参数编写类或方法的规范。
当编译器遇到类的构造函数或方法的函数调用时，它会生成代码来处理指定的数据类型。

<a id="markdown-泛型使用" name="泛型使用"></a>
### 泛型使用
泛型类：
```cs
/// <summary>
/// 泛型数组类
/// 数组类型由调用者决定
/// </summary>
/// <typeparam name="T"></typeparam>
public class MyGenericArray<T>
{
    private T[] array;
    public MyGenericArray(int size)
    {
        array = new T[size + 1];
    }
    public T getItem(int index)
    {
        return array[index];
    }
    public void setItem(int index, T value)
    {
        array[index] = value;
    }
}
```

泛型方法：
```cs
/// <summary>
/// 泛型方法
/// 同样的交换逻辑，不同数据类型的交换不需要重复的定义方法，调用的时候决定类型即可
/// </summary>
/// <typeparam name="T"></typeparam>
/// <param name="t1"></param>
/// <param name="t2"></param>
static void Swap<T>(ref T t1, ref T t2)
{
    T temp = t1;
    t1 = t2;
    t2 = temp;
}

static void Main()
{
    int a = 1, b = 2;
    string str1 = "hello", str2 = "world";

    Swap<int>(ref a, ref b);
    Swap<string>(ref str1, ref str2);

    Console.WriteLine("交换后a:{0}\t b:{1}", a, b);
    Console.WriteLine("交换后str1:{0}\t str2:{1}", str1, str2);
}
```

<a id="markdown-泛型集合listt" name="泛型集合listt"></a>
### 泛型集合List<T>
List<T>类是 ArrayList 类的泛型等效类。

不会强行对值类型进行装箱和拆箱，或对引用类型进行向下强制类型转换，所以性能得到提高。

```cs
//限制类型只能是string，同样的限定类型也可以是值类型
List<string> lstRes = new List<string>();
//添加对象到结尾处
lstRes.Add("a");
lstRes.Add("b");
lstRes.Add("c");

//长度
int len = lstRes.Count;

//删除
lstRes.Remove("a");

//是否包含某个对象
lstRes.Contains("a");
```
更多的方法等待你去探索。。。

<a id="markdown-dictionaytkeytvalue" name="dictionaytkeytvalue"></a>
### Dictionay<Tkey,Tvalue>
在初始化的时候也必须指定其类型，而且他还需要指定一个Key,并且这个Key是唯一的。正因为这样，Dictionary的索引速度非常快。但是也因为他增加了一个Key,Dictionary占用的内存空间比其他类型要大。他是通过Key来查找元素的，元素的顺序是不定的。

```cs
Dictionary<string, string> dicRes = new Dictionary<string, string>();
dicRes.Add("zhangsan","张三");
dicRes.Add("zhaofugui", "赵富贵");
```


