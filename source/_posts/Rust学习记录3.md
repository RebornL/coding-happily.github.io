---
title: Rust学习记录3
date: 2016-03-23 20:26:37
categories: 学习记录
tags: Rust
---

(前话，博主怎么也没想到Rust语言，接着学下去，会这么的困恼，感觉又回到c语言的指针的时代，而且比c语言的指针感觉更加复杂，弄了三个特奇葩的概念---所有权，借用和引用，生命周期等等概念，搞得晕乎乎，难怪这是一门系统级的编程语言，要了解好引用借用等概念，才能用它来写程序，要是用错了&，<>等这些符号，真容易造成内存方面的各种bug，所以此次，我也只能简单的做记录，不敢随意乱写。等以后，有更大的兴趣的时候，再重新研读一下，原谅博主太过懒惰了！！！)

<!--more-->
```Rust
fn main() {
	//之前这种麻烦的方式
	// fn foo(v1: Vec<i32>, v2: Vec<i32>) -> (Vec<i32>, Vec<i32>, i32) {
		// do stuff with v1 and v2

		// hand back ownership, and the result of our function
		// (v1, v2, 42)
	// }

	// let v1 = vec![1, 2, 3];
	// let v2 = vec![1, 2, 3];
	//可以看得出这种方式很麻烦！
	// let (v1, v2, answer) = foo(v1, v2);
	
	//第一种引用，&Vec<i32>
	//	 &T	类型为一个”引用“，而与其拥有这个资源，它借用了所有权
	// fn foo(v1: &Vec<i32>, v2: &Vec<i32>) -> i32 {
		//return the answer
		// 42
	// }
	let v1 = vec![1, 2, 3];
	let v2 = vec![1, 2, 3];
	let answer = foo(&v1, &v2);//这样之后，v1和v2还是能够调用
	//引用的是不可改变的
	
	//第二种引用的类型，&mut,允许改变你所引用的类型
	let mut x = 5;
	{
		let y = &mut x;
		*y += 1;
	}
	println!("{}",x);
	
	//作用域的问题
	//迭代器失效
	let mut v = vec![1,2,3];
	for i in &v {
		println!("{}",i);
		v.push(4);//这个会出错，因为v已经被借用出去了
	}
	//释放后使用
	let y : i32;
	{
		let x = 5;
		y = &x;//这样也是不行的，当被引用的变量放在比引用变量的变量之前，也是会出错的
	}
	println!("{}",y);//这个会出错，因为x已经不存在了，无法引用x的值
	
	//生命周期
	//(写的函数应该放在main函数之外，为了便于写笔记，放在了main里面)
	fn bar<'a, 'b>(x: &'a i32,y: &'b i32) {
		//..具体的例子见第一篇连接地址中的讲解
	}
	
	//关于生命周期和作用域需要各位去认真读文档了，博主自己读得是懂非懂，不敢随便分享
	
	//可变性
	//使用mut
	let mut x = 5;
	x = 6;//定义了mut的绑定变量就可以改变自己的值
	//可变引用
	let mut x = 5;
	let y = &mut x;
	
	//两者都可变
	let mut x = 5;
	let mut y = &mut x;//这样y就可以随便改变绑定的值
	
	//结构体
	struct Point {
		x: i32,
		y: i32,
	}
	//更新语法
	struct Point3d {
		x: i32,
		y: i32,
		z: i32,
	}
	let mut ponit = Point3d { x: 0,y: 0,z: 0};
	point = Point3d { y: 1, ..point}//更新了y，保留原来的x和z
	
}

```



<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=26524326&auto=1&height=66"></iframe>