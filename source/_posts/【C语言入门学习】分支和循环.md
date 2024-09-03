---
title: 【C语言入门学习】分支和循环
top: false
cover: /img/blog_cover/01-c base.jpg
toc: true
mathjax: false
author: Szturin
password:
  - C语言
  - C/C++
  - 编程
tags: C语言
categories:
  - - 学习笔记
    - C语言
  - - C/C++
abbrlink: 6621
date: 2024-02-23 23:21:38
img:
coverImg:
summary:
---

# 【C语言入门学习】分支和循环

**2024.2.20更新**

## #基本概念
### 一、语句
 **什么是语句？**
c语言中语句是用于控制计算机执行相关操作的指令，一个==语句==会被==编译==成若干条==机器命令==继而由计算机执行。

 **语句的类型**
 - 表达式语句
 - 函数调用语句
 - 控制语句
 - 复合语句
 - 空语句

>控制语句用于==控制程序的执行流程==，以实现程序的各种结构方式，它们由特定的语句定义符组成，C语言有九种控制语句。可分成以下三类：
>1. 条件判断语句也叫分支语句：if语句、switch语句；
>2. 循环执行语句：do while语句、while语句、for语句；
>3. 转向语句：break语句、goto语句、continue语句、return语句

---
## #代码部分
### 一、if分支语句
if语句的书写规范，跳转[【c语言入门学习】代码的书写规范](https://blog.csdn.net/qq_63100905/article/details/135834241?spm=1001.2014.3001.5502)
### 二、switch分支语句
switch中break的实际作用是把语句列表划分为不同的分支部分，不加break，会一直向下执行程序
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

#include <stdio.h>


int main()
{
	int n = 1;
	int m = 2;
	switch (n)//switch执行一次条件判断，然后指定到对应的case语句中
	{
	case 1:
		m++;//n=1,m=3
	case 2://此处也会执行，因为没有上句没有break跳出, case不需要判断条件,直接执行语句内容
		n++;//n=2,m=3
	case 3://执行
		switch (n)
		{//switch允许嵌套使用
		case 1:
			n++;
		case 2:
			m++;
			n++;//m=4,n=3
			break;//break跳出自己所在的switch语句
		}
	case 4:
		m++;//m=5,n=3
		break;
	default:
		break;
	}
	printf("m = %d, n = %d\n", m, n);
	return 0;
}
```
### 三、while循环语句
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	//在while循环中，break用于永久中止循环
	int i = 1;
	while (i <= 10)
	{
		if (i == 5)
		{
			break;
		}
		printf("%d\n", i);
		i++;
	}
}
```
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	//在while循环中，continue的作用是跳过本次循环,直接去判断部分，看是否进行下一次循环体
	int i = 1;
	while (i <= 10)
	{
		if (i == 5)
		{
			continue;
		}
		printf("%d\n", i);
		i++;
	}
}//执行结果：continue执行时会直接跳转到while判断部分，而i=5保持不变，程序无限循环
```
### #do while循环语句
先执行循环体，在执行循环判断
- do while较为少用
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	int i = 0;
	do
	{
		printf("hi\n");
		i++;
	} while (i < 5);
}
```
```
运行结果：
hi
hi
hi
hi
hi

```
### 三、for循环语句
-  for循环泛用性比while更好
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	int i = 0;//c语言风格for语句之前需要定义变量,c++可以在for循环内部定义
	for (i = 1; i <= 10; i++)
	{
		if (i == 5)
		{
			continue;
		}//会执行i++，之后i=6
		printf("%d\n", i);//结果跳过5
	}
	return 0;
}
```
#### for循环范例：
**for循环实现阶乘**
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	int n = 0;
	printf("请输入n：");
	scanf("%d", &n);
	
	int i = 0;
	int num = 1;
	for (i = 1; i <= n; i++)
	{
		num = num * i;
	}
	printf("%d\n", num);
	return 0;
}
```
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()// for循环 中最好不要在 循环体 内部 进行 变量再定义
{
	int i = 0;
	for (i = 0; i < 10; i++)
	{
		printf("%d", i);
		i = 5;
	}
	return 0;
}
```
**for循环实现1到10的阶乘和**
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	int i = 0;
	int num = 1;//1到10的阶乘
	int sum = 0;//1到10的阶乘总和

	for (i = 1; i <= 10; i++)
	{
		num *= i;
		sum += num;
		printf("第%d次和为:%d\n", i, sum);
	}
	//时间复杂度低，更高效的写法

	printf("总的和为:%d\n", sum);
	return 0;
}
```
**for循环输出1到100中3的倍数**
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>
//写一个代码打印1-100之间所有3的倍数的数字
int main008()
{
	int i = 0;
	for (i = 1; i <= 100; i++)
	{
		//判断i是否为3的倍数
		if (i % 3 == 0)
		{
			printf("%d\n", i);
		}
	}
	return 0;
}
```
### #字符操作语句
>**getchar**
>作用：read/print "abcde" from stdin
>可能的输出:
>1.End of File reached
>2.字符
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	//getchar() 获取一个字符
	//EOF end of file 文件结束的标识
	//putchar() 输出一个字符
	//int ch = getchar();
	//putchar(ch);

	int ch = 0;
	while ((ch = getchar()) != EOF)
	{
		putchar(ch);
	}
	return 0;
	//ctrl + z 读取到EOF结束
}
```
```
运行结果：
a
a
v
v
c
c
^Z
D:\2_c++_项目\0_C_Project\01 分支和循环\Release\01 选择结构.exe (进程 39324)已退出，代码为 0。
```
#### 范例：密码程序
```bash
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	char password[20] = { 0 };
	printf("请输入密码：");
	scanf("%s", password);
	printf("请确认密码(Y/N)：");

	//清除缓存区
	//getchar();//得到\n:回车
	//getchar();执行一次只能获取一个字符

	//清理缓冲区的多个字符
	int tmp = 0;
	while ((tmp = getchar()) != '\n') //getchar函数得到的是字符，但是返回值是ASCII值等等，所以可以用整型变量获取
	{
		;//空操作
	}

	int ch = getchar();
	if (ch == 'Y')
	{
		printf("确认成功\n");
	}

	else
	{
		printf("确认失败\n");
	}

	return 0;
}
```
固定范围字符
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main07()
{
	int ch = 0;

	while ((ch = getchar()) != EOF)
	{
		if (ch < '0' || ch >'9')//这里为字符0和字符9
		{
			continue;
		}
		putchar(ch);
	}
}
```
### 猜数字游戏
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

//写一个猜数字游戏
//1.自动产生一个1-100之间的数字
//2.猜数字
//	a.猜对了，游戏结束
//	b.猜错了，会告诉猜大了，还是猜小了，继续猜，直到猜对
//3.游戏可以一直玩，除非退出游戏
void meun()
{
	printf(" ************************ \n");
	printf("**************************\n");
	printf("******  猜数字游戏  ******\n");
	printf("****     1.开始      *****\n");
	printf("****     0.结束      *****\n");
	printf("**************************\n");
	printf(" ************************ \n");
}


void Game()
{
	//srand((unsigned int)time(NULL));//一个程序设置一次随机数种子函数就足够了，这里重复使用
	int ret = rand() & 100 + 1;//定义随机数，生成随机数的范围为0~32767,取模
	int guess = 0;
	while (1)
	{
		printf("请猜数字：");//输入猜测的数字
		scanf("%d", &guess);
		if (guess > ret)//判断比较
		{
			printf("猜大了\n");
		}
		else if (guess < ret)
		{
			printf("猜小了\n");
		}
		else
		{
			printf(" *         *\n");
			printf("* *       * *\n");
			printf("恭喜你猜对了！\n");
			break;//退出循环
		}
	}
}

int main()
{
	srand((unsigned int)time(NULL));//时间 - 时间戳
	int input = 0;
	do
	{
		meun();//显示菜单

		printf("请选择:>");
		scanf("%d", &input);

		switch (input)//输入选择
		{
		case 1:
			printf("<游戏开始>\n");
			Game();
			break;
		case 0:
			printf("<游戏结束>\n");
			break;
		default:
			printf("<输错了，请重新输入！>\n");
		}
	} while (input); //只要input不为0,程序继续执行

	return 0;
}
```
### 关机程序
```c
#include<stdlib.h>
#include<string.h>

int main()
{
	//关机
	//c语言提供了一个函数:system() -执行系统命令的
	char input[20] = { 0 }; //存放输入的信息
	system("shutdown -s -t 60");
again:
	printf("请注意，你的电脑将在1分钟内关机，如果输入：我爱玩原神，就取消关机\n");
	scanf("%s", input);
	if (strcmp(input, "我爱玩原神") == 0)
	{
		system("shutdown -a");
	}
	else
	{
		goto again;
	}
	return 0;
}
```
### 二分值法
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

//在一个有序数组中查找具体的某个数字n。
//算法：二分值法
int main()
{

	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int k = 7;//要查找的数字
	//在arr这个有序的数组中查找k对应的值
	int len = sizeof(arr) / sizeof(arr[0]);

	int left = 0;
	int right = len - 1;

	while (left <= right)
	{
		int mid = left + right;

		if (arr[mid] < k)
		{
			left = mid + 1;
		}

		else if (arr[mid] > k)
		{
			right = mid - 1;
		}
		
		else
		{
			printf("要查找的值对应数组中的下标[%d]\n", mid);
			break;
		}
	}
	if (left > right)
	{
		printf("数组中没有待查找的值");
	}
	return 0;
}
//当查找的范围在 6 ~ 7时，下标为5和6 ， 5+6/2 = 5 ，此时left +1 , mid = 6+6/2 =6 ，成功找到了7对应的下标
```
### 字符汇聚
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>
#include<string.h>
#include<Windows.h>
int main()
{
	char arr1[] = "Welcome to bit!!!!!!";
	char arr2[] = "####################";
	int left = 0;
	int right = strlen(arr1) - 1;

	for (;left <= right; left++, right--)
	{
		arr2[left] = arr1[left];
		arr2[right] = arr1[right];
		printf("%s\n", arr2);
		Sleep(1000);//休眠一秒
		system("cls");//清空屏幕
	}


	return 0;
}
```
### 密码验证程序
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>
#include<string.h>//strlen strcmp
int main()
{
	char password[20] = {0};//定义字符串 ， 假设密码为123456

	int i = 0;

	for (i = 0; i < 3; i++)//限制三次循环
	{
		printf("请输入密码:>");
		scanf("%s", password);//数组名本身就是地址
		//if(password == "123456") //字符串不能用判断操作符
		//if (strcmp(password, "123456")) //错误示例，if内要写条件“判断”，不然会直接执行！
		if ((strcmp(password, "123456")) == 0)//strcmp,依次比较ascii码值
		{
			printf("密码正确\n");
			break;
		}
		else
		{
			printf("密码错误\n");
		}
	}
	//printf("连续三次输入错误密码，程序退出..."); 直接写这一句，不正确，会导致输入正确密码后，跳出循环，也打印这句内容
	if (i == 3)
	{
		printf("连续三次输入错误密码，程序退出...\n");
	}
	return 0;
}
```
### 冒泡排序
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	
	int a = 5, b = 1, c = 9;
	int arr[3] = { a,b,c };
	int i, j = 0;

	for (i = 0; i < 3; i++)
	{
		scanf("%d", &arr[i]);
	}

	printf("原始数组为:");

	for (i = 0; i < 3; i++)
	{
		printf("%d ", arr[i]);
	}

	int len = sizeof(arr) / sizeof(arr[0]);
	int temp = 0;

	// 改变 a,b,c的值不能直接改变arr中元素的值,实际上在初始定义arr时将a,b,c的值传入了arr而不是变量本身

	for (i = 0; i < len - 1; i++)
	{
		for (j = 0; j < len - i - 1; j++)
		{
			if (arr[j] < arr[j + 1])
			{
				temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}

	printf("从高到低排序：");
	for (i = 0; i < len; i++)
	{
		printf("%d  ", arr[i]);
	}

	return 0;
}
```
### 求最大公约数
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

int main()
{
	int m = 0;
	int n = 0;
	scanf("%d %d", &m, &n);//24 18
	//如果两个数分别为24和18，最大公约数只能在18及以下
	int min = 0;//判断两个数谁更小
	if (m > n)
	{
		min = n;
	}
	else if (m < n)
	{
		min = m;
	}

	else
		min = m;
	int i = 0;

	//方法一
	//int maxgy = 0;//最大公约数
	//for (i = 1; i <= min; i++)
	//{
	//	if (m % i || n % i == 0)
	//	{
	//		maxgy = i;
	//	}
	//}

	////方法二
	//while (1)
	//{
	//	if (m % min == 0 && n % min == 0)
	//	{
	//		printf("最大公约数是：%d\n", min);
	//	}
	//	min--;
	//}

	//辗转相除法
	int t = 0;
	while (t = m % n)
	{
		//t = m % n;
		m = n;
		n = t;
	}
	printf("最大公约数是：%d\n", n);
	return 0;
}
```
### 闰年判断程序
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

//判断 1000~2000年 之间哪些年份是闰年

int main()
{
	int y, count = 0;
	for (y = 1000; y <= 2000; y++)
	{
		if ((y % 100 != 0 && y % 4 == 0) || (y % 400 == 0)) //y % 100 == n  n不是非零即1 n是任意整数
			//y % 100 == 0 & y % 400 == 0
			//y % 400 = 0 更简洁
		{
			printf("闰年为：%d年\n", y);
			count++;
		}
	}
	printf("闰年个数为：%d", count);
	return 0;
}
```
### 素数判断程序
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>

// 写一个代码, 打印100~200之间的素数
//素数-质数
//只能被1和他本身整除

//代码优化
//执行次数更少

int main()
{
	int i, j = 0;
	for (i = 100; i <= 200; i++)
	{

		for (j = 2; j < i; j++)
		{
			if (i % j == 0)
			{
				break;
			}
		}
		if (j == i)//如果i是素数,j会一直自加一直到等于i
		{
			printf("%d为素数\n", i);
		}
	}
	return 0;
}
```
```c
#define _CRT_SECURE_NO_WARNINGS 1
#include<stdio.h>
#include<math.h>

//写一个代码,打印100~200之间的素数
//素数-质数
//只能被1和他本身整除

//代码优化1：
//m=a*b;
//a和b中一定至少有一个数字是 <=开平方m的
//16 = 2*8 = 4*4
//所以，大于开平方m的就不需要判断是否为m的因子，减少循环执行次数

//sqrt用于计算开平方的函数 -需要用到库函数 math.h
//减少了循环的执行次数

//代码优化2：
//偶数不可能是素数
//修改for (i = 100; i <= 200; i ++)为for (i = 101; i <= 200; i += 2)

int main()
{
	int i, j = 0;

	//判断i是不是质数
	for (i = 101; i <= 200; i += 2)
	{
		int flag = 1;//定义一个参数，检测i是否能被 除了1和它本身的数 整除

		for (j = 2; j <= sqrt(i); j++)
		{
			if (i % j == 0)
			{
				flag = 0;//如果能被2到i-1之间的整除，记录flag=0;
				//break;
			}
		}

		if (flag == 1)//不能被2到i-1之间的数整除
		{
			printf("%d是质数\n", i);//那么i就是质数
		}
	}
	return 0;
}
```
