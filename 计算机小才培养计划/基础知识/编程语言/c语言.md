# 基础补充

## 数组
- char[]
- string 

### 多维数组
- 创建
	- int a[]【10】注意行可以为空，但是列必须有数字




### string函数

| 函数     | 作用    |     |
| ------ | ----- | --- |
| strcmp | 比较字符串 |     |
|        |       |     |




## 结构体Struct
```c
struct a{
int a;
//成员变量
}b;//创造的一个a结构体成员，可以再这里对其进行初始化
```

## 共用体Union
	同时只有一个有作用
	另一个可能可以使用，但是输出的结果是不对的 
	可能有点像其他语言中的泛型？
	char类型的数组，初始化可以通过字符串直接实现，但是后面赋值不可以 
总结：**可以是不同类型的类型，以最后一次的赋值为准** 
```c
union a{
int s1;
char s2;
//......
};
int main(){
a.s1=1;
a.s2='A';
}
```


## 枚举enum
- 实际上是整数类型 
- 当上一个已经赋值后，下一个自动赋值为上一个加1
- 和数组的区别：
```c
#include <stdio.h>
enum Weekday {
    SUNDAY=11,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY
};

int main() {
    enum Weekday today = SUNDAY;
    int i=0;
	while(i++<8)
	{
		printf("Today is day number %d of the week.\n", SATURDAY);
	} 
    // 输出枚举成员的值

    return 0;
}
```


## 创造数据类型
```c
typedef struct a{
	int r;
	struct a b;
};
```




## 输入
- 常用的
printf
fgets
fput








## 补充
### 数学
math:
- `double log(double x);` // 计算自然对数（以e为底）的x的值
- `double log10(double x);` // 计算常用对数（以10为底）的x的值
- `double pow(double x, double y);` // 计算x的y次方
-  `double sqrt(double x);` // 计算x的平方根
- `double cbrt(double x);` // 计算x的立方根（立方根）

### 文件处理
#### 1. 文件指针（FILE*）
在C语言中，文件操作通常通过文件指针（`FILE*` 类型）来实现。`<stdio.h>` 头文件中。

#### 2. 打开文件（fopen）
要操作文件，首先需要打开文件。`fopen` 函数用于打开文件，并返回一个指向 `FILE` 结构的指针。

```c
FILE *fopen(const char *filename, const char *mode);
```
- `filename`：文件的名称。
- `mode`：文件打开的模式，如 "r"（只读）、"w"（只写）、"a"（追加）、"r+"（读写）、"w+"（读写，清空文件内容）、"a+"（读写，追加）等。

#### 3. 读取文件（fread、fgetc、fgets）
- `fgetc`：从文件中读取一个字符。
- `fgets`：从文件中读取一行。
- `fread`：从文件中读取数据。

```c
int fgetc(FILE *stream);
char *fgets(char *str, int num, FILE *stream);
size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
```

#### 4. 写入文件（fwrite、fputc、fprintf）
- `fputc`：向文件写入一个字符。
- `fprintf`：向文件写入格式化字符串。**覆盖
- `fwrite`：向文件写入数据。

```c
int fputc(int c, FILE *stream);
int fprintf(FILE *stream, const char *format, ...);
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
```

#### 5. 文件定位（rewind、fseek）
- `rewind`：将文件指针重置到文件的开头。
- `fseek`：移动文件指针到指定位置。

```c
void rewind(FILE *stream);
int fseek(FILE *stream, long int offset, int whence);
```

#### 6. 文件结束检测（feof）
- `feof`：检查是否到达文件末尾。

```c
int feof(FILE *stream);
```

#### 7. 错误检测（ferror）
- `ferror`：检查文件操作是否发生错误。

```c
int ferror(FILE *stream);
```

#### 8. 关闭文件（fclose）
操作完成后，需要关闭文件以释放资源。

```c
int fclose(FILE *stream);
```

#### 示例代码
下面是一个简单的示例，演示如何使用这些函数读取和写入文件：

```c
#include <stdio.h>

int main() {
    FILE *fp;
    char filename[] = "example.txt";
    char ch;

    // 打开文件用于读取
    fp = fopen(filename, "r");
    if (fp == NULL) {
        perror("Error opening file");
        return -1;
    }

    // 读取文件内容
    while ((ch = fgetc(fp)) != EOF) {
        putchar(ch);
    }

    // 关闭文件
    fclose(fp);

    // 打开文件用于写入
    fp = fopen(filename, "w");
    if (fp == NULL) {
        perror("Error opening file");
        return -1;
    }

    // 写入文件内容
    fputs("Hello, World!\n", fp);

    // 关闭文件
    fclose(fp);

    return 0;
}
```

这个示例首先打开一个文件用于读取，读取文件内容并打印到标准输出，然后关闭文件。接着，它再次打开同一个文件用于写入，写入一行文本，最后关闭文件。





# 考试秘籍
- switch
	- 正常的switch函数每个后需要加上break
	- default,每一个都正常的加上break时，没有匹配的值时，才执行
	- 可以作为判断条件的条件：必须是常量表达式或者字符型
	- 什么可以作为被判断的值的:可以取表达式，但是必须是整型表达式


- 注意浮点数，计算的时候加上.0
- 可以使用pow函数开方，注意写成1.0/2.0的形式
- 乘法需要加上乘法号

- 用户标识符
	- 不以数字开头


- 大小写字母的检测
	- 第一种方法，通过字节码进行判断
	    大写字母65-90，小写字母97-122（相差32）
	- 第二种方法：通过头文件"ctype.h"
		- `isalpha(c)`：检查`c`是否是字母（大写或小写）。
		- `isupper(c)`：检查`c`是否是大写字母。
		- `islower(c)`：检查`c`是否是小写字母。


- 整数运算是向下取整的
	- int a=1+1.6      结果是2
	- int a=1/2=0


- c语言中的数字类型，基本的分成前缀和后缀
	- 1. 0x     16进制数字
	- 2. **八进制（Octal）数**：
     以`0`开头，表示该数是八进制的。
     例如：`015`表示十进制中的13。
	3. **二进制（Binary）数**（C99标准引入）：
	    - 以`0b`或`0B`开头，表示该数是二进制的
	    - 例如：`0b1010`表示十进制中的10。
	4. **浮点数（Floating-point）数**：
		- 注意e后面的数字是整数
	    - 也可以使用科学计数法表示，如`1.23e-2`表示`0.0123`。
	6. **指数形式（Exponential）数**：
	    - 浮点数也可以使用指数形式表示，如`1.23e2`表示`123`。
	7. **长整型（Long）数**：
	    - 长整型数可以用`L`或`l`后缀表示，如`123L`或`123l`。
	    - 对于无符号长整型，可以用`UL`或`ul`后缀，如`123UL`。
	8. **长长整型（Long long）数**：
	    - 长长整型数可以用`LL`或`ll`后缀表示，如`123LL`或`123ll`。
	    - 对于无符号长长整型，可以用`ULL`或`ull`后缀，如`123ULL`。
	9. **单精度浮点数**：
	    - 可以用`f`或`F`后缀表示，如`3.14f`。
	10. **长双精度浮点数**：
	    - 可以用`L`或`l`后缀表示，如`3.14L`。


- %取余运算只可以是整数类型

- sizeof是一个运算符号

- `&`用于整数的位操作，而`&&`用于布尔逻辑判断

- 判断素数
	- 素数（质数）：素数只能被1和它本身整除

- 运算符优先级
1. **后缀运算符**：
    - `() [] -> .`
    - 这些运算符具有最高的优先级，其中函数调用`()`、数组访问`[]`和结构体成员访问`->`（或`.`）。
2. **一元运算符**：
    - `++ --`
    - 递增和递减运算符。
3. **乘除和取模运算符**：
    - `* / %`
    - 乘法、除法和取模运算符。
4. **加减运算符**：
    - `+ -`
    - 加法和减法运算符。
5. **关系运算符**：
    - `< <= > >=`
    - 小于、小于等于、大于、大于等于运算符。
6. **相等运算符**：
    - `== !=`
    - 等于和不等于运算符。
7. **位运算符**：
    - `& ^ ~`
    - 按位与、按位异或和按位取反运算符。
8. **逻辑与运算符**
9. **逻辑或运算符**
10. **三元条件运算符**
11. **赋值运算符**

- 在C语言的if语句中，可以作为判断的表达式是任意表达式

- 最后的提醒：
	- easy!!!!
	- 

### 尾指针