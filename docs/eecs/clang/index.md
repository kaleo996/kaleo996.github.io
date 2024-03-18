# 浙大 C 小程纠错本

题目来自俞欢军老师在 2021 年秋冬学期布置的作业和 PTA 上的浙大版《 C 语言程序设计（第4版）》题目集。嗯，是的，我刷穿了课本配套的习题集，希望能帮大家复习，但请以后的同学们不要做这种傻事。

写这份文件的时候我也很稚嫩呢，需要趁我忘光 C 语言之前改改了。

小题里有很多神秘的缩进格式，是因为这些题目本来就长这样。我自己写代码是按照谷歌代码规范来的。

## 一、考前注意事项

避免初学者的经典错误：

- 小心除法。C 语言中 `5/9` 等于 0，而 `5.0/9` 等于 0.555……
- 检查该赋值的变量是否都赋值了或者初始化了。
- 判断相等关系是 `==` 不是 `=` ，单个等号是赋值符。
- for 循环的 `for(语句1; 语句2; 语句3)` 中是两个分号，不是逗号。
- do-while 循环的 `while(循环条件);` 最后面是有分号的。
- 检查 switch 语句中各个 case 后面是否需要 `break;`。
- 填空题注意检查有没有通过 `++`、`--` 和指针对变量的修改。
- 别忘了函数最后一般有return语句。
- 要用 `strlen( )` 等函数的话别忘了引用 `string.h` 头文件。

那些需要背诵且容易忘的概念题：

- C 程序由函数构成。
- 程序设计语言必须具备数据表达和流程控制的功能。
- C 语言中标识符由字母、数字、下划线构成，第一个字符不可以是数字。
- C 语言生成的目标代码质量高，运行效率高。
- C 语言是编译型语言，移植性比较不好。
- 算法是一组明确的解决问题的步骤，它产生结果并在有限的时间内终止，可以用自然语言、伪代码、流程图描述。
- 算数表达式是指用算数运算符（自增、自减运算符，四则运算符，求余数运算符）连接的符合 C 语言语法的表达式，例如 `(i++) * j % k`。
- 赋值表达式中，赋值运算符右侧的表达式的数据类型和左侧变量的类型不一样，会自动把右侧结果强制类型转换，再储存到左侧变量中，例如 `float a = 1;`。
- 位运算是 C 语言的特色，可以让 C 实现很多汇编语言可以做到但其他高级语言不行的操作。位运算不属于逻辑表达式，即 `a & b` 和 `a && b` 并不是同一类运算。

常见报错信息：

- 段错误，多半是 `scanf( )` 忘了加&，也可能是用了空指针。
- 运行超时，可能是因为用了太多 `pow( )` 这样很慢的函数导致复杂度过高，也可能是因为有死循环。
- 格式错误，就是空格、换行有问题而已，好解决。
- 非零返回，可能是主函数最后没有 `return 0;` 。但如果加上了 `return 0;` 主函数返回值依然是很大很怪的数字，可能是因为源代码中有语法错误或未定义行为，程序直接崩溃了，或者还能正常运行一部分产生正确的输出但最后不正常地结束运行了。

其他：

- 老师没教怎么用 IDE 的调试功能不代表我们不需要会。非常建议平时抽五分钟时间上 B 站找个视频学一下，可以提高 debug 效率。
- 翁恺老师：“实际编程的时候有 25% 的问题出在读入数据的时候。建议着重检查 `scanf( )`，调试的时候要在 `scanf( )` 之后立刻 `printf( )` 一下，以确认 `scanf( )` 真的读入了你想它读入的东西。这种在调试的时候让程序在运行中途输出一些数据来帮助我们确认程序是否按照我们所想的方式在运行的方法，就是所谓的‘输出日志’。”
- 这门课的考试题目有很多坑题，考试的时候应该稳一点，把自己当成电脑，要在草稿纸上跟踪程序中每个变量的一步步变化。切忌自以为理解了代码的用意就想当然地写下一个答案，很可能这段程序里藏了小 bug。
- 这门课考试是有题库的，会考往年真题，所以考前最好刷一下学解卖的往年真题，再记住那些坑题、难题，说不定考试的时候能捡回几分。
- 来不及刷完真题也别太焦虑。我当时不知道要刷真题，就对着课本和平时作业嗯复习，最后绩点还是有 4.8 / 5.0。只要知识点理解了就不会有大问题。

## 二、理论考

有判断、选择、填空题。

1\. 有一函数：

$y=
\begin{cases}
1,&\text{x>0}\\\\
0,&\text{x=0}\\\\
-1,&\text{x<0}
\end{cases}$

用 C 语言表示，以下程序段中错误的是（ C ）。

```c title='C'
y = 0;
if(x >= 0); // 首先，这个分号就让第一个if语句提前结束了
if(x > 0) y = 1;
else y = -1;
```

```c title='D'
if(x >= 0)
if(x > 0) y = 1;
else y = 0; // 这个else语句跟if(x > 0)
else y = -1; // 这个else语句跟if(x >= 0)
```

if-else 嵌套 if-else 时，else 语句跟离它最近的那个不带 else 语句的 if 语句。想让 else 跟前面离它更远的 if，可以把后面的 if 用 { } 括起来，剩 else 在大括号外，如下：

```c title='示例'
if (x >= 0)
    if (x > 0)
        y = 1;
else
    y = -1 // 这个else语句跟的是 if (x >= 0)
```

也可以用一个 `else;` 的空语句让后面的 if 不能再跟 else，接下来的 else 就会跟前面的 if。这样写代码真是丑极了，如果不是为了出考题恶心本科生谁会这样写呢？

```c title='示例'
if (x >= 0)
    if (x > 0)
        y = 1;
    else; // 这个else空语句跟的是if(x > 0)
else
    y = -1 // 这个else语句跟的是if(x >= 0)
```

2\. 设变量已正确定义，则以下（ C ）是合法的 switch 语句。

```c title='B'
switch(op) { // 不合法，不能有两个带一样常量的 case。这里 * 用了两次
    case '*': printf("%d\n", value1 * value2); break;
    case '+': printf("%d\n", value1 + value2); break;
    case '-': printf("%d\n", value1 - value2); break;
    case '*': printf("%d\n", value1 * value2); break;
    default: printf("Error\n"); break;
}
```

```c title='C'
switch('/') { // 合法，只是会一直 default 而已
    case '*': printf("%d\n", value1 * value2); break;
    case '-': printf("%d\n", value1 - value2); break;
    case '+': printf("%d\n", value1 + value2); break;
    default: printf("Error\n"); break;
}
```

3\. 写出能作这个条件判断的 C 表达式：“year 是闰年，即 year 能被 4 整除但不能被 100 整除，或 year 能被 400 整除。”

一种正确解答：`year%4==0 && year%100!=0 || year%400==0`

可以这么记：`||` 长得更高，优先级却反而比 `&&` 低。但是记不住这个优先级是很正常的，写代码的人最好考虑到读代码的人的感受，更好的解答是：`((year%4==0) && (year%100!=0)) || (year%400==0)`

4\. 在C程序运行过程中，其值不能被改变的量称为常量，其值可以改变的量称为变量。（✔️）

有些同学学到后来会把“标识符”和“变量”搞混，以为标识符就是变量名。标识符是用户编程时使用的名字，用于给变量、常量、函数等命名，以建立起名称与实体之间的关系。

<center>![标识符和变量](var.png)</center>

5\. 为了检查以下 if-else 语句的两个分支是否正确，至少需要设计 3 组测试用例。（✔️）

```c
if (x <= 15) { 
   y = 4 * x / 3;
} else {
   y = 2.5 * x - 10.5;
}
```

测试的时候一定要单独测试临界点。尽管这里 x 等于 15 的情况也是进入 `if (x <= 15)` 的分支，但必须单独测试，也就是需要 x 小于 / 等于 / 大于 15，三种测试用例。

6\. 以下程序段的功能是输出 1～100 之间每个整数的各位数字之和。（❌）

```c
for (num = 1; num <= 100; num++) { 
    s = 0;
    do{
       s = s + num % 10;
       num = num / 10;
    } while (num != 0);
    printf("%d\n", s); 
}
```

这个会死循环，一直输出 1，因为 do-while 直接用了 num 做循环变量，导致 num 被反复归零。

7\. 若变量已正确定义，以下 while 循环正常结束时，累加到 `pi` 的最后一项item的值满足（ A ）。

A. item 的绝对值小于 0.0001

C. item 的绝对值大于等于 0.0001

```c
flag = 1;
denominator = 1;
item = 1.0;
pi = 0;
while(fabs(item) >= 0.0001){ /*乙*/
  item = flag * 1.0 / denominator;  /*甲*/
  pi = pi + item;
  flag = -flag;
  denominator = denominator + 2;
}
```

甲处 item 的绝对值恰好大于 0.0001 时，回到乙后，再进入循环，在甲处计算出一个绝对值小于 0.0001 的新 item 再加上去，然后才结束循环。

8\. 在函数调用 `Func(exp1, exp2+exp3, exp4*exp5)` 中，实参的数量是（ 3 ）

实参可以是常量/变量/表达式。这里 `exp1`、`exp2+exp3`、`exp4*exp5` 各算一个实参。

9\. 下列程序的输出结果是( `(3,6)` )。

```c
# include <stdio.h>
int f(int n)
{
    static int k, s;
    n--;
    for(k=n; k>0; k--)
    s += k;
    return s;
}
int main(void)
{
    int k;
    k = f(3);
    printf("(%d,%d)", k, f(k));
    return 0;
}
```

最后的 `f(k)` 的确是 `f(3)`，但因为函数 `f( )` 中有静态局部变量，其值在 `f( )` 每次运行后会保留，并影响下一次调用 `f( )`，所以不能套用前面算过的 `f(3)=3`。

10\. 以下正确的函数定义形式是（ A ）。

A. `double fun(int x, int y)`

B. `double fun(int x ; int y)`

C. `double fun(int x, int y);`

D. `double fun(int x, y)`

这里问的“函数定义形式”是指函数定义时函数首部的形式，问“函数声明形式”才应该选 C。函数定义/声明时，参数表中的参数之间是逗号，且每个参数都需要单独声明其数据类型。

```c
#include<stdio.h>
void sayhello(int n); // 这一行是函数声明
int main()
{
    sayhello(5); // 这一行是函数调用
    return 0;
}
// 下面这一块是函数定义
void sayhello(int n) // 第一行称为函数首部，包括返回值类型声明、函数名、参数表
{
    int i = 0;
    for(; i<n; i++)
        printf("Hello World!\n");
}
```

11\. `08` 是正确的整型常量。（❌）

0 开头表示这个常量是八进制的，0x 开头表示是十六进制的。八进制中不会出现 8 这个数码，因为数到 8 就该进位了。

12\. 表达式 `!x` 等价于 `x!=1` 。（❌）

C 语言关系表达式中，不止 1，所有除 0 之外的数，包括非 0 浮点数，都表示 true。只有 0 表示 false。当 `x` 为 0 时，`!x` 的值是 1；当 `x` 非0时，`!x` 的值是0。所以 `!x` 等价于 `x==0`。很多程序员会用 `!x` 代替 `x==0`，因为位运算是最快的运算。

13\. 表达式 `(z=0, (x=2)||(z=1), z)` 的值是（ 0 ）

用 `printf( )` 打印这个逗号表达式的值，输出 0。整个逗号表达式的值是最后一个分句的值。在 `||` 处，`x=2` 的返回值是 2，表示 true，所以整个逻辑表达式的值一定是 true，所以后面的 `z=1` 就不执行了，直接返回整个逻辑表达式的值为 1。如果 `||` 左边是 `x=0`，返回 0，就得继续执行 `z=1` 才能判断整个逻辑表达式是 true 还是 false ，逻辑表达式的值为 1。这种只计算逻辑表达式的一部分就已经能确定整个逻辑表达式的值的现象称为“逻辑短路”。

14\. 设字符型变量 x 的值是064，表达式 `~x ^ x << 2 & x` 的值是（ 0333 ）

按运算符优先级，`~` 最高，其次 `<<`，其次 `&`，其次 `^`。064 是 0 开头，说明是八进制，转成二进制的一个 Byte 进行位运算，为 `00110100`。先算 `~x`，按位取反，`11001011`。再算 `x << 2` ，左移 2 位，`00110100 << 2` 即为 `11010000`。然后 `x << 2` 的结果和 `x` 按位与，`11010000 & 00110100`，即为 `00010000`。最后 `~x` 的结果与 `00010000` 按位异或，`11001011 ^ 00010000`，为 `11011011`，即为 8 进制 `0333`。

> 这种题也就考考大学生，真写代码的时候写成这样肯定被同事打死。
><p align=right>——翁恺先生</p>

15\.  定义各变量及初始化如下：`int a = 2, b = 3, c = 1, d, x=10;`

`printf("%d", d = a > b);` 输出( 0 )

⬆️赋值的优先级低于关系运算，这里会先算 `a > b` 输出 0 表示 false，再把 0 赋值给 d，整个表达式的值就是最后赋值表达式中赋的值，也就是 0。

`printf("%d", b–1 == a != c);` 输出( 0 )

⬆️判断相等/不相等是从左到右运算的。先算 `b-1 == a`，成立，输出 1 表示 true；再算 `1 != c`，不成立，输出 0 表示 false。

`printf("%d", 3 <= x <= 5);` 输出( 1 )

⬆️关系运算从左往右运算。先算 `3 <= x`，输出1表示true；再算 `1 <= 5`，输出1表示true。

16\. 下述对C语言字符数组的描述中错误的是（ C ）。

A. 字符数组可以存放字符串

B. 字符数组中的字符串可以整体输入、输出

C. 可以在赋值语句中通过赋值运算符"="对字符数组整体赋值

D. 不可以用关系运算符对字符数组中的字符串进行比较

我错选了 B。可以用 `puts( )` 和 `gets( )` 实现字符数组的整体输入输出，用 `printf("%s",str)` 整体输出。数组没法整体引用，每次只能用下标引用数组中的一个元素。只能在刚定义字符数组时用=给字符数组“赋值”，形如 `char name[MAXN] = "Kaleo";`，但这叫做“初始化”，和赋值的原理是不一样的。不能用=来整体赋值字符数组，要用 `strcpy( )`。同样的，字符串比较不能用关系运算符，要用 `strcmp( )`。

17\.  有以下定义：`char x[] = "abcdefg"; char y[] = {'a', 'b', 'c', 'd', 'e', 'f', 'g'};`，则正确的叙述为（ C ）。

A.数组 x 和数组 y 等价

B.数组 x 和数组 y 的长度相同

C.数组 x 的长度大于数组 y 的长度

D.数组 x 的长度小于数组 y 的长度

计算字符串的长度用 `strlen(x)`，它遇到 `'\0'` 才能停止，并且不会把 `'\0'` 计入字符总数；计算数组长度用 `sizeof(y)`，会把 `'\0'` 计入数组长度。`x` 最后比 `y` 多了一个 `'\0'`，所以 `x` 数组长度比 `y` 大。这里 `y[ ]` 最后没有 `'\0'`，所以不是字符串，不能用 `strlen(y)` 算它长度，不然 `strlen( )` 函数一直没读到 `'\0'`，程序就会停不下来，最后崩溃。同样地，`puts( )` 函数遇到 `'\0'` 才会停止，忘了在字符数组结尾放 `'\0'` 也会导致程序崩溃。

18\. `int c[2][ ]={{1, 2}, {3, 4}};`（❌）

这样定义矩阵是错的，超过一维的数组，只有从左往右第一个 index 可以是空的。

19\. `int m, *p = &m; printf("%d",p);`（✔️）

定义变量 `m` 的时候，就已经给它分配内存空间了，只不过这块内存空间没初始化，用指针访问这块内存空间完全是可行的。用 `%d` 格式输出指针也不会出问题，只不过它是用十进制表示了指针变量指向的内存空间地址。用 `%p` 格式当然更好，是用十六进制输出的，更加专业。

![printf( )中用%%才可以输出单个百分号，这也是一种转义符](https://cdn.nlark.com/yuque/0/2022/png/25775350/1649724465223-683cbb02-84e3-441e-b8f5-d47dbab8a220.png#clientId=u7e66d3f0-c702-4&errorMessage=unknown%20error&from=paste&height=291&id=ub01a64e0&originHeight=483&originWidth=829&originalType=binary&ratio=1&rotation=0&showTitle=true&size=115502&status=error&style=none&taskId=u05e0dbb6-067c-4389-8aeb-e814a2ca8ca&title=printf%28%20%29%E4%B8%AD%E7%94%A8%25%25%E6%89%8D%E5%8F%AF%E4%BB%A5%E8%BE%93%E5%87%BA%E5%8D%95%E4%B8%AA%E7%99%BE%E5%88%86%E5%8F%B7%EF%BC%8C%E8%BF%99%E4%B9%9F%E6%98%AF%E4%B8%80%E7%A7%8D%E8%BD%AC%E4%B9%89%E7%AC%A6&width=500 "printf( )中用%%才可以输出单个百分号，这也是一种转义符")

20\. 以下选项中，对基本类型相同的指针变量不能进行运算的运算符是 ( A )。

A. `+`  B. `-`  C. `=`  D. `==`

B 和 D 的用法如下：

```c
#include<stdio.h>
int main() {
    char c[20] = "I am learning C.";
    char *p1 = &c[0], *p2 = &c[10];
    printf("两指针相隔的元素个数为%d\n", p2 - p1);
    if (p1 == p2)
        printf("两指针指向同一内存空间");
    else if (p1 != p2)
        printf("两指针不指向同一内存空间");
    return 0;
}
```

21\. 一维数组定义的一般形式如下，其中的类型名指定数组变量的类型。（❌）

`类型名 数组名[数组长度];`类型名是指数组元素的类型。很多同学以为“数组变量”是指数组元素，其实对于C而言，数组变量就是数组名，它的值等于数组第一个元素的内存地址。这个名字起得很奇怪，因为数组变量里有“变量”两个字，它的值却是不能改变的，是个常量。🤔

22\. 对于以下程序段，叙述正确的是（ D ）。

```c
char s[] = "china"; 
char *p; 
p = s;
```

A. `s` 和 `p` 完全相同

B. 数组 `s` 中的内容和指针变量 `p` 中的内容相等

C. 数组 `s` 的长度和 `p` 所指向的字符串长度相等

D. `*p` 与 `s[0]` 相等

`s` 和 `p` 的数据类型不一样，`s` 是数组变量，`p` 是字符指针变量。`p` 被赋值为 `s`，也就指向了字符串（结尾带 `'\0'` 的字符数组）的第一个字符，变量 `p` 中的内容是 `'c'`。数组长度包括结尾的 `'\0'`，而字符串长度不包括。

23\.  下面程序段的运行结果是（ B ）。

A. LANGUAGE  B. ANGU  C. LANGU  D. LANG

```c
char s[ ] = "language", *p = s;
while( *p++ != 'u')
    printf("%c", *p – 'a' + 'A');
```

相同优先级的单目运算是从右到左结合的，所以这里 `*p++` 相当于 `*(p++)`。

24\. 下列程序的执行结果是( `4 6` )

```c
#include <stdio.h>
int main(void) {
    int a[10], b[10], *pa, *pb, i;
    pa = a;
    pb = b;
    for( i = 0; i < 3; i++, pa++, pb++){ 
        *pa = i;
        *pb = 2*i;
    }
    pa = &a[0];
    pb = &b[0];
    for ( i = 0; i < 3; i++, pa++, pb++){
        *pa = *pa + i;
        *pb = *pb + i;
    }
    printf("%d %d", *--pa, *--pb);  
    return 0;
}
```

考试的时候做这种比较复杂的程序阅读题，建议在草稿纸上用表格实时记录各个变量的值的变化，把自己当成电脑按字面意思读程序。不要太相信自己作为人类的记忆力和理解力。😇

25\.  下面程序段的运行结果是( `ef` )

```c
char str[]= "abc\0def\0ghi", *p = str;
printf("%s", p+5) ;
```

注意 `'\n'`、`'\t'`、`'\0'` 这样的转义符算一个字符，而不是两个。`printf( )` 函数按 `%s` 格式输出时遇到 `'\0'` 就直接结束输出。

26\.  下面程序段的运行结果是( `bcdBCD` )

```c
char s[20]= "abcd" ;
char *sp = s ;
puts(strcat(sp+1, "ABCD"+1)) ;
```

字符串常量的输出值也是首字符的地址，`"ABCD"+1` 返回的就是 `'B'` 的地址。`strcat( )` 函数把输入的两个地址指向的字符串 `"bcd"` 和 `"BCD"` 连接起来作为输出值。

27\.  如下代码块能输出最后 `i` 的值。（❌）

```c
for (int i=0; i<n; i++) {
    //随便什么循环体
}
printf("%d", i);
```

这个 `i` 是定义在 for 循环里的，离开 for 循环之后就没了。

## 三、上机考

### 1. 习题8-4 报数

报数游戏是这样的：有 `n` 个人围成一圈，按顺序从 `1` 到 `n` 编好号。从第一个人开始报数，报到 `m`（小于 `n`）的人退出圈子；下一个人从 `1` 开始报数，报到 `m` 的人退出圈子。如此下去，直到留下最后一个人。本题要求编写函数，给出每个人的退出顺序编号。函数接口如下：

```c
void CountOff( int n, int m, int out[] );
```

其中 `n` 是初始人数；`m` 是游戏规定的退出位次（保证为小于 `n` 的正整数）。函数 `CountOff` 将每个人的退出顺序编号存在数组 `out[]` 中。因为 C 语言数组下标是从 0 开始的，所以第 `i` 个位置上的人是第 `out[i-1]` 个退出的。

```c title='裁判测试程序样例'
#include <stdio.h>
#define MAXN 20

void CountOff( int n, int m, int out[] );

int main()
{
    int out[MAXN], n, m;
    int i;
    
    scanf("%d %d", &n, &m);
    CountOff( n, m, out );   
    for ( i = 0; i < n; i++ )
        printf("%d ", out[i]);
    printf("\n");
    
    return 0;
}

/* 你的代码将被嵌在这里 */

```

输入样例：11 3

输出样例：4 10 1 7 5 2 11 9 3 6 8

```c title='我的解答'
void CountOff(int n, int m, int out[]) {
    int count = 0, all = 0, i; /*count记录每次数到了第几个人，all记录退出了几个人*/
    for (i=0; i<n; i++) {
        out[i] = 0; /*预先把数组元素清零*/
    }
    i = 0; /*从下标为0的元素开始数*/
    while(all < n) { /*循环到n个人都退出为止*/
        if(!out[i] && count!=m-1) { /*必须要!out[i]。如果out[i]不是0说明这个人已经退出了*/
            count++;
        } else if (!out[i] && count==m-1) { /*数到m个人了，让第m个人退出*/
            out[i] = all + 1; /*在数组中注明这个人是第几个退出的人*/
            count = 0;
            all++;
        }
        i++;
        i %= n;
    }
}
```

这一题是经典的“猴子选大王”问题。

### 2. 习题8-5 使用函数实现字符串部分复制

本题要求编写函数，将输入字符串 `t` 中从第 `m` 个字符开始的全部字符复制到字符串 `s` 中。

```c
void strmcpy( char *t, int m, char *s );
```

函数 `strmcpy` 将输入字符串 `char *t` 中从第 `m` 个字符开始的全部字符复制到字符串 `char *s` 中。若 `m` 超过输入字符串的长度，则结果字符串应为空串。

```c title='裁判测试程序样例'
#include <stdio.h>
#define MAXN 20

void strmcpy( char *t, int m, char *s );
void ReadString( char s[] ); /* 由裁判实现，略去不表 */

int main()
{
    char t[MAXN], s[MAXN];
    int m;
    
    scanf("%d\n", &m);
    ReadString(t);
    strmcpy( t, m, s );
    printf("%s\n", s);

    return 0;
}

/* 你的代码将被嵌在这里 */
```

输入样例：

`7`

`happy new year`

输出样例：

`new year`

```c title='错误解答'
void strmcpy(char *t, int m, char *s) {
    int i = 0;
    m--;
    while (t[m] != NULL) { /*这样t中表示字符串结尾的'\0'就没复制到s里*/
        s[i] = t[m];
        m++; i++;
    }
}
```

```c title='正确解答'
#include <string.h> /*可以在自己写的函数前面调用库文件简化代码*/
void strmcpy(char *t, int m, char *s) {
    int n, i, j = 0;
    memset(s, 0, sizeof(s)); /*要初始化字符串s，因为主函数中没初始化*/
    n = strlen(t); /*计算字符串t的长度*/
    for(i=m-1; i<=n; i++, j++) {
        s[j]=t[i];
    }
    /*注意i<=n保证了t结尾的'\0'也被复制到s中。结尾没有'\0'的话主函数中以%s格式输出s会出错*/
}
```

### 3. 习题2-6 求阶乘序列前 N 项和

本题要求编写程序，计算序列 1!+2!+3!+⋯ 的前N项之和。

输入格式:输入在一行中给出一个不超过 12 的正整数 `N`。

输出格式:在一行中输出整数结果。

输入样例: `5`

输出样例: `153`

```c title='错误解答'
#include<stdio.h>

double fact() {
    static double n = 1;
    static int i = 1;
    n *= i;
    i++;
    return n;
}

int main() {
    int i, n;
    double sum = 0;
    
    scanf("%d", &n);
    for(i=1; i<=n; i++)
        sum += fact();
    printf("%d", sum); // 这一行错了！
    
    return 0;
}
```

这在我自己电脑上编译运行的结果是正确的，但 PTA 上运行出来都是 WA。原因是 `printf` 错了。`sum` 是 `double` 类型的变量，用 `int` 型格式输出double类型变量属于未定义行为。我自己电脑上的编译器会好心地帮我把 `double` 强制类型转换成 `int`，而 `PTA` 的编译器没那么聪明，需要学生自己写强制类型转换。改成 `printf("%d", (int)sum);` 就通过了。

### 4. 习题10-11 有序表的增删改查操作

首先输入一个正整数 N （1 ≤ N ≤ 1000）和一个无重复元素的、从小到大排列的、N 个元素的有序表，然后在屏幕上显示以下菜单（编号和选项）:

```txt
[1] Insert
[2] Delete
[3] Update
[4] Query
[Other option] End
```

用户可以反复对该有序表进行插入、删除、修改和查找操作，也可以选择结束。当用户输入编号 1～4 和相关参数时，将分别对该有序表进行插入、删除、修改和查找操作，输入其他编号，则结束操作。本题要求实现 4 个函数，分别在有序表（数组）中插入、删除、修改、查找一个值。

```c title='函数接口定义'
int insert(int a[ ], int value);    
int del(int a[ ], int value);
int modify(int a[ ], int value1, int value2); 
int query(int a[ ], int value);
```

函数 `insert` 在有序数组 `a` 中插入一个值为 `value` 的元素，如果在数组 `a` 中已有值为 `value` 的元素，则返回 `-1`。函数 `del` 删除有序数组 `a` 中等于 `value` 的元素，如果在数组 `a` 中没有找到值为 `value` 的元素，则返回 `-1`。函数`modify` 将有序数组 `a` 中等于 `value1` 的元素，替换为 `value2`，如果在数组 `a` 中没有找到值为 `value1` 的元素或者 `value2` 已在数组 `a` 中存在，则返回 `-1` 。函数 `query` 用二分法在有序数组 `a` 中查找元素 `value`，如果找到，则返回相应的下标；如果没有找到，则返回 `-1`。

```c title='裁判测试程序样例'
/* 有序表的增删改查操作 */
#include<stdio.h>
#define MAXN 10000    /* 定义符号常量表示数组a的长度 */

int Count = 0;        /* 用全局变量Count表示数组a中待处理的元素个数 */
void select(int a[], int option, int value); /* 决定对有序数组a进行何种操作的控制函数 */
int input_array(int a[ ]);    /* 输入有序数组a的函数 */
void print_array(int a[ ]);    /* 输出有序数组a的函数 */
int insert(int a[ ], int value);    /* 在有序数组a中插入一个值为value的元素的函数 */
int del(int a[ ], int value);    /* 删除有序数组a中等于value的元素的函数 */
int modify(int a[ ], int value1, int value2); /* 将有序数组a中等于value1的元素，替换为value2 */ 
int query(int a[ ], int value);     /* 用二分法在有序数组a中查找元素value的函数 */

int main(void) 
{
   int option, value, a[MAXN];
    
    if(input_array(a) == -1){     /* 调用函数输入有序数组 a */
         printf("Error");        /* a不是有序数组，则输出相应的信息 */
         return 0;
    }
    
    printf("[1] Insert\n");    /* 以下4行显示菜单*/
    printf("[2] Delete\n");
    printf("[3] Update\n");
    printf("[4] Query\n");
    printf("[Other option] End\n");
    while (1) {            /* 循环 */
        scanf("%d", &option);         /* 接受用户输入的编号 */
        if (option < 1 || option > 4) {    /* 如果输入1、2、3、4以外的编号，结束循环 */
            break;
        }
        scanf("%d", &value);         /* 接受用户输入的参数value */
        select(a, option, value);         /* 调用控制函数 */
        printf("\n");
    }
    printf("Thanks.");            /* 结束操作 */
    
    return 0;
}

/* 控制函数 */
void select(int a[ ], int option, int value) 
{
    int index, value2;
    
    switch (option) {
        case 1:
            index = insert(a, value);      /* 调用插入函数在有序数组 a 中插入元素value */
            if(index == -1){        /* 插入数据已存在，则输出相应的信息 */
                printf("Error");
            }else{                        
                print_array(a);        /* 调用输出函数，输出插入后的有序数组a */
            }
            break;
        case 2:
            index = del(a, value);      /* 调用删除函数在有序数组 a 中删除元素value */
            if(index == -1){        /* 没找到value，则输出相应的信息 */
                printf("Deletion failed.");
        }else{
            print_array(a);         /* 调用输出函数，输出删除后的有序数组a */
        }
            break;
        case 3:
            scanf("%d", &value2);         /* 接受用户输入的参数value2 */
            index = modify(a, value, value2);      /* 调用修改函数在有序数组 a 中修改元素value的值为value2 */
            if(index == -1){            /* 没找到value或者vaule2已存在，则输出相应的信息 */
                printf("Update failed.");
            }else{
            print_array(a);         /* 调用输出函数，输出修改后的有序数组a */
            }
            break;
        case 4:
            index = query(a, value);     /* 调用查询函数在有序数组 a 中查找元素value */
            if(index == -1){        /* 没找到value，则输出相应的信息 */
                printf( "Not found.");
            }else{            /* 找到，则输出对应的下标 */
            printf("%d", index);
            }
            break;
    }
}

/* 有序表输入函数 */
int input_array(int a[ ]) 
{
    scanf("%d", &Count);
    for (int i = 0; i < Count; i ++) {
        scanf("%d", &a[i]);
        if(i > 0 && a[i] <= a[i-1]){    /* a不是有序数组 */
            return -1;
        }
    }
    
    return 0;
}

/* 有序表输出函数 */
void print_array(int a[ ]) 
{
    for (int i = 0; i < Count; i ++) { /* 输出时相邻数字间用一个空格分开，行末无空格 */
        if(i == 0){     
           printf("%d", a[i]);
        }else{
           printf(" %d", a[i]);
        }
    }
}
 
/* 请在这里填写答案 */
```

```txt title='输入样例1 插入一个值'
6 -2 3 7 9 101 400
1
96
0
```

```txt title='输出样例1'
[1] Insert
[2] Delete
[3] Update
[4] Query
[Other option] End
-2 3 7 9 96 101 400
Thanks.
```

```txt title='输入样例2 删除一个值'
6 -2 3 7 9 101 400
2
400
0
```

```txt title='输出样例2'
[1] Insert
[2] Delete
[3] Update
[4] Query
[Other option] End
-2 3 7 9 101
Thanks.
```

```txt title='输入样例3 修改一次'
6 -2 3 7 9 101 400
3
7
10
0
```

```txt title='输出样例3'
[1] Insert
[2] Delete
[3] Update
[4] Query
[Other option] End
-2 3 9 10 101 400
Thanks.
```

```txt title='输入样例4 查询一次'
6 -2 3 7 9 101 400
4
-2
0
```

```txt title='输出样例4'
[1] Insert
[2] Delete
[3] Update
[4] Query
[Other option] End
0
Thanks.
```

```txt title='输入样例5 连续增删改查'
6 -2 3 7 9 101 400
2
101
1
-10
4
101
3
400
444
0
```

```txt title='输出样例5'
[1] Insert
[2] Delete
[3] Update
[4] Query
[Other option] End
-2 3 7 9 400
-10 -2 3 7 9 400
Not found.
-10 -2 3 7 9 444
Thanks.
```

```c title='我的错误解答'
int insert(int a[ ], int value) {
    int i = 0;
    while (a[i]<value && a[i]!=0) { // 已经有Count了，没必要自己找数组有几个元素
        i++;
    } 
    // 而且a[i]!=0这个判断标准也不对，有序表中完全有可能出现值为0的元素
    if (a[i] == value) {
        return -1;
    }
    int j = i;
    while (a[j] != 0) {
        j++;
    }
    for(; j>i; j--) {
        a[j] = a[j-1];
    }
    a[i] = value;
    Count++;
    return 0;
}

int del(int a[ ], int value) {
    int i = query(a, value);
    if (i == -1) {
        return -1;
    }
    while (a[i] != 0) {
        a[i] = a[i+1];
        i++;
    }
    Count--;
    return 0;
}

int modify(int a[ ], int value1, int value2) {
    int c = del(a, value1);
    int b = insert(a, value2);
    if (c==-1 || b==-1) { // 应该在del和insert之后各检查一次是否返回了-1
        return -1;
    } 
    return 0;
}

int query(int a[ ], int value) {
    int right = 0;
    while (a[right] != 0) {
        right++;
    }
    right--;
    int left = 0, mid = (left + right) / 2;
    while (left <= right) { // 二分查找改错改了好久，太不应该了……
        if (a[mid] < value) {
            left = mid+1;
        } else if (a[mid] > value) {
            right = mid-1;
        } else {
            return mid;
        }
        mid = (left + right) / 2;
    } 
    return -1;
}
```

![KTAC`TPDCCL]F(O__)(6[(M.png](https://cdn.nlark.com/yuque/0/2022/png/25775350/1649210866339-4f689392-3fe7-4b45-990e-552b0bfb97b4.png#clientId=ub1b0debf-f6a3-4&errorMessage=unknown%20error&from=paste&height=180&id=u2c76073f&originHeight=302&originWidth=420&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42351&status=error&style=none&taskId=ua9c674b1-f0bb-4382-acc5-f6739881a78&title=&width=250)这题里没用到野指针，也没有数组下标越界。后来发现是因为第4行用`a[i]!=0`判断是否结束循环，导致在测试样例的有序表中出现0时提前退出循环。而五个输入样例中都没出现0，所以我按照五个输入样例去试就发现不了错在哪。![“淆习”是河北话里的“学习”](https://cdn.nlark.com/yuque/0/2022/png/25775350/1649333564715-bedfcee7-c485-490a-8d67-2e2f4d0f66fb.png#clientId=u22296693-de05-4&errorMessage=unknown%20error&from=paste&height=559&id=uf814075f&originHeight=956&originWidth=766&originalType=binary&ratio=1&rotation=0&showTitle=true&size=131179&status=error&style=none&taskId=u6450dea5-b99d-40b8-b230-9081b087095&title=%E2%80%9C%E6%B7%86%E4%B9%A0%E2%80%9D%E6%98%AF%E6%B2%B3%E5%8C%97%E8%AF%9D%E9%87%8C%E7%9A%84%E2%80%9C%E5%AD%A6%E4%B9%A0%E2%80%9D&width=448 "“淆习”是河北话里的“学习”")

其实这题课本上有得抄的！我感觉初学者能完整抄下来就能复习许多了。

```c title='正确解答'
int insert(int a[ ], int value) {
    int i = 0;
    while (a[i]<value && i<Count) {
        i++;
    }
    if (a[i] == value) {
        return -1;
    }
    int j = Count;
    for (; j>i; j--) {
        a[j] = a[j-1];
    }
    a[i] = value;
    Count++;
    return 0;
}

int del(int a[ ], int value) {
    int i = query(a, value);
    if (i==-1) {
        return -1;
    }
    for (; i<Count; i++) {
        a[i] = a[i+1];
    }
    Count--;
    return 0;
}

int modify(int a[ ], int value1, int value2) {
    int c = del(a, value1);
    if (c == -1) {
        return -1;
    }
    int b = insert(a, value2);
    if (b == -1) {
        return -1;
    }
    return 0;
}

int query(int a[ ], int value) {
    int right = Count-1;
    int left = 0, mid = (left + right) / 2;
    while (left <= right) {
        if (a[mid] < value) {
            left = mid+1;
        } else if (a[mid] > value) {
            right = mid-1;
        } else {
            return mid;
        }
        mid = (left + right) / 2;
    }
    return -1;
}
```

### 5. 习题7-10 水仙花数

水仙花数是指一个 N 位正整数（N≥3），它的每个位上的数字的N次幂之和等于它本身。例如：153=13+53+33。 本题要求编写程序，计算所有 N 位水仙花数。

输入格式: 输入在一行中给出一个正整数 N（3≤N≤7）。

输出格式:按递增顺序输出所有 N 位水仙花数，每个数字占一行。

输入样例: `3`

输出样例: `153``370``371``407`

本题中寝室长 lry 同学遇到的困难是 N=7 的情况会运行超时。

思路1：打表，用原来的慢程序提前算好 N=7 时的水仙花数，写进新程序里，当用户输入 N=7 时不用计算，直接写成 if(N==7) 时输出预先算好的值。

思路2：程序慢的原因是对每个七位数都调用了七次 `pow( )` 函数计算其各位数字的七次方，而 `pow( )` 是非常费时的，不如提前用一个 10 元数组储存 $0^N$、$1^N$、……、$9^N$，这样就不需要每次都重新计算各位数字的 N 次方了。

```c title='正确解答'
#include<stdio.h>
#include<math.h>
int main() {
    int N, i, j, sum;
    scanf("%d", &N);
    int a[10];
    for(i=0; i<10; i++)
        a[i] = pow(i, N); // 用数组储存每个个位数的N次幂
    for(i=pow(10, N-1); i<pow(10, N); i++) {
        j = i; sum = 0;
        while(j>0) {
            sum +=  a[j % 10];
            j /= 10;
        }
        if(sum==i)
            printf("%d\n", i);
    }
    // 想省时间的话不要给判断是否为水仙花数单独建个函数，因为每次调用函数也要花时间的
    return 0;
}
```

### 6. 习题2-12 输出华氏-摄氏温度转换表

输入 2 个正整数 lower 和 upper（lower≤upper≤100），请输出一张取值范围为 [lower，upper]、且每次增加 2 华氏度的华氏-摄氏温度转换表。温度转换的计算公式：C=5×(F−32)/9，其中 C 表示摄氏温度，F 表示华氏温度。

输入格式：在一行中输入2个整数，分别表示 lower 和 upper 的值，中间用空格分开。

输出格式：第一行输出："fahr celsius"，接着每行输出一个华氏温度 fahr（整型）与一个摄氏温度 celsius（占据6个字符宽度，靠右对齐，保留1位小数）。若输入的范围不合法，则输出"Invalid."。

输入样例1：`32 35`

输出样例1：`fahr celsius``32   0.0``34   1.1`

输入样例2：`40 30`

输出样例2：`Invalid.`

```c
#include<stdio.h>
int main() {
    int low, upp;
    scanf("%d%d", &low, &upp);
    if(low>upp || low>100) {
        printf("Invalid.");
    } else {
        printf("fahr celsius\n");
        for(; low<=upp; low += 2)
            printf("%d%6.1f\n", low, 5.0*(low-32)/9);
    }   
}
```
这题主要是输出格式容易错，“占据6个字符宽度，靠右对齐，保留1位小数”就是`%6.1f`。可以参考这篇笔记来复习：[C语言printf()输出格式大全](https://blog.csdn.net/whalefall/article/details/80297752?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522164968288816780271993533%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=164968288816780271993533&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-80297752.142^v7^pc_search_result_cache,157^v4^new_style&utm_term=C%E8%AF%AD%E8%A8%80+%E8%BE%93%E5%87%BA%E6%A0%BC%E5%BC%8F&spm=1018.2226.3001.4187)

### 7. 习题3-2 高速公路超速处罚

按照规定，在高速公路上行使的机动车，达到或超出本车道限速的10%则处200元罚款；若达到或超出50%，就要吊销驾驶证。请编写程序根据车速和限速自动判别对该机动车的处理。输入格式:输入在一行中给出2个正整数，分别对应车速和限速，其间以空格分隔。输出格式:在一行中输出处理意见：若属于正常行驶，则输出“OK”；若应处罚款，则输出“Exceed x%. Ticket 200”；若应吊销驾驶证，则输出“Exceed x%. License Revoked”。其中x是超速的百分比，精确到整数。

输入样例1: `65 60`

输出样例1: `OK`

输入样例2: `110 100`

输出样例2: `Exceed 10%. Ticket 200`

输入样例3: `200 120`

输出样例3:`Exceed 67%. License Revoked`

```c
#include<stdio.h>
int main()
{
    int v, lim;
    scanf("%d%d", &v, &lim);
    if(v < 1.1*lim) printf("OK");
    else if(v < 1.5*lim) printf("Exceed %d%%. Ticket 200", (int)(100.0*(v-lim)/lim));
    else printf("Exceed %d%%. License Revoked", (int)(100.0*(v-lim)/lim));
    return 0;
}
```

这个解答的bug是：分段函数三段的临界值会出错，且输出的超速百分比有误差。这些都是计算机内浮点数运算自带的误差导致的。

```c
#include<stdio.h>
int main()
{
    int v, lim;
    scanf("%d%d", &v, &lim);
    if(v < 1.1*lim) printf("OK");
    else if(v < 1.5*lim) printf("Exceed %.0f%%. Ticket 200", 100.0*(v-lim)/lim);
    else printf("Exceed %.0f%%. License Revoked", 100.0*(v-lim)/lim);
    return 0;
}
```

改成这样，输出的百分比的误差就可容忍了。题目要求精确到整数，不一定要强制类型转换成int，也可以用浮点数运算，然后输出零位小数，这样算得更准。但是临界值处依然是错的，输入`110 100`会输出`OK`。![SD62UA))I1B76VS6}NE_D$H.png](https://cdn.nlark.com/yuque/0/2022/png/25775350/1649754387421-96949d1b-0407-4369-9801-4adf8cd5aeaa.png#clientId=u775d025a-5440-4&errorMessage=unknown%20error&from=paste&height=406&id=u62ca7819&originHeight=626&originWidth=924&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94104&status=error&style=none&taskId=uf5abaacd-e484-4816-9009-82e76791712&title=&width=600)![986V1JAZ(2KVM}{CV($}~OP.png](https://cdn.nlark.com/yuque/0/2022/png/25775350/1649754419413-481d8627-4e3b-4c3a-8b66-d58206a7a89f.png#clientId=u775d025a-5440-4&errorMessage=unknown%20error&from=paste&height=284&id=ud0dd9509&originHeight=429&originWidth=907&originalType=binary&ratio=1&rotation=0&showTitle=false&size=64931&status=error&style=none&taskId=u9d617736-3c73-43e2-b679-24b6fbf097f&title=&width=600)

### 8. 习题11-1 输出月份英文名

本题要求实现函数，可以返回一个给定月份的英文名称。函数接口定义：`char *getmonth( int n );`函数getmonth应返回存储了n对应的月份英文名称的字符串头指针。如果传入的参数n不是一个代表月份的数字，则返回空指针NULL。

```c
#include <stdio.h>

char *getmonth( int n );

int main()
{
    int n;
    char *s;
    
    scanf("%d", &n);
    s = getmonth(n);
    if ( s==NULL ) printf("wrong input!\n");
    else printf("%s\n", s);
    
    return 0;
}

/* 你的代码将被嵌在这里 */
```

输入样例1：`5`

输出样例1：`May`

输入样例2：`15`

输出样例2：`wrong input!`

```c
char *getmonth( int n ) {
    char* a[12] = {
        &"January", &"February", &"March", &"April",
        &"May", &"June", &"July", &"August",
        &"September", &"October", &"November", &"December"
        };
    if(n>0&&n<13)
        return a[n-1];
    else
        return NULL;
}
```

两个错误：

1. 不需要 `&`，字符串本身的返回值就是它首字符的地址。
2. 字符串是在 getmonth 函数里定义的，回到主函数之后这些字符串的内存空间被回收，主函数顺着 getmonth 函数返回的指针去找字符串，可能此时字符串还没被清理掉，也可能被清理掉了。所以运行的效果是有时候正常，有时候找不到字符串。

解决方法：

1. 多加了 `&` 是 C 语言的未定义行为（Undefined Behavior），聪明的编译器会明白程序员的意图，自动忽略 `&`。所以虽然这样写是错的，但也能正常运行。
2. 在 `char* a[12]` 前面加 `static`，或者干脆把这个字符指针数组定义为全局变量。

### 9. 习题4-11 兔子繁衍问题

一对兔子，从出生后第 3 个月起每个月都生一对兔子。小兔子长到第 3 个月后每个月又生一对兔子。假如兔子都不死，请问第 1 个月出生的一对兔子，至少需要繁衍到第几个月时兔子总数才可以达到 N 对？

输入格式: 输入在一行中给出一个不超过 10000 的正整数 N。

输出格式: 在一行中输出兔子总数达到 N 最少需要的月数。

输入样例: `30`

输出样例: `9`

```c
#include<stdio.h>
int main() {
    int n, month = 1;
    int f_0, f_1 = 0, f_2 = 1;
    scanf("%d", &n);
    while (f_2 < n) {
        f_0 = f_1;
        f_1 = f_2;
        f_2 += f_0;
        month++;
    }
    printf("%d", month);
    return 0;
}
```

其实这题的代码很好写，就是一般的斐波那契数列。但说实话我一开始没看出来这是斐波那契数列。第(n-1)个月已经出生了的兔子都能活到第n个月，而第(n-2)个月已经出生了的兔子到第n个月都能生小兔子，所以第n个月的兔子总数就是第(n-1)个月已出生的兔子数加上第(n-2)个月已出生的兔子数，是斐波那契数列。事实上，斐波那契数列也叫兔子数列，就是因为这个关于兔子的数学问题。

### 10. 练习7-10 查找指定字符

本题要求编写程序，从给定字符串中查找某指定的字符。

输入格式：输入的第一行是一个待查找的字符。第二行是一个以回车结束的非空字符串（不超过80个字符）。

输出格式：如果找到，在一行内按照格式“index = 下标”输出该字符在字符串中所对应的最大下标（下标从0开始）；否则输出"Not Found"。

输入样例1：`m``programming`

输出样例1：`index = 7`

输入样例2：`a``1234`

输出样例2：`Not Found`

```c
#include<stdio.h>
#define MAXN 80
int main() {
    int index = -1, i = 0;
    char c, s[MAXN];
    scanf("%c", &c);
    scanf("%s", s);
    while (s[i]) {
        if(s[i]==c)
            index = i;
        i++;
    }
    if (index==-1)
        printf("Not Found\n");
    else
        printf("index = %d\n", index);
    return 0;
}
```

有一个 index = 79，字符串中有空格的 case 没通过，在`scanf("%s", s);`后面加入`puts(s);`发现输出的字符串只有输入字符串空格之前的部分，原因是 `scanf( )` 函数以 `%s` 格式读取字符串只读到空格、制表符为止，要把空格及空格以后的部分读入字符串只能用 `getchar( )`。

```c
#include<stdio.h>
#define MAXN 81
int main() {
    int index = -1, i = 0;
    char c, ch, s[MAXN];
    scanf("%c", &c);
    while (((ch=getchar())!='\n')&&(i<MAXN-1)) {
        s[i] = ch;
        i++;
    }
    s[i] = '\0';
    i = 0;
    while (s[i]!='\0'&&i<MAXN) {
        if(s[i]==c)
            index = i;
        i++;
    }
    if (index==-1)
        printf("Not Found\n");
    else
        printf("index = %d\n", index);
    return 0;
}
```

这一次不管怎样输出都是 `Not Found`，在第一个 while 循环后用 `puts( )` 输出字符串，发现输出为空；再在第一个 while 循环里用 `printf( )` 输出每次读入的 `ch`，没有输出，说明没有进入第一个 while 循环。原因是输入的第一行除了一个字符，还有行末的一个回车，会在第一个 while 循环处被 `getchar( )` 读入储存给 `ch`。`ch=='\n'`，不满足循环条件，就直接退出了。

```c
#include<stdio.h>
#define MAXN 81
int main() {
    int index = -1, i = 0;
    char c, ch, s[MAXN];
    scanf("%c", &c);
    getchar(); //增加这一行代码，读走第一行结尾的\n即可
    while (((ch=getchar())!='\n')&&(i<MAXN-1)) {
        s[i] = ch;
        i++;
    }
    s[i] = '\0';
    i = 0;
    while (s[i]!='\0'&&i<MAXN) {
        if(s[i]==c)
            index = i;
        i++;
    }
    if(index==-1)
        printf("Not Found\n");
    else
        printf("index = %d\n", index);
    return 0;
}
```

### 11. 习题9-1 时间换算

本题要求编写程序，以 hh:mm:ss 的格式输出某给定时间再过 n 秒后的时间值（超过 23:59:59 就从 0 点开始计时）。

输入格式：输入在第一行中以 hh:mm:ss 的格式给出起始时间，第二行给出整秒数 n（<60）。

输出格式：输出在一行中给出 hh:mm:ss 格式的结果时间。

输入样例：`11:59:40` `30`

输出样例：`12:00:10`

```c
#include<stdio.h>
int main() {
    int hh, mm, ss, plus;
    scanf("%d%d%d", &hh, &mm, &ss); // 这一行有问题，改成"%d:%d:%d"就对了
    scanf("%d", &plus);
    ss += plus;
    mm += ss / 60;
    ss %= 60;
    hh += mm / 60;
    mm %= 60;
    hh %= 24;
    printf("%02d:%02d:%02d\n", hh, mm, ss); // 输出两位整数，不足两位左边补0
    return 0;
}
```

在 `scanf( )` 后面输出了hh、mm、ss，发现只有hh是正常的，原因是读入格式 `%d%d%d` 不对。平时这样写可以正常读入三个整数，那是因为 `scanf( )` 把空格和制表符当作正常的分隔符，会自动跳过它们去读数字；而冒号是 `scanf( )` 不认识的分隔符，要让 `scanf( )` 知道应该跳过冒号去找下一个数字，就得在读入格式中把冒号写出来。
