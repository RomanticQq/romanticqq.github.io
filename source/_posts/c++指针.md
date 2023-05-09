---
title: C++指针
tags: C++
categories: C++
abbrlink: 1390
date: 2023-03-02 20:23:46
---

1. 指针的定义

   ```c++
   int a=10;
   int* p;//定义一个指针
   p = &a;//p的值是一个地址,可以通过*把p位置的值取到，即*p(*p是一个数值，p是地址)
   ```

2. 指针所占内存空间

   指针所占用内存空间是固定的，所有指针类型在32位操作系统下是4个字节，在64位操作系统下是8个字节；

3. 空指针和野指针
   - 空指针指向内存中编号为0的空间；
   - 野指针指向非法的内存空间；
   - 空指针和野指针指向的内存空间都是不可访问的；

4. const修饰指针

   ```c++
   int a=10;
   const int* p;//此时*p是常量，且*p是数值，若写*p=a就会报错，p=&a正常；
   int* const p;//此时p的常量，且p的值是地址，若写p=&a就会报错，*p=a正常；
   const int* const p;//地址和值都不可修改
   ```

5. 指针和数组

   ```c++
   #include<iostream>
   using namespace std;
   //参数1 数组的首地址；参数2 数组的长度
   //void sortt(int arr[], int len)
   //void sortt(int* arr, int len)
   //这是两种不同的写法，都可以，传的都是地址
   void sortt(int arr[], int len)
   {
   	cout << arr << endl;
   	cout << arr[0] << endl;
   }
   int main()
   {
   	int arr[] = { 1,3,5,2,4 };
   	int len = 5;
   	sortt(arr, len);//数组名就是数组的首地址
   	for (int j = 0; j < len; j++)
   		cout << arr[j] << endl;
   	return 0;
   }
   ```

   ```c++
   #include<iostream>
   using namespace std;
   //参数1 数组的首地址；参数2 数组的长度
   void sortt(int* arr, int len)
   {
   	cout << *arr << endl;//1，对首地址进行解析
   	cout << arr << endl;//0000007E2EF2FB28，传过来的是地址
   	//[]前面必须紧跟着一个地址或者一个字母(这个字母用于简化这个地址)
   	cout << arr[2] << endl;//5，可以这样直接取，原因上一行
   }
   int main()
   {
   	int arr[] = {1,3,5,2,4};
   	int len = 5;
   	sortt(arr, len);//数组名就是数组的首地址
   	return 0;
   }
   ```


6. 利用指针进行数组遍历

   ```c++
   #include<iostream>
   using namespace std;
   int main()
   {
   	int arr[] = { 1,2,3,4,5 };
   	int* p = arr;
   	for (int i = 0; i < 5; i++)
   	{
   		cout << *p << endl;
   		p++;
   	}
   	return 0;
   }
   ```

7. 数组指针和指针数组

   ```c++
   #include<iostream>
   using namespace std;
   int main()
   {
   	int a[] = { 1,2,3 };
   	int b[] = { 4,5,6 };
   	int c[] = { 7,8,9 };
   	int* arr[] = { a,b,c }; //这时a,b,c存放在arr里面的都是地址
   	cout << arr[0] << endl;
   	for (int i = 0; i < 3; i++)
   	{
   		for (int j = 0; j < 3; j++)
   		{	
   			//对于一维数组来说，arr[i]取到的是值，对于二维数组来说arr[i]取到的是地址；
               //对于指针数组来说，它是开辟了新的地址，在新地址中把原来的地址存下来了
   			cout << arr[i] + j << endl;//输出地址
   			//下面两行输出的都是数值，可以对数组进行取值，这两种方法都可以
   			cout << *(arr[i]+j) << endl;
   			cout << arr[i][j] << endl;
   		}
   	}
   	return 0;
   }
   ```

   
