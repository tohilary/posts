#CoffeeScript学习笔记-3
- date: 2012-7-23
- tags: coffeescript

---

##in与of
`in`可以检查对象是否在数组中。
```coffeescript
coffee> a=[0..9]
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
coffee> 5 in a
true
```

`of`可以检查对象是否在字典中。
```coffeescript
coffee> a={'name':'whtsky'}
{ name: 'whtsky' }
coffee> 'name' of a
true
```

##迭代
迭代字典使用`for key, value of dict`语句进行迭代。注意是**of**
```coffeescript
a = 
	'name': 'whtsky'
	'website': 'http://whouz.com'

for k, v of a
	console.log k
	console.log v
```

OUTPUT:
```
name
whtsky
website
http://whouz.com
```

迭代数组使用`for value in array`。注意是**in**（真他喵的怀念Python里in统治天下的日子..）
```coffeescript
a = [0..9]

for x in a
	console.log x
```

OUTPUT:
```
0
1
2
3
4
5
6
7
8
9
```

迭代数组的`for in`支持`by`修饰符来定义迭代的间隔
```coffeescript
a = [0..9]

for x in a by 3
	console.log x
```

OUTPUT:
```
0
3
6
9
```

`by`可以很强大的支持分数：
```coffeescript
for x in [1/3..3] by 1/3
    console.log x
```

OUTPUT:
```
0.3333333333333333
0.6666666666666666
1
1.3333333333333333
1.6666666666666665
1.9999999999999998
2.333333333333333
2.6666666666666665
3
```

(貌似在用by 分数的时候只支持[start..end]这种数字数组.而且start和end必须都是by的那个分数的倍数，否则会出现不少undefined...)

负数也可以：
```coffeescript
a = [0..9]

for x in [6..0] by -2
	console.log x

```

OUTPUT:
```
6
4
2
0
```

(貌似在用by 负数的时候只支持[start..end]这种数字数组.而且start必须要大于end，否则会不断循环undefined...)


(总之负数和分数其实**意义都不大**...)

无论是`for of`还是`for in`都支持使用`when`进行过滤。
```coffeescript
a = [0..9]

for x in a when x % 2 is 0
	console.log x

b = 
	'cat': 'miao'
	'dog': 'wang'

for k, v of b when k is 'cat'
	console.log v

```

OUTPUT:
```
0
2
4
6
8
miao
```

使用for own`可以只迭代对象本身的属性（而不是共享/继承的属性）

##循环
基本的`while`与`until`循环：
```coffeescript
count = 0

miao = ->
	console.log 'miao'
	count += 1


wang = ->
	console.log 'wang'
	count -= 1


console.log 'while:'
miao() while count < 10

console.log ''
console.log 'until:'
wang() until count < 5

```

OUTPUT:
```
while:
miao
miao
miao
miao
miao
miao
miao
miao
miao
miao

until:
wang
wang
wang
wang
wang
wang
```

##列表解析
和Python不同，CoffeeScript中的列表解析包裹在**括号**中
```coffeescript
a = [0..9]

console.log (x*x for x in a)
```

OUTPUT:
```
[ 0, 1, 4, 9, 16, 25, 36, 49, 64, 81 ]
```

列表解析的时候依旧可以使用by
```coffeescript
a = [0..9]

console.log (x for x in a by 2)
```

OUTPUT:
```
[ 0, 2, 4, 6, 8 ]
```

甚至`while`都可以用到列表解析里面
```coffeescript
a = [0..9]
b = ->
	a.pop()

console.log (x while x = b())
```

OUTPUT:
```
[ 9, 8, 7, 6, 5, 4, 3, 2, 1 ]
```

##解构赋值
Python中的解构赋值是这样的：
```python
a, b = b, a
```
CoffeeScript中的则是这样的：
```coffeescript
[a, b] = [b, a]
```
恩，对，可以用解构赋值**交换变量的值**。

CoffeeScript中的解构赋值还可以使用Splat
```coffeescript
coffee> [a, b...] = [0..9]
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
coffee> a
0
coffee> b
[ 1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9 ]
```

而且还支持字典模式：
```coffeescript
a = 
	x: 1
	y: 2

{x: a, y: b} = a
console.log a
console.log b
```

OUTPUT:
```
1
2
```

而且数组模式和字典模式还能互相嵌套，比如这段代码
```coffeescript
{l: [a, b...]} = c
```
会把c里面的l取出来赋值给a, b...

