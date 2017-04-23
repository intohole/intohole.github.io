---
layout: post  
title: go语法   
city: 铁力   
tags: [lan]  
---

### 以下都为我现有基础知识面来说的 ###

Golang语法规则
---------------
+ go文件一般以.go结尾
+ 使用文件go编程方式：
	
```c
	
	go run go文件
	or
	go build go文件
	./go文件名
```

+ go文件基本格式
	
```c
		
		package main //可以为其它任意名称 ， main是表示程序主体，可运行代码
		import (
			//引用的包名
		) 
		//c 是一个struct或者其他类型体 ， 在函数体内可以引用
		//参数体，可以多个参数，使用...argv 
		//参数体，一般名称在前 ， 类型在后
		//返回值可以不选择 ， 相当于c语言的void
		func (c *XX) functionname(value int , name string //参数列表 )( return_value int )
		{
			//do somethring
		}
		func main(){
			//主函数体
		}
		
```

+ 基本语法
	+ 变量
		
```c
			
			var 变量名称 , 变量名称2... 类型 = 变量赋值1 , 变量赋值2 ,...
			or 
			变量名称1 := 变量值 // 程序会自动根据后面的类型，将变量名称转换成相应的类型 ， 并赋值
			
```
			
	+ 常量
		
```

			const 变量名称 变量类型 = 变量值

```
	
	+ 循环

```c
			
			for 条件判断 {
				
			}
			for {
			
			}
			for 变量声明 ; 条件判断 ; 循环操作 {

			}
```
	
	+ if/else(条件判断)
		
```c

			if 条件判断 {
			}
			or 
			if 程序操作1 ; ...;条件判断{
			}else if 条件判断 {
			}else{
			}
			
```

	+ switch(多条件)

```c
			
			switch 变量 {
				case 变量值:
					// do something
				case 变量值1：
					// do something
				default:
					// do something
			}		

```
	+ 数组

```ruby

			var 数组名称 [数组大小]类型 //初始化为0
			数组名称[数组位置] = 赋值 // 数组index从0开始
			数组名称 := [数组大小]类型{数值1,数值2,数值3,....}
			var 数组名称 [数组行数][数组列数]类型
			数组名称 := make([]类型 , 数组大小)
``` 
	+ 切片

```ruby
			数组名称[起始位置: 终结位置]
```
	+ map
```ruby
			字典名称 := make(map[key类型]value类型)
			字典名称 := make(map[key类型]value类型){key1 : value1 , key2 : value2}
			b: = make(map[string]int)
			b["a"] =  1
			delete(字典名称 , 删除的key) // delete(b , "a")
```

	+ range
```ruby

			for 数组值变量 , 数组index变量 := range 数组变量 {
				// do something
			}
			for 字典key , 字典value := range 字典变量 {
				//do something 
			}
```

参考
------------
+ [Go by Example](https://gobyexample.com/)
