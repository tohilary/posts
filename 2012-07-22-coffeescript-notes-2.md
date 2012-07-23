#CoffeeScript学习笔记-2
- date: 2012-7-21
- tags: coffeescript

-----

##上下文
补一句，`=>`这种胖箭头可以确保函数是在当前上下文中执行。

##Splat
好吧，我真不知道这东西中文名应该叫什么..
CoffeeScript中很强大的一个东西，足以秒杀Python中的`*args`
Splat是函数参数列表中的三个点`...`，可以接受任意长度的参数。
直接上代码吧：
```coffeescript
func_a = (args...) ->
	console.log args

func_b = (a, args...) ->
	console.log args

func_c = (args..., b) ->
	console.log args

func_d = (a, args..., b) ->
	console.log args

func_a 1,2,3,4
func_b 1,2,3,4
func_c 1,2,3,4
func_d 1,2,3,4
```

OUTPUT:
```
[ 1, 2, 3, 4 ]
[ 2, 3, 4 ]
[ 1, 2, 3 ]
[ 2, 3 ]
```

#数组与字典
CoffeeScript中可以用换行来隔开各个元素：
```coffeescript
a = [
	1
	2
	3
	4
	5
]
b = 
    name: 'whtsky'
    blog: 'http://whouz.com'
```
CoffeeScript能神奇的自动判断出你要定义一个字典：
```coffeescript
a = (arg) -> console.log arg

a 'name': 'whtsky' 
```

OUTPUT:
```
{ name: 'whtsky' }
```

CoffeeScript中，如果字典中的k=v，只要给出k就可以了
```coffeescript
f = {'whtsky'}
    
console.log f
```

OUTPUT:
```
{ whtsky: 'whtsky' }
```

调用字典对象时，用点号和方括号都可以。`dict.key`与`dict[key]`是等价的.

CoffeeScript中的切分方法和Ruby一样，三个点表示前开后闭，两个点表示前开后开；~~不支持像Python中负数那样的从后往前的切分方式~~。字符串也可以被切分。
```coffeescript
coffee> [0...9]
[ 0,
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8 ]
coffee> [0..9]
[ 0,
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9 ]
coffee> ints = [0..5]
[ 0,
  1,
  2,
  3,
  4,
  5 ]
coffee> ints[0..2]
[ 0, 1, 2 ]
coffee> 'I love cats'[0..5]
'I love'
coffee> 'I love cats'[-4..-1]
'cats'
```

##?-存在操作符
`?`是存在操作符.只有在对象不存在（值为null或undefined）时才会返回false.
```coffeescript
coffee> a=null
null
coffee> a?
false
coffee> a=0
0
coffee> a?
true
coffee> a=false
false
coffee> a?
true
```
`members?['whtsky']?.miao()`这段代码中，只要members或members['whtsky']不存在就不会执行（但也不会报错），若存在则正常执行.

