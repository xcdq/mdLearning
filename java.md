## 读写文件

如前所述，一个流被定义为一个数据序列。输入流用于从源读取数据，输出流用于向目标写数据。

下图是一个描述输入流和输出流的类层次图。

![img](https://www.runoob.com/wp-content/uploads/2013/12/iostream2xx.png)

下面将要讨论的两个重要的流是 FileInputStream 和 FileOutputStream：

------

## FileInputStream

该流用于从文件读取数据，它的对象可以用关键字 new 来创建。

有多种构造方法可用来创建对象。

可以使用字符串类型的文件名来创建一个输入流对象来读取文件：

InputStream f = new FileInputStream("C:/java/hello");

也可以使用一个文件对象来创建一个输入流对象来读取文件。我们首先得使用 File() 方法来创建一个文件对象：

File f = new File("C:/java/hello"); InputStream out = new FileInputStream(f);

创建了InputStream对象，就可以使用下面的方法来读取流或者进行其他的流操作。

| **序号** | **方法及描述**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public void close() throws IOException{}** 关闭此文件输入流并释放与此流有关的所有系统资源。抛出IOException异常。 |
| 2        | **protected void finalize()throws IOException {}** 这个方法清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。抛出IOException异常。 |
| 3        | **public int read(int r)throws IOException{}** 这个方法从 InputStream 对象读取指定字节的数据。返回为整数值。返回下一字节数据，如果已经到结尾则返回-1。 |
| 4        | **public int read(byte[] r) throws IOException{}** 这个方法从输入流读取r.length长度的字节。返回读取的字节数。如果是文件结尾则返回-1。 |
| 5        | **public int available() throws IOException{}** 返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取的字节数。返回一个整数值。 |

除了 InputStream 外，还有一些其他的输入流，更多的细节参考下面链接：

- [ByteArrayInputStream](https://www.runoob.com/java/java-bytearrayinputstream.html)
- [DataInputStream](https://www.runoob.com/java/java-datainputstream.html)

------

## FileOutputStream

该类用来创建一个文件并向文件中写数据。

如果该流在打开文件进行输出前，目标文件不存在，那么该流会创建该文件。

有两个构造方法可以用来创建 FileOutputStream 对象。

使用字符串类型的文件名来创建一个输出流对象：

OutputStream f = new FileOutputStream("C:/java/hello")

也可以使用一个文件对象来创建一个输出流来写文件。我们首先得使用File()方法来创建一个文件对象：

File f = new File("C:/java/hello"); OutputStream f = new FileOutputStream(f);

创建OutputStream 对象完成后，就可以使用下面的方法来写入流或者进行其他的流操作。

| **序号** | **方法及描述**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public void close() throws IOException{}** 关闭此文件输入流并释放与此流有关的所有系统资源。抛出IOException异常。 |
| 2        | **protected void finalize()throws IOException {}** 这个方法清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。抛出IOException异常。 |
| 3        | **public void write(int w)throws IOException{}** 这个方法把指定的字节写到输出流中。 |
| 4        | **public void write(byte[] w)** 把指定数组中w.length长度的字节写到OutputStream中。 |

除了OutputStream外，还有一些其他的输出流，更多的细节参考下面链接：

- [ByteArrayOutputStream](https://www.runoob.com/java/java-bytearrayoutputstream.html)
- [DataOutputStream](https://www.runoob.com/java/java-dataoutputstream.html)

### 实例

下面是一个演示 InputStream 和 OutputStream 用法的例子：

## fileStreamTest.java 文件代码：

import java.io.*;  public class fileStreamTest {    public static void main(String args[]) {        try {            byte bWrite[] = { 11, 21, 3, 40, 5 };            OutputStream os = new FileOutputStream("test.txt");            for (int x = 0; x < bWrite.length; x++) {                os.write(bWrite[x]); // writes the bytes            }            os.close();             InputStream is = new FileInputStream("test.txt");            int size = is.available();             for (int i = 0; i < size; i++) {                System.out.print((char) is.read() + "  ");            }            is.close();        } catch (IOException e) {            System.out.print("Exception");        }    } }

上面的程序首先创建文件test.txt，并把给定的数字以二进制形式写进该文件，同时输出到控制台上。

以上代码由于是二进制写入，可能存在乱码，你可以使用以下代码实例来解决乱码问题：

## fileStreamTest2.java 文件代码：

//文件名 :fileStreamTest2.java import java.io.*;  public class fileStreamTest2 {    public static void main(String[] args) throws IOException {         File f = new File("a.txt");        FileOutputStream fop = new FileOutputStream(f);        // 构建FileOutputStream对象,文件不存在会自动新建         OutputStreamWriter writer = new OutputStreamWriter(fop, "UTF-8");        // 构建OutputStreamWriter对象,参数可以指定编码,默认为操作系统默认编码,windows上是gbk         writer.append("中文输入");        // 写入到缓冲区         writer.append("\r\n");        // 换行         writer.append("English");        // 刷新缓存冲,写入到文件,如果下面已经没有写入的内容了,直接close也会写入         writer.close();        // 关闭写入流,同时会把缓冲区内容写入文件,所以上面的注释掉         fop.close();        // 关闭输出流,释放系统资源         FileInputStream fip = new FileInputStream(f);        // 构建FileInputStream对象         InputStreamReader reader = new InputStreamReader(fip, "UTF-8");        // 构建InputStreamReader对象,编码与写入相同         StringBuffer sb = new StringBuffer();        while (reader.ready()) {            sb.append((char) reader.read());            // 转成char加到StringBuffer对象中        }        System.out.println(sb.toString());        reader.close();        // 关闭读取流         fip.close();        // 关闭输入流,释放系统资源     } }





更改⽬录： 

* cd <路径>
* cd .. 移动到上级⽬录
* pushd <路径> 记住来源的同时移动到其他⽬录，
* popd 返回来源
* ⽬录列举： 
* ls 列举出当前⽬录下所有的⽂件和⼦⽬录名（不包含隐藏⽂件），
可以选择使⽤通配符 * 来缩⼩搜索范围。
  ⽰例(1)： 列举所有以“.?ava”结尾的⽂件，输⼊ ls *.?a
  ⽰例(2)： 列举所有以“F”开头，“.?ava”结尾的⽂件，输⼊
  创建⽬录：
* Mac/L?nux 系统：m?d?r
⽰例：m?d?r boo?s
  W?ndows 系统：md
  ⽰例：md boo?s
  移除⽂件：
  Mac/L?nux 系统：rm
  ⽰例：rm some??le.?ava
  W?ndows 系统：del
  ⽰例：del some??le.?ava
  移除⽬录：
  Mac/L?nux 系统：rm -r
  ⽰例：rm -r boo?s
  W?ndows 系统：deltree
  ⽰例：deltree boo?s
  重复命令： !! 重复上条命令
  ⽰例：!n 重复倒数第n条命令
  命令历史：
  Mac/L?nux 系统：h?story
  W?ndows 系统：按 F7 键
  ⽂件解压：
  L?nux/Mac 都有命令⾏解压程序 unz?p，你可以通过互联⽹为 W?ndow
  图形界⾯下（W?ndows 资源管理器，Mac F?nder，L?nux Naut?lus
  在 Mac 上选择“open”，在 L?nux 上选择“extract here”，或在 W?
  要了解关于 shell 的更多信息，请在维基百科中搜索 W?ndows shell，

数据存储
那么，程序在运⾏时是如何存储的呢？尤其是内存是怎么分配的。有5个
不同的地⽅可以存储数据：
1. 寄存器（Registers）最快的存储区域，位于 CPU 内部 。然⽽，寄
存器的数量⼗分有限，所以寄存器根据需求进⾏分配。我们对其没有
直接的控制权，也⽆法在⾃⼰的程序⾥找到寄存器存在的踪迹（另⼀
⽅⾯，C/C++ 允许开发者向编译器建议寄存器的分配）。
2. 栈内存（Stack）存在于常规内存 RAM（随机访问存储器，Random
Access Memory）区域中，可通过栈指针获得处理器的直接⽀持。栈
指针下移分配内存，上移释放内存，这是⼀种快速有效的内存分配⽅
法，速度仅次于寄存器。创建程序时，Java 系统必须准确地知道栈
内保存的所有项的⽣命周期。这种约束限制了程序的灵活性。因此，
虽然在栈内存上存在⼀些 Java 数据，特别是对象引⽤，但 Java 对
象却是保存在堆内存的。
3. 堆内存（Heap）这是⼀种通⽤的内存池（也在 RAM 区域），所有
Java 对象都存在于其中。与栈内存不同，编译器不需要知道对象必
须在堆内存上停留多⻓时间。因此，⽤堆内存保存数据更具灵活性。
创建⼀个对象时，只需⽤   new  命令实例化对象即可，当执⾏代码
时，会⾃动在堆中进⾏内存分配。这种灵活性是有代价的：分配和清
理堆内存要⽐栈内存需要更多的时间（如果可以⽤ Java 在栈内存上
创建对象，就像在 C++ 中那样的话）。随着时间的推移，Java 的堆
内存分配机制现在已经⾮常快，因此这不是⼀个值得关⼼的问题了。
4. 常量存储（Constant storage）常量值通常直接放在程序代码中，因
为它们永远不会改变。如需严格保护，可考虑将它们置于只读存储器
ROM （只读存储器，Read Only Memory）中 。

5. ⾮ RAM 存储（Non-RAM storage）数据完全存在于程序之外，在程
序未运⾏以及脱离程序控制后依然存在。两个主要的例⼦：（1）序
列化对象：对象被转换为字节流，通常被发送到另⼀台机器；（2）
持久化对象：对象被放置在磁盘上，即使程序终⽌，数据依然存在。
这些存储的⽅式都是将对象转存于另⼀个介质中，并在需要时恢复成
常规的、基于 RAM 的对象。Java 为轻量级持久化提供了⽀持。⽽诸
如 JDBC 和 Hibernate 这些类库为使⽤数据库存储和检索对象信息提
供了更复杂的⽀持。



Java 确定了每种基本类型的内存占⽤⼤⼩。 这些⼤⼩不会像其他⼀些语
⾔那样随着机器环境的变化⽽变化。这种不变性也是 Java 更具可移植性
的⼀个原因。

| 基本类型 | ⼤⼩   | 最⼩值 | 最⼤值 | 包装类型 |
| -------- | ------ | ------ | ------ | -------- |
| boolean  |        |        |        | Boolean  |
| char     | 16bits | bits   |        |          |
|          |        |        |        |          |
|          |        |        |        |          |
|          |        |        |        |          |
|          |        |        |        |          |
|          |        |        |        |          |
|          |        |        |        |          |
|          |        |        |        |          |

 — — — 
char


Unicode
0
Unicode 2
-1
Character
byte 8 bits -128 +127 Byte
short
16
bits

- 2 + 2 -1 Short
int
32
bits
- 2 + 2 -1 Integer
long
64
bits
- 2 + 2 -1 Long
float
32
bits
IEEE754 IEEE754 Float
double
64
bits
IEEE754 IEEE754 Double
void — — — Void
16
15 15
31 31
63 63
Introduction
59
所有的数值类型都是有正/负符号的。布尔（boolean）类型的⼤⼩没有明
确的规定，通常定义为取字⾯值 “true” 或 “false” 。基本类型有⾃⼰对应
的包装类型，如果你希望在堆内存⾥表⽰基本类型的数据，就需要⽤到它
们的包装类。代码⽰例：
char c = 'x';
Character ch = new Character(c);
或者你也可以使⽤下⾯的形式：
Character ch = new Character('x');
基本类型⾃动转换成包装类型（⾃动装箱）
Character ch = 'x';
相对的，包装类型转化为基本类型（⾃动拆箱）：
char c = ch;
个中原因将在以后的章节⾥解释。