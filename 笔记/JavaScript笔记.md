#JavaScript笔记

##基本语法
JavaScript语法与java类似，每个语句以;技术，语句块使用{...}。但是并不强制要求在每个语句的结尾加;。但是让JavaScript引擎自动加分号，在某些情况下会改变程序的语意，影响程序的运行结果。
赋值语句:
<pre><code>var x = 1;</code></pre>
代码块：
<pre><code>if(true){
    x=1;
}</code></pre>
注释：
<pre><code>//这是一行注释
alert('hello world'); //这也是注释
/* 这是一段注释
仍然是注释
注释结束*/</code></pre>
<font color = 'red'>请注意:JavaScript严格区分大小写，如果弄错，程序将会运行不正常</font>

##数据类型和变量
###数据类型
####Number
Javas不区分整数和浮点数，统一用number表示，一下都是合法的Number类型:
>123;
0.456;
1.2345e3;
-99;
NaN; //NaN表示Not a Number,当无法计算结果时用NaN表示
Infinity; //表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity

16进制用0x前缀和0-9，a-f表示：
>0xff00;
0xa34f12;

四则运算同数学一致，值得注意的是：
>2 / 0 ; // Infinity
0 / 0 ; // NaN


####字符串
字符串是以单引号或者双引号括起来的任意文本，比如'abc',"xyz"等等。

####布尔值
布尔值和布尔代数的表示完全一致，一个布尔值只有true,false两种。可以直接用true,false表示布尔值，也可以通过布尔运算得出：
>true ; 
false ;
2 > 1 ; // true 
2 < 1 ; // false

常用的运算还有 "&&"与运算，"||"或运算，"!"非运算，">、<、>=、<=、==、==="。其中值得注意的是"=="和"===":
>false == 0 ; // true
false === 0 ; // false

在JavaScript中：
"=="比较，会自动转换数据类型再比较，很多时候会得到诡异的结果。
"==="比较，不会自动转换数据类型，如果数据类型不一致，返回false，如果一致再比较。
<font color='red'>由于JavaScript这个设计缺陷，*不要*使用"=="比较，始终坚持使用"==="比较</font>
另外有个特例就是*NaN*这个特殊的Number与其他所有的值都不想等，包括他自己，唯一能够哦按段NaN的方法是通过isNaN()函数：
<pre><code>isNaN(NaN); // true </code></pre>
另外注意浮点数的比较：
<pre><code>1/3 === (1-2/3); // false </code></pre>
这是由于浮点数在运算的过程中会产生误差，因为计算机无法精确的表示无限循环的小数。要比较两个浮点数是否相等，只能计算他们之差的绝对值，会否小于某个阈值：
<pre><code>Math.abs(1/3 - (1-2/3)) &lt; 0.00000001; // true</code></pre>
####null和undefined
null表示一个空的值，它和0以及空字符串''不同，0是一个数值，''表示长度为0的字符串，而null表示"空"。
undefined表示值未定义。一般只在判断函数参数是否传递的情况下使用。
####数组
数组是一组按顺序排列的集合，集合的每个值称为元素。JavaScript的数组是可以包括任意的数据类型:
<pre><code>[1,2,3.14,'hello',null,true]</code></pre>
另一种创建数组的方法师通过Array()函数实现:
<pre><code>new Array(1,2,3); //创建了数组[1,2,3]</code></pre>
数组的索引是从0开始。
####对象
JavaScript对象是一组键-值组成的无序的集合：
<pre><code>var person = {
    name:'bob',
    age:20,
    tag:['js','web','mobile'],
    hasCar:true,
};</code></pre>
要获取一个对象的属性，我们用对象标量.属性名的方式:
<pre><code>person.name ; //'bob'</code></pre>

####变量
变量在JavaScript中就是用一个变量名表示，变量名是大小写英文，数字，$和_组合，且不能用数字开头。同时变量名也不能是JavaScript的关键字。申明一个变量用var语句：
<pre><code>var a;//申明了a变量，此时a的值为undefined</code></pre>
在JavaScript中，使用等号=对变量进行赋值。可以把任意的数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量。但是只能用var申明一次：
<pre><code>var a = 123; // a为整数123
a = 'a' ; // a转变为字符串a</code></pre>
这种变量本身类型的不固定的语言称为动态语言，与之相对的是静态语言。静态语言在定义变量时，必须制定变量的类型，如果赋值的时候类型不匹配。就会报错，比如Java。
#####strict模式
JavaScript设计之初，为了方便初学者学习，并不强制要求用var申明变量。这个设计错误带来了很严重的后果：如果一个变量没有通过var申明就被使用，那么该变量就自动被申明为全局变量：
<pre><code>i = 10 ; // i现在是全局变量</code></pre>
在同一个页面的不同JavaScript文件中，如果都不用var申明，恰好都使用了i这个变量，将会造成变量的互相影响，产生难以调试的错误。
使用var申明的变量则不是全局标量，它的范围被限制在该变量被申明的函数体内，同名变量在不同的函数体内互不冲突。
为了修补这一严重的缺陷，ECMA在后续规范中退出了strict模式，在strict模式下运行的JavaScript代码，强制通过var申明变量，未使用var申明的变量使用会导致运行错误。
启用strict模式的方法是在JavaScript代码的第一行写上：
<pre><code>'use strict';</code></pre>
##字符串
JavaScript的字符串是用''或""表示。
如果一个字符串既有'又有"字符，此时需要用\转义来标识：
<pre><code>'I\'m \"OK\"!'; //I'm "OK"!</code></pre>
转义字符\可以转义很多字符，比如*\n*表示换行，*\t*表示制表符，字符\本身也需要转义，所以\\\\表示的字符\\。
ASCII字符可以用\x##形式的十六进制表示：
>'\x41' ; // 等同'A'

还可以用\u####表示一个Unicode字符:
>'\u4e2d\u6587' ; //完全等同于'中文'

###多行字符串
由于多行字符串用\n比较费事，所以在ES6标准中新增了一种多行字符串的表示方法，用\`....\` 表示:
>\`这是一个
多行
字符串\`

###模板字符串
多个字符串连接用+号
但是很多变量需要连接，用+号就比较麻烦。ES6中新增了一种模板字符串，表示方法和上面的多行字符串一样，但是他会自动替换字符串中的变量：
<pre><code>var name = '小明';
var age = 20;
var message = `你好，${name},你今年${age}岁了！`;</code></pre>
###操作字符串
字符串常见的操作如下：
<pre><code>var s = 'hello,world!';
s.length ; // 13 </code></pre>
要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引从0开始：
>略

值得注意的是超出范围的索引不会报错，一律返回undefined
<font color='red'>特别注意，字符串是不可变的，如果对一个字符串的某个索引赋值，不会有任何错误，也不会有任何效果</font>
<pre><code>var s = 'Test';
s[0] = 'X';
alert(s); // s仍为Test</code></pre>
JavaScript为字符串提供了一些常用的方法，调用这些方法本身不会改变原有字符串的内容，而是*返回一个新的字符串*:
####toUpperCase
将一个字符串全变变为大写
例：略
####toLowerCase
将一个字符串全部变为小写
例：略
####indeOf
搜索指定字符串出现的位置：
<pre><code>var s = 'hello, world';
s.indexof('world'); // 7
s.indexof('World'); // 没有找到， -1</code></pre>
####substring
substring()返回指定索引区间的字符串：
<pre><code>var s = 'hello, world'
s.substring(0,5) ; // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'</code></pre>