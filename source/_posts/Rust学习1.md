---
title: Rust学习记录1
date: 2016-03-19 20:42:30
categories: 学习记录
tags: Rust
---

Rust介绍：详情点击[查看](https://www.wikiwand.com/zh-cn/Rust),[官方网站](https://www.rust-lang.org/)


看了晚上那么多文章，对这种语言感到了兴趣，于是在网上找到了一些[官方的教程](https://kaisery.gitbooks.io/rust-book-chinese/content/)进行了解学习！
<!-- more -->

以下是我做的简单笔记：
```Rust
fn main() {
    //println!("Hello, world!");
	//变量绑定
	let x = 5;
	
	//模式pattern
	let (x1,y1) = (1,2);
	
	//类型注释，在变量后用":类型"
	//不过rust自带类型推断的功能
	let y2: i32 = 5;//i32-->32位有符号整数，u32-->无符号
	
	//immutable，绑定默认不可变
	let x2 = 5;
	x2 = 10;//这样编译会不通过
	//编译结果：
	/* error: re-assignment of immutable variable `x`
		x = 10;
		^~~~~~~
	*/
	
	//使用mut，使绑定可变
	let mut x3 = 5;
	x3 = 10;//这个编译可以通过
	
	//初始化绑定
	let x4: i32;
	println!("x4 is {}",x4);//编译时会提示不允许使用未初始化的变量
	
	//作用域和隐藏(scope and shadowing)
	let x5: i32 = 7;
	{//y的作用域仅在这个大括号内
		let y: i32 = 11;
		println!("x5 is {} and y is {}.",x5,y);
	}
	println!("x5 is {} and y is {}.",x5,y);//不起作用，会报错
	{//变量隐藏
		println!("x5 is {}",x5);//7
		let x5 = 12;
		println!("x5 is {}",x5);//12
	}
	println!("x5 is {}",x5);//7
	let x5 = 15;//这也是一种隐藏
	println!("x5 is {}",x5);//15
	
	//可变绑定和隐藏
	let mut x6 = 5;
	x6 = 6;//这是可变的
	let x6 = x6;//x6现在变成不可变的
	let y6 = 5;
	let y6 = "This is shadowing!";//这是隐藏的做法
	
	//使用函数
	print_num(5);	
	print_num(5,6);
	
	//表达式和语句
	//rust赋值的值是一个空的元组()
	let mut y7 = 6;
	let x7 = (y7 = 8);//x7 has the value "()",not the "6"
	
	//函数指针
	let x8: fn(i32) -> i32 = plus_one;
	let y8 = plus_one;
	let six = x8(5);//y8(5)
	
	//原生类型
	//布尔型（bool）
	let x9 = true;
	let y9: bool = false;
	
	//char Unicode字符 '' 4个字节
	let c = 'x';
	let kong = '';
	
	//数字类型
	//详见：https://kaisery.gitbooks.io/rust-book-chinese/content/content/Primitive%20Types%20%E5%8E%9F%E7%94%9F%E7%B1%BB%E5%9E%8B.html
	
	//数组
	let a = [1, 2, 3]; // a: [i32; 3] 不可变 let a = [1:4]
	let mut m = [1, 2, 3]; // m: [i32; 3] 可变
	//数组长度
	a.len();
	//下标访问
	m[0];//1
	
	//切片语法
	let arr = [0, 1, 2, 3, 4];
	//&作用类似于引用
	let complete = &arr[..]; // A slice containing all of the elements in a
	let middle = &arr[1..4]; // A slice of a: just the elements 1, 2, and 3
	
	//str
	//Rust的str类型是最原始的字符串类型。作为一个不定长类型，它本身并不是非常有用，不过当它用在引用后是就有用了，例如&str。
	
	//元组(Tuples)
	let tu = (1,"hello");
	let mut tu2 = (1,3);
	//一个逗号消除单元素和括号中的值的区别
	(0,); // single-element tuple
	(0); // zero in parentheses
	//元组索引
	let tu3 = (0,1,2,3,4,5);
	let one = tu3.0
	
}

//函数,函数必须声明参数类型
fn print_num(x: i32) {
	println!("x is {}",x);
}

fn print_sum(x: i32,y: i32) {
	println!("x +y = {}",x+y)
}
//rust只能返回一个值,"->"返回声明的类型
fn add_one(x: i32) -> i32{
	//没有分号
	x+1
}

//提早返回（Early returns）
fn  foo(x: i32) -> i32 {
	return x+1;
	//以下这一句不会执行
	x+1
}

//发散函数（Diverging functions），这类函数不返回
fn diverges() -> ! {
	panic!("this function never returns!");
	//panic!()导致当前的执行线程崩溃并返回指定信息
}

fn plus_one(i :i32) -> i32 {
	i+1
}
```


<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=26524326&auto=1&height=66"></iframe>