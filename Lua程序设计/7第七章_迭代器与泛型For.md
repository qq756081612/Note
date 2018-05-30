##第七章 迭代器与泛型for
###1.迭代器与closure
- 迭代器是一种遍历一种集合中所有元素的机制
- 迭代器在两次成功调用之间需要保存一些状态，非常契合closure(闭合函数的特性)
- 一个Closure结构由两部分组成：Closure本身及为它提供“非局部的变量”的Factory函数  
- 泛型for是为迭代器而设计的他在内部保存了迭代器函数，在每次新迭代的时候调用迭代器，在迭代器返回nil的时候结束循环

``` lua
function values(t)	--Factory函数
	local i = 0
	retrun function()	--Closure函数
		i = i + 1
		return t[i]
	end
end
```
###2.泛型for的语义
- 泛型For自身可以保存状态 以节省创建Closure的开销
- `for 控制变量,... in 迭代器函数（恒定状态）do 循环事件 end`
- for所做的第一件事是对in后面的表达式求值，依次返回迭代器函数、恒定状态和控制变量的初值

###3.无状态的迭代器
- 依靠泛型for的语义迭代器就能不再创建Closure,变为无状态的迭代器，而由for去保存中间状态
- 迭代器函数的作用是返回三个参数，故也可使用直接传入三个参数的写法   
``` lua
for k,v in next,t do --省略了控制变量nil
	print(v) 
end

--这种写法等价于
for k,v in pairs(t) do --pairs是调用next函数实现的
	print(v) 
end
```