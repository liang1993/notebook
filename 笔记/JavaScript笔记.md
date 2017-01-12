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
##数组 
JavaScript的Array可以包含任意的数据类型，并且通过索引来访问每个元素。
通过length属性直接取得数组的长度：
<pre><code>var arr = [1,2,3.14,'hello',null,true];
arr.length; // 6</code></pre>
请注意，*直接给Array的length赋一个新的值会导致Array的大小发生变化*：
<pre><code>var arr = [1,2,3];
arr.length; // 3
arr.length = 6; // arr变为[1,2,3,undefined,,undefined,undefined]
arr.length = 2; //arr变为[1,2]</code></pre>
Array可以通过索引把对应的元素修改为新的值，因此对Array的索引进行赋值会直接修改这个Array：
>略

请注意，*如果通过索引赋值时，索引超过了范围吗，同样会引起Array大小的变化*:
<pre><code>var arr = [1,2,3];
arr[5] = 'x'; // arr变为[1,2,3,undefined,undefined,x]</code></pre>
大多数的编程语言不允许直接改变数组的大小，越界访问索引会报错。然而，JavaScript的Array却不会有任何的错误。在编写代码的时候，不建议直接修改Array的大小，访问索引的时候要确保索引不会越界。
###indexOf
与String类似，Array也可以通过indexOf()来搜索一个指定位置的元素,如果不存在则返回-1：
>略

###slice
slice()是对应String的subString()方法，它截取Array的部分元素，然后返回一个新的Array:
<pre><code>var arr = [1,2,3,4,5,6,7];
arr.slice(0,3); // 从索引0开始，到索引3结束，但是不包括3：[1,2,3]
arr.slice(3); // 从索引3开始到结束：[4,5,6,7]</code></pre>
如果不给slice()传递任何参数，它就会从头到尾截取所有的元素。利用这一点，我们可以很容易的复制一个Array:
>略

###push和pop
push()是向Array的末尾添加若干元素，pop()则把Array的最后一个元素删除掉：
<pre><code>var arr = [1,2];
arr.push('A','B'); // 返回Arra的新的长度 4
arr; // [1,2,'A','B']
arr.pop(); // 返回‘B’
arr; // [1,2,'A']
arr.pop();arr.pop();arr.pop(); //arr = []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined</code></pre>
###unshift和shift
如果要往Array的头部添加若干元素，使用unshift()方法，shift()方法则是把Array的第一个元素删除(与push和pop相对应)：
>略

###sort 
sort()可以对当前的Array进行排序，它会直接修改当前Array的元素位置，直接调用时，按照默认顺序排序:
<pre><code>var arr = [3,1,2];
arr.sort();
arr; // [1,2,3]</code></pre>
###reverse
reverse()把整个Array反转：
<pre><code>var arr = [1,2,3];
arr.reverse(); // arr [3,2,1]</code></pre>
###splice
splice()方法是修改Array的“万能方法”，它可以从指定索引开始删除若干的元素，然后再从该位置添加若干的元素：
<pre><code>var arr = ['Microsoft','Apple','Yahoo','AOL','Excite','Oracle']; 
//从索引2开始删除3个元素，然后再添加两个元素
arr.splice(2,3,'Google','Facebook'); // 返回删除的元素['Yahoo','AOL','Excite']
arr; // ['Microsoft','Apple','Google','Facebook','Oracle']
//只删除不添加
arr.splice(2,2); // 返回['Google','Facebook']
//只添加不删除
arr.splice(2,0,'Google','Facebook'); // 返回[]，因为没有删除任何元素</code></pre>
###concat
connact()方法把当前的Array和另一个Array连接起来，并返回一个新的Array：
<pre><code>var arr = [1,2,3];
var added = arr.concat(['A','B','C']); // added = [1,2,3,'A','B','C']</code></pre>
请注意，*concat()方法没有修改当前的Array，而是返回一个新的Array*
实际上concat()方法可以接受任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里：
<pre><code>var arr = [1,2,3];
arr.concat('A','B',[4,5,6]); // 返回[1,2,3,'A','B',4,5,6]</code></pre>
###join
join()方法是一个非常实用的方法，它把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串:
<pre><code>var arr = [1,2,3,4];
arr.join('-'); // 返回'1-2-3-4'</code></pre>
如果Array的元素不是字符串，则将自动转换为字符串后连接。
###多维数组
如果数组的某个元素又是一个Array，则可以形成多维数组:
>略