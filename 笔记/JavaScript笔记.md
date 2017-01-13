参考自[这里](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000)

#快速入门
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

##对象
JavaScript对象是一种无序的集合数据类型，它由若干键值对组成：
<pre><code>var xiaoming = {
    name:'小明',
    birth:1990,
    school:'No.1 Middle School',
    height:1.70,
    weight:65,
    score:null
};</code></pre>
注意，*最后一个键值对不需要在末尾加,*
访问变量是通过.操作符来完成，但是要求属性名必须是一个有效的变量名，如果属性名包含特殊字符，就必须用''括起来：
<pre><code>var xiaohong{
    name:'xiaohong',
    'middle-school':'No.1 Middle School'
};</code></pre>
xiaohong的属性名middle-school不是一个有效的变量，就需要用''括起来。访问这个属性也无法使用.操作符必须使用['xxx']来访问:
<pre><code>xiaohong['middle-school']; // 'No.1 Middle School'</code></pre>
实际上JavaScript对象的所有的属性都是字符串，不过属性对应的值可以是任意的数据类型。
如果访问一个不存在的属性会放回什么呢？JavaScript规定，访问不存在的属性不报错，而是返回undefined：
<pre><code>var xiaoming = {
    name:'小明'
}；
xiaoming.age; // undefined</code></pre>
由于JavaScript的对象是动态类型，你可以自由的给一个对象添加或者删除属性：
<pre><code>var xiaoming={
    name = 'xiaoming'
};
xiaoming.age = 18; // 新增一个age属性
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
delete xiaoming.school; // 删除一个不存在的属性也不会报错 </code></pre>
如果我们要检测xiaoming是否拥有某一属性，可以用in操作符：
<pre><code>var xiaoming = {
    name:'小明',
    birth:1990,
    school:'No.1 Middle School',
    height:1.70,
    school:null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
</code></pre>
如果in判断一个属性存在，这个属性不一定是xiaoming的，它可能是xiaoming继承得到的：
<pre><code>'toString' in xiaoming; // true</code></pre>
因为toString定义在Object对象中，而所有的对象最终都会在原型链上只想Object，所以xiaoming也拥有toString属性。
要判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法：
<pre><code>var xiaoming={
    name:'小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false</code></pre>
##条件判断
JavaScript使用if(){...}else{...}来进行条件判断：
>略

###多行条件判断
如果还要更细致的判断条件，可以使用过个if(){...}else if(){...}else{...}组合：
>略

请注意，if...else...语句的执行特点是二选一，在多个if...else...语句中，如果某个条件成立，就不会再继续判断了：
<pre><code>var age = 20;
if(age >= 6){
    alert('teenager');
}else if(age >= 18){
    alert('adult');
}else{
    alert('kid');
}; // only alert teenager</code></pre>

如果判断条件语句的结果不是true和false怎么办？例如：
<pre><code>var s = '123';
if(s.length){ // 计算结果为3
}</code></pre>
JavaScript把null，undefined，0，NaN和空字符串''视为false，其他值一概视为true，因此上述代码判断的结果是true。
##循环
JavaScript的循环有两种，一种是for循环，通过初始条件，结束条件和递增条件来循环执行语句：
<pre><code>var x= 0;
var i;
for(i=0; i<=10000; i++){
    x = x+i;
}
x; // 50005000</code></pre>
for循环最常用的地方就是利用索引来遍历数组:
>略

for循环的3个条件都是可以省略的，如果没有退出循环的判断条件，就必须使用break语句来中断循环，否则会产生死循环:
<pre><code>var x = 0;
for(;;){ // 将无限循环下去
    if(x > 10000){
        break; // 通过满足的if的判断，执行break跳出循环
    }
    x++;
}</code></pre>
###for...in
for循环的一个变体是for...in 循环，它可以把一个对象的所有的属性依次循环出来:
<pre><code>var o = {
    name:'Jack',
    age:20,
    city:'Beijing'
};
for(var key in o){
    alert key;
}</code></pre>
要过滤掉对象继承的属性，只需要在循环体里面对hasOwnProperty()进行判断:
>略

由于Array也是对象，而它的每个元素的索引被视为对象的属性，因此，for...in循环可以直接循环出Array的索引：
<pre><code>var a = ['A','B','C'];
for(var i in a){
    alert(i); // 0,1,2
    alert(a[i]); //'A','B','C'
}</code></pre>
请注意，*for...in对Array的循环得到的是String而不是Number*
###while
for循环在已知循环的初始和结束条件时非常有用，而上述忽略了条件的for循环很容易让人看不懂循环的逻辑，此时使用while循环更加：
<pre><code>var x = 0;
var n = 99;
while(n > 0){
    x = x + n;
    n = n - 2;
} // x = 2500 </code></pre>
###do...while
最后一种循环是do{...}while()循环，他和while循环的唯一区别在于，不是每次循环开始时的判断条件，而是在每次循环完成时的判断条件：
<pre><code>var n = 0;
do{
    n = n + 1;
}while(n < 100); // n = 100</code></pre>
用do{...}while()时注意，*循环体至少执行11次，而for和while循环体可能一次都不执行*
##Map和Set
JavaScript的默认对象的表现方式是{}，可以视为其他语言中的Map和Dictionary的数据结构，即一组键值对。
但是JavaScript的对象有个小问题，就是键必须是字符串。但实际上Number或其他数据类型作为键也是很合理的。
为了解决这个问题，ES6规范引入了新的数据类型Map。
###Map
Map是一组键值对的结构，具有极快的查询速度。初始化一个map:
<pre><code>//二维数组创建
var m = new Map([['Michael',95],['Bob',75],['Tracy',85]]);
m.get('Micheal'); // 95
//初始化空map，通过api添加元素
var m = new Map();
m.set('Adam',67);
m.has('Adam'); // 是否存在，true;
m.get('Adam'); //67
m.delete('Adam');
m.get('Adam'); // undefined
</code></pre>
由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会覆盖掉前面的值：
>略

###Set
Set和Map类似，也是一组key的集合，但是不存储value。由于key不能重复，所以，在Set中，没有重复的元素。
<pre><code>//通过输入Array来创建set
var s1 = new Set([1,2,3]);
//创建一个空的set，通过api来添加元素
var s2 = new Set();
s2.add(1); // {1}
s2.add(1); // {1} 可以重复添加相同的元素，但是没有效果
s2.delete(1);</code></pre>
*创建时的重复的元素会被自动过滤掉*
##iterable
遍历Array可以采用下标循环，循环Map和Set就无法使用下标，为了统一集合类型，ES6标准引入了新的iterable类型，Array,Map和Set都属于iterable类型。具有iterable类型的集合都可以通过新的for...of循环来遍历。
for...of循环是ES6引入的新的语法。
<pre><code>var a = ['A','B','C'];
var s = new Set(['A','B','C']);
var m - new Map([[1,'x'],[2,'y'],[3,'z']]);
for(var x of a){ // } // 遍历Array
for(var x of s){ // } // 遍历Set
for(var x of m){ // } // 遍历Map</code></pre>
for...of循环和for...in循环有何区别？
for...in循环由于历史遗留问题，它遍历的实际上是对象的属性名称。一个Array数组实际上也是一个对象，它的每个元素的所以被视为一个属性。
当我们手动给Array对象添加了额外的属性后，for...in循环会带来意想不到效果:
<pre><code>var a = [1,2,3];
a.name = 'hello';
for(var x in a){
  // '1','2','3','name'
}</code></pre>
for...in 将数组的属性name也包括在内了，但Array的length属性却不包括在内。
for...of循环则完全修复了这个问题，它只循环了数组的元素。
>略

这就是为什么要引入for...of循环的原因。
然后，更好的方式是直接使用iterable内置的forEach方法，它接受一个函数，每次迭代就自动回调该函数：
<pre><code>var = ['a','b','c'];
a.forEach(function(elementm ,index,array)){
    //element:指向当前元素的值
    //index:指向当前索引
    //array:指向Array对象本身
};</code></pre>
Set和Array类似，但是Set没有索引，因此回调函数的前两个参数都指向元素本身：
>略

Map的回调函数参数一次是value，key和map本身：
>略

如果对某些参数不感兴趣，由于JavaScript的函数调用不要求参数必须一致，因此可以忽略他们。
