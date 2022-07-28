本文主要阐述对于结构体初始化，使用默认构造函数和自定义构造函数有什么区别。

## 使用默认构造函数

使用默认构造函数的好处在于可以不经初始化就定义结构体变量，下面给出实例：

```cpp
#include <stdio.h>
//使用默认构造函数 
struct student {
	int id;
	char gender;
        student(){} //默认构造函数一般不可见，此处专门写出
}pig;  //能不经初始化就定义变量 

int main(){
	pig = {23,'F'};//使用该语句必须整体赋值，不能单独赋值
	printf("pig ID = %d\npig Gender = %c",pig.id,pig.gender);
	return 0;
}
```

虽然默认构造函数能不经初始化就定义变量，但是赋值的时候就有局限性，要么就通过上面的代码来对所有的结构体变量一起赋值，但是不能够单独赋值；要么逐一赋值，如下所示：

```c
pig.id = 23;
pig.gender = 'F'
```

但是这样当变量很多的时候就不方便，所以有了自定义构造函数。

## 使用自定义构造函数

使用自定义构造函数就能够单独初始化某些变量，而不需要全部变量必须整体赋值。实例如下

```cpp
#include <stdio.h>
//使用自定义构造函数 
struct student {
	int id;
	char gender;

	//自定义构造函数 
	//可以同时初始化id和gender 
	student(int _id, char _gender) : id(_id), gender(_gender){} 
	//也可以单独初始化gender
	student(char _gender) : gender(_gender){} 
};  //不能不经初始化就定义变量 

int main(){
	student pig = student(23,'F');//定义变量，同时赋值
	student Pig = student('M'); //定义变量，单独赋值 
	printf("pig ID = %d\npig Gender = %c\n\n",pig.id,pig.gender);
	printf("Pig ID = %d\nPig Gender = %c",Pig.id,Pig.gender);
	return 0;
}
```

不过仅仅使用自定义构造函数仍旧有着不足之处，一旦自定义构造函数了，那么默认不可见的构造函数就被覆盖了，所以定义结构体变量的时候必须对其初始化才行，没有使用默认函数那么方便，所以！！！就有了两者一起使用的方法。

## 同时使用默认构造函数和自定义构造函数

同时使用默认构造函数和自定义构造函数既能够不初始化就可以定义结构体变量，也可以单独对于某些结构体变量进行赋值，是最佳的选择，实例如下：

```cpp
#include <stdio.h>
//同时用默认构造函数和自定义构造函数 
struct student {
	int id;
	char gender;
	student(){};  //显示默认构造函数 
	
	//自定义构造函数 
	//可以同时初始化id和gender 
	student(int _id, char _gender) : id(_id), gender(_gender){} 
	//也可以单独初始化gender
	student(char _gender) : gender(_gender){} 
}pig,Pig;  //能不经初始化就定义变量 

int main(){
	pig = student(23,'F');//直接使用构造函数，同时赋值
	Pig = student('M'); //直接使用构造函数，单独赋值 
	printf("pig ID = %d\npig Gender = %c\n\n",pig.id,pig.gender);
	printf("Pig ID = %d\nPig Gender = %c",Pig.id,Pig.gender);
	return 0;
}
```


文章出处:[C++ 结构体的构造函数使用 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/392077524)

*2022-07-28 周四*