#CoffeeScript学习笔记-1
- date: 2012-7-21
- tags: coffeescript
-----

基本上是给自己写的，所以会省略不少东西。
想要靠这玩意自学CoffeeScript的请慎重，被我带沟里了我不负一切责任。

##安装
`npm install -g coffee-script`
加上`-g`会自动把这东西安成全局的。不加的话就会存到`./node_module`里面。

在OS X下，需要把`export PATH=/usr/local/bin:$PATH` 加到 `~/.profile`里面。

##基本操作
直接运行：`coffee filename`
查看编译后的js：`coffee -p filename`
编译：`coffee -c filename`
目录编译：`coffee -co input output`
目录监听编译：`coffee -cwo input output`

##函数与字符串插值
CoffeeScript使用`->`或`=>`来定义函数。用缩进来区分函数/条件分支什么的。
和Ruby相同，在有参数的情况下函数调用的括号可以省略；但是在没参数的情况下必须有括号，否则会返回函数对象。
字符串插值的方法和Ruby一样，都是`#{var}`
```coffeescript
hello = ->
	"hello!"

console.log hello

console.log hello()

hello_2 = (name) ->
	"hello " + name

console.log hello_2 "coffee"

hello_3 = (name)->
	"hello #{name}"

console.log hello_3 "World"
```

OUTPUT:
```
[Function]
hello!
hello coffee
hello World
```

`+`号前后的空格不能被省略.

在函数调用中，可以用`arguments`数组来调用收到的所有参数。
```coffeescript
f = -> "hello,#{arguments[0]}"

console.log f "arguments"
```

OUTPUT:
```
hello,arguments
```

##表达式
+-*/不谈。
and/or = &&/||
`is`和`==`会被编译成JavaScript中的`===`，`!=`会被编译成`!===`。
要注意没有`is not`这种用法，在目前的版本中(1.3.3)，`is not`会被编译成`=== !`。
`unless`，这个应该都懂..
```coffeescript
f = -> arguments[0] == arguments[1] and arguments[1] != arguments[2] and arguments[2] is arguments[3]
```

```javascript
$ coffee -p hello.coffee 
(function() {
  var f;

  f = function() {
	return arguments[0] === arguments[1] && arguments[1] !== arguments[2] && arguments[2] === arguments[3];
  };

}).call(this);
```

`%`能够自动把字符串转换为数字。
```coffeescript
odd = (int) -> int % 2 is 1

console.log odd '3'
console.log odd '4'
```

OUTPUT:
```
true
false
```

##异常
使用`throw`来抛出异常，用`try...catch...`来捕获异常。
```coffeescript
check = (name) ->
	if name != 'whtsky'
		throw "out!"
	else
		console.log "welcome."

try
	check 'Moon'
catch e
	console.log e

check 'whtsky'
check 'Moon'
```

OUTPUT:
```
out!
welcome.
ERROR: out!
```

补一句，CoffeeScript支持后缀表达式，所以`check`可以写成这样：
```coffeescript
check = (name) ->
throw "out!" unless name is 'whtsky'
console.log "welcome."
```

##作用域
基本上同Python.
不过函数里改变全局变量不用声明`global`

##上下文
同JavaScript