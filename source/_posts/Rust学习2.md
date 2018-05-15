---
title: Rust学习记录2
date: 2016-03-20 22:22:24
categories: 学习记录
tags: Rust
---
[Rust学习记录1](http://qingxiao.site/2016/03/19/Rust%E5%AD%A6%E4%B9%A01/)

<!-- more -->
```rust
fn main() {
	//条件语句
	let x = 5;
	if x == 5 {
		println!("x is five!");
	} else if x == 6 {
		println!("x is six!");
	} else {
		println!("x is not five or six!");
	}
	//you can do in this way
	let y = if x == 5{
		10
	} else {
		15
	};
	
	//循环（loop,while,for）
	//无线loop，其实相当于while true
	loop {
		println!("this is loop");
		//break;//可以打断循环
	}
	//while
	let mut x1 = 5;
	let mut done = false;
	while !done {
		x1 += x1 - 2;//x1每次跟自己小2的数相加
		
		println!("{}",x1);//相加完的结果打印出来
		
		if x1%5 == 0 {
			done = true;//当遇到x1是5的倍数时，退出while循环
		}
		
	}
	//for循环,抽象形式
	// for var in expression {
	//		code
	//}
	for x in 0..10 {
		println!("{}",x);
	}
	//Enumerate方法，记录你循环多少次
	//on range
	for (index,value) in (5..10).enumerate() {
		println!("index is {} and value is {}",index,value);
	}
	//对迭代器（on iterators）
	let lines = "Hello\nWorld".lines();
	for (linenumber,line) in lines.enumerate() {
		println!("linenumber {} : {}",linenumber,line);
	}
	//循环标签
	'outer: for i in 0..10 {
		'inter: for j in 0..10 {
			if i % 2 == 0 {
				continue 'outer;//直接跳到下一个外循环
			}
			if j%2 == 0 {
				continue 'inter;//直接跳到下一个内循环
			}
			
			println!("i : {}, j : {}",i,j);
			
		}
	}
	
	//移动语义(Rust 确保了对于任何给定的资源都正好（只）有一个绑定与之对应。)
	let v = vec![1,2,3];
	let v2 = v;//这样之后，v就不能在被调用了,这应该是所有权转移
	//fn take(x: Vec<i32>){
	//	...
	//}
	//take(v);vector参量传递，这个函数取得了这个变量所有权，导致v变量无法再使用
	
	let integer = 1;
	let integer2 = integer;//这样只是复制而已，就像C语言中指针跟定义的普通变量的那样
	//官方解释：这是因为i32并没有指向其它数据的指针，对它的拷贝是一个完整的拷贝。所有基本类型都实现了Copy trait
	
	//返还所有权
	fn foo(v: Vec<i32>) -> Vec<i32> {
		// do stuff with v

		// hand back ownership
		v
	}
	fn foo(v1: Vec<i32>, v2: Vec<i32>) -> (Vec<i32>, Vec<i32>, i32) {
		// do stuff with v1 and v2

		// hand back ownership, and the result of our function
		(v1, v2, 42)
	}

	let v1 = vec![1, 2, 3];
	let v2 = vec![1, 2, 3];
	//可以看得出这种方式很麻烦！
	let (v1, v2, answer) = foo(v1, v2);
	
	
}

//所有权  （这个给我的感觉更像是作用域的范围）
fn foo() {
	let v = vec![1,2,3];
	//当v进入作用域，一个新的Vec<T>被创建，向量（vector）也在堆上为它的3个元素分配了空间。当v在foo()的末尾离开作用域，Rust将会清理掉与向量（vector）相关的一切，甚至是堆上分配的内存。这在作用域的结尾是一定（deterministically）会发生的。
}
```


<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=26524326&auto=1&height=66"></iframe>