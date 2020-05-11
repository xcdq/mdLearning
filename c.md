### strcmp函数

strcmp函数是string compare(字符串比较)的缩写，用于比较两个字符串并根据比较结果返回整数。基本形式为strcmp(str1,str2)，若str1=str2，则返回零；若str1<str2，则返回负数；若str1>str2，则返回正数。

### %g

%g 根据具体的数值选择 %e 或 %f   （当数据非常小时后面的可能省略，会用%e表示）

%g 用于打印浮点型数据时，会去掉多余的零

printf("%.2g",0.0123); ====> 0.012 效果相当于除去0后的有效位数

### strstr

strstr(str1,str2) 函数用于判断字符串str2是否是str1的子串。

如果是，则该函数返回 str1字符串从 str2第一次出现的位置开始到 str1结尾的字符串；

否则，返回NULL。

###  fgets与gets

1、 fgets比gets安全，使用gets编译时会警告

为了安全，gets少用，因为其没有指定输入字符的大小，限制输入缓冲区得大小，如果输入的字符大于定义的数组长度，会发生内存越界，堆栈溢出。后果非常怕怕

 fgets会指定大小，如果超出数组大小，会自动根据定义数组的长度截断。

2、 用strlen检测两者的输入的字符串长度，结果不一样

回车输入结束时，fgets会把回车换行符也存入到字符串里

fgets函数fgets函数用来从文件中读入字符串。fgets函数的调用形式如下：fgets（str，n，fp）；

此处，fp是文件指针；str是存放在字符串的起始地址；n是一个int类型变量。函数的功能是从fp所指文件中读入n-1个字符放入str为起始地址的空间内；如果在未读满n-1个字符之时，已读到一个换行符或一个EOF（文件结束标志），则结束本次读操作，读入的字符串中最后包含读到的换行符。

因此，确切地说，调用fgets函数时，最多只能读入n-1个字符。读入结束后，系统将自动在最后加'\0'，并以str作为函数值返回。

gets()将删除新行符， fgets()则保留新行符.

要去掉fgets()最后带的“\0"，只要用 s[strlen(s)-1]='\0';即可。

fgets不会像gets那样自动地去掉结尾的\n，所以程序中手动将\n位置处的值变为\0,代表输入的结束。



针对于fgets，还要再说两句，下面这种用法，是安全的判断文件读取结束或者出错的好方式，切忌不能使用while(!feof(fp)) ，还有对于fgets的第二个参数是最大能读取文件字符的个数，一般最大的长度是1024字节。
