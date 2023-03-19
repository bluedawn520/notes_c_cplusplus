[TOC]

---

# 0.c的概述

- C特性:

  > 1. 能够直接操作硬件；
  >
  > 2. C语言**追求最高的运行时效率**；
  >
  >    a. 不会检查数组是否越界
  >
  >    b. 没有异常机制
  >
  > 3. 和汇编语言有很强的的对应性；

- 访问没有默认初始化的变量，其行为是未定义的。



---

# 1.I/O模型

> 引入**缓存**：键盘 --> stdin（标准输入缓冲区）  -->  程序  --> stdout（标准输出缓冲区）  -->  屏幕



---

# 2.`printf()` & `scanf()`

> - `printf` 函数 将格式化的字符串打印输出；
> - `printf` 函数包含 **普通字符**、**转换说明**。
> - 转换说明：本质是一个占位符；
>   - 作用：1.将对应的二进制机器码按照转换说明转换成相应的字符输出；2.指定了打印输出的格式。
> - `%m.pX`
>   - `m`:最小字段宽度；
>   - `p`:
>     - 对于`%d`而言，表示待显示数字的最小个数，不足补0。
>     - 对于`%f`而言，表示小数点后的显示的位数。
>   - `X`:指定如何将二进制机器码转换成相应的字符；
> - `scanf` 函数根据格式化的字符串进行**模式匹配**，按照指定格式读取输入；
> - `scanf` 函数包含 普通字符、**空白字符**(换页符、换行符、制表符、空格等)、转换说明。
>   - 对于普通字符，精确匹配；
>   - 对于空白字符，一个或若干个空白字符匹配任意个空白字符，包括零个。
>   - 对于转换说明：
>     - `%d`：忽略若干个空白字符，一直到数字字符或正负号字符，读取到第一个非数字为止；
>     - `%f`: 忽略之前的若干个空白字符；
>     - `%c`: 字符匹配；
>   - 注意：当 scanf 函数遇到一个不属于当前项的字符时，不会读取该字符，而是在下一次读取。 



---

# 3.基本数据类型

> 类型：
>
> - 确定了存储空间大小；
> - 指定了编码方式；
> - 指定了可以进行的操作；

> - 十进制整数的字面值：是 `int`，`long`，`long long` 中可以存储下且表示范围最小的一个类型；  
> - 八进制整数的字面值：是 `int`，`unsigned int`， `long`，`unsigned long`，`long long`,`unsigned long long` 中可以存储下且表示范围最小的一个类型；
> - 十六进制整数的字面值：是 `int`，`unsigned int`， `long`，`unsigned long`，`long long`,`unsigned long long` 中可以存储下且表示范围最小的一个类型；

> - `%d` 只适合读写`int`类型数据；
> - 读写`unsigned int`时，使用`%u`(十进制形式),`%o`（八进制形式）,`%x`（十六进制形式）;
> - 读写`short`时，之前添加`h`；
> - 读写`long`时，之前添加`l`；
> - 读写`long long`时，之前添加`ll`
> - 读写`float`时，用`%f`；
> - 读写`double`时，用`%lf`；
> - 读写`long double`时，用`%Lf`；

> - 转义序列：
>   - **字符转义序列**：`\n`,`\v`,`\r`,`\b`,`\a`,`\t`,`\f`,`\?`,`\\`,`\"`,`\'`;
>   - **数字转义序列**：
>     - 八进制转义序列：`\`和一个**最多3位**的八进制数字组成；
>     - 十六进制转义序列：`\x`和十六进制数字组成；（注意：`x`必须小写）；



---

# 4.getchar()` & `putchar()

> - int getchar(void);
>   - 从stdin读入一个字符，并将读入的字符返回；读取到文件末尾或读的过程中发生错误，则返回`EOF`;
> - int putchar(int);
>   - 向stdout写入一个字符；若写入成功则返回写入的字符，否则返回`EOF`;
> - 这两个函数的执行效率要高于printf和scanf。



---

# 5.类型转换

> - 隐式类型转换：
>
>   - 当算术表达式或逻辑表达式中 操作数的类型不匹配时；
>
>     - 算术转换：
>
>       > 1. **整数提升**：操作数中有任何低于`int`或`unsigned int`类型，会首先将其转换为`int`或`unsigned int`；
>       > 2. `int --> long --> long long --> float --> double --> long double`;
>       > 3. 同一转换等级的 `signed --> unsigned`;
>
>   - 当赋值运算符 右侧表达式的类型和左侧类型不匹配时；
>
>   - 当函数调用中 实参类型和形参类型不匹配时；
>
>   - 当return语句 中表达式类型和函数返回值类型不匹配时；
>
> - 显示类型转换：



---

# 6.为什么定义别名？

> - 增加代码的**可读性**；
> - 增加代码的**可移植性**；



---

# 7.位操作常见面试题

![](\pics\位操作常见面试题.png)

> 1. `n % 2 != 0` 或 `n & 1`;
>
> 2. `n & (n-1) == 0`;
>
> 3. `n & (~n + 0x1)`;
>
> 4. `a = a ^ b;  b = a ^ b;   a = a ^ b;`;
>
> 5. ```c
>    int result = 0;
>    for(int i  = 0; i< sizeof(nums)/sizeof(int); ++i)
>    {
>        result ^= nums[i];
>    }
>    ```
>
> 6. ```c
>    int exclusiveOR = 0;
>    for(int i  = 0; i< sizeof(nums)/sizeof(int); ++i)
>    {
>        exclusiveOR ^= nums[i];
>    }
>
>    int lowestValidBit = exclusiveOR & (~exclusiveOR + 0x1);
>
>    int result1 = 0, result2 = 0;
>    for(int i  = 0; i< sizeof(nums)/sizeof(int); ++i)
>    {
>        if(nums[i] & lowestValidBit){
>            result1 ^= nums[i];
>        }else{
>            result2 ^= nums[i];
>        }
>    }
>    ```
>
>  7. ```c
>     int exclusiveOR1 = 0;
>     for(int i=0; i < sizeof(nums)/sizeof(int); ++i)
>     {
>         exclusiveOR1 ^= nums[i];
>     }
>     
>     //找出可以划分为包含1个和包含2个的最低有效位
>     int lowestBit = 0;
>     for(int i=0; i < sizeof(nums)/sizeof(int); ++i)
>     {
>         lowestBit ^= (exclusiveOR1^nums[i]) & (~(exclusiveOR1^nums[i])+0x1);
>     }
>     //若其最低有效位为 udge_num， 则即为包含1的那一部分
>     int judge_num = lowestBit & exclusiveOR1;
>     int result1 = 0；
>     for(int i=0; i < sizeof(nums) /sizeof(int); ++i)
>     {
>         if(lowestBit & nums[i] == exclusiveOR1){
>         	result1 ^= nums[i];
>         }
>     }
>     
>     //求解包含2个的那一部分
>     int siveOR2 = exclusiveOR1 ^ result1;
>     int lowestBit1 = exlusiveOR2 ^ (~exlusiveOR2 + 0x1);
>     int result2 = 0, result3 = 0;
>     
>     for(int i=0; i < sizeof(nums) /sizeof(int); ++i)
>     {
>             if(lowestBit & nums[i] != exclusiveOR1)
>             {
>                     if(lowestBit1 & nums[i]){
>                             result2 ^= nums[i];
>                       }else{
>                             result3 ^= nums[i];
>                     }
>             }
>     }
>     ```
>

> - **情形１**　101数，其中50个只出现两次，1个只出现一次，求出现一次的数。
>
>   > 将所有数进行异或。
>
> - **情形２**　102数，其中50个只出现两次，2个只出现一次，求出现一次的数。
>
>   > - step1 将所有数进行异或，得数a
>   >
>   > - step2 求得该数a的最低位为1的那一位，将102个数分为两组
>   > - step3 分别对两个组的所有数进行异或
>
> - **情形３**　103数，其中50个只出现两次，3个只出现一次，求出现一次的数。
>
>   > - step1 将所有数进行异或，得数a
>   > - step2 对所有数`n_i`依次进行以下操作：将a和`n_i` 异或的值求得最低位为1的那一位数，然后将该数和上次所得结果进行异或。得数b，
>   > - step3 由 `a&b` 将所有数分为两组，一组符合情形1，一组符合情形2。
>   > - step4 依次可得3个数。
>
>   > x = a^b^c;
>   >
>   > - Lemma 1. ` low_bit(x,p) XOR low_bit(x,p) = 0`；
>   >
>   > - Conclusion 2. `low_bit(b^c)`，`low_bit(a^c)`，`low_bit(a^b)` **仅有两个相等**;
>   >
>   >   > ```txt
>   >   > PF:	
>   >   > 	若low_bit(b^c)，low_bit(a^c)，low_bit(a^b)都不同，不妨依次设为l1<l2<l3，则可知：
>   >   > 		i. b,c的l1之前所有位相等
>   >   > 		ii. a,c的l2之前所有位相等
>   >   > 		iii. a,b的l3之前所有位相等
>   >   > 	=> a,b,c的l2之前所有位相等 => b,c的l2之前所有位相等 => b,c的l1位相等 
>   >   > 	又b,c的l1不等。矛盾。
>   >   > 故low_bit(b^c)，low_bit(a^c)，low_bit(a^b)不完全不等。
>   >   > 	若low_bit(b^c)，low_bit(a^c)，low_bit(a^b)都相同，不妨设为l，则可知：在l位，b,c不同、a,c不同 => b,c相同，而b,c不同。矛盾。
>   >   > 故low_bit(b^c)，low_bit(a^c)，low_bit(a^b)仅有两个相等。
>   >   > ```
>   >
>   > ```TXT
>   > index = low_bit(x,p)^...^...^low_bit(x,p)^...^low_bit(x,a)^low_bit(x,b)^low_bit(x,c) 
>   > 	= low_bit(x,a)^low_bit(x,b)^low_bit(x,c)
>   > 	= low_bit(b^c)^low_bit(a^c)^low_bit(a^b) 
>   > ```
>   >
>   > 由②可以确定a,b,c中至少某一对的index位是不等的。不妨假设a,b不等，又由x可知，
>   >
>   > - 若bit(x,index)==0,故分为位index为0的一组和不为0的一组，而为0的一组符合第一种情况，不为0的符合第二种情况。
>   > - 若bit(x,index)==1,故分为位index为1的一组和不为1的一组，而为1的一组符合第一种情况，不为1的符合第二种情况。

# 8.++ & --

> - ```C
>   a = 5;
>   b = a++ * a++;
>   ```
>
> - C语言并没有规定进行`++`或`--`是立即自增、自减，是由编译器决定的；
>
> - 上述`a++`，首先表达式的值为5，但a自增到底是立即还是表达式执行之后的某个时刻进行是由编译器决定的。

---

# 9.C的六大语句

- **标号语句 / 空语句**

- **复合语句**

- **表达式语句**

  > - 条件表达式的计算中只执行一个`:`左右的表达式；
  >
  > - 条件表达式的类型：是`:`左右两个表达式的**最大类型**；
  >
  >   ```c
  >   int a = 2, b = 3;
  >   a > b ? a+1.0 : b;		//该表达式的值的类型为double类型
  >   ```

- **选择语句**

  > 在c语言中，else和**最近的**if进行匹配。
  >
  > ```c
  > if(y != 0)				// 1
  >     if(x != 0)			    // 2
  >         result = x / y;
  > else                                   // 该else与2匹配
  >     printf("Error: y is equal to 0\n");
  > 
  > //正确应为
  > if(y != 0){				// 1
  >     if(x != 0)			    // 2
  >         result = x / y;
  > }else                                  // 该else与1匹配
  >     printf("Error: y is equal to 0\n");
  > ```

- **迭代语句 / 循环语句**

- **跳转语句**

  > - `break`： 跳出所在循环或switch语句；
  > - `continue`： 跳转到当前循环体的末尾；
  > - `goto`: 可以跳转到**所在函数体内**的任意有标号的语句处；
  > - `return`： 返回当前函数值；对于`main`函数结束程序；

---

# 10.数组

> - 定义数组时，数组长度必须为**常量表达式**（即在编译期间即可求得其值的表达式）。 
> - C语言的数组 **不检查越界**(追求更高运行时效率)。因此，越界之后程序的行为是未定义的。
> - C语言的数组 **不能作为函数返回值**；
> - 数组名可以当做为指向数组首元素的指针，但该指针是**指针常量**，不能修改。

> 访问数组：
>
> - 索引方式(下标)
> - 指针



---

# 11.函数

> - 数组名作为参数传递时，会自动转换为指向数组首元素的指针；
> - 若编译器在函数调用之前，没有任何关于该函数的相关信息；此时，编译器将会为该函数创建一个**隐式声明**，**假定**该函数返回值类型为`int`，参数根据实参的类型和个数进行推断。

> - 局部变量
>
>   > 1. **自动存储期限**；
>   > 2. **块作用域**；
>
>   - 静态局部变量
>
>     > 具有**静态存储期限**（1.在编译时进行初始化；2.只能在所在函数内使用；3.其在整个程序运行期间都会保留其内存空间）；
>
>   - 自动局部变量
>
> - 外部变量
>
>   > 1. **静态存储期限**；
>   > 2. **文件作用域**；
>
> - 注意：在函数之间传递信息使用形参进行通信会比通过共享外部变量更好，**使用外部变量不易于程序的排错和维护**。



---

# 12.recursion

> **递归三问：**
>
> - 什么情况下考虑使用递归？
>
>   当问题具有递归结构时。即该问题可以分解为若干个子问题，子问题的求解方式和原问题一致，只是问题规模减小；子问题的解可以合并称为原问题的解。
>
> - 到底要不要使用递归？
>
>   若不存在重复计算或递归的层次不是太深的话，可以使用递归。
>
> - 如何写递归？
>
>   递归边界条件；递归式。

> - 约瑟夫环是一个数学的应用问题：已知 n 个人 (以编号1，2，3, ..., n 分别表示) 围坐在一张圆桌周围。从编号为 1 的人开始，每m个人出列一个人，直至只剩一个人。问：最终剩下的这个人的编号是多少？

> - 递归式：`f(n) = ((f(n-1)+m)%n) ? ((f(n-1)+m)%n) : n`;
> - 优化: 将编号从0开始；`f(n) = (f(n-1)+m)%n`； 最终结果`f(n)+1`;

---

# 13.pointer

> - **野指针**：未初始化 或 指向一片未知的内存空间的指针。 
>- 对野指针的操作（解引用）会导致未定义的行为。
>   
>- 当指针作为函数返回值时，禁止返回指向当前栈帧区域的指针（因为在执行返回语句之后，该函数栈帧已被释放，会成为一个野指针）。
> - `*p` 即为所指对象的 **引用**。
>  - 比如对于`&arr[SIZE(arr)]`，`arr[SIZE(arr)]`相当于`*(arr + SIZE(arr))`，`*(arr + SIZE(arr))`可以作为左值、也可以作为右值。因此其是一个引用。而对于`&arr[SIZE(arr)]`而言相当于对其引用对象的取地址。故此时不会涉及到数组越界访问的情况。
> - 指针可以当做一个数组名来使用，如`p[i] = *(p+i) = *(i+p) = i[p]`。

> 操作：
>
> - **解引用**： 
>
> - **偏移**： 
>
>   - 两个指针相减时，必须指向同一数组，否则，其值是**未定义**的。
>   - 当然 指针的大小的判断是通过减法确定的，因此也需要指向同一数组，否则是未定义的行为。
>
>   



---

# 14.string

> - C中没有string类型，只是一个逻辑类型。
> - C中，对于两个相邻的字符串字面值，编译器会将其合并成为一个。
> - C语言中，字符串字面值是当做字符数组处理的。

> 用字符串字面值做初始值，
>
> - 对于`char str[] = "hello";`，前者是将字符串字面值当做数组依次将元素拷贝存入到str字符数组中。此时str的长度是字符串字面值的长度加1。
> - 对于`char *p = "hello";` 后者是将字符串字面值的地址赋值给指针变量p。而字符串字面值放在常量区，不能修改。（注意在c++，必须是赋值给一个常量字符指针）

> - scanf("%s", str); 忽略前置空白字符，当遇到一个空白字符为止。
> - gets();  不会忽略前置空白符，一直读入直到遇到换行符才停止。gets会忽略换行符，并用空字符替代换行符。
> - 前两者都不会检查数组是否越界。故不安全。
> - puts与printf相比，多输出一个换行符。

> 设计输入函数：
>
> - 是否跳过前置空白字符?
> - 什么字符导致函数停止读取？（换行符、空白字符、某种特定字符...）这种字符需要存储？
> - 如果输入的字符串太长以致于无法存储时，如何处理？
>
> ```C
> //不跳过前置空白字符
> //读取指定最大大小n，遇到换行符停止，不存储换行符
> //超过则读入忽略
> int read_line1(char str[], int n){
> 	char c;
> 	int cnt = 0;
> 	while((c = getchar()) !='\n'){
>         	if(cnt < n) {
>                 	str[cnt++] = c;
>         	}
> 	}
> 	str[n-1] = '\0';
>         return cnt;
> }
> ```
>
> ```c
> //不跳过前置空白字符
> //读取指定最大大小n，遇到换行符停止或已读取了最大大小，不存储换行符
> //超过则不读入
> int read_line2(char str[], int n){
> 	char c;
> 	int cnt = 0;
> 	while(cnt < n  &&  (c = getchar()) !='\n'){
>                 str[cnt++] = c;
> 	}
> 	str[n-1] = '\0';
>         return cnt;
> }
> ```

> 库函数
>
> - `strlen()` 
>
> - `strcmp()`  
>
> - `strcpy()` 不安全，会存在数组越界访问。
>
> - `strcat()` 不安全，会存在数组越界访问。
>
> - `strncpy()` 指定了拷贝的最大长度，注意留一个位置给空字符
>
>   ```c
>   strncpy(str1, str2, strlen(str1)-1);
>   ```
>
> - `strncat()` 指定了能连接的最大长度，注意留一个位置给空字符
>
>   ```c
>   strncat(str1, str2, strlen(str2) - strlen(str1) - 1);
>   ```

> 惯用法：
>
> - 求字符串的长度
>
>   - ```c
>     //遍历完指向空字符
>     const char *p = str;
>     while(*p){
>     	p++;
>     }
>     ```
>
>   - ```c
>     //遍历完指向空字符的下一位置
>     const char *p = str;
>     while(*p++)
>      	;
>     ```
>
> - 字符串的复制
>
>   ```c
>   while(*str1++ = *str2++)
>   	;
>   ```

---

# 15.struct

> - 为什么结构体中成员的内存地址必须要对齐？
>
>   从内存中读取数据，要以其地址进行访问，并且访问时可以指定要读取的数据的字节数（字、半字、字节）。



---

# 16. void*

> `void *`是指不指向任何对象的指针。
>
> - 在C中，`void*`和其他类型指针可以相互转换。（c++中将一个void*转换为其他类型指针需要强制转换）

> `malloc()`: 从堆区分配指定大小的内存空间，若分配失败返回一个NULL；成功返回void*指针。
>
> `calloc()`: 比malloc多了将内存空间清零。
>
> `void* realloc(void* ptr, size_t size)`: ptr必须指向堆区的内存空间。
>
> - C标准关于realloc函数的规则：
>   - 若申请新内存不成功，则返回空指针，并且旧内存块数据不会发生改变；
>   - 若新内存块比旧内存块大，则超过的部分**不会被初始化**；
>   - 若realloc的第一个参数为空指针，则行为和malloc一样；
>   - 若realloc的第二个参数为0,则将会释放ptr所指的内存空间。
> - C没有明确指明realloc的工作原理：（约定）
>   - 当新内存块比旧内存块小时，会**截断**旧内存块；
>   - 当新内存块比旧内存块大时，首先会**试图**扩大旧内存块；若不可行，再在其他地方申请内存块，并将旧内存块中的内容复制到新内存块中，并释放旧内存块。
>
> `free()`:
>
> - 传给free函数的参数必须是指向堆区内存空间的指针，否则其行为是未定义的。
> - 同一堆区内存空间不能释放两次以上。

> **垃圾**：对于程序，不可再访问的内存块。
>
> **内存泄漏**：若程序中留有垃圾，这种现象称为内存泄漏。

---

# 17.file

> 文件缓冲区：
>
> - 全缓冲 （写满才能读，读完才能写）
> - 行缓冲 （每次从输入流/输出流中读入/输出一行数据）（`stdin` `stdout`）
> - 无缓冲 （`stderr`）

> 文本文件：
>
> - 存在**行**的概念。（Windows:\r\n   Unix:\n）
> - 可能包含一个特殊的**文件末尾标记**。(Windows:crtl+z Unix:无)
>
> 二进制文件：

> 库函数
>
> - fgetc fputc
> - fgets fputs
> - fprintf fscanf   实现**序列化**和**反序列化**
> - 二进制文件：read write

---

# 18.errno

>  `error` 是一个`int`类型的全局变量。（C11修改其为**线程本地变量**，即每个线程都有一个独有的errno变量）
>
>  - 定义在`errno.h`中；
>  - 标准库的一些函数（如与文件相关的一些函数），若在调用过程中发生了错误，则会设置errno值，以表明发生了何种类型的错误。
>  - 程序启动时初始为0。
>  - `perror` stdio.h
>  - `strerror` string.h



---



# 19.`stdin` `stdout`重新绑定

> - **文件描述符**：
>
>   - 在Linux/Unix系统中，文件描述符是一个**整数类型**的**标识符**，用于表示一个打开的文件、套接字、或其他可读/可写的资源。
>   - 文件描述符是**进程级**的。（进程是资源分配的基本单位。在进程PCB中有文件打开表，系统中有一个系统文件打开表）
>   - 文件描述符的值是非负整数，通常从0开始递增，它是由**OS内核负责分配**的。
>   - 在Linux/Unix中，stdin,stdout,stderr分别对应的描述符是0,1,2。当进程启动时，这些文件描述符已经存入到进程的文件打开标记中了。
>
> - `open()`:
>
>   - **系统调用**。用于打开文件，返回值是一个文件描述符。定义在`fcntl.h`中。
>   - 如果出现错误，返回-1。并且会设置errno。
>   - 与fopen()区别：fopen()函数一个标准库函数，用于打开一个文件，返回一个文件指针FILE*；定义在stdio.h中。该文件结构结构体FILE描述了打开的文件信息。
>   - fopen()的底层实现通常是通过open()系统调用来打开文件的，封装了open()。
>   
> - `dup2()`:
>
>   - ```c
>     int dup2(int oldfd, int newfd);
>     //将oldfd赋值到newfd中，并返回newfd
>     //若newfd已经打开，则先会将其关闭，然后将oldfd复制给newfd
>     //若oldfd和newfd相等则不会进行任何操作，直接返回newfd
>     ```
>
>   - 系统调用。
>
>   - 用于复制文件描述符并将其指向另一个文件描述符。
>
>   - 返回值值是新的文件描述符。出现错误返回-1.并设置errno。
>
>   - 定义在unistd.h中。
>
> - `dup()`:
>
>   - ```c
>     int dup(int oldfd);
>     //用于复制文件描述符。
>     ```
>
>   - 系统调用。
>
>   - 将oldfd复制到指定的文件描述符，并返回一个新的文件描述符。新的文件描述符和旧的文件描述符**共享一个文件表项**，即其都指向同一个打开的文件或设备。旧的文件符和新的文件描述符之间没有关联，可以单独地进行写、读、关闭等操作。
>

> ```c
> #include <stdio.h>
> #include <fcntl.h>
> #include <unistd.h>
> 
> int main() {
>     int fd;
> 
>     // 打开文件，并获取文件描述符
>     fd = open("output.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
>     if (fd == -1) {
>         perror("open");
>         return 1;
>     }
> 
>     // 重定向标准输出
>     if (dup2(fd, STDOUT_FILENO) == -1) {
>         perror("dup2");
>         return 1;
>     }
> 
>     // 使用标准输出
>     printf("Hello, world!\n");
> 
>     // 关闭文件描述符
>     close(fd);
> 
>     return 0;
> }
> ```
>
> 在上述示例中，首先使用open函数打开一个名为output.txt的文件，并获取文件描述符。然后使用dup2函数将文件描述符fd重定向到标准输出文件描述符（STDOUT_FILENO），即将标准输出重定向到output.txt文件中。接着，使用printf函数向标准输出写入一行文字，即将输出写入到output.txt文件中。最后，使用close函数关闭文件描述符，释放系统资源。

---

# 20.sort and seach algrithm

> 选择排序
>
> - idea: 每次选择一个最小的放到最终的位置，循环n-1次。
>
> - demo: 
>
>   ```c
>   void select_sort(int arr[], int n){
>           for(int i = 0; i < n-1;  i++){
>   		int min = i; 
>   		for(int j = i+1;j<n;j++){
>   			if(arr[j] < arr[min]){
>   				min = j;
>   			}
>   		}
>   		if(min == i) continue;
>   		swap(arr, min, i);
>   	}
>   }
>   ```
>
>   

> 冒泡排序
>
> - idea:每次将相邻的两两比较，将最大的一个放置最终的位置，循环n-1次。
>
> - demo:
>
>   ```c
>   void bulbble_sort(int arr[], int n){
>   	for(int i = 0; i < n-1; i++){
>   		int isSwapped = 0;
>   		for(int j = 0; j < n - i - 1; j++){
>   			if(arr[j] > arr[j+1]){
>                   		swap(arr, j , j+1);
>                   		isSwapped = 1;
>   			}
>   		}
>   		if(isSwapped == 0) return;
>   	}
>   }
>   ```

> 简单插入排序
>
> - idea:将待排的数分为有序区和无序区，每次将无序区的一次元素插入到有序区，循环n-1次。
>
> - demo:
>
>   ```C
>   void insert_sort(int arr[], int n){
>   	for(int i = 1; i < n; i++){
>   		int val = arr[i];
>   		int j = i-1;
>   		while(j >= 0 && arr[j] > val){
>   			arr[j+1] = arr[j];
>   			j--;
>   		}
>   		arr[j+1] = val;
>   	}
>   }
>   ```

> 希尔排序
>
> - idea:由于简单插入排序时间复杂度最好情况为O(N),最坏的情况和平均的情况都是O(N*N)。因此，尽量使待排的数据整体基本有序，那么其效率将会提升。因此，希尔排序是分组进行插入排序，随着步长减小到1，则进行最后一趟插入排序。（因此，步长最后一次一定是1，即最后一次进行一次直接插入排序）
>
> - demo:
>
>   ```c
>   void shell_sort(int arr[], int n）{
>   	int gap = n / 2;
>   	while(gap >= 1){
>   		for(int i = gap; i < n; i++){
>   			int val = arr[i];
>           		int j = i - gap;
>   			while(j >= 0 && arr[j] > val){
>   				arr[j+gap] = arr[j];
>   				j -= gap;
>   			}
>   			arr[j+gap] = val;
>   		}
>   		gap /= 2;
>   	}
>   }
>   ```

> 快速排序：
>
> - idea:首先通过选取基准值，将待排数据划分为两个区域，然后递归进行划分。
>
> - demo:
>
>   ```c
>   void quick_sort(int arr[], int n){
>   	if(n <= 1) return;
>   	srand((unsigned)time(NULL));
>   	qucik_sort_helper(arr, 0, n-1);
>   }
>   void quick_sort_helper(int arr[], int left, int right){
>   	if(left >= right) return;
>   	int mid = partition(arr, left, right); 
>   	qucick_sort_helper(arr, left, mid);
>   	qucick_sort_helper(arr, mid + 1, right);
>   }
>   int partition(int arr[], int left, int right){
>   	int pivot = rand() %(right - left) + left;
>   	swap(arr, pivot, right);
>   	int idx = left, i = left;
>   	while(i < right){
>   		if(arr[i] < arr[right]){
>   			if(idx != i){
>   				swap(arr, idx, i);
>   			}
>   			++idx;
>   		}
>   		++i;
>   	}
>   	swap(arr,idx,right);
>   	return idx;
>   }
>   ```
>
> - 优化：
>
>   1. 随机选取基准值
>   2. 选取3个或5个的中位数作为基准值（O(NlogN)）

> 归并排序
>
> - idea:采用分治思想，将待排数据划分为两个有序区，然后将这两个有序区进行归并。递归。
>
> - demo:
>
>   ```C
>   void merge_sort(int arr[], int n){
>   	if(n <= 1) return;
>   	int *new_arr = malloc(sizeof(int) *n);
>   	if(!new_arr){
>   		fprintf(stderr, "malloc failed in merge_sort\n");
>   		exit(1);
>   	}
>   	merge_sort_helper(arr, 0, n-1, new_arr);
>   	free(new_arr);
>   }
>   void merge_sort_helper(int arr[], int left, int right, int new_arr[]){
>   	if(left >= right) return;
>   	int mid = left + (right - left >> 1);
>   	merge_sort_helper(arr, left, mid, new_arr);
>   	merge_sort_helper(arr, mid + 1, right, new_arr);
>   	merge(arr, left, mid, right, new_arr);
>   }
>   void merge(int arr[], int left, int mid, int right, int new_arr[]){
>   	int i = left , j = mid + 1, k = left;
>   	while(i <= mid && j <= right){
>   		if(arr[i] <= arr[j]){
>   			new_arr[k++] = arr[i++];
>   		}else{
>   			arr[k++] = arr[j++];
>   		}
>   	} 
>   	while(i <= mid){
>   		new_arr[k++] = arr[i++];
>   	}
>   	while(j <= right){
>   		new_arr[k++] = arr[j++];
>   	}
>   
>   	for(int k = left; k <= right; k++){
>   		arr[k] = new_arr[k];
>   	}
>   }
>   ```

> 堆排序:
>
> - idea: 构建一个大顶堆，然后将最大元素放在最终的位置上，将交换的元素放在堆顶，调整堆。循环n-1此。
>
> - demo:
>
>   ```c
>   void heap_sort(int arr[], int n){
>   	build_max_heap(arr, n);
>   	for(int i = n - 1; i > 0; i--){
>   		swap(arr, 0, i);
>   		heapify(arr, i, 0);
>   	}
>   }
>   void build_max_heap(int arr[], int n){
>   	int idx = (n - 2) / 2;
>   	while(idx >= 0){
>   		heapify(arr, n, idx);
>   		idx--;
>   	}
>   }
>   void heapify(int arr[], int n, int idx){
>   	int left = 2 * idx + 1;
>   	int right = 2 * idx + 2;
>   	int max = idx;
>   	if(left < n && arr[left] > arr[max]){
>   		max = left;
>   	}
>   	if(right < n && arr[right] > arr[max){
>           	max = right;
>   	}
>   	if(max == idx) return;
>   	swap(arr, idx, max);
>   	idx = max;
>   }
>   ```
>
> - 建堆的时间复杂度是：O(N)。

> 二分查找
>
> - ```C
>   int binarySearch(int arr[], int n, int key) {
>   	int left = 0, right = n - 1;
>   	while(left <= right) {
>   		int mid =  left + (right - left >> 1);
>   		int cmp = arr[mid] - key;
>   		if(cmp == 0){
>   			return mid;
>   		} else if (cmp < 0){
>   			left = mid + 1;
>   		}else{
>   			right = mid - 1;
>   		}
>   	}
>   	return -1;
>   }
>   ```
>
> - 变形：
>
>   - 查找等于key的最后一个元素
>
>     ```c
>     int binarySearch(int arr[], int n, int key) {
>     	int left = 0, right = n - 1;
>     	while(left <= right) {
>     		int mid =  left + (right - left >> 1);
>     		int cmp = arr[mid] - key;
>     		if(cmp == 0){
>     			if(mid == right || arr[mid + 1] > key){
>     				return mid;
>     			}else{
>     				left = mid + 1;
>     			}
>     		} else if (cmp < 0){
>     			left = mid + 1;
>     		}else{
>     			right = mid - 1;
>     		}
>     	}
>     	return -1;
>     }
>     ```
>
>   - 查找等于key的第一个元素
>
>     ```C
>     int binarySearch(int arr[], int n, int key) {
>     	int left = 0, right = n - 1;
>     	while(left <= right) {
>     		int mid =  left + (right - left >> 1);
>     		int cmp = arr[mid] - key;
>     		if(cmp == 0){
>     			if(mid == left || arr[mid - 1] < key){
>     				return mid;
>     			}else{
>     				right = mid - 1;
>     			}
>     		} else if (cmp < 0){
>     			left = mid + 1;
>     		}else{
>     			right = mid - 1;
>     		}
>     	}
>     	return -1;
>     }
>     ```
>
>   - 查找小于等于key的最后一个元素
>
>     ```C
>     int binarySearch(int arr[], int n, int key) {
>     	int left = 0, right = n - 1;
>     	while(left <= right) {
>     		int mid =  left + (right - left >> 1);
>     		int cmp = arr[mid] - key;
>     		if(cmp <= 0){
>     			if(mid == right || arr[mid+1] > key){
>     				return  mid;
>     			}else{
>     				left = mid + 1;
>     			}
>     		}else{
>     			right = mid - 1;
>     		}
>     	}
>     	return -1;
>     }
>     ```
>
>   - 查找大于等于key的第一个元素
>
>     ```C
>     int binarySearch(int arr[], int n, int key) {
>     	int left = 0, right = n - 1;
>     	while(left <= right) {
>     		int mid =  left + (right - left >> 1);
>     		int cmp = arr[mid] - key;
>     		if(cmp >= 0){
>     			if(mid == left || arr[mid-1] < key){
>     				return  mid;
>     			}else{
>     				right = mid - 1;
>     			}
>     		}else{
>     			left = mid + 1;
>     		}
>     	}
>     	return -1;
>     }
>     ```

> - 找到n个数据中第k大的数据（k<n）
>
>   - **用二分法以及分区的思想**★★★
>
>     ```c
>     int find_kth_number(int arr[], int n, int k){
>     	int left = 0, right = n - 1;
>     	srand(time(NULL));
>     	while(left < right){
>     		int pivot = partition(arr, left, right);
>     		if(pivot == n - k){
>     			return arr[pivot];
>     		}else if(pivot < n - k){
>     			left = pivot + 1;
>     		}else{
>     			right = pivot - 1;
>     		}
>     	}
>     }
>     int partition(int arr[], int low, int high){
>     	int pivot = rand()%(high - low) + low;
>     	swap(arr, pivot, high);
>     	int i = low, idx = low;
>     	while(i < high){
>     		if(arr[i] < arr[high]){
>     			if(i != idx){
>     				swap(arr, i ,idx);
>     			}
>     			idx++;
>     		}
>     		i++;
>     	}
>     	swap(arr,idx,high);
>     }
>     ```



---

# 21.red-black tree

> - **2-3-4树**（是一棵4阶B树）
> - 插入：
>   - 2-结点 的插入会导致 其变成为 3-结点；
>   - 3-结点 的插入会导致 其变成为 4-结点；
>   - 4-结点的插入需要进行**分裂**：
>     - **自底向上**：分成三部分，二个2-结点，一个插入到父结点。若有重复此操作。
>     - **自顶向下**：在查找插入位置时，自顶向下凡是遇到4-结点都将其分裂。
> - 删除
> - 查找
>
> > 2-3-4树的增加、删除、查找取决于其高度h。
> >
> > 最坏的情况：log_2_(n), `O(log(n))`
> >
> > 最好的情况：log_4_(n), `O(log(n))`

> IDEAS: 用简单的BST树来表示2-3-4树。
>
> ![](E:\Sources\c\day01\pics\2-3-4树的结点对应于BST树.png)
>
> 即：BST树中将两个结点通过“**红色边**"连接形成一个2-3-4树中的结点。
>
> 由于“边”只是逻辑上的，因此 用 **孩子结点的颜色** 表示从孩子结点到双亲结点的边。

> 1. 结点是红色或黑色;
> 2. 根结点是黑色;
> 3. 叶子结点（NIL）是黑色的。
> 4. 任何一个红色节点有两个黑色节点；（即表示2-3-4树中度为4的结点表示只有一种）
> 5. 从根节点到任一叶子结点的黑色节点数相等；（黑高平衡；即表示2-3-4树是一个完美平衡的树）

---

## **插入**：

（插入的结点默认是红色的）

> ![](\pics\RBT_insert_case3.png)
>
> ![](\pics\RBT_insert_case4.png)
>
> ![](\pics\RBT_insert_case4.png)
>
> 1. 新节点N位于树的根上，没有父节点。置黑即可。
>
> 2. 新节点的父节点P是黑色，则直接插入即可。
>
> 3. 如果父节点P和叔父节点U二者都是红色。
>
>    > 则此时将P和U的颜色置黑，并将G节点的颜色置红；向上传递判断。
>   >
>    > （即相当于此时插入一个4-结点，需要进行分裂）
> 
> 4. 父节点P是红色而叔父节点U是黑色或缺少，并且新节点N是其父节点P的右子节点而父节点P又是其父节点的左子节点。（LL型）
>
>    > （LL）右旋G节点，置P节点为G节点的颜色，置G节点的颜色为红色。
>   >
>    > （RR）左旋G节点，置P节点为G节点的颜色，置G节点的颜色为红色。
>    >
>    >  (不符合4-结点的表示，将其调整符合4-结点的表示)
> 
> 5. 父节点P是红色而叔父节点U是黑色或缺少，新节点N是其父节点的左子节点，而父节点P又是其父节点G的左子节点。（LR型）
>
>    > （LR）左旋P节点，右旋G节点，置N节点的颜色为G节点的颜色，置G节点的颜色为红色。
>   >
>    > （RL）右旋P节点，左旋G节点，置N节点的颜色为G节点的颜色，置G节点的颜色为红色。
>    >
>    >  (不符合4-结点的表示，将其调整符合4-结点的表示)

> <img src="\pics\2-3-4insert.png" style="zoom: 67%;" />
>
> <img src="\pics\2-3-4Node转RBNode.png" style="zoom: 67%;" />
>
> <img src="\pics\RBinsert.png"  />

---

## **删除**:

> - 2-3-4树：
>  - 对于3-结点、4-结点直接删除对应的key即可。
>   - 若是非叶结点，
>     - 对于2-结点，找其前驱或后继进行代替。
>       - 孩子结点至少一个非2-结点，则直接代替；
>       - 孩子结点都为2-结点或不存在，将孩子结点合并。
>   - 若是叶子结点，
>     - 对于2-结点，找兄弟结点借。
>       - 若左右兄弟至少一个非2-结点，则将对应的key和借的key调整位置。
>       - 若左右兄弟都为2-结点或不存在，则将兄弟进行合并。

> - RB树：
>
>   > 删除一个两个不为空的结点，为了保持原有的BST树的特性，即用该结点的前驱或后继结点进行替换（即左子树的最右结点或右子树的最左结点），进而将一个删除有两个孩子的结点的问题转换为删除至多有一个孩子的问题。
>   >
>   > 故，以下只考虑至多只有一个孩子的结点。
>
>   - 若是根节点，直接删除；
>
>   - 若删除结点v和删除后进行替代的结点u的颜色**不全为黑色**，则直接删除，并置黑色（删除之前是一棵RBtree，因因此不会存在两者都为红色的情况）（NIL视为是一个黑色结点）；
>
>   - 若删除结点v和删除后进行替代的结点u的颜色**都为黑色**，
>
>     > 此时由于删除了一个黑色结点，会导致结点的**黑高**（:从当前结点到达叶子结点路径的黑色结点数，不包括当前结点，NIL当做黑色）发生变化，使得性质5不满足。因此，考虑删除结点v的parent结点以及其兄弟结点s,兄弟结点的左右孩子结点sl,sr。
>     >
>     > - 删除之前：`bh(p) = bh(v)+1 = bh(s) + (1 or 0) = bh(u) + 2` 
>     > - 删除之后：经过u结点路径的黑色结点数将会比不经过u结点路径的黑色结点数减一。
>
>     - 当u是双黑结点，并且u是根节点：
>
>       则只用将u变成单黑结点，并且将树的黑高减一。
>
>     - 当u是双黑结点，并且不是根节点：
>
>       - 当s是黑色，sl,sr中至少一个为红色：
>
>         - "LL"(s,s的红色孩子的位置关系):
>
>           将s的颜色置为p的颜色，将s的红色孩子的颜色以及p的颜色置为黑色；右旋p。
>
>         - "LR"：
>
>           将s的红色孩子的颜色置为p的颜色；左旋s；右旋p;将p的颜色置为黑色。
>
>         - "RR":
>
>           将s的颜色置为p的颜色，将s的红色孩子的颜色以及p的颜色置为黑色；左旋p。
>
>         - "RL"：
>
>           将s的红色孩子的颜色置为p的颜色；右旋s；左旋p;将p的颜色置为黑色。
>
>       - 当s,sl,sr都为黑色：
>
>         - 若p不是红色，则将s的颜色置为红色，将p置为双黑。向上继续。
>         - 若p是红色，则将s的颜色置为红色，将p置为黑色。
>
>       - 当s为红色：
>
>         - 当p->left == u，
>
>           左旋p;交换s和p的颜色；此时可能发生前两者情况，继续判断。
>
>         - 当p->right == u，
>
>           右旋p;交换s和p的颜色；此时可能发生前两者情况，继续判断。





---













