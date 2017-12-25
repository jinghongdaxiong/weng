#php7的五大新特性
如果你使用的是基于composer和PSR-4的框架,这
种写法是否能成功的加载类文件?其实是可以的
,composer注册的自动加载方法是在类被调用的
时候根据类的命名空间去查找位置,这种写法对
其没有影响.

##1运算符(NULL)
把这个放在第一个说是因为我觉得它很有用.
用法:
$a = $GET['a'] ?? 1;
它相当于
<php
$a = isset($_GET['a']) ? $_GET['a'] : 1;
我们知道三元运算符是可以这样用:
$a ?: 1
但是这是建立在$a已经定义了的前提上.
新增的??可以简化判断.

##2函数返回值类型声明
官方文档提供的例子(注意...的边长参数
语法在PHP5.6以上的版本中才有):

<php
function arraysSum(array ...$arrays):array
{
    return array_map(function(array $array):int{
        return array_sum($array); 
    },$arrays);
}
从这个例子中可以看出现在函数(包括匿名函数)
都可以指定返回值的类型
这种声明的写法有些类似于swift:
func sayHello(personName: String) -> String
{
    let greeting = "Hello" + personName + "!"
    return greeting
}

这个特性可以帮助我们避免一些PHP的隐式
类型转换带来的问题.在定义一个函数之前
就想好预期的结果可以避免一些不必要的
错误.

不过这里也有一个特点需要注意.PHP7增加了
一个declare指令: strict_types,即使用严格
模式.

使用返回值类型声明时,如果没有声明为严格模式
,如果返回值不是预期的类型,PHP还是会对其进行
强制类型转换.但是如果是严格模式,则会发出一个
TypeError的Fatalerror.

强制模式
<php
function foo($a):int
{
    return $a;
}
foo(1.0);
以上代码可以正常执行,foo函数返回int 1,没有
任何错误.

严格模式
<php
declare(strict_types=1);

function foo($a):int
{
    return $a;
}
foo(1.0);
PHP Fatal error:  Uncaught TypeError: Return value of foo() must be of the type integer, float returned in test.php:6 
在声明之后,就会触发致命错误.
是不是有点类似与js的strict mode?

##标量类型声明
php7中的函数的形参类型声明可以是标量了.
在PHP5中只能是类名.接口 Array或者
callable(PHP5.4,即可以是函数,包括匿名函数)
,现在也可以使用String int float和bool了.
###官方示例:
<php
//Coercive mode
function sumOfInts(int ...$ints)
{
    return array_sum($ints);
}
var_dump(sumOfints(2,'3',4.1));
需要注意的是上文提到的严格模式的问题在这里
同样同样适用:强制模式(默认,即强制类型转换)
下还是会对不符合预期的参数进行强制类型转换
,严格模式下则触发TypeError的致命错误.

##4.use批量
PHP7中use可以在一句话中声明多个类或者函数或
const了:
<php
use some/namespace/{ClassA,ClassB,ClassC as C};
use function some/namespace/{fn_a,fn_b,fn_c};
use const some/namespace/{ConstA,ConstB,ConstC};
但还是要写出每个类或函数或const的名称(并没有
像Python一样的from some import *的方法).

需要留意的问题是:如果你使用的是是基于
composer和PSR-4的框架,这种写法是否能
成功加载类文件?其实是可以的,composer
注册的自动加载方法是在类被调用的时候
根据类的命名空间去查找位置,这种写法对
其没有影响.

##5.其他的特性
其他的一些特性我就不一一介绍了，有兴趣可以查看官方文档：http://php.net/manual/en/migration70.new-features.php

.PHP5.3开始有了匿名函数,现在又有了匿名类了;
.define现在可以定义常量数组;
.闭包(Closure)增加了一个call方法;
.生成器(或者叫迭代器更合适)可以有
一个最终返回值(return),也可以通过
yield from的新语法进入另一个生成
器中(生成器委托).

生成器的两个新特性(return和yield from
可以组合).具体的表象可以自行测试.
PHP7现在已经cr5了,最终的版本应该会很快到来


























