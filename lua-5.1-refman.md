> **Original post: http://www.codingnow.com/2000/download/lua_manual.html**

<!-- saved from url=(0054)http://www.codingnow.com/2000/download/lua_manual.html -->

<!--
<html><div class="oneNoteWebClipperIsInstalledOnThisBrowser" style="display: none;"></div><head><meta http-equiv="Content-Type" content="text/html; charset=GBK">
<title>Lua 5.1 参考手册</title>
 
<style id="style-1-cropbar-clipper">/* Copyright 2014 Evernote Corporation. All rights reserved. */
.en-markup-crop-options {
    top: 18px !important;
    left: 50% !important;
    margin-left: -100px !important;
    width: 200px !important;
    border: 2px rgba(255,255,255,.38) solid !important;
    border-radius: 4px !important;
}

.en-markup-crop-options div div:first-of-type {
    margin-left: 0px !important;
}
</style></head>

<body data-feedly-mini="yes">
-->

<hr>
<h1>
Lua 5.1 参考手册
</h1>

by Roberto Ierusalimschy, Luiz Henrique de Figueiredo, Waldemar Celes
<p>
云风 译 <a href="http://www.codingnow.com/">www.codingnow.com</a>

</p><p>
<small>
<a href="http://www.lua.org/copyright.html">Copyright</a>
&#169; 2006 Lua.org, PUC-Rio.  All rights reserved.
</small>
</p><hr>

<!-- ====================================================================== -->
<p>





</p><h1>1 - <a name="1">介绍</a></h1>

<p>
Lua 是一个扩展式程序设计语言，它被设计成支持通用的过程式编程，并有相关数据描述的设施。
Lua 也能对面向对象编程，函数式编程，数据驱动式编程提供很好的支持。
它可以作为一个强大、轻量的脚本语言，供任何需要的程序使用。
Lua 以一个用 <em>clean</em> C 写成的库形式提供。（所谓 Clean C ，指的 ANSI C 和 C++ 中共通的一个子集）

</p><p>
作为一个扩展式语言，Lua 没有 "main" 程序的概念：它只能 <em>嵌入</em> 一个宿主程序中工作，这个宿主程序被称作
<em>embedding program</em> 或简称为 <em>host</em> 。
宿主程序可以通过调用函数执行一小段 Lua 代码，可以读写 Lua 变量，可以注入 C 函数让 Lua 代码调用。
这些扩展的 C 函数，可以大大的扩展了 Lua 可以处理事务的领域，这样就可以订制出各种语言，
而它们共享一个统一的句法格式的框架。
Lua 的官方发布版就包含了一个叫做 <code>lua</code> 的简单的宿主程序，它用 Lua 库提供了一个保证独立的 Lua 解释器。


</p><p>
Lua 是一个自由软件，它的使用许可决定了对它的使用过程一般没有任何保证。
这份手册中描述的东西的实现，可以在 Lua 的官方网站 <code>www.lua.org</code> 找到，


</p><p>
跟其它的许多参考手册一样，这份文档有些地方比较枯燥。
关于 Lua 的设计想法的探讨，可以看看 Lua 网站上提供的技术论文。
有关用 Lua 编程的细节介绍，可以读一下 Roberto 的书，<em>Programming in Lua (Second Edition)</em> 。


</p><h1>2 - <a name="2">语言</a></h1>

<p>
这一节从词法、语法、句法上描述 Lua 。
换句话说，这一节描述了哪些 token （符记）是有效的，它们如何被组合起来，这些组合方式有什么含义。

</p><p>
关于语言的构成概念将用常见的扩展 BNF 表达式写出。也就是这个样子：
{<em>a</em>} 意思是 0 或多个 <em>a</em> ，
[<em>a</em>] 意思是一个可选的 <em>a</em> 。
非最终的符号会保留原来的样子，关键字则看起来像这样 <b>kword</b> ，
其它最终的符号则写成 `<b>=</b>′ 。
完整的 Lua 语法可以在本手册最后找到。

</p><h2>2.1 - <a name="2.1">词法约定</a></h2>

<p>
Lua 中用到的 <em>名字</em>（也称作 <em>标识符</em>）可以是任何非数字开头的字母、数字、下划线组成的字符串。
这符合几乎所有编程语言中关于名字的定义。
（字母的定义依赖于当前环境：系统环境中定义的字母表中的字母都可以被用于标识符。）
标识符用来命名变量，或作为表的域名。

</p><p>
下面的关键字是保留的，不能用作名字：

</p><pre>     and       break     do        else      elseif
     end       false     for       function  if
     in        local     nil       not       or
     repeat    return    then      true      until     while
</pre>

<p>
Lua 是一个大小写敏感的语言：
<code>and</code> 是一个保留字，但是 <code>And</code> 和 <code>AND</code> 则是两个不同的合法的名字。
一般约定，以下划线开头连接一串大写字母的名字（比如 <code>_VERSION</code>）被保留用于 Lua 内部全局变量。

</p><p>
下面这些是其它的 token ：

</p><pre>     +     -     *     /     %     ^     #
     ==    ~=    &lt;=    &gt;=    &lt;     &gt;     =
     (     )     {     }     [     ]
     ;     :     ,     .     ..    ...
</pre>

<p>
字符串既可以用一对单引号引起，也可以是双引号，里面还可以包含类似 C 的转义符：
'<code>\a</code>' （响铃），
'<code>\b</code>' （退格），
'<code>\f</code>' （表单），
'<code>\n</code>' （换行），
'<code>\r</code>' （回车），
'<code>\t</code>' （横向制表），
'<code>\v</code>' （纵向制表），
'<code>\\</code>' （反斜杠），
'<code>\"</code>' （双引号），
以及 '<code>\'</code>' （单引号)。
而且，如果在一个反斜杠后跟了一个真正的换行符，其结果就是在字符串中产生一个换行符。
我们还可以用反斜杠加数字的形式 <code>\<em>ddd</em></code> 来描述一个字符。这里，
<em>ddd</em> 是一串最多三位的十进制数字。（注意，如果需要在这种描述方法后接一个是数字的字符，
那么反斜杠后必须写满三个数字。）Lua 中的字符串可以包含任何 8 位的值。包括用 '<code>\0</code>' 表示的零。

</p><p>
只有在你需要把不同的引号、换行、反斜杠、或是零结束符这些字符置入字符串时，
你才必须使用转义符。别的任何字符都可以直接写在文本里。（一些控制符可以会影响文件系统造成某些问题，
但是不会引起 Lua 的任何问题。）

</p><p>
字符串还可以用一种长括号括起来的方式定义。
我们把两个正的方括号间插入 n 个等号定义为第 n 级正长括号。
就是说，0 级正的长括号写作 <code>[[</code> ，
一级正的长括号写作 <code>[=[</code> ，如此等等。
反的长扩展也作类似定义；
举个例子，4 级反的长括号写作 <code>]====]</code> 。
一个长字符串可以由任何一级的正的长括号开始，而由第一个碰到的同级反的长括号结束。
整个词法分析过程将不受分行限制，不处理任何转意符，并且忽略掉任何不同级别的长括号。
这种方式描述的字符串可以包含任何东西，当然特定级别的反长括号除外。

</p><p>
另一个约定是，当正的长括号后面立即跟了一个换行符，
这个换行符就不包含在这个字符串内。
举个例子，假设一个系统使用 ASCII 码
（这时，'<code>a</code>' 编码为 97 ，换行符编码为 10 ，'<code>1</code>' 编码为 49 ），
下面五种方式描述了完全相同的字符串：

</p><pre>     a = 'alo\n123"'
     a = "alo\n123\""
     a = '\97lo\10\04923"'
     a = [[alo
     123"]]
     a = [==[
     alo
     123"]==]
</pre>

<p>
数字常量可以分两部分写，十进制底数部分和十进制的指数部分。指数部分是可选的。
Lua 也支持十六进制整数常量，只需要在前面加上前缀 <code>0x</code> 。
下面是一些合法的数字常量的例子：

</p><pre>     3   3.0   3.1416   314.16e-2   0.31416E1   0xff   0x56
</pre>

<p>
注释可以在除字符串内的任何地方是以两横 (<code>--</code>) 开始。
如果跟在两横后面的不是一个长括号，这就是一个短注释，它的作用范围直到行末；
否则就是一个长注释，其作用范围直到遇到反的长括号。
长注释通常被用来临时屏蔽代码块。

</p><h2>2.2 - <a name="2.2">值与类型</a></h2>

<p>
Lua 是一种 <em>动态类型语言</em>。
这意味着变量没有类型，只有值才有类型。
语言中不存在类型定义。而所有的值本身携带它们自己的类型信息。

</p><p>
Lua 中的所有值都是一致 (first-class) 的。
这意味着所有的值都可以被放在变量里，当作参数传递到另一个函数中，并被函数作为结果返回。

</p><p>
Lua 中有八种基本类型：
<em>nil</em>, <em>boolean</em>, <em>number</em>,
<em>string</em>, <em>function</em>, <em>userdata</em>,
<em>thread</em>, and <em>table</em>.
<em>Nil</em> 类型只有一种值 <b>nil</b> ，它的主要用途用于标表识和别的任何值的差异；
通常，当需要描述一个无意义的值时会用到它。
<em>Boolean</em> 类型只有两种值：<b>false</b> 和 <b>true</b>。
<b>nil</b> 和 <b>false</b> 都能导致条件为假；而另外所有的值都被当作真。
<em>Number</em> 表示实数（双精度浮点数）。
（编译一个其它内部数字类型的 Lua 解释器是件很容易的事；比如把内部数字类型改作
单精度浮点数或长整型。参见文件 <code>luaconf.h</code> 。）
<em>String</em> 表示一串字符的数组。

Lua 是 8-bit clean 的：
字符串可以包含任何 8 位字符，
包括零结束符 ('<code>\0</code>') （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">§2.1</a>）。


</p><p>
Lua 可以调用（和处理）用 Lua 写的函数以及用 C 写的函数（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">§2.5.8</a>）.


</p><p>
<em>userdata</em> 类型用来将任意 C 数据保存在 Lua 变量中。
这个类型相当于一块原生的内存，除了赋值和相同性判断，Lua 没有为之预定义任何操作。
然而，通过使用 <em>metatable （元表）</em> ，程序员可以为 userdata 自定义一组操作
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。
userdata 不能在 Lua 中创建出来，也不能在 Lua 中修改。这样的操作只能通过 C API。
这一点保证了宿主程序完全掌管其中的数据。

</p><p>
<em>thread</em> 类型用来区别独立的执行线程，它被用来实现 coroutine （协同例程）（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.11">§2.11</a>）。
不要把 Lua 线程跟操作系统的线程搞混。
Lua 可以在所有的系统上提供对 coroutine 的支持，即使系统并不支持线程。

</p><p>
<em>table</em> 类型实现了一个关联数组。也就是说，
数组可以用任何东西（除了<b>nil</b>）做索引，而不限于数字。
table 可以以不同类型的值构成；它可以包含所有的类型的值（除 <b>nil</b> 外）。
table 是 lua 中唯一的一种数据结构；它可以用来描述原始的数组、符号表、集合、
记录、图、树、等等。
用于表述记录时，lua 使用域名作为索引。
语言本身采用一种语法糖，支持以 <code>a.name</code> 的形式表示 <code>a["name"]</code>。
有很多形式用于在 lua 中创建一个 table （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.7">§2.5.7</a>）。

</p><p>
跟索引一样， table 每个域中的值也可以是任何类型（除 <b>nil</b>外）。
特别的，因为函数本身也是值，所以 table 的域中也可以放函数。
这样 table 中就可以有一些 <em>methods</em> 了 （参见see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">§2.5.9</a>）。

</p><p>
table， function ，thread ，和 (full) userdata 这些类型的值是所谓的对象：
变量本身并不会真正的存放它们的值，而只是放了一个对对象的引用。
赋值，参数传递，函数返回，都是对这些对象的引用进行操作；
这些操作不会做暗地里做任何性质的拷贝。

</p><p>
库函数 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-type"><code>type</code></a> 可以返回一个描述给定值的类型的字符串。

</p><h3>2.2.1 - <a name="2.2.1">强制转换</a></h3>

<p>
Lua 提供运行时字符串到数字的自动转换。
任何对字符串的数学运算操作都会尝试用一般的转换规则把这个字符串转换成一个数字。
相反，无论何时，一个数字需要作为字符串来使用时，数字都会以合理的格式转换为字符串。
需要完全控制数字怎样转换为字符串，可以使用字符串库中的 <code>format</code> 函数
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a>）。


</p><h2>2.3 - <a name="2.3">变量</a></h2>

<p>
写上变量的地方意味着当以其保存的值来替代之。

Lua 中有三类变量：全局变量，局部变量，还有 table 的域。

</p><p>
一个单一的名字可以表示一个全局变量，也可以表示一个局部变量 （或者是一个函数的参数，这是一种特殊形式的局部变量）：

</p><pre>	var ::= Name
</pre><p>
Name 就是 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">§2.1</a> 中所定义的标识符。

</p><p>
任何变量都被假定为全局变量，除非显式的以 local 修饰定义 
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.7">§2.4.7</a>）。
局部变量有其作用范围：
局部变量可以被定义在它作用范围中的函数自由使用
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.6">§2.6</a>）。


</p><p>
在变量的首次赋值之前，变量的值均为 <b>nil</b>。


</p><p>
方括号被用来对 table 作索引：

</p><pre>	var ::= prefixexp `<b>[</b>′ exp `<b>]</b>′
</pre><p>
对全局变量以及 table 域之访问的含义可以通过 metatable 来改变。
以取一个变量下标指向的量 <code>t[i]</code> 等价于调用 <code>gettable_event(t,i)</code>。
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a> ，有一份完整的关于
<code>gettable_event</code> 函数的说明。
这个函数并没有在 lua 中定义出来，也不能在 lua 中调用。
这里我们把它列出来只是方便说明。）

</p><p>
<code>var.Name</code> 这种语法只是一个语法糖，用来表示
<code>var["Name"]</code>：

</p><pre>	var ::= prefixexp `<b>.</b>′ Name
</pre>

<p>
所有的全局变量都是放在一个特定 lua table 的诸个域中，这个特定的 table
叫作 <em>environment （环境）table</em> 或者简称为
<em>环境</em> （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.9">§2.9</a>）。
每个函数都有对一个环境的引用，
所以一个函数中可见的所有全局变量都放在这个函数所引用的环境表（environment table）中。
当一个函数被创建出来，它会从创建它的函数中继承其环境，你可以调用
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-getfenv"><code>getfenv</code></a> 取得其环境。
如果想改变环境，可以调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setfenv"><code>setfenv</code></a>。
（对于 C 函数，你只能通过 debug 库来改变其环境；
参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#5.9">§5.9</a>）。

</p><p>
对一个全局变量 <code>x</code> 的访问
等价于 <code>_env.x</code>，而这又可以等价于

</p><pre>     gettable_event(_env, "x")
</pre>

<p>
这里，<code>_env</code> 是当前运行的函数的环境。
（函数 <code>gettable_event</code> 的完整说明参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>。
这个函数并没有在 lua 中定义出来，也不能调用。
当然，<code>_env</code> 这个变量也同样没有在 Lua 中定义出来。
我们在这里使用它们，仅仅只是方便解释而已。）


</p><h2>2.4 - <a name="2.4">语句段（Statement）</a></h2>

<p>
Lua 支持惯例形式的语句段，它和 Pascal 或是 C 很相象。
这个集合包括赋值，控制结构，函数调用，还有变量声明。

</p><h3>2.4.1 - <a name="2.4.1">Chunk（语句组）</a></h3>

<p>
Lua 的一个执行单元被称作 <em>chunk</em>。
一个 chunk 就是一串语句段，它们会被循序的执行。
每个语句段可以以一个分号结束：

</p><pre>	chunk ::= {stat [`<b>;</b>′]}
</pre><p>
这儿不允许有空的语句段，所以 '<code>;;</code>' 是非法的。

</p><p>
lua 把一个 chunk 当作一个拥有不定参数的匿名函数
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">§2.5.9</a>）处理。
正是这样，chunk 内可以定义局部变量，接收参数，并且返回值。

</p><p>
chunk 可以被保存在一个文件中，也可以保存在宿主程序的一个字符串中。
当一个 chunk 被执行，首先它会被预编译成虚拟机中的指令序列，
然后被虚拟机解释运行这些指令。


</p><p>
chunk 也可以被预编译成二进制形式；细节参考程序 <code>luac</code>。
用源码形式提供的程序和被编译过的二进制形式的程序是可以相互替换的；
Lua 会自动识别文件类型并做正确的处理。


</p><h3>2.4.2 - <a name="2.4.2">语句块</a></h3><p>
语句块是一列语句段；从语法上来说，一个语句块跟一个 chunk 相同：

</p><pre>	block ::= chunk
</pre>

<p>
一个语句块可以被显式的写成一个单独的语句段：

</p><pre>	stat ::= <b>do</b> block <b>end</b>
</pre><p>
显式的语句块对于控制变量的作用范围很有用。
有时候，显式的语句块被用来在另一个语句块中插入
<b>return</b> 或是 <b>break</b> （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.4">§2.4.4</a>）。


</p><h3>2.4.3 - <a name="2.4.3">赋值</a></h3>

<p>
Lua 允许多重赋值。
因此，赋值的语法定义是等号左边放一系列变量，
而等号右边放一系列的表达式。
两边的元素都用逗号间开：

</p><pre>	stat ::= varlist1 `<b>=</b>′ explist1
	varlist1 ::= var {`<b>,</b>′ var}
	explist1 ::= exp {`<b>,</b>′ exp}
</pre><p>
表达式放在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5">§2.5</a> 里讨论。


</p><p>
在作赋值操作之前，
那一系列的右值会被对齐到左边变量需要的个数。
如果右值比需要的更多的话，多余的值就被扔掉。
如果右值的数量不够需求，
将会按所需扩展若干个 <b>nil</b>。
如果表达式列表以一个函数调用结束，
这个函数所返回的所有值都会在对齐操作之前被置入右值序列中。
（除非这个函数调用被用括号括了起来；参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5">§2.5</a>）。

</p><p>
赋值段首先会做运算完所有的表达式，然后仅仅做赋值操作。
因此，下面这段代码

</p><pre>     i = 3
     i, a[i] = i+1, 20
</pre><p>
会把 <code>a[3]</code> 设置为 20，而不会影响到 <code>a[4]</code> 。
这是因为 <code>a[i]</code> 中的 <code>i</code> 在被赋值为 4 之前就被拿出来了（那时是 3 ）。
简单说 ，这样一行

</p><pre>     x, y = y, x
</pre>
<p>
可以用来交换 <code>x</code> 和 <code>y</code> 中的值。


</p><p>
对全局变量以及 table 中的域的赋值操作的含义可以通过 metatable 来改变。
对变量下标指向的赋值，即 <code>t[i] = val</code> 等价于
<code>settable_event(t,i,val)</code>。
（关于函数 <code>settable_event</code> 的详细说明，参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>。
这个函数并没有在 Lua 中定义出来，也不可以被调用。
这里我们列出来，仅仅出于方便解释的目的）


</p><p>
对于全局变量的赋值 <code>x = val</code>
等价于
<code>_env.x = val</code>，这个又可以等价于

</p><pre>     settable_event(_env, "x", val)
</pre><p>
这里，<code>_env</code> 指的是正在运行中的函数的环境。
（变量 <code>_env</code> 并没有在 Lua 中定义出来。
我们仅仅出于解释的目的在这里写出来。）

</p><h3>2.4.4 - <a name="2.4.4">控制结构</a></h3><p>
<b>if</b>、 <b>while</b>、以及 <b>repeat</b> 这些控制结构符合通常的意义，而且也有类似的语法：

</p><pre>	stat ::= <b>while</b> exp <b>do</b> block <b>end</b>
	stat ::= <b>repeat</b> block <b>until</b> exp
	stat ::= <b>if</b> exp <b>then</b> block {<b>elseif</b> exp <b>then</b> block} [<b>else</b> block] <b>end</b>
</pre><p>

Lua 也有一个 <b>for</b> 语句，它有两种形式（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.5">§2.4.5</a>）。


</p><p>
控制结构中的条件表达式可以返回任何值。
<b>false</b> 和 <b>nil</b> 两者都被认为是假条件。
所有不同于 <b>nil</b> 和 <b>false</b> 的其它值都被认为是真
（特别需要注意的是，数字 0 和空字符串也被认为是真）。


</p><p>
在 <b>repeat</b>–<b>until</b> 循环中，
内部语句块的结束点不是在 <b>until</b> 这个关键字处，
它还包括了其后的条件表达式。
因此，条件表达式中可以使用循环内部语句块中的定义的局部变量。

</p><p>
<b>return</b> 被用于从函数或是 chunk（其实它就是一个函数）中
返回值。

函数和 chunk 可以返回不只一个值，
所以 <b>return</b> 的语法为

</p><pre>	stat ::= <b>return</b> [explist1]
</pre>

<p>
<b>break</b> 被用来结束
<b>while</b>、 <b>repeat</b>、或 <b>for</b> 循环，
它将忽略掉循环中下面的语句段的运行：

</p><pre>	stat ::= <b>break</b>
</pre><p>

<b>break</b> 跳出最内层的循环。


</p><p>
<b>return</b> 和 <b>break</b> 只能被写在一个语句块的最后一句。
如果你真的需要从语句块的中间 <b>return</b> 或是 <b>break</b> ，
你可以使用显式的声名一个内部语句块。
一般写作 <code>do return end</code> 或是 <code>do break end</code>，
可以这样写是因为现在 <b>return</b> 或 <b>break</b> 都成了一个语句块的最后一句了。


</p><h3>2.4.5 - <a name="2.4.5">For 语句</a></h3>

<p>

<b>for</b> 有两种形式：一种是数字形式，另一种是一般形式。

</p><p>
数字形式的 <b>for</b> 循环，通过一个数学运算不断的运行内部的代码块。
下面是它的语法：

</p><pre>	stat ::= <b>for</b> Name `<b>=</b>′ exp `<b>,</b>′ exp [`<b>,</b>′ exp] <b>do</b> block <b>end</b>
</pre><p>
<em>block</em> 将把 <em>name</em> 作循环变量。从第一个 <em>exp</em> 开始起，直到第二个 <em>exp</em> 的值为止，其步长为
第三个 <em>exp</em> 。
更确切的说，一个 <b>for</b> 循环看起来是这个样子

</p><pre>     for v = <em>e1</em>, <em>e2</em>, <em>e3</em> do <em>block</em> end
</pre><p>
这等价于代码：

</p><pre>     do
       local <em>var</em>, <em>limit</em>, <em>step</em> = tonumber(<em>e1</em>), tonumber(<em>e2</em>), tonumber(<em>e3</em>)
       if not (<em>var</em> and <em>limit</em> and <em>step</em>) then error() end
       while (<em>step</em> &gt; 0 and <em>var</em> &lt;= <em>limit</em>) or (<em>step</em> &lt;= 0 and <em>var</em> &gt;= <em>limit</em>) do
         local v = <em>var</em>
         <em>block</em>
         <em>var</em> = <em>var</em> + <em>step</em>
       end
     end
</pre><p>

注意下面这几点：

</p><ul>

<li>
所有三个控制表达式都只被运算一次，表达式的计算在循环开始之前。
这些表达式的结果必须是数字。
</li>

<li>
<code><em>var</em></code> 、<code><em>limit</em></code> 、以及 <code><em>step</em></code> 都是一些不可见的变量。
这里给它们起的名字都仅仅用于解释方便。
</li>

<li>
如果第三个表达式（步长）没有给出，会把步长设为 1 。
</li>

<li>
你可以用 <b>break</b> 来退出 <b>for</b> 循环。
</li>

<li>
循环变量 <code>v</code> 是一个循环内部的局部变量；
当 <b>for</b> 循环结束后，你就不能在使用它。
如果你需要这个值，在退出循环前把它赋给另一个变量。
</li>

</ul>

<p>
一般形式的 <b>for</b> 通过一个叫作迭代器（<em>iterators</em>）的函数工作。
每次迭代，迭代器函数都会被调用以产生一个新的值，
当这个值为 <b>nil</b> 时，循环停止。
一般形式的 <b>for</b> 循环的语法如下：

</p><pre>	stat ::= <b>for</b> namelist <b>in</b> explist1 <b>do</b> block <b>end</b>
	namelist ::= Name {`<b>,</b>′ Name}
</pre><p>
<b>for</b> 语句好似这样

</p><pre>     for <em>var_1</em>, ···, <em>var_n</em> in <em>explist</em> do <em>block</em> end
</pre><p>
它等价于这样一段代码：

</p><pre>     do
       local <em>f</em>, <em>s</em>, <em>var</em> = <em>explist</em>
       while true do
         local <em>var_1</em>, ···, <em>var_n</em> = <em>f</em>(<em>s</em>, <em>var</em>)
         <em>var</em> = <em>var_1</em>
         if <em>var</em> == nil then break end
         <em>block</em>
       end
     end
</pre><p>
注意以下几点：

</p><ul>

<li>
<code><em>explist</em></code> 只会被计算一次。
它返回三个值， 一个迭代器函数，一个状态，一个迭代器的初始值。
</li>

<li>
<code><em>f</em></code>、 <code><em>s</em></code>、 以及 <code><em>var</em></code> 都是不可见的变量。
这里给它们起的名字都只是为了解说方便。
</li>

<li>
你可以使用 <b>break</b> 来跳出 <b>for</b> 循环。
</li>

<li>
循环变量 <code><em>var_i</em></code> 对于循环来说是一个局部变量；
你不可以在 <b>for</b> 循环结束后继续使用。
如果你需要保留这些值，那么就在循环结束前赋值到别的变量里去。
</li>

</ul>




<h3>2.4.6 - <a name="2.4.6">把函数调用作为语句段</a></h3><p>
为了允许使用可能的副作用，
函数调用可以被作为一个语句段执行：

</p><pre>	stat ::= functioncall
</pre><p>
在这种情况下，所有的返回值都被舍弃。
函数调用在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">§2.5.8</a> 中解释。


</p><h3>2.4.7 - <a name="2.4.7">局部变量声名</a></h3><p>
局部变量可以在语句块中任何地方声名。
声名可以包含一个初始化赋值操作：

</p><pre>	stat ::= <b>local</b> namelist [`<b>=</b>′ explist1]
</pre><p>
如果有的话，初始化赋值操作的行为等同于赋值操作（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.3">§2.4.3</a>）。
否则，所有的变量将被初始化为 <b>nil</b>。


</p><p>
一个 chunk 同时也是一个语句块（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.1">§2.4.1</a>），
所以局部变量可以放在 chunk 中那些显式注明的语句块之外。
这些局部变量的作用范围从声明起一直延伸到 chunk 末尾。

</p><p>
局部变量的可见规则在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.6">§2.6</a> 中解释。


</p><h2>2.5 - <a name="2.5">表达式</a></h2>

<p>
Lua 中有这些基本表达式：

</p><pre>	exp ::= prefixexp
	exp ::= <b>nil</b> | <b>false</b> | <b>true</b>
	exp ::= Number
	exp ::= String
	exp ::= function
	exp ::= tableconstructor
	exp ::= `<b>...</b>′
	exp ::= exp binop exp
	exp ::= unop exp
	prefixexp ::= var | functioncall | `<b>(</b>′ exp `<b>)</b>′
</pre>

<p>
数字和字符串在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">§2.1</a> 中解释；
变量在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.3">§2.3</a> 中解释；
函数定义在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">§2.5.9</a> 中解释；
函数调用在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">§2.5.8</a> 中解释；
table 的构造在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.7">§2.5.7</a> 中解释；
可变参数的表达式写作三个点 ('<code>...</code>') ，它只能被用在有可变参数的函数中；
这些在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">§2.5.9</a> 中解释。


</p><p>
二元操作符包含有数学运算操作符（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.1">§2.5.1</a>），
比较操作符（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.2">§2.5.2</a>），逻辑操作符（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.3">§2.5.3</a>），
以及连接操作符（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.4">§2.5.4</a>）。
一元操作符包括负号（参见see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.1">§2.5.1</a>），
取反 <b>not</b>（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.3">§2.5.3</a>），
和取长度操作符（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">§2.5.5</a>）。


</p><p>
函数调用和可变参数表达式都可以放在多重返回值中。
如果表达式作为一个独立语句段出现（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.6">§2.4.6</a>）
（这只能是一个函数调用），
它们的返回列表将被对齐到零个元素，也就是忽略所有返回值。
如果表达式用于表达式列表的最后（或者是唯一）的元素，
就不会有任何的对齐操作（除非函数调用用括号括起来）。
在任何其它的情况下，Lua 将把表达式结果看成单一元素，
忽略除第一个之外的任何值。

</p><p>
这里有一些例子：

</p><pre>     f()                -- 调整到 0 个结果
     g(f(), x)          -- f() 被调整到一个结果
     g(x, f())          -- g 被传入 x 加上所有 f() 的返回值
     a,b,c = f(), x     -- f() 被调整到一个结果 （ c 在这里被赋为 nil ）
     a,b = ...          -- a 被赋值为可变参数中的第一个，
                        -- b 被赋值为第二个 （如果可变参数中并没有对应的值，
						-- 这里 a 和 b 都有可能被赋为 nil）
     
     a,b,c = x, f()     -- f() 被调整为两个结果
     a,b,c = f()        -- f() 被调整为三个结果
     return f()         -- 返回 f() 返回的所有结果
     return ...         -- 返回所有从可变参数中接收来的值
     return x,y,f()     -- 返回 x, y, 以及所有 f() 的返回值
     {f()}              -- 用 f() 的所有返回值创建一个列表
     {...}              -- 用可变参数中的所有值创建一个列表
     {f(), nil}         -- f() 被调整为一个结果
</pre>

<p>
被括号括起来的表达式永远被当作一个值。所以，
<code>(f(x,y,z))</code> 即使 <code>f</code> 返回多个值，这个表达式永远是一个单一值。
（<code>(f(x,y,z))</code> 的值是 <code>f</code> 返回的第一个值。如果 <code>f</code>
不返回值的话，那么它的值就是 <b>nil</b> 。）


</p><h3>2.5.1 - <a name="2.5.1">数学运算操作符</a></h3><p>
Lua 支持常见的数学运算操作符：
二元操作 <code>+</code> （加法），
<code>-</code> （减法），<code>*</code> （乘法），
<code>/</code> （除法）， <code>%</code> （取模），以及 <code>^</code> （幂）；
和一元操作 <code>-</code> （取负）。
如果对数字操作，或是可以转换为数字的字符串（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">§2.2.1</a>），
所有这些操作都依赖它通常的含义。
幂操作可以对任何幂值都正常工作。比如，
<code>x^(-0.5)</code> 将计算出 <code>x</code> 平方根的倒数。
取模操作被定义为

</p><pre>     a % b == a - math.floor(a/b)*b
</pre><p>
这就是说，其结果是商相对负无穷圆整后的余数。（译注：负数对正数取模的结果为正数）


</p><h3>2.5.2 - <a name="2.5.2">比较操作符</a></h3><p>
Lua 中的比较操作符有

</p><pre>     ==    ~=    &lt;     &gt;     &lt;=    &gt;=
</pre><p>
这些操作的结果不是 <b>false</b> 就是 <b>true</b>。


</p><p>
等于操作 (<code>==</code>) 首先比较操作数的类型。
如果类型不同，结果就是 <b>false</b>。
否则，继续比较值。
数字和字符串都用常规的方式比较。
对象 （table ，userdata ，thread ，以及函数）以引用的形式比较：
两个对象只有在它们指向同一个东西时才认为相等。
每次你创建一个新对象（一个 table 或是 userdata ，thread 函数），
它们都各不相同，即不同于上次创建的东西。


</p><p>
你可以改变 Lua 比较 table 和 userdata 的方式，这需要使用 "eq" 这个原方法
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">§2.2.1</a> 中提及的转换规则并不作用于比较操作。
所以， <code>"0"==0</code> 等于 <b>false</b>，
而且 <code>t[0]</code> 和 <code>t["0"]</code> 描述的是 table 中不同的域。

</p><p>
操作符 <code>~=</code> 完全等价于 (<code>==</code>) 操作的反值。


</p><p>
大小比较操作以以下方式进行。
如果参数都是数字，那么就直接做数字比较。
否则，如果参数都是字符串，就用字符串比较的方式进行。
再则，Lua 就试着调用 "lt" 或是 "le" 元方法
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。

</p><h3>2.5.3 - <a name="2.5.3">逻辑操作符</a></h3><p>
Lua 中的逻辑操作符有
<b>and</b>, <b>or</b>, 以及 <b>not</b>。
和控制结构（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.4">§2.4.4</a>）一样，
所有的逻辑操作符把 <b>false</b> 和 <b>nil</b> 都作为假，
而其它的一切都当作真。


</p><p>
取反操作 <b>not</b> 总是返回 <b>false</b> 或 <b>true</b> 中的一个。
与操作符 <b>and</b> 在第一个参数为 <b>false</b> 或 <b>nil</b> 时
返回这第一个参数；
否则，<b>and</b> 返回第二个参数。
或操作符 <b>or</b> 在第一个参数不为 <b>nil</b> 也不为 <b>false</b> 时，
返回这第一个参数，否则返回第二个参数。
<b>and</b> 和 <b>or</b> 都遵循短路规则；
也就是说，第二个操作数只在需要的时候去求值。
这里有一些例子：

</p><pre>     10 or 20            --&gt; 10
     10 or error()       --&gt; 10
     nil or "a"          --&gt; "a"
     nil and 10          --&gt; nil
     false and error()   --&gt; false
     false and nil       --&gt; false
     false or nil        --&gt; nil
     10 and 20           --&gt; 20
</pre><p>
（在这本手册中，
--&gt; 指前面表达式的结果。）



</p><h3>2.5.4 - <a name="2.5.4">连接符</a></h3><p>
Lua 中字符串的连接操作符写作两个点 ('<code>..</code>')。
如果两个操作数都是字符串或都是数字，连接操作将以 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">§2.2.1</a> 中提到的规则把其转换为字符串。
否则，会取调用元方法 "concat" （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。


</p><h3>2.5.5 - <a name="2.5.5">取长度操作符</a></h3>

<p>
取长度操作符写作一元操作 <code>#</code>。
字符串的长度是它的字节数（就是以一个字符一个字节计算的字符串长度）。


</p><p>
table <code>t</code> 的长度被定义成一个整数下标 <code>n</code> 。
它满足 <code>t[n]</code> 不是 <b>nil</b> 而 <code>t[n+1]</code> 为 <b>nil</b>；
此外，如果 <code>t[1]</code> 为 <b>nil</b> ，<code>n</code> 就可能是零。
对于常规的数组，里面从 1 到 <code>n</code> 放着一些非空的值的时候，
它的长度就精确的为 <code>n</code>，即最后一个值的下标。
如果数组有一个“空洞” （就是说，<b>nil</b> 值被夹在非空值之间），
那么 <code>#t</code> 可能是指向任何一个是 <b>nil</b> 值的前一个位置的下标
（就是说，任何一个 <b>nil</b> 值都有可能被当成数组的结束）。





</p><h3>2.5.6 - <a name="2.5.6">优先级</a></h3><p>
Lua 中操作符的优先级写在下表中，从低到高优先级排序：

</p><pre>     or
     and
     &lt;     &gt;     &lt;=    &gt;=    ~=    ==
     ..
     +     -
     *     /     %
     not   #     - (unary)
     ^
</pre><p>
通常，你可以用括号来改变运算次序。
连接操作符 ('<code>..</code>') 和幂操作 ('<code>^</code>') 是从右至左的。
其它所有的操作都是从左至右。


</p><h3>2.5.7 - <a name="2.5.7">Table 构造</a></h3><p>
table 构造子是一个构造 table 的表达式。
每次构造子被执行，都会构造出一个新的 table 。
构造子可以被用来构造一个空的 table，
也可以用来构造一个 table 并初始化其中的一些域。
一般的构造子的语法如下

</p><pre>	tableconstructor ::= `<b>{</b>′ [fieldlist] `<b>}</b>′
	fieldlist ::= field {fieldsep field} [fieldsep]
	field ::= `<b>[</b>′ exp `<b>]</b>′ `<b>=</b>′ exp | Name `<b>=</b>′ exp | exp
	fieldsep ::= `<b>,</b>′ | `<b>;</b>′
</pre>

<p>
每个形如 <code>[exp1] = exp2</code> 的域向 table 中增加新的一项，
其键值为 <code>exp1</code> 而值为 <code>exp2</code>。
形如 <code>name = exp</code> 的域等价于
<code>["name"] = exp</code>。
最后，形如 <code>exp</code> 的域等价于
<code>[i] = exp</code> ， 这里的 <code>i</code> 是一个从 1 开始不断增长的数字。
这这个格式中的其它域不会破坏其记数。
举个例子：

</p><pre>     a = { [f(1)] = g; "x", "y"; x = 1, f(x), [30] = 23; 45 }
</pre><p>
等价于

</p><pre>     do
       local t = {}
       t[f(1)] = g
       t[1] = "x"         -- 1st exp
       t[2] = "y"         -- 2nd exp
       t.x = 1            -- t["x"] = 1
       t[3] = f(x)        -- 3rd exp
       t[30] = 23
       t[4] = 45          -- 4th exp
       a = t
     end
</pre>

<p>
如果表单中最后一个域的形式是 <code>exp</code> ，
而且其表达式是一个函数调用或者是一个可变参数，
那么这个表达式所有的返回值将连续的进入列表
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">§2.5.8</a>）。
为了避免这一点，你可以用括号把函数调用（或是可变参数）括起来
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5">§2.5</a>）。


</p><p>
初始化域表可以在最后多一个分割符，
这样设计可以方便由机器生成代码。



</p><h3>2.5.8 - <a name="2.5.8">函数调用</a></h3><p>
Lua 中的函数调用的语法如下：

</p><pre>	functioncall ::= prefixexp args
</pre><p>
函数调用时，第一步，prefixexp 和 args 先被求值。
如果 prefixexp 的值的类型是 <em>function</em>，
那么这个函数就被用给出的参数调用。
否则 prefixexp 的元方法 "call" 就被调用，
第一个参数就是 prefixexp 的值，跟下来的是原来的调用参数
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。


</p><p>
这样的形式

</p><pre>	functioncall ::= prefixexp `<b>:</b>′ Name args
</pre><p>
可以用来调用 "方法"。
这是 Lua 支持的一种语法糖。像 <code>v:name(<em>args</em>)</code>
这个样子，被解释成 <code>v.name(v,<em>args</em>)</code>，
这里 <code>v</code> 只会被求值一次。


</p><p>
参数的语法如下：

</p><pre>	args ::= `<b>(</b>′ [explist1] `<b>)</b>′
	args ::= tableconstructor
	args ::= String
</pre><p>
所有参数的表达式求值都在函数调用之前。
这样的调用形式 <code>f{<em>fields</em>}</code> 是一种语法糖用于表示
 <code>f({<em>fields</em>})</code>；
这里指参数列表是一个单一的新创建出来的列表。
而这样的形式 <code>f'<em>string</em>'</code> 
（或是 <code>f"<em>string</em>"</code> 亦或是 <code>f[[<em>string</em>]]</code>）
也是一种语法糖，用于表示 <code>f('<em>string</em>')</code>；
这里指参数列表是一个单独的字符串。


</p><p>
因为表达式语法在 Lua 中比较自由，
所以你不能在函数调用的 '<code>(</code>' 前换行。
这个限制可以避免语言中的一些歧义。
比如你这样写

</p><pre>     a = f
     (g).x(a)
</pre><p>
Lua 将把它当作一个单一语句段， <code>a = f(g).x(a)</code> 。
因此，如果你真的想作为成两个语句段，你必须在它们之间写上一个分号。
如果你真的想调用 <code>f</code>，
你必须从 <code>(g)</code> 前移去换行。


</p><p>
这样一种调用形式：<code>return</code> <em>functioncall</em> 将触发一个尾调用。
Lua 实现了适当的尾部调用（或是适当的尾递归）：
在尾调用中，
被调用的函数重用调用它的函数的堆栈项。
因此，对于程序执行的嵌套尾调用的层数是没有限制的。
然而，尾调用将删除调用它的函数的任何调试信息。
注意，尾调用只发生在特定的语法下，
这时， <b>return</b> 只有单一函数调用作为参数；
这种语法使得调用函数的结果可以精确返回。
因此，下面这些例子都不是尾调用：

</p><pre>     return (f(x))        -- 返回值被调整为一个
     return 2 * f(x)
     return x, f(x)       -- 最加若干返回值
     f(x); return         -- 无返回值
     return x or f(x)     -- 返回值被调整为一个
</pre>




<h3>2.5.9 - <a name="2.5.9">函数定义</a></h3>

<p>
函数定义的语法如下：

</p><pre>	function ::= <b>function</b> funcbody
	funcbody ::= `<b>(</b>′ [parlist1] `<b>)</b>′ block <b>end</b>
</pre>

<p>
另外定义了一些语法糖简化函数定义的写法：

</p><pre>	stat ::= <b>function</b> funcname funcbody
	stat ::= <b>local</b> <b>function</b> Name funcbody
	funcname ::= Name {`<b>.</b>′ Name} [`<b>:</b>′ Name]
</pre><p>
这样的写法：
</p><pre>     function f () <em>body</em> end
</pre><p>
被转换成
</p><pre>     f = function () <em>body</em> end
</pre><p>
这样的写法：
</p><pre>     function t.a.b.c.f () <em>body</em> end
</pre><p>
被转换成
</p><pre>     t.a.b.c.f = function () <em>body</em> end
</pre><p>
这样的写法：
</p><pre>     local function f () <em>body</em> end
</pre><p>
被转换成
</p><pre>     local f; f = function () <em>body</em> end
</pre><p>
注意，并不是转换成
</p><pre>     local f = function () <em>body</em> end
</pre><p>
（这个差别只在函数体内需要引用 <code>f</code> 时才有。）


</p><p>
一个函数定义是一个可执行的表达式，
执行结果是一个类型为 <em>function</em> 的值。
当 Lua 预编译一个 chunk 的时候，
chunk 作为一个函数，整个函数体也就被预编译了。
那么，无论何时 Lua 执行了函数定义，
这个函数本身就被实例化了（或者说是关闭了）。
这个函数的实例（或者说是 <em>closure</em>（闭包））
是表达式的最终值。
相同函数的不同实例有可能引用不同的外部局部变量，
也可能拥有不同的环境表。

</p><p>
形参（函数定义需要的参数）是一些由实参（实际传入参数）的值初始化的局部变量：

</p><pre>	parlist1 ::= namelist [`<b>,</b>′ `<b>...</b>′] | `<b>...</b>′
</pre><p>
当一个函数被调用，
如果函数没有被定义为接收不定长参数，即在形参列表的末尾注明三个点 ('<code>...</code>')，
那么实参列表就会被调整到形参列表的长度，
变长参数函数不会调整实参列表；
取而代之的是，它将把所有额外的参数放在一起通过变长参数表达式传递给函数，
其写法依旧是三个点。
这个表达式的值是一串实参值的列表，看起来就跟一个可以返回多个结果的函数一样。
如果一个变长参数表达式放在另一个表达式中使用，或是放在另一串表达式的中间，
那么它的返回值就会被调整为单个值。
若这个表达式放在了一系列表达式的最后一个，就不会做调整了（除非用括号给括了起来）。


</p><p>
我们先做如下定义，然后再来看一个例子：

</p><pre>     function f(a, b) end
     function g(a, b, ...) end
     function r() return 1,2,3 end
</pre><p>
下面看看实参到形参数以及可变长参数的映射关系：

</p><pre>     CALL            PARAMETERS
     
     f(3)             a=3, b=nil
     f(3, 4)          a=3, b=4
     f(3, 4, 5)       a=3, b=4
     f(r(), 10)       a=1, b=10
     f(r())           a=1, b=2
     
     g(3)             a=3, b=nil, ... --&gt;  (nothing)
     g(3, 4)          a=3, b=4,   ... --&gt;  (nothing)
     g(3, 4, 5, 8)    a=3, b=4,   ... --&gt;  5  8
     g(5, r())        a=5, b=1,   ... --&gt;  2  3
</pre>

<p>
结果由 <b>return</b> 来返回（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.4">§2.4.4</a>）。
如果执行到函数末尾依旧没有遇到任何 <b>return</b> 语句，
函数就不会返回任何结果。


</p><p>
冒号语法可以用来定义方法，
就是说，函数可以有一个隐式的形参 <code>self</code>。
因此，如下写法：

</p><pre>     function t.a.b.c:f (<em>params</em>) <em>body</em> end
</pre><p>
是这样一种写法的语法糖：

</p><pre>     t.a.b.c.f = function (self, <em>params</em>) <em>body</em> end
</pre>






<h2>2.6 - <a name="2.6">可视规则</a></h2>

<p>
Lua 是一个有词法作用范围的语言。
变量的作用范围开始于声明它们之后的第一个语句段，
结束于包含这个声明的最内层语句块的结束点。
看下面这些例子：

</p><pre>     x = 10                -- 全局变量
     do                    -- 新的语句块
       local x = x         -- 新的一个 'x', 它的值现在是 10
       print(x)            --&gt; 10
       x = x+1
       do                  -- 另一个语句块
         local x = x+1     -- 又一个 'x'
         print(x)          --&gt; 12
       end
       print(x)            --&gt; 11
     end
     print(x)              --&gt; 10  （取到的是全局的那一个）
</pre>

<p>
注意这里，类似 <code>local x = x</code> 这样的声明，
新的 <code>x</code> 正在被声明，但是还没有进入它的作用范围，
所以第二个 <code>x</code> 指向的是外面一层的变量。


</p><p>
因为有这样一个词法作用范围的规则，
所以可以在函数内部自由的定义局部变量并使用它们。
当一个局部变量被更内层的函数中使用的时候，
它被内层函数称作
<em>upvalue</em>（上值），或是 <em>外部局部变量</em>。

</p><p>
注意，每次执行到一个 local 语句都会定义出一个新的局部变量。
看看这样一个例子：

</p><pre>     a = {}
     local x = 20
     for i=1,10 do
       local y = 0
       a[i] = function () y=y+1; return x+y end
     end
</pre><p>
这个循环创建了十个 closure（这指十个匿名函数的实例）。
这些 closure 中的每一个都使用了不同的 <code>y</code> 变量，
而它们又共享了同一份 <code>x</code>。


</p><h2>2.7 - <a name="2.7">错误处理</a></h2>

<p>
因为 Lua 是一个嵌入式的扩展语言，
所有的 Lua 动作都是从宿主程序的 C 代码调用 Lua 库
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a>）中的一个函数开始的。
在 Lua 编译或运行的任何时候发生了错误，控制权都会交还给 C ，
而 C 可以来做一些恰当的措施（比如打印出一条错误信息）。

</p><p>
Lua 代码可以显式的调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-error"><code>error</code></a> 函数来产生一条错误。
如果你需要在 Lua 中捕获发生的错误，
你可以使用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-pcall"><code>pcall</code></a> 函数。

</p><h2>2.8 - <a name="2.8">Metatable（元表）</a></h2>

<p>
Lua 中的每个值都可以用一个 <em>metatable</em>。
这个 <em>metatable</em> 就是一个原始的 Lua table ，
它用来定义原始值在特定操作下的行为。
你可以通过在 metatable 中的特定域设一些值来改变拥有这个 metatable 的值
的指定操作之行为。
举例来说，当一个非数字的值作加法操作的时候，
Lua 会检查它的 metatable 中 <code>"__add"</code> 域中的是否有一个函数。
如果有这么一个函数的话，Lua 调用这个函数来执行一次加法。


</p><p>
我们叫 metatable 中的键名为 <em>事件 (event)</em> ，把其中的值叫作 <em>元方法 (metamethod)</em>。
在上个例子中，事件是 <code>"add"</code> 而元方法就是那个执行加法操作的函数。


</p><p>
你可以通过 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-getmetatable"><code>getmetatable</code></a> 函数来查询到任何一个值的 metatable。


</p><p>
你可以通过 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setmetatable"><code>setmetatable</code></a> 函数来替换掉 table 的 metatable 。
你不能从 Lua 中改变其它任何类型的值的 metatable （使用 debug 库例外）；
要这样做的话必须使用 C API 。


</p><p>
每个 table 和 userdata 拥有独立的 metatable （当然多个 table 和 userdata
可以共享一个相同的表作它们的 metatable）；
其它所有类型的值，每种类型都分别共享唯一的一个 metatable。
因此，所有的数字一起只有一个 metatable ，所有的字符串也是，等等。


</p><p>
一个 metatable 可以控制一个对象做数学运算操作、比较操作、连接操作、取长度操作、取下标操作时的行为，
metatable 中还可以定义一个函数，让 userdata 作垃圾收集时调用它。
对于这些操作，Lua 都将其关联上一个被称作事件的指定健。
当 Lua 需要对一个值发起这些操作中的一个时，
它会去检查值中 metatable 中是否有对应事件。
如果有的话，键名对应的值（元方法）将控制 Lua 怎样做这个操作。


</p><p>
metatable 可以控制的操作已在下面列出来。
每个操作都用相应的名字区分。
每个操作的键名都是用操作名字加上两个下划线 '<code>__</code>' 前缀的字符串；
举例来说，"add" 操作的键名就是字符串 <code>"__add"</code>。
这些操作的语义用一个 Lua 函数来描述解释器如何执行更为恰当。

</p><p>
这里展示的用 Lua 写的代码仅作解说用；
实际的行为已经硬编码在解释器中，其执行效率要远高于这些模拟代码。
这些用于描述的的代码中用到的函数
（ <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-rawget"><code>rawget</code></a> ， <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-tonumber"><code>tonumber</code></a> ，等等。）
都可以在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#5.1">§5.1</a> 中找到。
特别注意，我们使用这样一个表达式来从给定对象中提取元方法

</p><pre>     metatable(obj)[event]
</pre><p>

这个应该被解读作

</p><pre>     rawget(getmetatable(obj) or {}, event)
</pre><p>

这就是说，访问一个元方法不再会触发任何的元方法，
而且访问一个没有 metatable 的对象也不会失败（而只是简单返回 <b>nil</b>）。


</p><ul>

<li><b>"add":</b>
<code>+</code> 操作。



<p>
下面这个 <code>getbinhandler</code> 函数定义了 Lua 怎样选择一个处理器来作二元操作。
首先，Lua 尝试第一个操作数。
如果这个东西的类型没有定义这个操作的处理器，然后 Lua 会尝试第二个操作数。

</p><pre>     function getbinhandler (op1, op2, event)
       return metatable(op1)[event] or metatable(op2)[event]
     end
</pre><p>
通过这个函数， <code>op1 + op2</code> 的行为就是

</p><pre>     function add_event (op1, op2)
       local o1, o2 = tonumber(op1), tonumber(op2)
       if o1 and o2 then  -- 两个操作数都是数字？
         return o1 + o2   -- 这里的 '+' 是原生的 'add'
       else  -- 至少一个操作数不是数字时
         local h = getbinhandler(op1, op2, "__add")
         if h then
           -- 以两个操作数来调用处理器
           return h(op1, op2)
         else  -- 没有处理器：缺省行为
           error(···)
         end
       end
     end
</pre><p>
</p></li>

<li><b>"sub":</b>
<code>-</code> 操作。

其行为类似于 "add" 操作。
</li>

<li><b>"mul":</b>
<code>*</code> 操作。

其行为类似于 "add" 操作。
</li>

<li><b>"div":</b>
<code>/</code> 操作。

其行为类似于 "add" 操作。
</li>

<li><b>"mod":</b>
<code>%</code> 操作。

其行为类似于 "add" 操作，
它的原生操作是这样的
<code>o1 - floor(o1/o2)*o2</code>
</li>

<li><b>"pow":</b>
<code>^</code> （幂）操作。

其行为类似于 "add" 操作，
它的原生操作是调用 <code>pow</code> 函数（通过 C math 库）。
</li>

<li><b>"unm":</b>
一元 <code>-</code> 操作。


<pre>     function unm_event (op)
       local o = tonumber(op)
       if o then  -- 操作数是数字？
         return -o  -- 这里的 '-' 是一个原生的 'unm'
       else  -- 操作数不是数字。
         -- 尝试从操作数中得到处理器
         local h = metatable(op).__unm
         if h then
           -- 以操作数为参数调用处理器
           return h(op)
         else  -- 没有处理器：缺省行为
           error(···)
         end
       end
     end
</pre><p>
</p></li>

<li><b>"concat":</b>
<code>..</code> （连接）操作，


<pre>     function concat_event (op1, op2)
       if (type(op1) == "string" or type(op1) == "number") and
          (type(op2) == "string" or type(op2) == "number") then
         return op1 .. op2  -- 原生字符串连接
       else
         local h = getbinhandler(op1, op2, "__concat")
         if h then
           return h(op1, op2)
         else
           error(···)
         end
       end
     end
</pre><p>
</p></li>

<li><b>"len":</b>
<code>#</code> 操作。


<pre>     function len_event (op)
       if type(op) == "string" then
         return strlen(op)         -- 原生的取字符串长度
       elseif type(op) == "table" then
         return #op                -- 原生的取 table 长度
       else
         local h = metatable(op).__len
         if h then
           -- 调用操作数的处理器
           return h(op)
         else  -- 没有处理器：缺省行为
           error(···)
         end
       end
     end
</pre><p>
关于 table 的长度参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">§2.5.5</a> 。
</p></li>

<li><b>"eq":</b>
<code>==</code> 操作。

函数 <code>getcomphandler</code> 定义了 Lua 怎样选择一个处理器来作比较操作。
元方法仅仅在参于比较的两个对象类型相同且有对应操作相同的元方法时才起效。

<pre>     function getcomphandler (op1, op2, event)
       if type(op1) ~= type(op2) then return nil end
       local mm1 = metatable(op1)[event]
       local mm2 = metatable(op2)[event]
       if mm1 == mm2 then return mm1 else return nil end
     end
</pre><p>
"eq" 事件按如下方式定义：

</p><pre>     function eq_event (op1, op2)
       if type(op1) ~= type(op2) then  -- 不同的类型？
         return false   -- 不同的对象
       end
       if op1 == op2 then   -- 原生的相等比较结果？
         return true   -- 对象相等
       end
       -- 尝试使用元方法
       local h = getcomphandler(op1, op2, "__eq")
       if h then
         return h(op1, op2)
       else
         return false
       end
     end
</pre><p>
<code>a ~= b</code> 等价于 <code>not (a == b)</code> 。
</p></li>

<li><b>"lt":</b>
<code>&lt;</code> 操作。


<pre>     function lt_event (op1, op2)
       if type(op1) == "number" and type(op2) == "number" then
         return op1 &lt; op2   -- 数字比较
       elseif type(op1) == "string" and type(op2) == "string" then
         return op1 &lt; op2   -- 字符串按逐字符比较
       else
         local h = getcomphandler(op1, op2, "__lt")
         if h then
           return h(op1, op2)
         else
           error(···);
         end
       end
     end
</pre><p>
<code>a &gt; b</code> 等价于 <code>b &lt; a</code>.
</p></li>

<li><b>"le":</b>
<code>&lt;=</code> 操作。


<pre>     function le_event (op1, op2)
       if type(op1) == "number" and type(op2) == "number" then
         return op1 &lt;= op2   -- 数字比较
       elseif type(op1) == "string" and type(op2) == "string" then
         return op1 &lt;= op2   -- 字符串按逐字符比较
       else
         local h = getcomphandler(op1, op2, "__le")
         if h then
           return h(op1, op2)
         else
           h = getcomphandler(op1, op2, "__lt")
           if h then
             return not h(op2, op1)
           else
             error(···);
           end
         end
       end
     end
</pre><p>
<code>a &gt;= b</code> 等价于 <code>b &lt;= a</code> 。
注意，如果元方法 "le" 没有提供，Lua 就尝试 "lt" ，
它假定 <code>a &lt;= b</code> 等价于 <code>not (b &lt; a)</code> 。
</p></li>

<li><b>"index":</b>
取下标操作用于访问 <code>table[key]</code> 。


<pre>     function gettable_event (table, key)
       local h
       if type(table) == "table" then
         local v = rawget(table, key)
         if v ~= nil then return v end
         h = metatable(table).__index
         if h == nil then return nil end
       else
         h = metatable(table).__index
         if h == nil then
           error(···);
         end
       end
       if type(h) == "function" then
         return h(table, key)      -- 调用处理器
       else return h[key]          -- 或是重复上述操作
       end
     end
</pre><p>
</p></li>

<li><b>"newindex":</b>
赋值给指定下标 <code>table[key] = value</code> 。


<pre>     function settable_event (table, key, value)
       local h
       if type(table) == "table" then
         local v = rawget(table, key)
         if v ~= nil then rawset(table, key, value); return end
         h = metatable(table).__newindex
         if h == nil then rawset(table, key, value); return end
       else
         h = metatable(table).__newindex
         if h == nil then
           error(···);
         end
       end
       if type(h) == "function" then
         return h(table, key,value)    -- 调用处理器
       else h[key] = value             -- 或是重复上述操作
       end
     end
</pre><p>
</p></li>

<li><b>"call":</b>
当 Lua 调用一个值时调用。


<pre>     function function_event (func, ...)
       if type(func) == "function" then
         return func(...)   -- 原生的调用
       else
         local h = metatable(func).__call
         if h then
           return h(func, ...)
         else
           error(···)
         end
       end
     end
</pre><p>
</p></li>

</ul>




<h2>2.9 - <a name="2.9">环境</a></h2>

<p>
类型为 thread ，function ，以及 userdata 
的对象，除了 metatable 外还可以用另外一个与之关联的被称作
它们的环境的一个表，
像 metatable 一样，环境也是一个常规的 table ，多个对象可以共享
同一个环境。

</p><p>
userdata 的环境在 Lua 中没有意义。
这个东西只是为了在程序员想把一个表关联到一个 userdata 上时提供便利。

</p><p>
关联在线程上的环境被称作全局环境。
全局环境被用作它其中的线程以及线程创建的非嵌套函数
（通过 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-loadfile"><code>loadfile</code></a> ， <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-loadstring"><code>loadstring</code></a> 或是
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-load"><code>load</code></a> ）的缺省环境。
而且它可以被 C 代码直接访问（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.3">§3.3</a>）。


</p><p>
关联在 C 函数上的环境可以直接被 C 代码访问（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.3">§3.3</a>）。
它们会作为这个 C 函数中创建的其它函数的缺省环境。


</p><p>
关联在 Lua 函数上的环境用来接管在函数内对全局变量（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.3">§2.3</a>）的所有访问。
它们也会作为这个函数内创建的其它函数的缺省环境。

</p><p>
你可以通过调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setfenv"><code>setfenv</code></a> 来改变一个 Lua 函数
或是正在运行中的线程的环境。
而想操控其它对象（userdata、C 函数、其它线程）的环境的话，就必须使用 C API 。



</p><h2>2.10 - <a name="2.10">垃圾收集</a></h2>

<p>
Lua 提供了一个自动的内存管理。
这就是说你不需要关心创建新对象的分配内存操作，也不需要在这些对象不再需要时的主动释放内存。
Lua 通过运行一个垃圾收集器来自动管理内存，以此一遍又一遍的回收死掉的对象
（这是指 Lua 中不再访问的到的对象）占用的内存。
Lua 中所有对象都被自动管理，包括：
table, userdata、 函数、线程、和字符串。


</p><p>
Lua 实现了一个增量标记清除的收集器。
它用两个数字来控制垃圾收集周期：
<em>garbage-collector pause</em> 和 <em>garbage-collector step multiplier</em> 。


</p><p>
garbage-collector pause 控制了收集器在开始一个新的收集周期之前要等待多久。
随着数字的增大就导致收集器工作工作的不那么主动。
小于 1 的值意味着收集器在新的周期开始时不再等待。
当值为 2 的时候意味着在总使用内存数量达到原来的两倍时再开启新的周期。

</p><p>
step multiplier 控制了收集器相对内存分配的速度。
更大的数字将导致收集器工作的更主动的同时，也使每步收集的尺寸增加。
小于 1 的值会使收集器工作的非常慢，可能导致收集器永远都结束不了当前周期。
缺省值为 2 ，这意味着收集器将以内存分配器的两倍速运行。


</p><p>
你可以通过在 C 中调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_gc"><code>lua_gc</code></a> 或是在 Lua 中调用 
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-collectgarbage"><code>collectgarbage</code></a> 来改变这些数字。
两者都接受百分比数值（因此传入参数 100 意味着实际值 1 ）。
通过这些函数，你也可以直接控制收集器（例如，停止或是重启）。


</p><h3>2.10.1 - <a name="2.10.1">垃圾收集的元方法</a></h3>

<p>
使用 C API　，
你可以给 userdata （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）设置一个垃圾收集的元方法。
这个元方法也被称为结束子。
结束子允许你用额外的资源管理器和 Lua 的内存管理器协同工作
（比如关闭文件、网络连接、或是数据库连接，也可以说释放你自己的内存）。

</p><p>
一个 userdata 可被回收，若它的 metatable 中有 <code>__gc</code> 这个域　，
垃圾收集器就不立即收回它。
取而代之的是，Lua 把它们放到一个列表中。
最收集结束后，Lua 针对列表中的每个 userdata 执行了下面这个函数的等价操作：

</p><pre>     function gc_event (udata)
       local h = metatable(udata).__gc
       if h then
         h(udata)
       end
     end
</pre>

<p>
在每个垃圾收集周期的结尾，每个在当前周期被收集起来的 userdata 的结束子会以
它们构造时的逆序依次调用。
也就是说，收集列表中，最后一个在程序中被创建的 userdata 的
结束子会被第一个调用。


</p><h3>2.10.2 - <a name="2.10.2">Weak Table（弱表）</a></h3>

<p>
<em>weak table</em> 是一个这样的 table，它其中的元素都被弱引用。
弱引用将被垃圾收集器忽略掉，
换句话说，
如果对一个对象的引用只有弱引用，
垃圾收集器将回收这个对象。

</p><p>
weak table 的键和值都可以是 weak 的。
如果一个 table 只有键是 weak 的，那么将运行收集器回收它们的键，
但是会阻止回收器回收对应的值。
而一个 table 的键和值都是 weak 时，就即允许收集器回收键又允许收回值。
任何情况下，如果键和值中任一个被回收了，整个键值对就会从 table 中拿掉。
table 的 weak 特性可以通过在它的 metatable 中设置 <code>__mode</code> 域来改变。
如果 <code>__mode</code> 域中是一个包含有字符 '<code>k</code>' 的字符串时，
table 的键就是 weak 的。
如果 <code>__mode</code> 域中是一个包含有字符 '<code>v</code>' 的字符串时，
table 的值就是 weak 的。

</p><p>
在你把一个 table 当作一个 metatable 使用之后，
就不能再修改 <code>__mode</code> 域的值。
否则，受这个 metatable 控制的 table 的 weak 行为就成了未定义的。


</p><h2>2.11 - <a name="2.11">Coroutine （协同例程）</a></h2>

<p>
Lua 支持 coroutine ，这个东西也被称为协同式多线程 (<em>collaborative multithreading</em>)　。
Lua 为每个 coroutine 提供一个独立的运行线路。
然而和多线程系统中的线程不同，coroutine 只在显式的调用了 yield 函数时才会挂起。

</p><p>
创建一个 coroutine 需要调用一次 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.create"><code>coroutine.create</code></a> 。
它只接收单个参数，这个参数是 coroutine 的主函数。
<code>create</code> 函数仅仅创建一个新的 coroutine 然后返回它的控制器
（一个类型为 <em>thread</em> 的对象）；
它并不会启动 coroutine 的运行。


</p><p>
当你第一次调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 时，
所需传入的第一个参数就是 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.create"><code>coroutine.create</code></a> 的返回值。
这时，coroutine 从主函数的第一行开始运行。
接下来传入 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 的参数将被传进 coroutine 的主函数。
在 coroutine 开始运行后，它讲运行到自身终止或是遇到一个 <em>yields</em> 。


</p><p>
coroutine 可以通过两种方式来终止运行：
一种是正常退出，指它的主函数返回（最后一条指令被运行后，无论有没有显式的返回指令）;
另一种是非正常退出，它发生在未保护的错误发生的时候。
第一种情况中， <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 返回 <b>true</b> ，
接下来会跟着 coroutine 主函数的一系列返回值。
第二种发生错误的情况下， <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 返回 <b>false</b> ，
紧接着是一条错误信息。

</p><p>
coroutine 中切换出去，可以调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.yield"><code>coroutine.yield</code></a>。
当 coroutine 切出，与之配合的 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 就立即返回，
甚至在 yield 发生在内层的函数调用中也可以（就是说，
这不限于发生在主函数中，也可以是主函数直接或间接调用的某个函数里）。
在 yield 的情况下，<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 也是返回 <b>true</b>，
紧跟着那些被传入 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.yield"><code>coroutine.yield</code></a> 的参数。
等到下次你在继续同样的 coroutine ，将从调用 yield 的断点处运行下去。
断点处 yield 的返回值将是 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 传入的参数。


</p><p>
类似 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.create"><code>coroutine.create</code></a> ，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.wrap"><code>coroutine.wrap</code></a> 这个函数也将创建一个 coroutine ，
但是它并不返回 coroutine 本身，而是返回一个函数取而代之。一旦你调用这个返回函数，就会切入 coroutine 运行。
所有传入这个函数的参数等同于传入 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 的参数。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.wrap"><code>coroutine.wrap</code></a> 会返回所有应该由除第一个（错误代码的那个布尔量）
之外的由 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 返回的值。
和 <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> 不同，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.wrap"><code>coroutine.wrap</code></a> 不捕获任何错误；
所有的错误都应该由调用者自己传递。


</p><p>
看下面这段代码展示的一个例子：

</p><pre>     function foo (a)
       print("foo", a)
       return coroutine.yield(2*a)
     end
     
     co = coroutine.create(function (a,b)
           print("co-body", a, b)
           local r = foo(a+1)
           print("co-body", r)
           local r, s = coroutine.yield(a+b, a-b)
           print("co-body", r, s)
           return b, "end"
     end)
            
     print("main", coroutine.resume(co, 1, 10))
     print("main", coroutine.resume(co, "r"))
     print("main", coroutine.resume(co, "x", "y"))
     print("main", coroutine.resume(co, "x", "y"))
</pre><p>
当你运行它，将得到如下输出结果：

</p><pre>     co-body 1       10
     foo     2
     
     main    true    4
     co-body r
     main    true    11      -9
     co-body x       y
     main    true    10      end
     main    false   cannot resume dead coroutine
</pre>


<h1>3 - <a name="3">程序接口（API）</a></h1>

<p>

这个部分描述了 Lua 的 C API ，
也就是宿主程序跟 Lua 通讯用的一组 C 函数。
所有的 API 函数按相关的类型以及常量都声明在头文件
<a name="pdf-lua.h"><code>lua.h</code></a> 中。


</p><p>
虽然我们说的是“函数”，但一部分简单的 API 是以宏的形式提供的。
所有的这些宏都只使用它们的参数一次
（除了第一个参数，也就是 lua 状态机），
因此你不需担心这些宏的展开会引起一些副作用。


</p><p>
在所有的 C 库中，Lua API 函数都不去检查参数的有效性和坚固性。
然而，你可以在编译 Lua 时加上打开一个宏开关来
开启 <code>luaconf.h</code> 文件中的宏 <a name="pdf-luai_apicheck"><code>luai_apicheck</code></a>
以改变这个行为。

</p><h2>3.1 - <a name="3.1">堆栈</a></h2>

<p>
Lua 使用一个虚拟栈来和 C 传递值。
栈上的的每个元素都是一个 Lua 值
（<b>nil</b>，数字，字符串，等等）。


</p><p>
无论何时 Lua 调用 C，被调用的函数都得到一个新的栈，
这个栈独立于 C 函数本身的堆栈，也独立于以前的栈。
（译注：在 C 函数里，用 Lua API 不能访问到 Lua 状态机中本次调用之外的堆栈中的数据）
它里面包含了 Lua 传递给 C 函数的所有参数，
而 C 函数则把要返回的结果也放入堆栈以返回给调用者
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_CFunction"><code>lua_CFunction</code></a>）。


</p><p>
方便起见，所有针对栈的 API 查询操作都不严格遵循栈的操作规则。
而是可以用一个索引来指向栈上的任何元素：
正的索引指的是栈上的绝对位置（从一开始）；
负的索引则指从栈顶开始的偏移量。
更详细的说明一下，如果堆栈有 n 个元素，
那么索引 1 表示第一个元素（也就是最先被压入堆栈的元素）
而索引 n 则指最后一个元素；
索引 -1 也是指最后一个元素（即栈顶的元素），
索引 -n 是指第一个元素。
如果索引在 1 到栈顶之间（也就是，<code>1 ≤ abs(index) ≤ top</code>）
我们就说这是个有效的索引。


</p><h2>3.2 - <a name="3.2">堆栈尺寸</a></h2>

<p>
当你使用 Lua API 时，就有责任保证其坚固性。
特别需要注意的是，你有责任控制不要堆栈溢出。
你可以使用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_checkstack"><code>lua_checkstack</code></a> 这个函数来扩大可用堆栈的尺寸。

</p><p>
无论何时 Lua 调用 C ，
它都只保证 <a name="pdf-LUA_MINSTACK"><code>LUA_MINSTACK</code></a> 这么多的堆栈空间可以使用。
<code>LUA_MINSTACK</code> 一般被定义为 20　，
因此，只要你不是不断的把数据压栈，通常你不用关心堆栈大小。


</p><p>
所有的查询函数都可以接收一个索引，只要这个索引是任何栈提供的空间中的值。
栈能提供的最大空间是通过 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_checkstack"><code>lua_checkstack</code></a> 来设置的。
这些索引被称作可接受的索引，通常我们把它定义为：

</p><pre>     (index &lt; 0 &amp;&amp; abs(index) &lt;= top) ||
     (index &gt; 0 &amp;&amp; index &lt;= stackspace)
</pre><p>
注意，0 永远都不是一个可接受的索引。（译注：下文中凡提到的索引，没有特别注明的话，都指可接受的索引。）


</p><h2>3.3 - <a name="3.3">伪索引</a></h2>

<p>
除了特别声明外，任何一个函数都可以接受另一种有效的索引，它们被称作“伪索引”。
这个可以帮助 C 代码访问一些并不在栈上的 Lua 值。
伪索引被用来访问线程的环境，函数的环境，注册表，还有 C 函数的 upvalue
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.4">§3.4</a>）。


</p><p>
线程的环境（也就是全局变量放的地方）通常在伪索引 <a name="pdf-LUA_GLOBALSINDEX"><code>LUA_GLOBALSINDEX</code></a> 处。
正在运行的 C 函数的环境则放在伪索引 <a name="pdf-LUA_ENVIRONINDEX"><code>LUA_ENVIRONINDEX</code></a> 之处。


</p><p>
你可以用常规的 table 操作来访问和改变全局变量的值，只需要指定环境表的位置。
举例而言，要访问全局变量的值，这样做：

</p><pre>     lua_getfield(L, LUA_GLOBALSINDEX, varname);
</pre>




<h2>3.4 - <a name="3.4">C Closure</a></h2>

<p>
当 C 函数被创建出来，我们有可能会把一些值关联在一起，
也就是创建一个 C closure ；
这些被关联起来的值被叫做 upvalue ，
它们可以在函数被调用的时候访问的到。
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushcclosure"><code>lua_pushcclosure</code></a>）。


</p><p>
无论何时去调用 C 函数，函数的 upvalue 都被放在指定的伪索引处。
我们可以用 <a name="lua_upvalueindex"><code>lua_upvalueindex</code></a> 这个宏来生成这些伪索引。
第一个关联到函数的值放在 <code>lua_upvalueindex(1)</code> 位置处，依次类推。
任何情况下都可以用 <code>lua_upvalueindex(<em>n</em>)</code> 产生一个 upvalue 的索引，
即使　n 大于实际的 upvalue 数量也可以。它都可以产生一个可接受但不一定有效的索引。


</p><h2>3.5 - <a name="3.5">注册表</a></h2>

<p>
Lua 提供了一个注册表，这是一个预定义出来的表，可以用来保存任何 C 代码想保存的 Lua 值。
这个表可以用伪索引 <a name="pdf-LUA_REGISTRYINDEX"><code>LUA_REGISTRYINDEX</code></a> 来定位。
任何 C 库都可以在这张表里保存数据，为了防止冲突，你需要特别小心的选择键名。
一般的用法是，你可以用一个包含你的库名的字符串做为键名，或者可以取你自己 C 代码
中的一个地址，以 light userdata 的形式做键。

</p><p>
注册表里的整数健被用于补充库中实现的引用系统的工作，一般说来不要把它们用于别的用途。


</p><h2>3.6 - <a name="3.6">C 中的错误处理</a></h2>

<p>
在内部实现中，Lua 使用了 C 的 <code>longjmp</code> 机制来处理错误。
（如果你使用 C++ 的话，也可以选择换用异常；参见 <code>luaconf.h</code> 文件。）
当 Lua 碰到任何错误（比如内存分配错误、类型错误、语法错误、还有一些运行时错误）
它都会产生一个错误出去；
也就是调用一个 long jump 。
在保护环境下，Lua 使用 <code>setjmp</code> 来设置一个恢复点；
任何发生的错误都会激活最近的一个恢复点。

</p><p>
几乎所有的 API 函数都可能产生错误，例如内存分配错误。
但下面的一些函数运行在保护环境中（也就是说它们创建了一个保护环境再在其中运行），
因此它们不会产生错误出来：
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a>, <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_close"><code>lua_close</code></a>, <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a>, and <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_cpcall"><code>lua_cpcall</code></a>。


</p><p>
在 C 函数里，你也可以通过调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_error"><code>lua_error</code></a> 产生一个错误。


</p><h2>3.7 - <a name="3.7">函数和类型</a></h2>

<p>
在这里我们按字母次序列出了所有 C API 中的函数和类型。


</p><hr><h3><a name="lua_Alloc"><code>lua_Alloc</code></a></h3>
<pre>typedef void * (*lua_Alloc) (void *ud,
                             void *ptr,
                             size_t osize,
                             size_t nsize);</pre>

<p>
Lua 状态机中使用的内存分配器函数的类型。
内存分配函数必须提供一个功能类似于 <code>realloc</code> 但又不完全相同的函数。
它的参数有
<code>ud</code> ，一个由 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> 传给它的指针；
<code>ptr</code> ，一个指向已分配出来或是将被重新分配或是要释放的内存块指针；
<code>osize</code> ，内存块原来的尺寸；
<code>nsize</code> ，新内存块的尺寸。
如果且只有 <code>osize</code> 是零时，<code>ptr</code> 为 <code>NULL</code> 。
当 <code>nsize</code> 是零，分配器必须返回 <code>NULL</code>；
如果 <code>osize</code> 不是零，分配器应当释放掉 <code>ptr</code> 指向的内存块。
当 <code>nsize</code> 不是零，若分配器不能满足请求时，分配器返回 <code>NULL</code> 。
当 <code>nsize</code> 不是零而 <code>osize</code> 是零时，分配器应该和 <code>malloc</code>
有相同的行为。
当 <code>nsize</code> 和 <code>osize</code> 都不是零时，分配器则应和 <code>realloc</code>
保持一样的行为。
Lua 假设分配器在 <code>osize &gt;= nsize</code> 时永远不会失败。

</p><p>
这里有一个简单的分配器函数的实现。
这个实现被放在补充库中，由 <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newstate"><code>luaL_newstate</code></a> 提供。

</p><pre>     static void *l_alloc (void *ud, void *ptr, size_t osize,
                                                size_t nsize) {
       (void)ud;  (void)osize;  /* not used */
       if (nsize == 0) {
         free(ptr);
         return NULL;
       }
       else
         return realloc(ptr, nsize);
     }
</pre><p>
这段代码假设 <code>free(NULL)</code> 啥也不影响，而且
<code>realloc(NULL, size)</code> 等价于 <code>malloc(size)</code>。
这两点是 ANSI C 保证的行为。


</p><hr><h3><a name="lua_atpanic"><code>lua_atpanic</code></a></h3>
<pre>lua_CFunction lua_atpanic (lua_State *L, lua_CFunction panicf);</pre>

<p>
设置一个新的 panic （恐慌） 函数，并返回前一个。


</p><p>
如果在保护环境之外发生了任何错误，
Lua 就会调用一个 panic 函数，接着调用 <code>exit(EXIT_FAILURE)</code>，
这样就开始退出宿主程序。
你的 panic 函数可以永远不返回（例如作一次长跳转）来避免程序退出。

</p><p>
panic 函数可以从栈顶取到出错信息。


</p><hr><h3><a name="lua_call"><code>lua_call</code></a></h3>
<pre>void lua_call (lua_State *L, int nargs, int nresults);</pre>

<p>
调用一个函数。


</p><p>
要调用一个函数请遵循以下协议：
首先，要调用的函数应该被压入堆栈；
接着，把需要传递给这个函数的参数按正序压栈；
这是指第一个参数首先压栈。
最后调用一下 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a>；
<code>nargs</code> 是你压入堆栈的参数个数。
当函数调用完毕后，所有的参数以及函数本身都会出栈。
而函数的返回值这时则被压入堆栈。
返回值的个数将被调整为 <code>nresults</code> 个，
除非 <code>nresults</code> 被设置成 <a name="pdf-LUA_MULTRET"><code>LUA_MULTRET</code></a>。
在这种情况下，所有的返回值都被压入堆栈中。
Lua 会保证返回值都放入栈空间中。
函数返回值将按正序压栈（第一个返回值首先压栈），
因此在调用结束后，最后一个返回值将被放在栈顶。


</p><p>
被调用函数内发生的错误将（通过 <code>longjmp</code>）一直上抛。


</p><p>
下面的例子中，这行 Lua 代码等价于在宿主程序用 C 代码做一些工作：

</p><pre>     a = f("how", t.x, 14)
</pre><p>
这里是 C 里的代码：

</p><pre>     lua_getfield(L, LUA_GLOBALSINDEX, "f");          /* 将调用的函数 */
     lua_pushstring(L, "how");                          /* 第一个参数 */
     lua_getfield(L, LUA_GLOBALSINDEX, "t");          /* table 的索引 */
     lua_getfield(L, -1, "x");         /* 压入 t.x 的值（第 2 个参数）*/
     lua_remove(L, -2);                           /* 从堆栈中移去 't' */
     lua_pushinteger(L, 14);                           /* 第 3 个参数 */
     lua_call(L, 3, 1); /* 调用 'f'，传入 3 个参数，并索取 1 个返回值 */
     lua_setfield(L, LUA_GLOBALSINDEX, "a");      /* 设置全局变量 'a' */
</pre><p>
注意上面这段代码是“平衡”的：
到了最后，堆栈恢复成原由的配置。
这是一种良好的编程习惯。


</p><hr><h3><a name="lua_CFunction"><code>lua_CFunction</code></a></h3>
<pre>typedef int (*lua_CFunction) (lua_State *L);</pre>

<p>
C 函数的类型。


</p><p>
为了正确的和 Lua 通讯，C 函数必须使用下列
定义了参数以及返回值传递方法的协议：
C 函数通过 Lua 中的堆栈来接受参数，参数以正序入栈（第一个参数首先入栈）。
因此，当函数开始的时候，
<code>lua_gettop(L)</code> 可以返回函数收到的参数个数。
第一个参数（如果有的话）在索引 1 的地方，而最后一个参数在索引 <code>lua_gettop(L)</code> 处。
当需要向 Lua 返回值的时候，C 函数只需要把它们以正序压到堆栈上（第一个返回值最先压入），
然后返回这些返回值的个数。
在这些返回值之下的，堆栈上的东西都会被 Lua 丢掉。
和 Lua 函数一样，从 Lua 中调用 C 函数也可以有很多返回值。

</p><p>
下面这个例子中的函数将接收若干数字参数，并返回它们的平均数与和：

</p><pre>     static int foo (lua_State *L) {
       int n = lua_gettop(L);    /* 参数的个数 */
       lua_Number sum = 0;
       int i;
       for (i = 1; i &lt;= n; i++) {
         if (!lua_isnumber(L, i)) {
           lua_pushstring(L, "incorrect argument");
           lua_error(L);
         }
         sum += lua_tonumber(L, i);
       }
       lua_pushnumber(L, sum/n);   /* 第一个返回值 */
       lua_pushnumber(L, sum);     /* 第二个返回值 */
       return 2;                   /* 返回值的个数 */
     }
</pre>




<hr><h3><a name="lua_checkstack"><code>lua_checkstack</code></a></h3>
<pre>int lua_checkstack (lua_State *L, int extra);</pre>

<p>
确保堆栈上至少有 <code>extra</code> 个空位。
如果不能把堆栈扩展到相应的尺寸，函数返回 false 。
这个函数永远不会缩小堆栈；
如果堆栈已经比需要的大了，那么就放在那里不会产生变化。


</p><hr><h3><a name="lua_close"><code>lua_close</code></a></h3>
<pre>void lua_close (lua_State *L);</pre>

<p>
销毁指定 Lua 状态机中的所有对象（如果有垃圾收集相关的元方法的话，会调用它们），
并且释放状态机中使用的所有动态内存。
在一些平台上，你可以不必调用这个函数，
因为当宿主程序结束的时候，所有的资源就自然被释放掉了。
另一方面，长期运行的程序，比如一个后台程序或是一个 web 服务器，
当不再需要它们的时候就应该释放掉相关状态机。这样可以避免状态机扩张的过大。


</p><hr><h3><a name="lua_concat"><code>lua_concat</code></a></h3>
<pre>void lua_concat (lua_State *L, int n);</pre>

<p>
连接栈顶的 <code>n</code> 个值，
然后将这些值出栈，并把结果放在栈顶。
如果 <code>n</code> 为 1 ，结果就是一个字符串放在栈上（即，函数什么都不做）；
如果 <code>n</code> 为 0 ，结果是一个空串。

连接依照 Lua 中创建语义完成（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.4">§2.5.4</a> ）。




</p><hr><h3><a name="lua_cpcall"><code>lua_cpcall</code></a></h3>
<pre>int lua_cpcall (lua_State *L, lua_CFunction func, void *ud);</pre>

<p>
以保护模式调用 C 函数 <code>func</code> 。
<code>func</code> 只有能从堆栈上拿到一个参数，就是包含有 <code>ud</code> 的 light userdata。
当有错误时，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_cpcall"><code>lua_cpcall</code></a> 返回和 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 相同的错误代码，
并在栈顶留下错误对象；
否则它返回零，并不会修改堆栈。
所有从 <code>func</code> 内返回的值都会被扔掉。





</p><hr><h3><a name="lua_createtable"><code>lua_createtable</code></a></h3>
<pre>void lua_createtable (lua_State *L, int narr, int nrec);</pre>

<p>
创建一个新的空 table 压入堆栈。
这个新 table 将被预分配 <code>narr</code> 个元素的数组空间
以及 <code>nrec</code> 个元素的非数组空间。
当你明确知道表中需要多少个元素时，预分配就非常有用。
如果你不知道，可以使用函数 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newtable"><code>lua_newtable</code></a>。





</p><hr><h3><a name="lua_dump"><code>lua_dump</code></a></h3>
<pre>int lua_dump (lua_State *L, lua_Writer writer, void *data);</pre>

<p>
把函数 dump 成二进制 chunk 。
函数接收栈顶的 Lua 函数做参数，然后生成它的二进制 chunk 。
若被 dump 出来的东西被再次加载，加载的结果就相当于原来的函数。
当它在产生 chunk 的时候，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> 
通过调用函数 <code>writer</code> （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Writer"><code>lua_Writer</code></a>）
来写入数据，后面的 <code>data</code> 参数会被传入 <code>writer</code> 。

</p><p>
最后一次由写入器 (writer) 返回值将作为这个函数的返回值返回；
0 表示没有错误。

</p><p>
这个函数不会把 Lua 返回弹出堆栈。



</p><hr><h3><a name="lua_equal"><code>lua_equal</code></a></h3>
<pre>int lua_equal (lua_State *L, int index1, int index2);</pre>

<p>
如果依照 Lua 中 <code>==</code> 操作符语义，索引 <code>index1</code> 和 <code>index2</code>
中的值相同的话，返回 1 。
否则返回 0 。
如果任何一个索引无效也会返回 0。



</p><hr><h3><a name="lua_error"><code>lua_error</code></a></h3>
<pre>int lua_error (lua_State *L);</pre>

<p>
产生一个 Lua 错误。
错误信息（实际上可以是任何类型的 Lua 值）必须被置入栈顶。
这个函数会做一次长跳转，因此它不会再返回。
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_error"><code>luaL_error</code></a>）。





</p><hr><h3><a name="lua_gc"><code>lua_gc</code></a></h3>
<pre>int lua_gc (lua_State *L, int what, int data);</pre>

<p>
控制垃圾收集器。


</p><p>
这个函数根据其参数 <code>what</code> 发起几种不同的任务：

</p><ul>

<li><b><code>LUA_GCSTOP</code>:</b>
停止垃圾收集器。
</li>

<li><b><code>LUA_GCRESTART</code>:</b>
重启垃圾收集器。
</li>

<li><b><code>LUA_GCCOLLECT</code>:</b>
发起一次完整的垃圾收集循环。
</li>

<li><b><code>LUA_GCCOUNT</code>:</b>
返回 Lua 使用的内存总量（以 K 字节为单位）。
</li>

<li><b><code>LUA_GCCOUNTB</code>:</b>
返回当前内存使用量除以 1024 的余数。
</li>

<li><b><code>LUA_GCSTEP</code>:</b>
发起一步增量垃圾收集。
步数由 <code>data</code> 控制（越大的值意味着越多步），
而其具体含义（具体数字表示了多少）并未标准化。
如果你想控制这个步数，必须实验性的测试
<code>data</code> 的值。
如果这一步结束了一个垃圾收集周期，返回返回 1 。
</li>

<li><b><code>LUA_GCSETPAUSE</code>:</b>
把 <code>data</code>/100 设置为 <em>garbage-collector pause</em> 的新值（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">§2.10</a>）。
函数返回以前的值。
</li>

<li><b><code>LUA_GCSETSTEPMUL</code>:</b>
把 <code>arg</code>/100 设置成 <em>step multiplier</em> （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">§2.10</a>）。
函数返回以前的值。
</li>

</ul>




<hr><h3><a name="lua_getallocf"><code>lua_getallocf</code></a></h3>
<pre>lua_Alloc lua_getallocf (lua_State *L, void **ud);</pre>

<p>
返回给定状态机的内存分配器函数。
如果 <code>ud</code> 不是 <code>NULL</code> ，Lua 把调用
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> 时传入的那个指针放入 <code>*ud</code> 。




</p><hr><h3><a name="lua_getfenv"><code>lua_getfenv</code></a></h3>
<pre>void lua_getfenv (lua_State *L, int index);</pre>

<p>
把索引处值的环境表压入堆栈。




</p><hr><h3><a name="lua_getfield"><code>lua_getfield</code></a></h3>
<pre>void lua_getfield (lua_State *L, int index, const char *k);</pre>

<p>
把 <code>t[k]</code> 值压入堆栈，
这里的 <code>t</code> 是指有效索引 <code>index</code> 指向的值。
在 Lua 中，这个函数可能触发对应 "index" 事件的元方法
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。





</p><hr><h3><a name="lua_getglobal"><code>lua_getglobal</code></a></h3>
<pre>void lua_getglobal (lua_State *L, const char *name);</pre>

<p>
把全局变量 <code>name</code> 里的值压入堆栈。
这个是用一个宏定义出来的：

</p><pre>     #define lua_getglobal(L,s)  lua_getfield(L, LUA_GLOBALSINDEX, s)
</pre>




<hr><h3><a name="lua_getmetatable"><code>lua_getmetatable</code></a></h3>
<pre>int lua_getmetatable (lua_State *L, int index);</pre>

<p>
把给定索引指向的值的元表压入堆栈。
如果索引无效，或是这个值没有元表，
函数将返回 0 并且不会向栈上压任何东西。


</p><hr><h3><a name="lua_gettable"><code>lua_gettable</code></a></h3>
<pre>void lua_gettable (lua_State *L, int index);</pre>

<p>
把 <code>t[k]</code> 值压入堆栈，
这里的 <code>t</code> 是指有效索引 <code>index</code> 指向的值，
而 <code>k</code> 则是栈顶放的值。

</p><p>
这个函数会弹出堆栈上的 key （把结果放在栈上相同位置）。
在 Lua 中，这个函数可能触发对应 "index" 事件的元方法
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。



</p><hr><h3><a name="lua_gettop"><code>lua_gettop</code></a></h3>
<pre>int lua_gettop (lua_State *L);</pre>

<p>
返回栈顶元素的索引。
因为索引是从 1 开始编号的，
所以这个结果等于堆栈上的元素个数（因此返回 0 表示堆栈为空）。



</p><hr><h3><a name="lua_insert"><code>lua_insert</code></a></h3>
<pre>void lua_insert (lua_State *L, int index);</pre>

<p>
把栈顶元素插入指定的有效索引处，
并依次移动这个索引之上的元素。
不要用伪索引来调用这个函数，
因为伪索引不是真正指向堆栈上的位置。



</p><hr><h3><a name="lua_Integer"><code>lua_Integer</code></a></h3>
<pre>typedef ptrdiff_t lua_Integer;</pre>

<p>
这个类型被用于 Lua API 接收整数值。

</p><p>
缺省时这个被定义为 <code>ptrdiff_t</code> ，
这个东西通常是机器能处理的最大整数类型。



</p><hr><h3><a name="lua_isboolean"><code>lua_isboolean</code></a></h3>
<pre>int lua_isboolean (lua_State *L, int index);</pre>

<p>
当给定索引的值类型为 boolean 时，返回 1 ，否则返回 0 。



</p><hr><h3><a name="lua_iscfunction"><code>lua_iscfunction</code></a></h3>
<pre>int lua_iscfunction (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个 C 函数时，返回 1 ，否则返回 0 。




</p><hr><h3><a name="lua_isfunction"><code>lua_isfunction</code></a></h3>
<pre>int lua_isfunction (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个函数（ C 或 Lua 函数均可）时，返回 1 ，否则返回 0 。


</p><hr><h3><a name="lua_islightuserdata"><code>lua_islightuserdata</code></a></h3>
<pre>int lua_islightuserdata (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个 light userdata 时，返回 1 ，否则返回 0 。


</p><hr><h3><a name="lua_isnil"><code>lua_isnil</code></a></h3>
<pre>int lua_isnil (lua_State *L, int index);</pre>

<p>
当给定索引的值是 <b>nil</b> 时，返回 1 ，否则返回 0 。



</p><hr><h3><a name="lua_isnumber"><code>lua_isnumber</code></a></h3>
<pre>int lua_isnumber (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个数字，或是一个可转换为数字的字符串时，返回 1 ，否则返回 0 。



</p><hr><h3><a name="lua_isstring"><code>lua_isstring</code></a></h3>
<pre>int lua_isstring (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个字符串或是一个数字（数字总能转换成字符串）时，返回 1 ，否则返回 0 。


</p><hr><h3><a name="lua_istable"><code>lua_istable</code></a></h3>
<pre>int lua_istable (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个 table 时，返回 1 ，否则返回 0 。



</p><hr><h3><a name="lua_isthread"><code>lua_isthread</code></a></h3>
<pre>int lua_isthread (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个 thread 时，返回 1 ，否则返回 0 。


</p><hr><h3><a name="lua_isuserdata"><code>lua_isuserdata</code></a></h3>
<pre>int lua_isuserdata (lua_State *L, int index);</pre>

<p>
当给定索引的值是一个 userdata （无论是完整的 userdata 还是 light userdata ）时，返回 1 ，否则返回 0 。


</p><hr><h3><a name="lua_lessthan"><code>lua_lessthan</code></a></h3>
<pre>int lua_lessthan (lua_State *L, int index1, int index2);</pre>

<p>
如果索引 <code>index1</code> 处的值小于
索引 <code>index2</code> 处的值时，返回 1 ；
否则返回 0 。
其语义遵循 Lua 中的 <code>&lt;</code> 操作符（就是说，有可能调用元方法）。
如果任何一个索引无效，也会返回 0 。


</p><hr><h3><a name="lua_load"><code>lua_load</code></a></h3>
<pre>int lua_load (lua_State *L,
              lua_Reader reader,
              void *data,
              const char *chunkname);</pre>

<p>
加载一个 Lua chunk 。
如果没有错误，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> 把一个编译好的 chunk 作为一个
Lua 函数压入堆栈。
否则，压入出错信息。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> 的返回值可以是：

</p><ul>

<li><b>0:</b> 没有错误；</li>

<li><b><a name="pdf-LUA_ERRSYNTAX"><code>LUA_ERRSYNTAX</code></a>:</b>
在预编译时碰到语法错误；</li>

<li><b><a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_ERRMEM"><code>LUA_ERRMEM</code></a>:</b>
内存分配错误。</li>

</ul>

<p>
这个函数仅仅加栽 chunk ；而不会去运行它。


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> 会自动检测 chunk 是文本的还是二进制的，
然后做对应的加载操作（参见程序 <code>luac</code>）。


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> 函数使用一个用户提供的 <code>reader</code> 函数来
读取 chunk （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Reader"><code>lua_Reader</code></a>）。
<code>data</code> 参数会被传入读取器函数。


</p><p>
<code>chunkname</code> 这个参数可以赋予 chunk 一个名字，
这个名字被用于出错信息和调试信息（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.8">§3.8</a>）。



</p><hr><h3><a name="lua_newstate"><code>lua_newstate</code></a></h3>
<pre>lua_State *lua_newstate (lua_Alloc f, void *ud);</pre>

<p>
创建的一个新的独立的状态机。
如果创建不了（因为内存问题）返回 <code>NULL</code> 。
参数 <code>f</code> 是一个分配器函数；
Lua 将通过这个函数做状态机内所有的内存分配操作。
第二个参数 <code>ud</code> ，这个指针将在每次调用分配器时被直接传入。


</p><hr><h3><a name="lua_newtable"><code>lua_newtable</code></a></h3>
<pre>void lua_newtable (lua_State *L);</pre>

<p>
创建一个空 table ，并将之压入堆栈。
它等价于 <code>lua_createtable(L, 0, 0)</code> 。





</p><hr><h3><a name="lua_newthread"><code>lua_newthread</code></a></h3>
<pre>lua_State *lua_newthread (lua_State *L);</pre>

<p>
创建一个新线程，并将其压入堆栈，
并返回维护这个线程的 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_State"><code>lua_State</code></a> 指针。
这个函数返回的新状态机共享原有状态机中的所有对象（比如一些 table），
但是它有独立的执行堆栈。

</p><p>
没有显式的函数可以用来关闭或销毁掉一个线程。
线程跟其它 Lua 对象一样是垃圾收集的条目之一。


</p><hr><h3><a name="lua_newuserdata"><code>lua_newuserdata</code></a></h3>
<pre>void *lua_newuserdata (lua_State *L, size_t size);</pre>

<p>
这个函数分配分配一块指定大小的内存块，
把内存块地址作为一个完整的 userdata 压入堆栈，并返回这个地址。


</p><p>
userdata 代表 Lua 中的 C 值。
完整的 userdata 代表一块内存。
它是一个对象（就像 table 那样的对象）：
你必须创建它，它有着自己的元表，而且它在被回收时，可以被监测到。
一个完整的 userdata 只和它自己相等（在等于的原生作用下）。

</p><p>
当 Lua 通过 <code>gc</code> 元方法回收一个完整的 userdata 时，
Lua 调用这个元方法并把 userdata 标记为已终止。
等到这个 userdata 再次被收集的时候，Lua 会释放掉相关的内存。


</p><hr><h3><a name="lua_next"><code>lua_next</code></a></h3>
<pre>int lua_next (lua_State *L, int index);</pre>

<p>
从栈上弹出一个 key（键），
然后把索引指定的表中 key-value（健值）对压入堆栈
（指定 key 后面的下一 (next) 对）。
如果表中以无更多元素，
那么 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_next"><code>lua_next</code></a> 将返回 0 （什么也不压入堆栈）。


</p><p>
典型的遍历方法是这样的：

</p><pre>     /* table 放在索引 't' 处 */
     lua_pushnil(L);  /* 第一个 key */
     while (lua_next(L, t) != 0) {
       /* 用一下 'key' （在索引 -2 处） 和 'value' （在索引 -1 处） */
       printf("%s - %s\n",
              lua_typename(L, lua_type(L, -2)),
              lua_typename(L, lua_type(L, -1)));
       /* 移除 'value' ；保留 'key' 做下一次迭代 */
       lua_pop(L, 1);
     }
</pre>

<p>
在遍历一张表的时候，
不要直接对 key 调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> ，
除非你知道这个 key 一定是一个字符串。
调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> 有可能改变给定索引位置的值；
这会对下一次调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_next"><code>lua_next</code></a> 造成影响。




</p><hr><h3><a name="lua_Number"><code>lua_Number</code></a></h3>
<pre>typedef double lua_Number;</pre>

<p>
Lua 中数字的类型。
确省是 double ，但是你可以在 <code>luaconf.h</code> 中修改它。


</p><p>
通过修改配置文件你可以改变 Lua 让它操作其它数字类型（例如：float 或是 long ）。



</p><hr><h3><a name="lua_objlen"><code>lua_objlen</code></a></h3>
<pre>size_t lua_objlen (lua_State *L, int index);</pre>

<p>
返回指定的索引处的值的长度。
对于 string ，那就是字符串的长度；
对于 table ，是取长度操作符 ('<code>#</code>') 的结果；
对于 userdata ，就是为其分配的内存块的尺寸；
对于其它值，为 0 。


</p><hr><h3><a name="lua_pcall"><code>lua_pcall</code></a></h3>
<pre>lua_pcall (lua_State *L, int nargs, int nresults, int errfunc);</pre>

<p>
以保护模式调用一个函数。


</p><p>
<code>nargs</code> 和 <code>nresults</code> 的含义与
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a> 中的相同。
如果在调用过程中没有发生错误，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 的行为和 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a> 完全一致。
但是，如果有错误发生的话，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 会捕获它，
然后把单一的值（错误信息）压入堆栈，然后返回错误码。
同 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a> 一样，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 总是把函数本身和它的参数从栈上移除。


</p><p>
如果 <code>errfunc</code> 是 0 ，
返回在栈顶的错误信息就和原始错误信息完全一致。
否则，<code>errfunc</code> 就被当成是错误处理函数在栈上的索引。
（在当前的实现里，这个索引不能是伪索引。）
在发生运行时错误时，
这个函数会被调用而参数就是错误信息。
错误处理函数的返回值将被 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 作为出错信息返回在堆栈上。


</p><p>
典型的用法中，错误处理函数被用来在出错信息上加上更多的调试信息，比如栈跟踪信息 (stack traceback) 。
这些信息在 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 返回后，因为栈已经展开 (unwound) ，
所以收集不到了。


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> 函数在调用成功时返回 0 ，
否则返回以下（定义在 <code>lua.h</code> 中的）错误代码中的一个：

</p><ul>

<li><b><a name="pdf-LUA_ERRRUN"><code>LUA_ERRRUN</code></a>:</b>
运行时错误。
</li>

<li><b><a name="pdf-LUA_ERRMEM"><code>LUA_ERRMEM</code></a>:</b>
内存分配错误。
对于这种错，Lua 调用不了错误处理函数。
</li>

<li><b><a name="pdf-LUA_ERRERR"><code>LUA_ERRERR</code></a>:</b>
在运行错误处理函数时发生的错误。
</li>

</ul>




<hr><h3><a name="lua_pop"><code>lua_pop</code></a></h3>
<pre>void lua_pop (lua_State *L, int n);</pre>

<p>
从堆栈中弹出 <code>n</code> 个元素。


</p><hr><h3><a name="lua_pushboolean"><code>lua_pushboolean</code></a></h3>
<pre>void lua_pushboolean (lua_State *L, int b);</pre>

<p>
把 <code>b</code> 作为一个 boolean 值压入堆栈。



</p><hr><h3><a name="lua_pushcclosure"><code>lua_pushcclosure</code></a></h3>
<pre>void lua_pushcclosure (lua_State *L, lua_CFunction fn, int n);</pre>

<p>
把一个新的 C closure 压入堆栈。

</p><p>
当创建了一个 C 函数后，你可以给它关联一些值，这样就是在创建一个 C closure
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.4">§3.4</a>）；
接下来无论函数何时被调用，这些值都可以被这个函数访问到。
为了将一些值关联到一个 C 函数上，
首先这些值需要先被压入堆栈（如果有多个值，第一个先压）。
接下来调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushcclosure"><code>lua_pushcclosure</code></a>
来创建出 closure 并把这个 C 函数压到堆栈上。
参数 <code>n</code> 告之函数有多少个值需要关联到函数上。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushcclosure"><code>lua_pushcclosure</code></a> 也会把这些值从栈上弹出。



</p><hr><h3><a name="lua_pushcfunction"><code>lua_pushcfunction</code></a></h3>
<pre>void lua_pushcfunction (lua_State *L, lua_CFunction f);</pre>

<p>
将一个 C 函数压入堆栈。
这个函数接收一个 C 函数指针，并将一个类型为 <code>function</code> 的 Lua 值
压入堆栈。当这个栈顶的值被调用时，将触发对应的 C 函数。

</p><p>
注册到 Lua 中的任何函数都必须遵循正确的协议来接收参数和返回值
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_CFunction"><code>lua_CFunction</code></a>）。


</p><p>
<code>lua_pushcfunction</code> 是作为一个宏定义出现的：

</p><pre>     #define lua_pushcfunction(L,f)  lua_pushcclosure(L,f,0)
</pre>




<hr><h3><a name="lua_pushfstring"><code>lua_pushfstring</code></a></h3>
<pre>const char *lua_pushfstring (lua_State *L, const char *fmt, ...);</pre>

<p>
把一个格式化过的字符串压入堆栈，然后返回这个字符串的指针。
它和 C 函数 <code>sprintf</code> 比较像，不过有一些重要的区别：

</p><ul>

<li>
摸你需要为结果分配空间：
其结果是一个 Lua 字符串，由 Lua 来关心其内存分配
（同时通过垃圾收集来释放内存）。
</li>

<li>
这个转换非常的受限。
不支持 flag ，宽度，或是指定精度。
它只支持下面这些：
'<code>%%</code>' （插入一个 '<code>%</code>'），
'<code>%s</code>' （插入一个带零终止符的字符串，没有长度限制），
'<code>%f</code>' （插入一个 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Number"><code>lua_Number</code></a>），
'<code>%p</code>' （插入一个指针或是一个十六进制数），
'<code>%d</code>' （插入一个 <code>int</code>)，
'<code>%c</code>' （把一个 <code>int</code> 作为一个字符插入）。
</li>

</ul>




<hr><h3><a name="lua_pushinteger"><code>lua_pushinteger</code></a></h3>
<pre>void lua_pushinteger (lua_State *L, lua_Integer n);</pre>

<p>
把 <code>n</code> 作为一个数字压栈。





</p><hr><h3><a name="lua_pushlightuserdata"><code>lua_pushlightuserdata</code></a></h3>
<pre>void lua_pushlightuserdata (lua_State *L, void *p);</pre>

<p>
把一个 light userdata 压栈。


</p><p>
userdata 在 Lua 中表示一个 C 值。
light userdata 表示一个指针。
它是一个像数字一样的值：
你不需要专门创建它，它也没有独立的 metatable ，
而且也不会被收集（因为从来不需要创建）。
只要表示的 C 地址相同，两个 light userdata 就相等。



</p><hr><h3><a name="lua_pushlstring"><code>lua_pushlstring</code></a></h3>
<pre>void lua_pushlstring (lua_State *L, const char *s, size_t len);</pre>

<p>
把指针 <code>s</code> 指向的长度为 <code>len</code> 的字符串压栈。
Lua 对这个字符串做一次内存拷贝（或是复用一个拷贝），
因此 <code>s</code> 处的内存在函数返回后，可以释放掉或是重用于其它用途。
字符串内可以保存有零字符。



</p><hr><h3><a name="lua_pushnil"><code>lua_pushnil</code></a></h3>
<pre>void lua_pushnil (lua_State *L);</pre>

<p>
把一个 nil 压栈。




</p><hr><h3><a name="lua_pushnumber"><code>lua_pushnumber</code></a></h3>
<pre>void lua_pushnumber (lua_State *L, lua_Number n);</pre>

<p>
把一个数字 <code>n</code> 压栈。




</p><hr><h3><a name="lua_pushstring"><code>lua_pushstring</code></a></h3>
<pre>void lua_pushstring (lua_State *L, const char *s);</pre>

<p>
把指针 <code>s</code> 指向的以零结尾的字符串压栈。
Lua 对这个字符串做一次内存拷贝（或是复用一个拷贝），
因此 <code>s</code> 处的内存在函数返回后，可以释放掉或是重用于其它用途。
字符串中不能包含有零字符；第一个碰到的零字符会认为是字符串的结束。




</p><hr><h3><a name="lua_pushthread"><code>lua_pushthread</code></a></h3>
<pre>int lua_pushthread (lua_State *L);</pre>

<p>
把 <code>L</code> 中提供的线程压栈。
如果这个线程是当前状态机的主线程的话，返回 1 。


</p><hr><h3><a name="lua_pushvalue"><code>lua_pushvalue</code></a></h3>
<pre>void lua_pushvalue (lua_State *L, int index);</pre>

<p>
把堆栈上给定有效处索引处的元素作一个拷贝压栈。



</p><hr><h3><a name="lua_pushvfstring"><code>lua_pushvfstring</code></a></h3>
<pre>const char *lua_pushvfstring (lua_State *L,
                              const char *fmt,
                              va_list argp);</pre>

<p>
等价于 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushfstring"><code>lua_pushfstring</code></a>，
不过是用 <code>va_list</code> 接收参数，而不是用可变数量的实际参数。



</p><hr><h3><a name="lua_rawequal"><code>lua_rawequal</code></a></h3>
<pre>int lua_rawequal (lua_State *L, int index1, int index2);</pre>

<p>
如果两个索引 <code>index1</code> 和 <code>index2</code> 处的值简单地相等
（不调用元方法）则返回 1 。
否则返回 0 。
如果任何一个索引无效也返回 0 。


</p><hr><h3><a name="lua_rawget"><code>lua_rawget</code></a></h3>
<pre>void lua_rawget (lua_State *L, int index);</pre>

<p>
类似于 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_gettable"><code>lua_gettable</code></a>，
但是作一次直接访问（不触发元方法）。



</p><hr><h3><a name="lua_rawgeti"><code>lua_rawgeti</code></a></h3>
<pre>void lua_rawgeti (lua_State *L, int index, int n);</pre>

<p>
把 <code>t[n]</code> 的值压栈，
这里的 <code>t</code> 是指给定索引 <code>index</code> 处的一个值。
这是一个直接访问；就是说，它不会触发元方法。


</p><hr><h3><a name="lua_rawset"><code>lua_rawset</code></a></h3>
<pre>void lua_rawset (lua_State *L, int index);</pre>

<p>
类似于 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_settable"><code>lua_settable</code></a>，
但是是作一个直接赋值（不触发元方法）。


</p><hr><h3><a name="lua_rawseti"><code>lua_rawseti</code></a></h3>
<pre>void lua_rawseti (lua_State *L, int index, int n);</pre>

<p>
等价于 <code>t[n] = v</code>，
这里的 <code>t</code> 是指给定索引 <code>index</code> 处的一个值，
而 <code>v</code> 是栈顶的值。


</p><p>
函数将把这个值弹出栈。
赋值操作是直接的；就是说，不会触发元方法。


</p><hr><h3><a name="lua_Reader"><code>lua_Reader</code></a></h3>
<pre>typedef const char * (*lua_Reader) (lua_State *L,
                                    void *data,
                                    size_t *size);</pre>

<p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> 用到的读取器函数，
每次它需要一块新的 chunk 的时候，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> 就调用读取器，
每次都会传入一个参数 <code>data</code> 。
读取器需要返回含有新的 chunk 的一块内存的指针，
并把 <code>size</code> 设为这块内存的大小。
内存块必须在下一次函数被调用之前一直存在。
读取器可以通过返回一个 <code>NULL</code> 来指示 chunk 结束。
读取器可能返回多个块，每个块可以有任意的大于零的尺寸。



</p><hr><h3><a name="lua_register"><code>lua_register</code></a></h3>
<pre>void lua_register (lua_State *L,
                   const char *name,
                   lua_CFunction f);</pre>

<p>
把 C 函数 <code>f</code> 设到全局变量 <code>name</code> 中。
它通过一个宏定义：

</p><pre>     #define lua_register(L,n,f) \
            (lua_pushcfunction(L, f), lua_setglobal(L, n))
</pre>




<hr><h3><a name="lua_remove"><code>lua_remove</code></a></h3>
<pre>void lua_remove (lua_State *L, int index);</pre>

<p>
从给定有效索引处移除一个元素，
把这个索引之上的所有元素移下来填补上这个空隙。
不能用伪索引来调用这个函数，
因为伪索引并不指向真实的栈上的位置。




</p><hr><h3><a name="lua_replace"><code>lua_replace</code></a></h3>
<pre>void lua_replace (lua_State *L, int index);</pre>

<p>
把栈顶元素移动到给定位置（并且把这个栈顶元素弹出），
不移动任何元素（因此在那个位置处的值被覆盖掉）。





</p><hr><h3><a name="lua_resume"><code>lua_resume</code></a></h3>
<pre>int lua_resume (lua_State *L, int narg);</pre>

<p>
在给定线程中启动或继续一个 coroutine 。

</p><p>
要启动一个 coroutine 的话，首先你要创建一个新线程
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newthread"><code>lua_newthread</code></a> ）；
然后把主函数和若干参数压到新线程的堆栈上；
最后调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> ，
把 <code>narg</code> 设为参数的个数。
这次调用会在 coroutine 挂起时或是结束运行后返回。
当函数返回时，堆栈中会有传给 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_yield"><code>lua_yield</code></a> 的所有值，
或是主函数的所有返回值。
如果 coroutine 切换时，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> 返回
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_YIELD"><code>LUA_YIELD</code></a> ，
而当 coroutine 结束运行且没有任何错误时，返回 0 。
如果有错则返回错误代码（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a>）。
在发生错误的情况下，
堆栈没有展开，
因此你可以使用 debug API 来处理它。
出错信息放在栈顶。
要继续运行一个 coroutine 的话，你把需要传给 <code>yield</code>
作结果的返回值压入堆栈，然后调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> 。





</p><hr><h3><a name="lua_setallocf"><code>lua_setallocf</code></a></h3>
<pre>void lua_setallocf (lua_State *L, lua_Alloc f, void *ud);</pre>

<p>
把指定状态机的分配器函数换成带上指针 <code>ud</code> 的 <code>f</code> 。



</p><hr><h3><a name="lua_setfenv"><code>lua_setfenv</code></a></h3>
<pre>int lua_setfenv (lua_State *L, int index);</pre>

<p>
从堆栈上弹出一个 table 并把它设为指定索引处值的新环境。
如果指定索引处的值即不是函数又不是线程或是 userdata ，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_setfenv"><code>lua_setfenv</code></a> 会返回 0 ，
否则返回 1 。



</p><hr><h3><a name="lua_setfield"><code>lua_setfield</code></a></h3>
<pre>void lua_setfield (lua_State *L, int index, const char *k);</pre>

<p>
做一个等价于 <code>t[k] = v</code> 的操作，
这里 <code>t</code> 是给出的有效索引 <code>index</code> 处的值，
而 <code>v</code> 是栈顶的那个值。


</p><p>
这个函数将把这个值弹出堆栈。
跟在 Lua 中一样，这个函数可能触发一个 "newindex" 事件的元方法
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。





</p><hr><h3><a name="lua_setglobal"><code>lua_setglobal</code></a></h3>
<pre>void lua_setglobal (lua_State *L, const char *name);</pre>

<p>
从堆栈上弹出一个值，并将其设到全局变量 <code>name</code> 中。
它由一个宏定义出来：

</p><pre>     #define lua_setglobal(L,s)   lua_setfield(L, LUA_GLOBALSINDEX, s)
</pre>




<hr><h3><a name="lua_setmetatable"><code>lua_setmetatable</code></a></h3>
<pre>int lua_setmetatable (lua_State *L, int index);</pre>

<p>
把一个 table 弹出堆栈，并将其设为给定索引处的值的 metatable 。



</p><hr><h3><a name="lua_settable"><code>lua_settable</code></a></h3>
<pre>void lua_settable (lua_State *L, int index);</pre>

<p>
作一个等价于 <code>t[k] = v</code> 的操作，
这里 <code>t</code> 是一个给定有效索引 <code>index</code> 处的值，
<code>v</code> 指栈顶的值，
而 <code>k</code> 是栈顶之下的那个值。


</p><p>
这个函数会把键和值都从堆栈中弹出。
和在 Lua 中一样，这个函数可能触发 "newindex" 事件的元方法
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">§2.8</a>）。





</p><hr><h3><a name="lua_settop"><code>lua_settop</code></a></h3>
<pre>void lua_settop (lua_State *L, int index);</pre>

<p>
参数允许传入任何可接受的索引以及 0 。
它将把堆栈的栈顶设为这个索引。
如果新的栈顶比原来的大，超出部分的新元素将被填为 <b>nil</b> 。
如果 <code>index</code> 为 0 ，把栈上所有元素移除。





</p><hr><h3><a name="lua_State"><code>lua_State</code></a></h3>
<pre>typedef struct lua_State lua_State;</pre>

<p>
一个不透明的结构，它保存了整个 Lua 解释器的状态。
Lua 库是完全可重入的：
它没有任何全局变量。
（译注：从 C 语法上来说，也不尽然。例如，在 table 的实现中
用了一个静态全局变量 dummynode_ ，但这在正确使用时并不影响可重入性。
只是万一你错误链接了 lua 库，不小心在同一进程空间中存在两份 lua 库实现的代码的话，
多份 dummynode_ 不同的地址会导致一些问题。）
所有的信息都保存在这个结构中。

</p><p>
这个状态机的指针必须作为第一个参数传递给每一个库函数。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> 是一个例外，
这个函数会从头创建一个 Lua 状态机。





</p><hr><h3><a name="lua_status"><code>lua_status</code></a></h3>
<pre>int lua_status (lua_State *L);</pre>

<p>
返回线程 <code>L</code> 的状态。


</p><p>
正常的线程状态是 0 。
当线程执行完毕或发生一个错误时，状态值是错误码。
如果线程被挂起，状态为 <a name="pdf-LUA_YIELD"><code>LUA_YIELD</code></a> 。





</p><hr><h3><a name="lua_toboolean"><code>lua_toboolean</code></a></h3>
<pre>int lua_toboolean (lua_State *L, int index);</pre>

<p>
把指定的索引处的的 Lua 值转换为一个 C 中的 boolean 值（ 0 或是 1 ）。
和 Lua 中做的所有测试一样，
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_toboolean"><code>lua_toboolean</code></a> 会把任何
不同于 <b>false</b> 和 <b>nil</b> 的值当作 1 返回；
否则就返回 0 。
如果用一个无效索引去调用也会返回 0 。
（如果你想只接收真正的 boolean 值，就需要使用
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_isboolean"><code>lua_isboolean</code></a> 来测试值的类型。）





</p><hr><h3><a name="lua_tocfunction"><code>lua_tocfunction</code></a></h3>
<pre>lua_CFunction lua_tocfunction (lua_State *L, int index);</pre>

<p>
把给定索引处的 Lua 值转换为一个 C 函数。
这个值必须是一个 C 函数；如果不是就返回
<code>NULL</code> 。





</p><hr><h3><a name="lua_tointeger"><code>lua_tointeger</code></a></h3>
<pre>lua_Integer lua_tointeger (lua_State *L, int idx);</pre>

<p>
把给定索引处的 Lua 值转换为 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Integer"><code>lua_Integer</code></a> 
这样一个有符号整数类型。
这个 Lua 值必须是一个数字或是一个可以转换为数字的字符串
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">§2.2.1</a>）；
否则，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tointeger"><code>lua_tointeger</code></a> 返回 0 。


</p><p>
如果数字不是一个整数，
截断小数部分的方式没有被明确定义。




</p><hr><h3><a name="lua_tolstring"><code>lua_tolstring</code></a></h3>
<pre>const char *lua_tolstring (lua_State *L, int index, size_t *len);</pre>

<p>
把给定索引处的 Lua 值转换为一个 C 字符串。
如果 <code>len</code> 不为 <code>NULL</code> ，
它还把字符串长度设到 <code>*len</code> 中。
这个 Lua 值必须是一个字符串或是一个数字；
否则返回返回 <code>NULL</code> 。
如果值是一个数字，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> 
还会把堆栈中的那个值的实际类型转换为一个字符串。
（当遍历一个表的时候，把 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a>
作用在键上，这个转换有可能导致 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_next"><code>lua_next</code></a> 弄错。）


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> 返回 Lua 状态机中
字符串的以对齐指针。
这个字符串总能保证 （ C 要求的）最后一个字符为零 ('<code>\0</code>') ，
而且它允许在字符串内包含多个这样的零。
因为 Lua 中可能发生垃圾收集，
所以不保证 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> 返回的指针，
在对应的值从堆栈中移除后依然有效。




</p><hr><h3><a name="lua_tonumber"><code>lua_tonumber</code></a></h3>
<pre>lua_Number lua_tonumber (lua_State *L, int index);</pre>

<p>
把给定索引处的 Lua 值转换为 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Number"><code>lua_Number</code></a>
这样一个 C 类型（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Number"><code>lua_Number</code></a> ）。
这个 Lua 值必须是一个数字或是一个可转换为数字的字符串
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">§2.2.1</a> ）；
否则，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tonumber"><code>lua_tonumber</code></a> 返回 0 。




</p><hr><h3><a name="lua_topointer"><code>lua_topointer</code></a></h3>
<pre>const void *lua_topointer (lua_State *L, int index);</pre>

<p>
把给定索引处的值转换为一般的 C 指针 (<code>void*</code>) 。
这个值可以是一个 userdata ，table ，thread 或是一个 function ；
否则，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_topointer"><code>lua_topointer</code></a> 返回 <code>NULL</code> 。
不同的对象有不同的指针。
不存在把指针再转回原有类型的方法。


</p><p>
这个函数通常只为产生 debug 信息用。




</p><hr><h3><a name="lua_tostring"><code>lua_tostring</code></a></h3>
<pre>const char *lua_tostring (lua_State *L, int index);</pre>

<p>
等价于 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> ，而参数 <code>len</code> 设为 <code>NULL</code> 。


</p><hr><h3><a name="lua_tothread"><code>lua_tothread</code></a></h3>
<pre>lua_State *lua_tothread (lua_State *L, int index);</pre>

<p>
把给定索引处的值转换为一个 Lua 线程（由 <code>lua_State*</code> 代表）。
这个值必须是一个线程；否则函数返回 <code>NULL</code> 。




</p><hr><h3><a name="lua_touserdata"><code>lua_touserdata</code></a></h3>
<pre>void *lua_touserdata (lua_State *L, int index);</pre>

<p>
如果给定索引处的值是一个完整的 userdata ，函数返回内存块的地址。
如果值是一个 light userdata ，那么就返回它表示的指针。
否则，返回 <code>NULL</code> 。



</p><hr><h3><a name="lua_type"><code>lua_type</code></a></h3>
<pre>int lua_type (lua_State *L, int index);</pre>

<p>
返回给定索引处的值的类型，
当索引无效时则返回 <code>LUA_TNONE</code>
（那是指一个指向堆栈上的空位置的索引）。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_type"><code>lua_type</code></a> 返回的类型是一些个在 <code>lua.h</code> 中定义的常量：
<code>LUA_TNIL</code> ，
<code>LUA_TNUMBER</code> ，
<code>LUA_TBOOLEAN</code> ，
<code>LUA_TSTRING</code> ，
<code>LUA_TTABLE</code> ，
<code>LUA_TFUNCTION</code> ，
<code>LUA_TUSERDATA</code> ，
<code>LUA_TTHREAD</code> ，
<code>LUA_TLIGHTUSERDATA</code> 。





</p><hr><h3><a name="lua_typename"><code>lua_typename</code></a></h3>
<pre>const char *lua_typename  (lua_State *L, int tp);</pre>

<p>
返回 <code>tp</code> 表示的类型名，
这个 <code>tp</code> 必须是 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_type"><code>lua_type</code></a> 可能返回的值中之一。





</p><hr><h3><a name="lua_Writer"><code>lua_Writer</code></a></h3>
<pre>typedef int (*lua_Writer) (lua_State *L,
                           const void* p,
                           size_t sz,
                           void* ud);</pre>

<p>
由 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> 用到的写入器函数。
每次 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> 产生了一块新的 chunk ，它都会调用写入器。
传入要写入的缓存 (<code>p</code>) 和它的尺寸 (<code>sz</code>) ，
还有 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> 的参数 <code>data</code> 。


</p><p>
写入器会返回一个错误码：
0 表示没有错误；
别的值均表示一个错误，并且会让 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> 停止再次调用写入器。


</p><hr><h3><a name="lua_xmove"><code>lua_xmove</code></a></h3>
<pre>void lua_xmove (lua_State *from, lua_State *to, int n);</pre>

<p>
传递 <em>同一个</em> 全局状态机下不同线程中的值。

</p><p>
这个函数会从 <code>from</code> 的堆栈中弹出 <code>n</code> 个值，
然后把它们压入 <code>to</code> 的堆栈中。





</p><hr><h3><a name="lua_yield"><code>lua_yield</code></a></h3>
<pre>int lua_yield  (lua_State *L, int nresults);</pre>

<p>
切出一个 coroutine 。

</p><p>
这个函数只能在一个 C 函数的返回表达式中调用。如下：

</p><pre>     return lua_yield (L, nresults);
</pre><p>
当一个 C 函数这样调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_yield"><code>lua_yield</code></a> ，
正在运行中的 coroutine 将从运行中挂起，
然后启动这个 coroutine 用的那次对 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> 的调用就返回了。
参数 <code>nresults</code> 指的是堆栈中需要返回的结果个数，这些返回值将被传递给
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> 。







</p><h2>3.8 - <a name="3.8">调试接口</a></h2>

<p>
Lua 没有内建的调试设施。
取而代之的是提供了一些函数接口和钩子。
利用这些接口，可以做出一些不同类型的调试器，
性能分析器，或是其它一些需要从解释器中取到“内部信息”的工具。


</p><hr><h3><a name="lua_Debug"><code>lua_Debug</code></a></h3>
<pre>typedef struct lua_Debug {
  int event;
  const char *name;           /* (n) */
  const char *namewhat;       /* (n) */
  const char *what;           /* (S) */
  const char *source;         /* (S) */
  int currentline;            /* (l) */
  int nups;                   /* (u) upvalue 个数 */
  int linedefined;            /* (S) */
  int lastlinedefined;        /* (S) */
  char short_src[LUA_IDSIZE]; /* (S) */
  /* 私有部分 */
  <em>其它域</em>
} lua_Debug;</pre>

<p>
一个用来携带活动中函数的各种信息的结构。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> 仅填写这个结构中的私有部分，
这些部分以后会用到。
调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a> 则可以填上
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Debug"><code>lua_Debug</code></a>
中有用信息的那些域。

</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Debug"><code>lua_Debug</code></a> 中的各个域有下列含义：

</p><ul>

<li><b><code>source</code>:</b>
如果函数是定义在一个字符串中，<code>source</code> 就是这个字符串。
如果函数定义在一个文件中，
<code>source</code> 是一个以 '<code>@</code>' 开头的文件名。
</li>

<li><b><code>short_src</code>:</b>
一个“可打印版本”的 <code>source</code>，用于出错信息。
</li>

<li><b><code>linedefined</code>:</b>
函数定义开始处的行号。
</li>

<li><b><code>lastlinedefined</code>:</b>
函数定义结束处的行号。
</li>

<li><b><code>what</code>:</b>
如果函数是一个 Lua 函数，则为一个字符串 <code>"Lua"</code> ；
如果是一个 C 函数，则为 <code>"C"</code>；
如果它是一个 chunk 的主体部分，则为 <code>"main"</code>；
如果是一个作了尾调用的函数，则为 <code>"tail"</code> 。
别的情况下，Lua 没有关于函数的别的信息。
</li>

<li><b><code>currentline</code>:</b>
给定函数正在执行的那一行。
当提供不了行号信息的时候，<code>currentline</code> 被设为 -1 。
</li>

<li><b><code>name</code>:</b>
给定函数的一个合理的名字。
因为 Lua 中的函数也是一个值，
所以它们没有固定的名字：
一些函数可能是全局复合变量的值，
另一些可能仅仅只是被保存在一个 table 中。
<code>lua_getinfo</code> 函数会检查函数是这样被调用的，以此来找到一个适合的名字。
如果它找不到名字，<code>name</code> 就被设置为 <code>NULL</code> 。
</li>

<li><b><code>namewhat</code>:</b>
结实 <code>name</code> 域。
<code>namewhat</code> 的值可以是
<code>"global"</code>, <code>"local"</code>, <code>"method"</code>,
<code>"field"</code>, <code>"upvalue"</code>, 或是 <code>""</code> （空串）。
这取决于函数怎样被调用。
（Lua 用空串表示其它选项都不符合）
</li>

<li><b><code>nups</code>:</b>
函数的 upvalue 的个数。
</li>

</ul>




<hr><h3><a name="lua_gethook"><code>lua_gethook</code></a></h3>
<pre>lua_Hook lua_gethook (lua_State *L);</pre>

<p>
返回当前的钩子函数。




</p><hr><h3><a name="lua_gethookcount"><code>lua_gethookcount</code></a></h3>
<pre>int lua_gethookcount (lua_State *L);</pre>

<p>
返回当前钩子记数。





</p><hr><h3><a name="lua_gethookmask"><code>lua_gethookmask</code></a></h3>
<pre>int lua_gethookmask (lua_State *L);</pre>

<p>
返回当前的钩子掩码 (mask) 。




</p><hr><h3><a name="lua_getinfo"><code>lua_getinfo</code></a></h3>
<pre>int lua_getinfo (lua_State *L, const char *what, lua_Debug *ar);</pre>

<p>
返回一个指定的函数或函数调用的信息。


</p><p>
当用于取得一次函数调用的信息时，
参数 <code>ar</code> 必须是一个有效的活动的记录。
这条记录可以是前一次调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> 得到的，
或是一个钩子 （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Hook"><code>lua_Hook</code></a>）得到的参数。


</p><p>
用于获取一个函数的信息时，可以把这个函数压入堆栈，
然后把 <code>what</code> 字符串以字符 '<code>&gt;</code>' 起头。
（这个情况下，<code>lua_getinfo</code> 从栈顶上弹出函数。）

例如，想知道函数 <code>f</code> 在哪一行定义的，
你可以下下列代码：

</p><pre>     lua_Debug ar;
     lua_getfield(L, LUA_GLOBALSINDEX, "f");  /* 取到全局变量 'f' */
     lua_getinfo(L, "&gt;S", &amp;ar);
     printf("%d\n", ar.linedefined);
</pre>

<p>
<code>what</code> 字符串中的每个字符都筛选出结构 <code>ar</code>
结构中一些域用于填充，或是把一个值压入堆栈：

</p><ul>

<li><b>'<code>n</code>':</b> 填充 <code>name</code> 及 <code>namewhat</code> 域；
</li>

<li><b>'<code>S</code>':</b>
填充 <code>source</code>， <code>short_src</code>，
<code>linedefined</code>， <code>lastlinedefined</code>，以及 <code>what</code> 域；
</li>

<li><b>'<code>l</code>':</b> 填充 <code>currentline</code> 域；
</li>

<li><b>'<code>u</code>':</b> 填充 <code>nups</code> 域；
</li>

<li><b>'<code>f</code>':</b>
把正在运行中指定级别处函数压入堆栈；
（译注：一般用于获取函数调用中的信息，
级别是由 ar 中的私有部分来提供。
如果用于获取静态函数，那么就直接把指定函数重新压回堆栈，
但这样做通常无甚意义。） 

</li>

<li><b>'<code>L</code>':</b>
压一个 table 入栈，这个 table 中的整数索引用于描述函数中哪些行是有效行。
（有效行指有实际代码的行，
即你可以置入断点的行。
无效行包括空行和只有注释的行。）
</li>

</ul>

<p>
这个函数出错会返回 0
（例如，<code>what</code> 中有一个无效选项）。


</p><hr><h3><a name="lua_getlocal"><code>lua_getlocal</code></a></h3>
<pre>const char *lua_getlocal (lua_State *L, lua_Debug *ar, int n);</pre>

<p>
从给定活动记录中获取一个局部变量的信息。
参数 <code>ar</code> 必须是一个有效的活动的记录。
这条记录可以是前一次调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> 得到的，
或是一个钩子 （参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Hook"><code>lua_Hook</code></a>）得到的参数。
索引 <code>n</code> 用于选择要检阅哪个局部变量
（ 1 表示第一个参数或是激活的第一个局部变量，以此类推，直到最后一个局部变量）。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getlocal"><code>lua_getlocal</code></a> 把变量的值压入堆栈并返回它的名字。


</p><p>
以 '(' （正小括号）开始的变量指内部变量
（循环控制变量，临时变量，C 函数局部变量）。


</p><p>
当索引大于局部变量的个数时，返回 <code>NULL</code> （什么也不压入）。



</p><hr><h3><a name="lua_getstack"><code>lua_getstack</code></a></h3>
<pre>int lua_getstack (lua_State *L, int level, lua_Debug *ar);</pre>

<p>
获取解释器的运行时栈的信息。


</p><p>
这个函数用正在运行中的给定级别处的函数的活动记录来填写
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Debug"><code>lua_Debug</code></a> 结构的一部分。
0 级表示当前运行的函数，
而 n+1 级处的函数就是调用第 n 级函数的那一个。
如果没有错误，<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> 返回 1 ；
当调用传入的级别大于堆栈深度的时候，返回 0 。



</p><hr><h3><a name="lua_getupvalue"><code>lua_getupvalue</code></a></h3>
<pre>const char *lua_getupvalue (lua_State *L, int funcindex, int n);</pre>

<p>
获取一个 closure 的 upvalue 信息。
（对于 Lua 函数，upvalue 是函数需要使用的外部局部变量，
因此这些变量被包含在 closure 中。）
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getupvalue"><code>lua_getupvalue</code></a> 获取第 <code>n</code> 个 upvalue ，
把这个 upvalue 的值压入堆栈，并且返回它的名字。
<code>funcindex</code> 指向堆栈上 closure 的位置。
（ 因为 upvalue 在整个函数中都有效，所以它们没有特别的次序。
因此，它们以字母次序来编号。）


</p><p>
当索引号比 upvalue 数量大的时候，返回 <code>NULL</code> （而且不会压入任何东西）
对于 C 函数，这个函数用空串 <code>""</code> 表示所有 upvalue 的名字。


</p><hr><h3><a name="lua_Hook"><code>lua_Hook</code></a></h3>
<pre>typedef void (*lua_Hook) (lua_State *L, lua_Debug *ar);</pre>

<p>
用于调试的钩子函数类型。

</p><p>
无论何时钩子被调用，它的参数 <code>ar</code> 中的 <code>event</code> 域
都被设为触发钩子的事件。
Lua 把这些事件定义为以下常量：
<a name="pdf-LUA_HOOKCALL"><code>LUA_HOOKCALL</code></a>， <a name="pdf-LUA_HOOKRET"><code>LUA_HOOKRET</code></a>,
<a name="pdf-LUA_HOOKTAILRET"><code>LUA_HOOKTAILRET</code></a>， <a name="pdf-LUA_HOOKLINE"><code>LUA_HOOKLINE</code></a>，
and <a name="pdf-LUA_HOOKCOUNT"><code>LUA_HOOKCOUNT</code></a>。
除此之外，对于 line 事件，<code>currentline</code> 域也被设置。
要想获得 <code>ar</code> 中的其他域，
钩子必须调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a>。
对于返回事件，<code>event</code> 的正常值可能是 <code>LUA_HOOKRET</code>，
或者是 <code>LUA_HOOKTAILRET</code> 。
对于后一种情况，Lua 会对一个函数做的尾调用也模拟出一个返回事件出来；
对于这个模拟的返回事件，调用 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a> 没有什么作用。

</p><p>
当 Lua 运行在一个钩子内部时，它将屏蔽掉其它对钩子的调用。
也就是说，如果一个钩子函数内再调回 Lua 来执行一个函数或是一个 chunk ，
这个执行操作不会触发任何的钩子。



</p><hr><h3><a name="lua_sethook"><code>lua_sethook</code></a></h3>
<pre>int lua_sethook (lua_State *L, lua_Hook f, int mask, int count);</pre>

<p>
设置一个调试用钩子函数。

</p><p>
参数 <code>f</code> 是钩子函数。
<code>mask</code> 指定在哪些事件时会调用：
它由下列一组位常量构成
<a name="pdf-LUA_MASKCALL"><code>LUA_MASKCALL</code></a>，
<a name="pdf-LUA_MASKRET"><code>LUA_MASKRET</code></a>，
<a name="pdf-LUA_MASKLINE"><code>LUA_MASKLINE</code></a>，
以及 <a name="pdf-LUA_MASKCOUNT"><code>LUA_MASKCOUNT</code></a>。
参数 <code>count</code> 只在 mask 中包含有 <code>LUA_MASKCOUNT</code> 才有意义。
对于每个事件，钩子被调用的情况解释如下：

</p><ul>

<li><b>call hook:</b> 在解释器调用一个函数时被调用。
钩子将于 Lua 进入一个新函数后，函数获取参数前被调用。
</li>

<li><b>return hook:</b> 在解释器从一个函数中返回时调用。
钩子将于 Lua 离开函数之前的那一刻被调用。
你无权访问被函数返回出去的那些值。
<small>（译注：原文 (You have no access to the values to be returned by the function) 如此。
但“无权访问”一词值得商榷。
某些情况下你可以访问到一些被命名为 (*temporary) 的局部变量，
那些索引被排在最后的 (*temporary) 变量指的就是返回值。
但是由于 Lua 对特殊情况做了一些优化，比如直接返回一个被命名的局部变量，
那么就找不到对应的 (*temporary) 变量了。本质上，返回值一定存在于此刻的局部变量中，
并且可以访问它，只是无法确定是哪些罢了。至于这个时候函数体内的其它局部变量，
是不保证有效的。进入 return hook 的那一刻起，实际已经退出函数内部的运行环节，
返回值占用的局部变量空间以后的部分，都有可能因 hook 本身复用它们而改变。）
</small>
</li>

<li><b>line hook:</b> 在解释器准备开始执行新的一行代码时，
或是跳转到这行代码中时（即使在同一行内跳转）被调用。
（这个事件仅仅在 Lua 执行一个 Lua 函数时发生。）
</li>

<li><b>count hook:</b> 在解释器每执行 <code>count</code> 条指令后被调用。
（这个事件仅仅在 Lua 执行一个 Lua 函数时发生。）
</li>

</ul>

<p>
钩子可以通过设置 <code>mask</code> 为零屏蔽。




</p><hr><h3><a name="lua_setlocal"><code>lua_setlocal</code></a></h3>
<pre>const char *lua_setlocal (lua_State *L, lua_Debug *ar, int n);</pre>

<p>
设置给定活动记录中的局部变量的值。
参数 <code>ar</code> 与 <code>n</code> 和 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getlocal"><code>lua_getlocal</code></a> 中的一样
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getlocal"><code>lua_getlocal</code></a>）。
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_setlocal"><code>lua_setlocal</code></a> 把栈顶的值赋给变量然后返回变量的名字。
它会将值从栈顶弹出。


</p><p>
当索引大于局部变量的个数时，返回 <code>NULL</code> （什么也不弹出）。




</p><hr><h3><a name="lua_setupvalue"><code>lua_setupvalue</code></a></h3>
<pre>const char *lua_setupvalue (lua_State *L, int funcindex, int n);</pre>

<p>
设置 closure 的 upvalue 的值。
它把栈顶的值弹出并赋于 upvalue 并返回 upvalue 的名字。
参数 <code>funcindex</code> 与 <code>n</code> 和 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getupvalue"><code>lua_getupvalue</code></a> 中的一样
（参见 <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getupvalue"><code>lua_getupvalue</code></a>）。


</p><p>
当索引大于 upvalue 的个数时，返回 <code>NULL</code> （什么也不弹出）。





</p><h1>4 - <a name="4">The Auxiliary Library</a></h1>

<p>

The <em>auxiliary library</em> provides several convenient functions
to interface C with Lua.
While the basic API provides the primitive functions for all 
interactions between C and Lua,
the auxiliary library provides higher-level functions for some
common tasks.


</p><p>
All functions from the auxiliary library
are defined in header file <code>lauxlib.h</code> and
have a prefix <code>luaL_</code>.


</p><p>
All functions in the auxiliary library are built on
top of the basic API,
and so they provide nothing that cannot be done with this API.


</p><p>
Several functions in the auxiliary library are used to
check C&nbsp;function arguments.
Their names are always <code>luaL_check*</code> or <code>luaL_opt*</code>.
All of these functions raise an error if the check is not satisfied.
Because the error message is formatted for arguments
(e.g., "<code>bad argument #1</code>"),
you should not use these functions for other stack values.



</p><h2>4.1 - <a name="4.1">Functions and Types</a></h2>

<p>
Here we list all functions and types from the auxiliary library
in alphabetical order.



</p><hr><h3><a name="luaL_addchar"><code>luaL_addchar</code></a></h3>
<pre>void luaL_addchar (luaL_Buffer *B, char c);</pre>

<p>
Adds the character <code>c</code> to the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).





</p><hr><h3><a name="luaL_addlstring"><code>luaL_addlstring</code></a></h3>
<pre>void luaL_addlstring (luaL_Buffer *B, const char *s, size_t l);</pre>

<p>
Adds the string pointed to by <code>s</code> with length <code>l</code> to
the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
The string may contain embedded zeros.





</p><hr><h3><a name="luaL_addsize"><code>luaL_addsize</code></a></h3>
<pre>void luaL_addsize (luaL_Buffer *B, size_t n);</pre>

<p>
Adds to the buffer <code>B</code> (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>)
a string of length <code>n</code> previously copied to the
buffer area (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_prepbuffer"><code>luaL_prepbuffer</code></a>).





</p><hr><h3><a name="luaL_addstring"><code>luaL_addstring</code></a></h3>
<pre>void luaL_addstring (luaL_Buffer *B, const char *s);</pre>

<p>
Adds the zero-terminated string pointed to by <code>s</code>
to the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
The string may not contain embedded zeros.





</p><hr><h3><a name="luaL_addvalue"><code>luaL_addvalue</code></a></h3>
<pre>void luaL_addvalue (luaL_Buffer *B);</pre>

<p>
Adds the value at the top of the stack
to the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
Pops the value.


</p><p>
This is the only function on string buffers that can (and must)
be called with an extra element on the stack,
which is the value to be added to the buffer.





</p><hr><h3><a name="luaL_argcheck"><code>luaL_argcheck</code></a></h3>
<pre>void luaL_argcheck (lua_State *L,
                    int cond,
                    int narg,
                    const char *extramsg);</pre>

<p>
Checks whether <code>cond</code> is true.
If not, raises an error with the following message,
where <code>func</code> is retrieved from the call stack:

</p><pre>     bad argument #&lt;narg&gt; to &lt;func&gt; (&lt;extramsg&gt;)
</pre>




<hr><h3><a name="luaL_argerror"><code>luaL_argerror</code></a></h3>
<pre>int luaL_argerror (lua_State *L, int narg, const char *extramsg);</pre>

<p>
Raises an error with the following message,
where <code>func</code> is retrieved from the call stack:

</p><pre>     bad argument #&lt;narg&gt; to &lt;func&gt; (&lt;extramsg&gt;)
</pre>

<p>
This function never returns,
but it is an idiom to use it in C&nbsp;functions
as <code>return luaL_argerror(<em>args</em>)</code>.





</p><hr><h3><a name="luaL_Buffer"><code>luaL_Buffer</code></a></h3>
<pre>typedef struct luaL_Buffer luaL_Buffer;</pre>

<p>
Type for a <em>string buffer</em>.


</p><p>
A string buffer allows C&nbsp;code to build Lua strings piecemeal.
Its pattern of use is as follows:

</p><ul>

<li>First you declare a variable <code>b</code> of type <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>.</li>

<li>Then you initialize it with a call <code>luaL_buffinit(L, &amp;b)</code>.</li>

<li>
Then you add string pieces to the buffer calling any of
the <code>luaL_add*</code> functions.
</li>

<li>
You finish by calling <code>luaL_pushresult(&amp;b)</code>.
This call leaves the final string on the top of the stack.
</li>

</ul>

<p>
During its normal operation,
a string buffer uses a variable number of stack slots.
So, while using a buffer, you cannot assume that you know where
the top of the stack is.
You can use the stack between successive calls to buffer operations
as long as that use is balanced;
that is,
when you call a buffer operation,
the stack is at the same level
it was immediately after the previous buffer operation.
(The only exception to this rule is <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_addvalue"><code>luaL_addvalue</code></a>.)
After calling <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_pushresult"><code>luaL_pushresult</code></a> the stack is back to its
level when the buffer was initialized,
plus the final string on its top.





</p><hr><h3><a name="luaL_buffinit"><code>luaL_buffinit</code></a></h3>
<pre>void luaL_buffinit (lua_State *L, luaL_Buffer *B);</pre>

<p>
Initializes a buffer <code>B</code>.
This function does not allocate any space;
the buffer must be declared as a variable
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).





</p><hr><h3><a name="luaL_callmeta"><code>luaL_callmeta</code></a></h3>
<pre>int luaL_callmeta (lua_State *L, int obj, const char *e);</pre>

<p>
Calls a metamethod.


</p><p>
If the object at index <code>obj</code> has a metatable and this
metatable has a field <code>e</code>,
this function calls this field and passes the object as its only argument.
In this case this function returns 1 and pushes onto the
stack the value returned by the call.
If there is no metatable or no metamethod,
this function returns 0 (without pushing any value on the stack).





</p><hr><h3><a name="luaL_checkany"><code>luaL_checkany</code></a></h3>
<pre>void luaL_checkany (lua_State *L, int narg);</pre>

<p>
Checks whether the function has an argument
of any type (including <b>nil</b>) at position <code>narg</code>.





</p><hr><h3><a name="luaL_checkint"><code>luaL_checkint</code></a></h3>
<pre>int luaL_checkint (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number cast to an <code>int</code>.





</p><hr><h3><a name="luaL_checkinteger"><code>luaL_checkinteger</code></a></h3>
<pre>lua_Integer luaL_checkinteger (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number cast to a <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Integer"><code>lua_Integer</code></a>.





</p><hr><h3><a name="luaL_checklong"><code>luaL_checklong</code></a></h3>
<pre>long luaL_checklong (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number cast to a <code>long</code>.





</p><hr><h3><a name="luaL_checklstring"><code>luaL_checklstring</code></a></h3>
<pre>const char *luaL_checklstring (lua_State *L, int narg, size_t *l);</pre>

<p>
Checks whether the function argument <code>narg</code> is a string
and returns this string;
if <code>l</code> is not <code>NULL</code> fills <code>*l</code>
with the string's length.





</p><hr><h3><a name="luaL_checknumber"><code>luaL_checknumber</code></a></h3>
<pre>lua_Number luaL_checknumber (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number.





</p><hr><h3><a name="luaL_checkoption"><code>luaL_checkoption</code></a></h3>
<pre>int luaL_checkoption (lua_State *L,
                      int narg,
                      const char *def,
                      const char *const lst[]);</pre>

<p>
Checks whether the function argument <code>narg</code> is a string and
searches for this string in the array <code>lst</code>
(which must be NULL-terminated).
Returns the index in the array where the string was found.
Raises an error if the argument is not a string or
if the string cannot be found.


</p><p>
If <code>def</code> is not <code>NULL</code>,
the function uses <code>def</code> as a default value when
there is no argument <code>narg</code> or if this argument is <b>nil</b>.


</p><p>
This is a useful function for mapping strings to C&nbsp;enums.
(The usual convention in Lua libraries is
to use strings instead of numbers to select options.)





</p><hr><h3><a name="luaL_checkstack"><code>luaL_checkstack</code></a></h3>
<pre>void luaL_checkstack (lua_State *L, int sz, const char *msg);</pre>

<p>
Grows the stack size to <code>top + sz</code> elements,
raising an error if the stack cannot grow to that size.
<code>msg</code> is an additional text to go into the error message.





</p><hr><h3><a name="luaL_checkstring"><code>luaL_checkstring</code></a></h3>
<pre>const char *luaL_checkstring (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a string
and returns this string.





</p><hr><h3><a name="luaL_checktype"><code>luaL_checktype</code></a></h3>
<pre>void luaL_checktype (lua_State *L, int narg, int t);</pre>

<p>
Checks whether the function argument <code>narg</code> has type <code>t</code>.





</p><hr><h3><a name="luaL_checkudata"><code>luaL_checkudata</code></a></h3>
<pre>void *luaL_checkudata (lua_State *L, int narg, const char *tname);</pre>

<p>
Checks whether the function argument <code>narg</code> is a userdata
of the type <code>tname</code> (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newmetatable"><code>luaL_newmetatable</code></a>).





</p><hr><h3><a name="luaL_dofile"><code>luaL_dofile</code></a></h3>
<pre>int luaL_dofile (lua_State *L, const char *filename);</pre>

<p>
Loads and runs the given file.
It is defined as the following macro:

</p><pre>     (luaL_loadfile(L, filename) || lua_pcall(L, 0, LUA_MULTRET, 0))
</pre><p>
It returns 0 if there are no errors
or 1 in case of errors.





</p><hr><h3><a name="luaL_dostring"><code>luaL_dostring</code></a></h3>
<pre>int luaL_dostring (lua_State *L, const char *str);</pre>

<p>
Loads and runs the given string.
It is defined as the following macro:

</p><pre>     (luaL_loadstring(L, str) || lua_pcall(L, 0, LUA_MULTRET, 0))
</pre><p>
It returns 0 if there are no errors
or 1 in case of errors.





</p><hr><h3><a name="luaL_error"><code>luaL_error</code></a></h3>
<pre>int luaL_error (lua_State *L, const char *fmt, ...);</pre>

<p>
Raises an error.
The error message format is given by <code>fmt</code>
plus any extra arguments,
following the same rules of <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushfstring"><code>lua_pushfstring</code></a>.
It also adds at the beginning of the message the file name and
the line number where the error occurred,
if this information is available.


</p><p>
This function never returns,
but it is an idiom to use it in C&nbsp;functions
as <code>return luaL_error(<em>args</em>)</code>.





</p><hr><h3><a name="luaL_getmetafield"><code>luaL_getmetafield</code></a></h3>
<pre>int luaL_getmetafield (lua_State *L, int obj, const char *e);</pre>

<p>
Pushes onto the stack the field <code>e</code> from the metatable
of the object at index <code>obj</code>.
If the object does not have a metatable,
or if the metatable does not have this field,
returns 0 and pushes nothing.





</p><hr><h3><a name="luaL_getmetatable"><code>luaL_getmetatable</code></a></h3>
<pre>void luaL_getmetatable (lua_State *L, const char *tname);</pre>

<p>
Pushes onto the stack the metatable associated with name <code>tname</code>
in the registry (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newmetatable"><code>luaL_newmetatable</code></a>).





</p><hr><h3><a name="luaL_gsub"><code>luaL_gsub</code></a></h3>
<pre>const char *luaL_gsub (lua_State *L,
                       const char *s,
                       const char *p,
                       const char *r);</pre>

<p>
Creates a copy of string <code>s</code> by replacing
any occurrence of the string <code>p</code>
with the string <code>r</code>.
Pushes the resulting string on the stack and returns it.





</p><hr><h3><a name="luaL_loadbuffer"><code>luaL_loadbuffer</code></a></h3>
<pre>int luaL_loadbuffer (lua_State *L,
                     const char *buff,
                     size_t sz,
                     const char *name);</pre>

<p>
Loads a buffer as a Lua chunk.
This function uses <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> to load the chunk in the
buffer pointed to by <code>buff</code> with size <code>sz</code>.


</p><p>
This function returns the same results as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>.
<code>name</code> is the chunk name,
used for debug information and error messages.





</p><hr><h3><a name="luaL_loadfile"><code>luaL_loadfile</code></a></h3>
<pre>int luaL_loadfile (lua_State *L, const char *filename);</pre>

<p>
Loads a file as a Lua chunk.
This function uses <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> to load the chunk in the file
named <code>filename</code>.
If <code>filename</code> is <code>NULL</code>,
then it loads from the standard input.
The first line in the file is ignored if it starts with a <code>#</code>.


</p><p>
This function returns the same results as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>,
but it has an extra error code <a name="pdf-LUA_ERRFILE"><code>LUA_ERRFILE</code></a>
if it cannot open/read the file.


</p><p>
As <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>, this function only loads the chunk;
it does not run it.





</p><hr><h3><a name="luaL_loadstring"><code>luaL_loadstring</code></a></h3>
<pre>int luaL_loadstring (lua_State *L, const char *s);</pre>

<p>
Loads a string as a Lua chunk.
This function uses <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> to load the chunk in
the zero-terminated string <code>s</code>.


</p><p>
This function returns the same results as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>.


</p><p>
Also as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>, this function only loads the chunk;
it does not run it.





</p><hr><h3><a name="luaL_newmetatable"><code>luaL_newmetatable</code></a></h3>
<pre>int luaL_newmetatable (lua_State *L, const char *tname);</pre>

<p>
If the registry already has the key <code>tname</code>,
returns 0.
Otherwise,
creates a new table to be used as a metatable for userdata,
adds it to the registry with key <code>tname</code>,
and returns 1.


</p><p>
In both cases pushes onto the stack the final value associated
with <code>tname</code> in the registry.





</p><hr><h3><a name="luaL_newstate"><code>luaL_newstate</code></a></h3>
<pre>lua_State *luaL_newstate (void);</pre>

<p>
Creates a new Lua state.
It calls <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> with an
allocator based on the standard&nbsp;C <code>realloc</code> function
and then sets a panic function (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_atpanic"><code>lua_atpanic</code></a>) that prints
an error message to the standard error output in case of fatal
errors.


</p><p>
Returns the new state,
or <code>NULL</code> if there is a memory allocation error.





</p><hr><h3><a name="luaL_openlibs"><code>luaL_openlibs</code></a></h3>
<pre>void luaL_openlibs (lua_State *L);</pre>

<p>
Opens all standard Lua libraries into the given state.





</p><hr><h3><a name="luaL_optint"><code>luaL_optint</code></a></h3>
<pre>int luaL_optint (lua_State *L, int narg, int d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number cast to an <code>int</code>.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optinteger"><code>luaL_optinteger</code></a></h3>
<pre>lua_Integer luaL_optinteger (lua_State *L,
                             int narg,
                             lua_Integer d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number cast to a <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Integer"><code>lua_Integer</code></a>.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optlong"><code>luaL_optlong</code></a></h3>
<pre>long luaL_optlong (lua_State *L, int narg, long d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number cast to a <code>long</code>.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optlstring"><code>luaL_optlstring</code></a></h3>
<pre>const char *luaL_optlstring (lua_State *L,
                             int narg,
                             const char *d,
                             size_t *l);</pre>

<p>
If the function argument <code>narg</code> is a string,
returns this string.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.


</p><p>
If <code>l</code> is not <code>NULL</code>,
fills the position <code>*l</code> with the results's length.





</p><hr><h3><a name="luaL_optnumber"><code>luaL_optnumber</code></a></h3>
<pre>lua_Number luaL_optnumber (lua_State *L, int narg, lua_Number d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optstring"><code>luaL_optstring</code></a></h3>
<pre>const char *luaL_optstring (lua_State *L,
                            int narg,
                            const char *d);</pre>

<p>
If the function argument <code>narg</code> is a string,
returns this string.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_prepbuffer"><code>luaL_prepbuffer</code></a></h3>
<pre>char *luaL_prepbuffer (luaL_Buffer *B);</pre>

<p>
Returns an address to a space of size <a name="pdf-LUAL_BUFFERSIZE"><code>LUAL_BUFFERSIZE</code></a>
where you can copy a string to be added to buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
After copying the string into this space you must call
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_addsize"><code>luaL_addsize</code></a> with the size of the string to actually add 
it to the buffer.





</p><hr><h3><a name="luaL_pushresult"><code>luaL_pushresult</code></a></h3>
<pre>void luaL_pushresult (luaL_Buffer *B);</pre>

<p>
Finishes the use of buffer <code>B</code> leaving the final string on
the top of the stack.





</p><hr><h3><a name="luaL_ref"><code>luaL_ref</code></a></h3>
<pre>int luaL_ref (lua_State *L, int t);</pre>

<p>
Creates and returns a <em>reference</em>,
in the table at index <code>t</code>,
for the object at the top of the stack (and pops the object).


</p><p>
A reference is a unique integer key.
As long as you do not manually add integer keys into table <code>t</code>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a> ensures the uniqueness of the key it returns.
You can retrieve an object referred by reference <code>r</code>
by calling <code>lua_rawgeti(L, t, r)</code>.
Function <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_unref"><code>luaL_unref</code></a> frees a reference and its associated object.


</p><p>
If the object at the top of the stack is <b>nil</b>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a> returns the constant <a name="pdf-LUA_REFNIL"><code>LUA_REFNIL</code></a>.
The constant <a name="pdf-LUA_NOREF"><code>LUA_NOREF</code></a> is guaranteed to be different
from any reference returned by <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a>.





</p><hr><h3><a name="luaL_Reg"><code>luaL_Reg</code></a></h3>
<pre>typedef struct luaL_Reg {
  const char *name;
  lua_CFunction func;
} luaL_Reg;</pre>

<p>
Type for arrays of functions to be registered by
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_register"><code>luaL_register</code></a>.
<code>name</code> is the function name and <code>func</code> is a pointer to
the function.
Any array of <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Reg"><code>luaL_Reg</code></a> must end with an sentinel entry
in which both <code>name</code> and <code>func</code> are <code>NULL</code>.





</p><hr><h3><a name="luaL_register"><code>luaL_register</code></a></h3>
<pre>void luaL_register (lua_State *L,
                    const char *libname,
                    const luaL_Reg *l);</pre>

<p>
Opens a library.


</p><p>
When called with <code>libname</code> equal to <code>NULL</code>,
it simply registers all functions in the list <code>l</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Reg"><code>luaL_Reg</code></a>) into the table on the top of the stack.


</p><p>
When called with a non-null <code>libname</code>,
<code>luaL_register</code> creates a new table <code>t</code>,
sets it as the value of the global variable <code>libname</code>,
sets it as the value of <code>package.loaded[libname]</code>,
and registers on it all functions in the list <code>l</code>.
If there is a table in <code>package.loaded[libname]</code> or in
variable <code>libname</code>,
reuses this table instead of creating a new one.


</p><p>
In any case the function leaves the table
on the top of the stack.





</p><hr><h3><a name="luaL_typename"><code>luaL_typename</code></a></h3>
<pre>const char *luaL_typename (lua_State *L, int idx);</pre>

<p>
Returns the name of the type of the value at index <code>idx</code>.





</p><hr><h3><a name="luaL_typerror"><code>luaL_typerror</code></a></h3>
<pre>int luaL_typerror (lua_State *L, int narg, const char *tname);</pre>

<p>
Generates an error with a message like the following:

</p><pre>     <em>location</em>: bad argument <em>narg</em> to '<em>func</em>' (<em>tname</em> expected, got <em>rt</em>)
</pre><p>
where <code><em>location</em></code> is produced by <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_where"><code>luaL_where</code></a>,
<code><em>func</em></code> is the name of the current function,
and <code><em>rt</em></code> is the type name of the actual argument.





</p><hr><h3><a name="luaL_unref"><code>luaL_unref</code></a></h3>
<pre>void luaL_unref (lua_State *L, int t, int ref);</pre>

<p>
Releases reference <code>ref</code> from the table at index <code>t</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a>).
The entry is removed from the table,
so that the referred object can be collected.
The reference <code>ref</code> is also freed to be used again.


</p><p>
If <code>ref</code> is <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_NOREF"><code>LUA_NOREF</code></a> or <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_REFNIL"><code>LUA_REFNIL</code></a>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_unref"><code>luaL_unref</code></a> does nothing.





</p><hr><h3><a name="luaL_where"><code>luaL_where</code></a></h3>
<pre>void luaL_where (lua_State *L, int lvl);</pre>

<p>
Pushes onto the stack a string identifying the current position
of the control at level <code>lvl</code> in the call stack.
Typically this string has the following format:

</p><pre>     <em>chunkname</em>:<em>currentline</em>:
</pre><p>
Level&nbsp;0 is the running function,
level&nbsp;1 is the function that called the running function,
etc.


</p><p>
This function is used to build a prefix for error messages.







</p><h1>5 - <a name="5">Standard Libraries</a></h1>

<p>
The standard Lua libraries provide useful functions
that are implemented directly through the C&nbsp;API.
Some of these functions provide essential services to the language
(e.g., <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-type"><code>type</code></a> and <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-getmetatable"><code>getmetatable</code></a>);
others provide access to "outside" services (e.g., I/O);
and others could be implemented in Lua itself,
but are quite useful or have critical performance requirements that
deserve an implementation in C (e.g., <code>sort</code>).


</p><p>
All libraries are implemented through the official C&nbsp;API
and are provided as separate C&nbsp;modules.
Currently, Lua has the following standard libraries:

</p><ul>

<li>basic library;</li>

<li>package library;</li>

<li>string manipulation;</li>

<li>table manipulation;</li>

<li>mathematical functions (sin, log, etc.);</li>

<li>input and output;</li>

<li>operating system facilities;</li>

<li>debug facilities.</li>

</ul><p>
Except for the basic and package libraries,
each library provides all its functions as fields of a global table
or as methods of its objects.


</p><p>
To have access to these libraries,
the C&nbsp;host program should call the <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_openlibs"><code>luaL_openlibs</code></a> function,
which opens all standard libraries.
Alternatively,
it can open them individually by calling
<a name="pdf-luaopen_base"><code>luaopen_base</code></a> (for the basic library),
<a name="pdf-luaopen_package"><code>luaopen_package</code></a> (for the package library),
<a name="pdf-luaopen_string"><code>luaopen_string</code></a> (for the string library),
<a name="pdf-luaopen_table"><code>luaopen_table</code></a> (for the table library),
<a name="pdf-luaopen_math"><code>luaopen_math</code></a> (for the mathematical library),
<a name="pdf-luaopen_io"><code>luaopen_io</code></a> (for the I/O and the Operating System libraries),
and <a name="pdf-luaopen_debug"><code>luaopen_debug</code></a> (for the debug library).
These functions are declared in <a name="pdf-lualib.h"><code>lualib.h</code></a>
and should not be called directly:
you must call them like any other Lua C&nbsp;function,
e.g., by using <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a>.



</p><h2>5.1 - <a name="5.1">Basic Functions</a></h2>

<p>
The basic library provides some core functions to Lua.
If you do not include this library in your application,
you should check carefully whether you need to provide 
implementations for some of its facilities.


</p><p>
</p><hr><h3><a name="pdf-assert"><code>assert (v [, message])</code></a></h3>
Issues an  error when
the value of its argument <code>v</code> is false (i.e., <b>nil</b> or <b>false</b>);
otherwise, returns all its arguments.
<code>message</code> is an error message;
when absent, it defaults to "assertion failed!"




<p>
</p><hr><h3><a name="pdf-collectgarbage"><code>collectgarbage (opt [, arg])</code></a></h3>


<p>
This function is a generic interface to the garbage collector.
It performs different functions according to its first argument, <code>opt</code>:

</p><ul>

<li><b>"stop":</b>
stops the garbage collector.
</li>

<li><b>"restart":</b>
restarts the garbage collector.
</li>

<li><b>"collect":</b>
performs a full garbage-collection cycle.
</li>

<li><b>"count":</b>
returns the total memory in use by Lua (in Kbytes).
</li>

<li><b>"step":</b>
performs a garbage-collection step.
The step "size" is controlled by <code>arg</code>
(larger values mean more steps) in a non-specified way.
If you want to control the step size
you must experimentally tune the value of <code>arg</code>.
Returns <b>true</b> if the step finished a collection cycle.
</li>

<li><b>"setpause":</b>
sets <code>arg</code>/100 as the new value for the <em>pause</em> of
the collector (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">§2.10</a>).
</li>

<li><b>"setstepmul":</b>
sets <code>arg</code>/100 as the new value for the <em>step multiplier</em> of
the collector (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">§2.10</a>).
</li>

</ul>



<p>
</p><hr><h3><a name="pdf-dofile"><code>dofile (filename)</code></a></h3>
Opens the named file and executes its contents as a Lua chunk.
When called without arguments,
<code>dofile</code> executes the contents of the standard input (<code>stdin</code>).
Returns all values returned by the chunk.
In case of errors, <code>dofile</code> propagates the error
to its caller (that is, <code>dofile</code> does not run in protected mode).




<p>
</p><hr><h3><a name="pdf-error"><code>error (message [, level])</code></a></h3>
Terminates the last protected function called
and returns <code>message</code> as the error message.
Function <code>error</code> never returns.


<p>
Usually, <code>error</code> adds some information about the error position
at the beginning of the message.
The <code>level</code> argument specifies how to get the error position.
With level&nbsp;1 (the default), the error position is where the
<code>error</code> function was called.
Level&nbsp;2 points the error to where the function
that called <code>error</code> was called; and so on.
Passing a level&nbsp;0 avoids the addition of error position information
to the message.




</p><p>
</p><hr><h3><a name="pdf-_G"><code>_G</code></a></h3>
A global variable (not a function) that
holds the global environment (that is, <code>_G._G = _G</code>).
Lua itself does not use this variable;
changing its value does not affect any environment,
nor vice-versa.
(Use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setfenv"><code>setfenv</code></a> to change environments.)




<p>
</p><hr><h3><a name="pdf-getfenv"><code>getfenv (f)</code></a></h3>
Returns the current environment in use by the function.
<code>f</code> can be a Lua function or a number
that specifies the function at that stack level:
Level&nbsp;1 is the function calling <code>getfenv</code>.
If the given function is not a Lua function,
or if <code>f</code> is 0,
<code>getfenv</code> returns the global environment.
The default for <code>f</code> is 1.




<p>
</p><hr><h3><a name="pdf-getmetatable"><code>getmetatable (object)</code></a></h3>


<p>
If <code>object</code> does not have a metatable, returns <b>nil</b>.
Otherwise,
if the object's metatable has a <code>"__metatable"</code> field,
returns the associated value.
Otherwise, returns the metatable of the given object.




</p><p>
</p><hr><h3><a name="pdf-ipairs"><code>ipairs (t)</code></a></h3>


<p>
Returns three values: an iterator function, the table <code>t</code>, and 0,
so that the construction

</p><pre>     for i,v in ipairs(t) do <em>body</em> end
</pre><p>
will iterate over the pairs (<code>1,t[1]</code>), (<code>2,t[2]</code>), ···,
up to the first integer key absent from the table.




</p><p>
</p><hr><h3><a name="pdf-load"><code>load (func [, chunkname])</code></a></h3>


<p>
Loads a chunk using function <code>func</code> to get its pieces.
Each call to <code>func</code> must return a string that concatenates
with previous results.
A return of <b>nil</b> (or no value) signals the end of the chunk.


</p><p>
If there are no errors, 
returns the compiled chunk as a function;
otherwise, returns <b>nil</b> plus the error message.
The environment of the returned function is the global environment.


</p><p>
<code>chunkname</code> is used as the chunk name for error messages
and debug information.




</p><p>
</p><hr><h3><a name="pdf-loadfile"><code>loadfile ([filename])</code></a></h3>


<p>
Similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-load"><code>load</code></a>,
but gets the chunk from file <code>filename</code>
or from the standard input,
if no file name is given.




</p><p>
</p><hr><h3><a name="pdf-loadstring"><code>loadstring (string [, chunkname])</code></a></h3>


<p>
Similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-load"><code>load</code></a>,
but gets the chunk from the given string.


</p><p>
To load and run a given string, use the idiom

</p><pre>     assert(loadstring(s))()
</pre>



<p>
</p><hr><h3><a name="pdf-next"><code>next (table [, index])</code></a></h3>


<p>
Allows a program to traverse all fields of a table.
Its first argument is a table and its second argument
is an index in this table.
<code>next</code> returns the next index of the table
and its associated value.
When called with <b>nil</b> as its second argument,
<code>next</code> returns an initial index
and its associated value.
When called with the last index,
or with <b>nil</b> in an empty table,
<code>next</code> returns <b>nil</b>.
If the second argument is absent, then it is interpreted as <b>nil</b>.
In particular,
you can use <code>next(t)</code> to check whether a table is empty.


</p><p>
The order in which the indices are enumerated is not specified,
<em>even for numeric indices</em>.
(To traverse a table in numeric order,
use a numerical <b>for</b> or the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-ipairs"><code>ipairs</code></a> function.)


</p><p>
The behavior of <code>next</code> is <em>undefined</em> if,
during the traversal,
you assign any value to a non-existent field in the table.
You may however modify existing fields.
In particular, you may clear existing fields.




</p><p>
</p><hr><h3><a name="pdf-pairs"><code>pairs (t)</code></a></h3>


<p>
Returns three values: the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-next"><code>next</code></a> function, the table <code>t</code>, and <b>nil</b>,
so that the construction

</p><pre>     for k,v in pairs(t) do <em>body</em> end
</pre><p>
will iterate over all key–value pairs of table <code>t</code>.


</p><p>
See function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-next"><code>next</code></a> for the caveats of modifying
the table during its traversal.




</p><p>
</p><hr><h3><a name="pdf-pcall"><code>pcall (f, arg1, ···)</code></a></h3>


<p>
Calls function <code>f</code> with
the given arguments in <em>protected mode</em>.
This means that any error inside&nbsp;<code>f</code> is not propagated;
instead, <code>pcall</code> catches the error
and returns a status code.
Its first result is the status code (a boolean),
which is true if the call succeeds without errors.
In such case, <code>pcall</code> also returns all results from the call,
after this first result.
In case of any error, <code>pcall</code> returns <b>false</b> plus the error message.




</p><p>
</p><hr><h3><a name="pdf-print"><code>print (···)</code></a></h3>
Receives any number of arguments,
and prints their values to <code>stdout</code>,
using the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-tostring"><code>tostring</code></a> function to convert them to strings.
<code>print</code> is not intended for formatted output,
but only as a quick way to show a value,
typically for debugging.
For formatted output, use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a>.




<p>
</p><hr><h3><a name="pdf-rawequal"><code>rawequal (v1, v2)</code></a></h3>
Checks whether <code>v1</code> is equal to <code>v2</code>,
without invoking any metamethod.
Returns a boolean.




<p>
</p><hr><h3><a name="pdf-rawget"><code>rawget (table, index)</code></a></h3>
Gets the real value of <code>table[index]</code>,
without invoking any metamethod.
<code>table</code> must be a table;
<code>index</code> may be any value.




<p>
</p><hr><h3><a name="pdf-rawset"><code>rawset (table, index, value)</code></a></h3>
Sets the real value of <code>table[index]</code> to <code>value</code>,
without invoking any metamethod.
<code>table</code> must be a table,
<code>index</code> any value different from <b>nil</b>,
and <code>value</code> any Lua value.


<p>
This function returns <code>table</code>.




</p><p>
</p><hr><h3><a name="pdf-select"><code>select (index, ···)</code></a></h3>


<p>
If <code>index</code> is a number,
returns all arguments after argument number <code>index</code>.
Otherwise, <code>index</code> must be the string <code>"#"</code>,
and <code>select</code> returns the total number of extra arguments it received.




</p><p>
</p><hr><h3><a name="pdf-setfenv"><code>setfenv (f, table)</code></a></h3>


<p>
Sets the environment to be used by the given function.
<code>f</code> can be a Lua function or a number
that specifies the function at that stack level:
Level&nbsp;1 is the function calling <code>setfenv</code>.
<code>setfenv</code> returns the given function.


</p><p>
As a special case, when <code>f</code> is 0 <code>setfenv</code> changes
the environment of the running thread.
In this case, <code>setfenv</code> returns no values.




</p><p>
</p><hr><h3><a name="pdf-setmetatable"><code>setmetatable (table, metatable)</code></a></h3>


<p>
Sets the metatable for the given table.
(You cannot change the metatable of other types from Lua, only from&nbsp;C.)
If <code>metatable</code> is <b>nil</b>,
removes the metatable of the given table.
If the original metatable has a <code>"__metatable"</code> field,
raises an error.


</p><p>
This function returns <code>table</code>.




</p><p>
</p><hr><h3><a name="pdf-tonumber"><code>tonumber (e [, base])</code></a></h3>
Tries to convert its argument to a number.
If the argument is already a number or a string convertible
to a number, then <code>tonumber</code> returns this number;
otherwise, it returns <b>nil</b>.


<p>
An optional argument specifies the base to interpret the numeral.
The base may be any integer between 2 and 36, inclusive.
In bases above&nbsp;10, the letter '<code>A</code>' (in either upper or lower case)
represents&nbsp;10, '<code>B</code>' represents&nbsp;11, and so forth,
with '<code>Z</code>' representing 35.
In base 10 (the default), the number may have a decimal part,
as well as an optional exponent part (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">§2.1</a>).
In other bases, only unsigned integers are accepted.




</p><p>
</p><hr><h3><a name="pdf-tostring"><code>tostring (e)</code></a></h3>
Receives an argument of any type and
converts it to a string in a reasonable format.
For complete control of how numbers are converted,
use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a>.


<p>
If the metatable of <code>e</code> has a <code>"__tostring"</code> field,
then <code>tostring</code> calls the corresponding value
with <code>e</code> as argument,
and uses the result of the call as its result.




</p><p>
</p><hr><h3><a name="pdf-type"><code>type (v)</code></a></h3>
Returns the type of its only argument, coded as a string.
The possible results of this function are
"<code>nil</code>" (a string, not the value <b>nil</b>),
"<code>number</code>",
"<code>string</code>",
"<code>boolean</code>",
"<code>table</code>",
"<code>function</code>",
"<code>thread</code>",
and "<code>userdata</code>".




<p>
</p><hr><h3><a name="pdf-unpack"><code>unpack (list [, i [, j]])</code></a></h3>
Returns the elements from the given table.
This function is equivalent to

<pre>     return list[i], list[i+1], ···, list[j]
</pre><p>
except that the above code can be written only for a fixed number
of elements.
By default, <code>i</code> is&nbsp;1 and <code>j</code> is the length of the list,
as defined by the length operator (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">§2.5.5</a>).




</p><p>
</p><hr><h3><a name="pdf-_VERSION"><code>_VERSION</code></a></h3>
A global variable (not a function) that
holds a string containing the current interpreter version.
The current contents of this variable is "<code>Lua 5.1</code>".




<p>
</p><hr><h3><a name="pdf-xpcall"><code>xpcall (f, err)</code></a></h3>


<p>
This function is similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-pcall"><code>pcall</code></a>,
except that you can set a new error handler.


</p><p>
<code>xpcall</code> calls function <code>f</code> in protected mode,
using <code>err</code> as the error handler.
Any error inside <code>f</code> is not propagated;
instead, <code>xpcall</code> catches the error,
calls the <code>err</code> function with the original error object,
and returns a status code.
Its first result is the status code (a boolean),
which is true if the call succeeds without errors.
In this case, <code>xpcall</code> also returns all results from the call,
after this first result.
In case of any error,
<code>xpcall</code> returns <b>false</b> plus the result from <code>err</code>.







</p><h2>5.2 - <a name="5.2">Coroutine Manipulation</a></h2>

<p>
The operations related to coroutines comprise a sub-library of
the basic library and come inside the table <a name="pdf-coroutine"><code>coroutine</code></a>.
See <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.11">§2.11</a> for a general description of coroutines.


</p><p>
</p><hr><h3><a name="pdf-coroutine.create"><code>coroutine.create (f)</code></a></h3>


<p>
Creates a new coroutine, with body <code>f</code>.
<code>f</code> must be a Lua function.
Returns this new coroutine,
an object with type <code>"thread"</code>.




</p><p>
</p><hr><h3><a name="pdf-coroutine.resume"><code>coroutine.resume (co [, val1, ···])</code></a></h3>


<p>
Starts or continues the execution of coroutine <code>co</code>.
The first time you resume a coroutine,
it starts running its body.
The values <code>val1</code>, ··· are passed
as the arguments to the body function.
If the coroutine has yielded,
<code>resume</code> restarts it;
the values <code>val1</code>, ··· are passed
as the results from the yield.


</p><p>
If the coroutine runs without any errors,
<code>resume</code> returns <b>true</b> plus any values passed to <code>yield</code>
(if the coroutine yields) or any values returned by the body function
(if the coroutine terminates).
If there is any error,
<code>resume</code> returns <b>false</b> plus the error message.




</p><p>
</p><hr><h3><a name="pdf-coroutine.running"><code>coroutine.running ()</code></a></h3>


<p>
Returns the running coroutine,
or <b>nil</b> when called by the main thread.




</p><p>
</p><hr><h3><a name="pdf-coroutine.status"><code>coroutine.status (co)</code></a></h3>


<p>
Returns the status of coroutine <code>co</code>, as a string:
<code>"running"</code>,
if the coroutine is running (that is, it called <code>status</code>);
<code>"suspended"</code>, if the coroutine is suspended in a call to <code>yield</code>,
or if it has not started running yet;
<code>"normal"</code> if the coroutine is active but not running
(that is, it has resumed another coroutine);
and <code>"dead"</code> if the coroutine has finished its body function,
or if it has stopped with an error.




</p><p>
</p><hr><h3><a name="pdf-coroutine.wrap"><code>coroutine.wrap (f)</code></a></h3>


<p>
Creates a new coroutine, with body <code>f</code>.
<code>f</code> must be a Lua function.
Returns a function that resumes the coroutine each time it is called.
Any arguments passed to the function behave as the
extra arguments to <code>resume</code>.
Returns the same values returned by <code>resume</code>,
except the first boolean.
In case of error, propagates the error.




</p><p>
</p><hr><h3><a name="pdf-coroutine.yield"><code>coroutine.yield (···)</code></a></h3>


<p>
Suspends the execution of the calling coroutine.
The coroutine cannot be running a C&nbsp;function,
a metamethod, or an iterator.
Any arguments to <code>yield</code> are passed as extra results to <code>resume</code>.







</p><h2>5.3 - <a name="5.3">Modules</a></h2>

<p>
The package library provides basic
facilities for loading and building modules in Lua.
It exports two of its functions directly in the global environment:
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> and <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-module"><code>module</code></a>.
Everything else is exported in a table <a name="pdf-package"><code>package</code></a>.


</p><p>
</p><hr><h3><a name="pdf-module"><code>module (name [, ···])</code></a></h3>


<p>
Creates a module.
If there is a table in <code>package.loaded[name]</code>,
this table is the module.
Otherwise, if there is a global table <code>t</code> with the given name,
this table is the module.
Otherwise creates a new table <code>t</code> and
sets it as the value of the global <code>name</code> and
the value of <code>package.loaded[name]</code>.
This function also initializes <code>t._NAME</code> with the given name,
<code>t._M</code> with the module (<code>t</code> itself),
and <code>t._PACKAGE</code> with the package name
(the full module name minus last component; see below).
Finally, <code>module</code> sets <code>t</code> as the new environment
of the current function and the new value of <code>package.loaded[name]</code>,
so that <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> returns <code>t</code>.


</p><p>
If <code>name</code> is a compound name
(that is, one with components separated by dots),
<code>module</code> creates (or reuses, if they already exist)
tables for each component.
For instance, if <code>name</code> is <code>a.b.c</code>,
then <code>module</code> stores the module table in field <code>c</code> of
field <code>b</code> of global <code>a</code>.


</p><p>
This function may receive optional <em>options</em> after
the module name,
where each option is a function to be applied over the module.




</p><p>
</p><hr><h3><a name="pdf-require"><code>require (modname)</code></a></h3>


<p>
Loads the given module.
The function starts by looking into the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.loaded"><code>package.loaded</code></a> table
to determine whether <code>modname</code> is already loaded.
If it is, then <code>require</code> returns the value stored
at <code>package.loaded[modname]</code>.
Otherwise, it tries to find a <em>loader</em> for the module.


</p><p>
To find a loader,
first <code>require</code> queries <code>package.preload[modname]</code>.
If it has a value,
this value (which should be a function) is the loader.
Otherwise <code>require</code> searches for a Lua loader using the
path stored in <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.path"><code>package.path</code></a>.
If that also fails, it searches for a C&nbsp;loader using the
path stored in <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.cpath"><code>package.cpath</code></a>.
If that also fails,
it tries an <em>all-in-one</em> loader (see below).


</p><p>
When loading a C&nbsp;library,
<code>require</code> first uses a dynamic link facility to link the
application with the library.
Then it tries to find a C&nbsp;function inside this library to
be used as the loader.
The name of this C&nbsp;function is the string "<code>luaopen_</code>"
concatenated with a copy of the module name where each dot
is replaced by an underscore.
Moreover, if the module name has a hyphen,
its prefix up to (and including) the first hyphen is removed.
For instance, if the module name is <code>a.v1-b.c</code>,
the function name will be <code>luaopen_b_c</code>.


</p><p>
If <code>require</code> finds neither a Lua library nor a
C&nbsp;library for a module,
it calls the <em>all-in-one loader</em>.
This loader searches the C&nbsp;path for a library for
the root name of the given module.
For instance, when requiring <code>a.b.c</code>,
it will search for a C&nbsp;library for <code>a</code>.
If found, it looks into it for an open function for
the submodule;
in our example, that would be <code>luaopen_a_b_c</code>.
With this facility, a package can pack several C&nbsp;submodules
into one single library,
with each submodule keeping its original open function.


</p><p>
Once a loader is found,
<code>require</code> calls the loader with a single argument, <code>modname</code>.
If the loader returns any value,
<code>require</code> assigns the returned value to <code>package.loaded[modname]</code>.
If the loader returns no value and
has not assigned any value to <code>package.loaded[modname]</code>,
then <code>require</code> assigns <b>true</b> to this entry.
In any case, <code>require</code> returns the
final value of <code>package.loaded[modname]</code>.


</p><p>
If there is any error loading or running the module,
or if it cannot find any loader for the module,
then <code>require</code> signals an error. 




</p><p>
</p><hr><h3><a name="pdf-package.cpath"><code>package.cpath</code></a></h3>


<p>
The path used by <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> to search for a C&nbsp;loader.


</p><p>
Lua initializes the C&nbsp;path <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.cpath"><code>package.cpath</code></a> in the same way
it initializes the Lua path <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.path"><code>package.path</code></a>,
using the environment variable <a name="pdf-LUA_CPATH"><code>LUA_CPATH</code></a>
(plus another default path defined in <code>luaconf.h</code>).




</p><p>

</p><hr><h3><a name="pdf-package.loaded"><code>package.loaded</code></a></h3>


<p>
A table used by <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> to control which
modules are already loaded.
When you require a module <code>modname</code> and
<code>package.loaded[modname]</code> is not false,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> simply returns the value stored there.




</p><p>
</p><hr><h3><a name="pdf-package.loadlib"><code>package.loadlib (libname, funcname)</code></a></h3>


<p>
Dynamically links the host program with the C&nbsp;library <code>libname</code>.
Inside this library, looks for a function <code>funcname</code>
and returns this function as a C&nbsp;function.
(So, <code>funcname</code> must follow the protocol (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_CFunction"><code>lua_CFunction</code></a>)).


</p><p>
This is a low-level function.
It completely bypasses the package and module system.
Unlike <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a>,
it does not perform any path searching and
does not automatically adds extensions.
<code>libname</code> must be the complete file name of the C&nbsp;library,
including if necessary a path and extension.
<code>funcname</code> must be the exact name exported by the C&nbsp;library
(which may depend on the C&nbsp;compiler and linker used).


</p><p>
This function is not supported by ANSI C.
As such, it is only available on some platforms
(Windows, Linux, Mac OS X, Solaris, BSD,
plus other Unix systems that support the <code>dlfcn</code> standard).




</p><p>
</p><hr><h3><a name="pdf-package.path"><code>package.path</code></a></h3>


<p>
The path used by <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> to search for a Lua loader.


</p><p>
At start-up, Lua initializes this variable with
the value of the environment variable <a name="pdf-LUA_PATH"><code>LUA_PATH</code></a> or
with a default path defined in <code>luaconf.h</code>,
if the environment variable is not defined.
Any "<code>;;</code>" in the value of the environment variable
is replaced by the default path.


</p><p>
A path is a sequence of <em>templates</em> separated by semicolons.
For each template, <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> will change each interrogation
mark in the template by <code>filename</code>,
which is <code>modname</code> with each dot replaced by a
"directory separator" (such as "<code>/</code>" in Unix);
then it will try to load the resulting file name.
So, for instance, if the Lua path is

</p><pre>     "./?.lua;./?.lc;/usr/local/?/init.lua"
</pre><p>
the search for a Lua loader for module <code>foo</code>
will try to load the files
<code>./foo.lua</code>, <code>./foo.lc</code>, and
<code>/usr/local/foo/init.lua</code>, in that order.




</p><p>
</p><hr><h3><a name="pdf-package.preload"><code>package.preload</code></a></h3>


<p>
A table to store loaders for specific modules
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a>).




</p><p>
</p><hr><h3><a name="pdf-package.seeall"><code>package.seeall (module)</code></a></h3>


<p>
Sets a metatable for <code>module</code> with
its <code>__index</code> field referring to the global environment,
so that this module inherits values
from the global environment.
To be used as an option to function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-module"><code>module</code></a>.







</p><h2>5.4 - <a name="5.4">String Manipulation</a></h2>

<p>
This library provides generic functions for string manipulation,
such as finding and extracting substrings, and pattern matching.
When indexing a string in Lua, the first character is at position&nbsp;1
(not at&nbsp;0, as in C).
Indices are allowed to be negative and are interpreted as indexing backwards,
from the end of the string.
Thus, the last character is at position -1, and so on.


</p><p>
The string library provides all its functions inside the table
<a name="pdf-string"><code>string</code></a>.
It also sets a metatable for strings
where the <code>__index</code> field points to the <code>string</code> table.
Therefore, you can use the string functions in object-oriented style.
For instance, <code>string.byte(s, i)</code>
can be written as <code>s:byte(i)</code>.


</p><p>
</p><hr><h3><a name="pdf-string.byte"><code>string.byte (s [, i [, j]])</code></a></h3>
Returns the internal numerical codes of the characters <code>s[i]</code>,
<code>s[i+1]</code>, ···, <code>s[j]</code>.
The default value for <code>i</code> is&nbsp;1;
the default value for <code>j</code> is&nbsp;<code>i</code>.


<p>
Note that numerical codes are not necessarily portable across platforms.




</p><p>
</p><hr><h3><a name="pdf-string.char"><code>string.char (···)</code></a></h3>
Receives zero or more integers.
Returns a string with length equal to the number of arguments,
in which each character has the internal numerical code equal
to its corresponding argument.


<p>
Note that numerical codes are not necessarily portable across platforms.




</p><p>
</p><hr><h3><a name="pdf-string.dump"><code>string.dump (function)</code></a></h3>


<p>
Returns a string containing a binary representation of the given function,
so that a later <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-loadstring"><code>loadstring</code></a> on this string returns
a copy of the function.
<code>function</code> must be a Lua function without upvalues.




</p><p>
</p><hr><h3><a name="pdf-string.find"><code>string.find (s, pattern [, init [, plain]])</code></a></h3>
Looks for the first match of
<code>pattern</code> in the string <code>s</code>.
If it finds a match, then <code>find</code> returns the indices of&nbsp;<code>s</code>
where this occurrence starts and ends;
otherwise, it returns <b>nil</b>.
A third, optional numerical argument <code>init</code> specifies
where to start the search;
its default value is&nbsp;1 and may be negative.
A value of <b>true</b> as a fourth, optional argument <code>plain</code>
turns off the pattern matching facilities,
so the function does a plain "find substring" operation,
with no characters in <code>pattern</code> being considered "magic".
Note that if <code>plain</code> is given, then <code>init</code> must be given as well.


<p>
If the pattern has captures,
then in a successful match
the captured values are also returned,
after the two indices.




</p><p>
</p><hr><h3><a name="pdf-string.format"><code>string.format (formatstring, ···)</code></a></h3>
Returns a formatted version of its variable number of arguments
following the description given in its first argument (which must be a string).
The format string follows the same rules as the <code>printf</code> family of
standard C&nbsp;functions.
The only differences are that the options/modifiers
<code>*</code>, <code>l</code>, <code>L</code>, <code>n</code>, <code>p</code>,
and <code>h</code> are not supported
and that there is an extra option, <code>q</code>.
The <code>q</code> option formats a string in a form suitable to be safely read
back by the Lua interpreter:
the string is written between double quotes,
and all double quotes, newlines, embedded zeros,
and backslashes in the string
are correctly escaped when written.
For instance, the call

<pre>     string.format('%q', 'a string with "quotes" and \n new line')
</pre><p>
will produce the string:

</p><pre>     "a string with \"quotes\" and \
      new line"
</pre>

<p>
The options <code>c</code>, <code>d</code>, <code>E</code>, <code>e</code>, <code>f</code>,
<code>g</code>, <code>G</code>, <code>i</code>, <code>o</code>, <code>u</code>, <code>X</code>, and <code>x</code> all
expect a number as argument,
whereas <code>q</code> and <code>s</code> expect a string.


</p><p>
This function does not accept string values
containing embedded zeros.




</p><p>
</p><hr><h3><a name="pdf-string.gmatch"><code>string.gmatch (s, pattern)</code></a></h3>
Returns an iterator function that,
each time it is called,
returns the next captures from <code>pattern</code> over string <code>s</code>.


<p>
If <code>pattern</code> specifies no captures,
then the whole match is produced in each call.


</p><p>
As an example, the following loop

</p><pre>     s = "hello world from Lua"
     for w in string.gmatch(s, "%a+") do
       print(w)
     end
</pre><p>
will iterate over all the words from string <code>s</code>,
printing one per line.
The next example collects all pairs <code>key=value</code> from the
given string into a table:

</p><pre>     t = {}
     s = "from=world, to=Lua"
     for k, v in string.gmatch(s, "(%w+)=(%w+)") do
       t[k] = v
     end
</pre>



<p>
</p><hr><h3><a name="pdf-string.gsub"><code>string.gsub (s, pattern, repl [, n])</code></a></h3>
Returns a copy of <code>s</code>
in which all occurrences of the <code>pattern</code> have been
replaced by a replacement string specified by <code>repl</code>,
which may be a string, a table, or a function.
<code>gsub</code> also returns, as its second value,
the total number of substitutions made.


<p>
If <code>repl</code> is a string, then its value is used for replacement.
The character&nbsp;<code>%</code> works as an escape character:
any sequence in <code>repl</code> of the form <code>%<em>n</em></code>,
with <em>n</em> between 1 and 9,
stands for the value of the <em>n</em>-th captured substring (see below).
The sequence <code>%0</code> stands for the whole match.
The sequence <code>%%</code> stands for a single&nbsp;<code>%</code>.


</p><p>
If <code>repl</code> is a table, then the table is queried for every match,
using the first capture as the key;
if the pattern specifies no captures,
then the whole match is used as the key.


</p><p>
If <code>repl</code> is a function, then this function is called every time a
match occurs, with all captured substrings passed as arguments,
in order;
if the pattern specifies no captures,
then the whole match is passed as a sole argument.


</p><p>
If the value returned by the table query or by the function call
is a string or a number,
then it is used as the replacement string;
otherwise, if it is <b>false</b> or <b>nil</b>,
then there is no replacement
(that is, the original match is kept in the string).


</p><p>
The optional last parameter <code>n</code> limits
the maximum number of substitutions to occur.
For instance, when <code>n</code> is 1 only the first occurrence of
<code>pattern</code> is replaced.


</p><p>
Here are some examples:

</p><pre>     x = string.gsub("hello world", "(%w+)", "%1 %1")
     --&gt; x="hello hello world world"
     
     x = string.gsub("hello world", "%w+", "%0 %0", 1)
     --&gt; x="hello hello world"
     
     x = string.gsub("hello world from Lua", "(%w+)%s*(%w+)", "%2 %1")
     --&gt; x="world hello Lua from"
     
     x = string.gsub("home = $HOME, user = $USER", "%$(%w+)", os.getenv)
     --&gt; x="home = /home/roberto, user = roberto"
     
     x = string.gsub("4+5 = $return 4+5$", "%$(.-)%$", function (s)
           return loadstring(s)()
         end)
     --&gt; x="4+5 = 9"
     
     local t = {name="lua", version="5.1"}
     x = string.gsub("$name%-$version.tar.gz", "%$(%w+)", t)
     --&gt; x="lua-5.1.tar.gz"
</pre>



<p>
</p><hr><h3><a name="pdf-string.len"><code>string.len (s)</code></a></h3>
Receives a string and returns its length.
The empty string <code>""</code> has length 0.
Embedded zeros are counted,
so <code>"a\000bc\000"</code> has length 5.




<p>
</p><hr><h3><a name="pdf-string.lower"><code>string.lower (s)</code></a></h3>
Receives a string and returns a copy of this string with all
uppercase letters changed to lowercase.
All other characters are left unchanged.
The definition of what an uppercase letter is depends on the current locale.




<p>
</p><hr><h3><a name="pdf-string.match"><code>string.match (s, pattern [, init])</code></a></h3>
Looks for the first <em>match</em> of
<code>pattern</code> in the string <code>s</code>.
If it finds one, then <code>match</code> returns
the captures from the pattern;
otherwise it returns <b>nil</b>.
If <code>pattern</code> specifies no captures,
then the whole match is returned.
A third, optional numerical argument <code>init</code> specifies
where to start the search;
its default value is&nbsp;1 and may be negative.




<p>
</p><hr><h3><a name="pdf-string.rep"><code>string.rep (s, n)</code></a></h3>
Returns a string that is the concatenation of <code>n</code> copies of
the string <code>s</code>.




<p>
</p><hr><h3><a name="pdf-string.reverse"><code>string.reverse (s)</code></a></h3>
Returns a string that is the string <code>s</code> reversed.




<p>
</p><hr><h3><a name="pdf-string.sub"><code>string.sub (s, i [, j])</code></a></h3>
Returns the substring of <code>s</code> that
starts at <code>i</code>  and continues until <code>j</code>;
<code>i</code> and <code>j</code> may be negative.
If <code>j</code> is absent, then it is assumed to be equal to -1
(which is the same as the string length).
In particular,
the call <code>string.sub(s,1,j)</code> returns a prefix of <code>s</code>
with length <code>j</code>,
and <code>string.sub(s, -i)</code> returns a suffix of <code>s</code>
with length <code>i</code>.




<p>
</p><hr><h3><a name="pdf-string.upper"><code>string.upper (s)</code></a></h3>
Receives a string and returns a copy of this string with all
lowercase letters changed to uppercase.
All other characters are left unchanged.
The definition of what a lowercase letter is depends on the current locale.



<h3>5.4.1 - <a name="5.4.1">Patterns</a></h3>


<h4>Character Class:</h4><p>
A <em>character class</em> is used to represent a set of characters.
The following combinations are allowed in describing a character class:

</p><ul>

<li><b><em>x</em>:</b>
(where <em>x</em> is not one of the <em>magic characters</em>
<code>^$()%.[]*+-?</code>)
represents the character <em>x</em> itself.
</li>

<li><b><code>.</code>:</b> (a dot) represents all characters.</li>

<li><b><code>%a</code>:</b> represents all letters.</li>

<li><b><code>%c</code>:</b> represents all control characters.</li>

<li><b><code>%d</code>:</b> represents all digits.</li>

<li><b><code>%l</code>:</b> represents all lowercase letters.</li>

<li><b><code>%p</code>:</b> represents all punctuation characters.</li>

<li><b><code>%s</code>:</b> represents all space characters.</li>

<li><b><code>%u</code>:</b> represents all uppercase letters.</li>

<li><b><code>%w</code>:</b> represents all alphanumeric characters.</li>

<li><b><code>%x</code>:</b> represents all hexadecimal digits.</li>

<li><b><code>%z</code>:</b> represents the character with representation 0.</li>

<li><b><code>%<em>x</em></code>:</b> (where <em>x</em> is any non-alphanumeric character)
represents the character <em>x</em>.
This is the standard way to escape the magic characters.
Any punctuation character (even the non magic)
can be preceded by a '<code>%</code>'
when used to represent itself in a pattern.
</li>

<li><b><code>[<em>set</em>]</code>:</b>
represents the class which is the union of all
characters in <em>set</em>.
A range of characters may be specified by
separating the end characters of the range with a '<code>-</code>'.
All classes <code>%</code><em>x</em> described above may also be used as
components in <em>set</em>.
All other characters in <em>set</em> represent themselves.
For example, <code>[%w_]</code> (or <code>[_%w]</code>)
represents all alphanumeric characters plus the underscore,
<code>[0-7]</code> represents the octal digits,
and <code>[0-7%l%-]</code> represents the octal digits plus
the lowercase letters plus the '<code>-</code>' character.


<p>
The interaction between ranges and classes is not defined.
Therefore, patterns like <code>[%a-z]</code> or <code>[a-%%]</code>
have no meaning.
</p></li>

<li><b><code>[^<em>set</em>]</code>:</b>
represents the complement of <em>set</em>,
where <em>set</em> is interpreted as above.
</li>

</ul><p>
For all classes represented by single letters (<code>%a</code>, <code>%c</code>, etc.),
the corresponding uppercase letter represents the complement of the class.
For instance, <code>%S</code> represents all non-space characters.


</p><p>
The definitions of letter, space, and other character groups
depend on the current locale.
In particular, the class <code>[a-z]</code> may not be equivalent to <code>%l</code>.





</p><h4>Pattern Item:</h4><p>
A <em>pattern item</em> may be

</p><ul>

<li>
a single character class,
which matches any single character in the class;
</li>

<li>
a single character class followed by '<code>*</code>',
which matches 0 or more repetitions of characters in the class.
These repetition items will always match the longest possible sequence;
</li>

<li>
a single character class followed by '<code>+</code>',
which matches 1 or more repetitions of characters in the class.
These repetition items will always match the longest possible sequence;
</li>

<li>
a single character class followed by '<code>-</code>',
which also matches 0 or more repetitions of characters in the class.
Unlike '<code>*</code>',
these repetition items will always match the <em>shortest</em> possible sequence;
</li>

<li>
a single character class followed by '<code>?</code>',
which matches 0 or 1 occurrence of a character in the class;
</li>

<li>
<code>%<em>n</em></code>, for <em>n</em> between 1 and 9;
such item matches a substring equal to the <em>n</em>-th captured string
(see below);
</li>

<li>
<code>%b<em>xy</em></code>, where <em>x</em> and <em>y</em> are two distinct characters;
such item matches strings that start with&nbsp;<em>x</em>, end with&nbsp;<em>y</em>,
and where the <em>x</em> and <em>y</em> are <em>balanced</em>.
This means that, if one reads the string from left to right,
counting <em>+1</em> for an <em>x</em> and <em>-1</em> for a <em>y</em>,
the ending <em>y</em> is the first <em>y</em> where the count reaches 0.
For instance, the item <code>%b()</code> matches expressions with
balanced parentheses.
</li>

</ul>




<h4>Pattern:</h4><p>
A <em>pattern</em> is a sequence of pattern items.
A '<code>^</code>' at the beginning of a pattern anchors the match at the
beginning of the subject string.
A '<code>$</code>' at the end of a pattern anchors the match at the
end of the subject string.
At other positions,
'<code>^</code>' and '<code>$</code>' have no special meaning and represent themselves.





</p><h4>Captures:</h4><p>
A pattern may contain sub-patterns enclosed in parentheses;
they describe <em>captures</em>.
When a match succeeds, the substrings of the subject string
that match captures are stored (<em>captured</em>) for future use.
Captures are numbered according to their left parentheses.
For instance, in the pattern <code>"(a*(.)%w(%s*))"</code>,
the part of the string matching <code>"a*(.)%w(%s*)"</code> is
stored as the first capture (and therefore has number&nbsp;1);
the character matching "<code>.</code>" is captured with number&nbsp;2,
and the part matching "<code>%s*</code>" has number&nbsp;3.


</p><p>
As a special case, the empty capture <code>()</code> captures
the current string position (a number).
For instance, if we apply the pattern <code>"()aa()"</code> on the
string <code>"flaaap"</code>, there will be two captures: 3&nbsp;and&nbsp;5.


</p><p>
A pattern cannot contain embedded zeros.  Use <code>%z</code> instead.











</p><h2>5.5 - <a name="5.5">Table Manipulation</a></h2><p>
This library provides generic functions for table manipulation.
It provides all its functions inside the table <a name="pdf-table"><code>table</code></a>.


</p><p>
Most functions in the table library assume that the table
represents an array or a list.
For these functions, when we talk about the "length" of a table
we mean the result of the length operator.


</p><p>
</p><hr><h3><a name="pdf-table.concat"><code>table.concat (table [, sep [, i [, j]]])</code></a></h3>
Given an array where all elements are strings or numbers,
returns <code>table[i]..sep..table[i+1] ··· sep..table[j]</code>.
The default value for <code>sep</code> is the empty string,
the default for <code>i</code> is 1,
and the default for <code>j</code> is the length of the table.
If <code>i</code> is greater than <code>j</code>, returns the empty string.




<p>
</p><hr><h3><a name="pdf-table.insert"><code>table.insert (table, [pos,] value)</code></a></h3>


<p>
Inserts element <code>value</code> at position <code>pos</code> in <code>table</code>,
shifting up other elements to open space, if necessary.
The default value for <code>pos</code> is <code>n+1</code>,
where <code>n</code> is the length of the table (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">§2.5.5</a>),
so that a call <code>table.insert(t,x)</code> inserts <code>x</code> at the end
of table <code>t</code>.




</p><p>
</p><hr><h3><a name="pdf-table.maxn"><code>table.maxn (table)</code></a></h3>


<p>
Returns the largest positive numerical index of the given table,
or zero if the table has no positive numerical indices.
(To do its job this function does a linear traversal of
the whole table.) 




</p><p>
</p><hr><h3><a name="pdf-table.remove"><code>table.remove (table [, pos])</code></a></h3>


<p>
Removes from <code>table</code> the element at position <code>pos</code>,
shifting down other elements to close the space, if necessary.
Returns the value of the removed element.
The default value for <code>pos</code> is <code>n</code>,
where <code>n</code> is the length of the table,
so that a call <code>table.remove(t)</code> removes the last element
of table <code>t</code>.




</p><p>
</p><hr><h3><a name="pdf-table.sort"><code>table.sort (table [, comp])</code></a></h3>
Sorts table elements in a given order, <em>in-place</em>,
from <code>table[1]</code> to <code>table[n]</code>,
where <code>n</code> is the length of the table.
If <code>comp</code> is given,
then it must be a function that receives two table elements,
and returns true
when the first is less than the second
(so that <code>not comp(a[i+1],a[i])</code> will be true after the sort).
If <code>comp</code> is not given,
then the standard Lua operator <code>&lt;</code> is used instead.


<p>
The sort algorithm is not stable;
that is, elements considered equal by the given order
may have their relative positions changed by the sort.







</p><h2>5.6 - <a name="5.6">Mathematical Functions</a></h2>

<p>
This library is an interface to the standard C&nbsp;math library.
It provides all its functions inside the table <a name="pdf-math"><code>math</code></a>.


</p><p>
</p><hr><h3><a name="pdf-math.abs"><code>math.abs (x)</code></a></h3>


<p>
Returns the absolute value of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.acos"><code>math.acos (x)</code></a></h3>


<p>
Returns the arc cosine of <code>x</code> (in radians).




</p><p>
</p><hr><h3><a name="pdf-math.asin"><code>math.asin (x)</code></a></h3>


<p>
Returns the arc sine of <code>x</code> (in radians).




</p><p>
</p><hr><h3><a name="pdf-math.atan"><code>math.atan (x)</code></a></h3>


<p>
Returns the arc tangent of <code>x</code> (in radians).




</p><p>
</p><hr><h3><a name="pdf-math.atan2"><code>math.atan2 (x, y)</code></a></h3>


<p>
Returns the arc tangent of <code>x/y</code> (in radians),
but uses the signs of both parameters to find the
quadrant of the result.
(It also handles correctly the case of <code>y</code> being zero.)




</p><p>
</p><hr><h3><a name="pdf-math.ceil"><code>math.ceil (x)</code></a></h3>


<p>
Returns the smallest integer larger than or equal to <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.cos"><code>math.cos (x)</code></a></h3>


<p>
Returns the cosine of <code>x</code> (assumed to be in radians).




</p><p>
</p><hr><h3><a name="pdf-math.cosh"><code>math.cosh (x)</code></a></h3>


<p>
Returns the hyperbolic cosine of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.deg"><code>math.deg (x)</code></a></h3>


<p>
Returns the angle <code>x</code> (given in radians) in degrees.




</p><p>
</p><hr><h3><a name="pdf-math.exp"><code>math.exp (x)</code></a></h3>


<p>
Returns the the value <em>e<sup>x</sup></em>.




</p><p>
</p><hr><h3><a name="pdf-math.floor"><code>math.floor (x)</code></a></h3>


<p>
Returns the largest integer smaller than or equal to <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.fmod"><code>math.fmod (x, y)</code></a></h3>


<p>
Returns the remainder of the division of <code>x</code> by <code>y</code>.




</p><p>
</p><hr><h3><a name="pdf-math.frexp"><code>math.frexp (x)</code></a></h3>


<p>
Returns <code>m</code> and <code>e</code> such that <em>x = m2<sup>e</sup></em>,
<code>e</code> is an integer and the absolute value of <code>m</code> is
in the range <em>[0.5, 1)</em>
(or zero when <code>x</code> is zero).




</p><p>
</p><hr><h3><a name="pdf-math.huge"><code>math.huge</code></a></h3>


<p>
The value <code>HUGE_VAL</code>,
a value larger than or equal to any other numerical value.




</p><p>
</p><hr><h3><a name="pdf-math.ldexp"><code>math.ldexp (m, e)</code></a></h3>


<p>
Returns <em>m2<sup>e</sup></em> (<code>e</code> should be an integer).




</p><p>
</p><hr><h3><a name="pdf-math.log"><code>math.log (x)</code></a></h3>


<p>
Returns the natural logarithm of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.log10"><code>math.log10 (x)</code></a></h3>


<p>
Returns the base-10 logarithm of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.max"><code>math.max (x, ···)</code></a></h3>


<p>
Returns the maximum value among its arguments.




</p><p>
</p><hr><h3><a name="pdf-math.min"><code>math.min (x, ···)</code></a></h3>


<p>
Returns the minimum value among its arguments.




</p><p>
</p><hr><h3><a name="pdf-math.modf"><code>math.modf (x)</code></a></h3>


<p>
Returns two numbers,
the integral part of <code>x</code> and the fractional part of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.pi"><code>math.pi</code></a></h3>


<p>
The value of <em>pi</em>.




</p><p>
</p><hr><h3><a name="pdf-math.pow"><code>math.pow (x, y)</code></a></h3>


<p>
Returns <em>x<sup>y</sup></em>.
(You can also use the expression <code>x^y</code> to compute this value.)




</p><p>
</p><hr><h3><a name="pdf-math.rad"><code>math.rad (x)</code></a></h3>


<p>
Returns the angle <code>x</code> (given in degrees) in radians.




</p><p>
</p><hr><h3><a name="pdf-math.random"><code>math.random ([m [, n]])</code></a></h3>


<p>
This function is an interface to the simple
pseudo-random generator function <code>rand</code> provided by ANSI&nbsp;C.
(No guarantees can be given for its statistical properties.)


</p><p>
When called without arguments,
returns a pseudo-random real number
in the range <em>[0,1)</em>.  
When called with a number <code>m</code>,
<code>math.random</code> returns
a pseudo-random integer in the range <em>[1, m]</em>.
When called with two numbers <code>m</code> and <code>n</code>,
<code>math.random</code> returns a pseudo-random
integer in the range <em>[m, n]</em>.




</p><p>
</p><hr><h3><a name="pdf-math.randomseed"><code>math.randomseed (x)</code></a></h3>


<p>
Sets <code>x</code> as the "seed"
for the pseudo-random generator:
equal seeds produce equal sequences of numbers.




</p><p>
</p><hr><h3><a name="pdf-math.sin"><code>math.sin (x)</code></a></h3>


<p>
Returns the sine of <code>x</code> (assumed to be in radians).




</p><p>
</p><hr><h3><a name="pdf-math.sinh"><code>math.sinh (x)</code></a></h3>


<p>
Returns the hyperbolic sine of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.sqrt"><code>math.sqrt (x)</code></a></h3>


<p>
Returns the square root of <code>x</code>.
(You can also use the expression <code>x^0.5</code> to compute this value.)




</p><p>
</p><hr><h3><a name="pdf-math.tan"><code>math.tan (x)</code></a></h3>


<p>
Returns the tangent of <code>x</code> (assumed to be in radians).




</p><p>
</p><hr><h3><a name="pdf-math.tanh"><code>math.tanh (x)</code></a></h3>


<p>
Returns the hyperbolic tangent of <code>x</code>.







</p><h2>5.7 - <a name="5.7">Input and Output Facilities</a></h2>

<p>
The I/O library provides two different styles for file manipulation.
The first one uses implicit file descriptors;
that is, there are operations to set a default input file and a
default output file,
and all input/output operations are over these default files.
The second style uses explicit file descriptors.


</p><p>
When using implicit file descriptors,
all operations are supplied by table <a name="pdf-io"><code>io</code></a>.
When using explicit file descriptors,
the operation <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.open"><code>io.open</code></a> returns a file descriptor
and then all operations are supplied as methods of the file descriptor.


</p><p>
The table <code>io</code> also provides
three predefined file descriptors with their usual meanings from C:
<a name="pdf-io.stdin"><code>io.stdin</code></a>, <a name="pdf-io.stdout"><code>io.stdout</code></a>, and <a name="pdf-io.stderr"><code>io.stderr</code></a>.


</p><p>
Unless otherwise stated,
all I/O functions return <b>nil</b> on failure
(plus an error message as a second result)
and some value different from <b>nil</b> on success.


</p><p>
</p><hr><h3><a name="pdf-io.close"><code>io.close ([file])</code></a></h3>


<p>
Equivalent to <code>file:close()</code>.
Without a <code>file</code>, closes the default output file.




</p><p>
</p><hr><h3><a name="pdf-io.flush"><code>io.flush ()</code></a></h3>


<p>
Equivalent to <code>file:flush</code> over the default output file.




</p><p>
</p><hr><h3><a name="pdf-io.input"><code>io.input ([file])</code></a></h3>


<p>
When called with a file name, it opens the named file (in text mode),
and sets its handle as the default input file.
When called with a file handle,
it simply sets this file handle as the default input file.
When called without parameters,
it returns the current default input file.


</p><p>
In case of errors this function raises the error,
instead of returning an error code.




</p><p>
</p><hr><h3><a name="pdf-io.lines"><code>io.lines ([filename])</code></a></h3>


<p>
Opens the given file name in read mode
and returns an iterator function that,
each time it is called,
returns a new line from the file.
Therefore, the construction

</p><pre>     for line in io.lines(filename) do <em>body</em> end
</pre><p>
will iterate over all lines of the file.
When the iterator function detects the end of file,
it returns <b>nil</b> (to finish the loop) and automatically closes the file.


</p><p>
The call <code>io.lines()</code> (with no file name) is equivalent
to <code>io.input():lines()</code>;
that is, it iterates over the lines of the default input file.
In this case it does not close the file when the loop ends.




</p><p>
</p><hr><h3><a name="pdf-io.open"><code>io.open (filename [, mode])</code></a></h3>


<p>
This function opens a file,
in the mode specified in the string <code>mode</code>.
It returns a new file handle,
or, in case of errors, <b>nil</b> plus an error message.


</p><p>
The <code>mode</code> string can be any of the following:

</p><ul>
<li><b>"r":</b> read mode (the default);</li>
<li><b>"w":</b> write mode;</li>
<li><b>"a":</b> append mode;</li>
<li><b>"r+":</b> update mode, all previous data is preserved;</li>
<li><b>"w+":</b> update mode, all previous data is erased;</li>
<li><b>"a+":</b> append update mode, previous data is preserved,
  writing is only allowed at the end of file.</li>
</ul><p>
The <code>mode</code> string may also have a '<code>b</code>' at the end,
which is needed in some systems to open the file in binary mode.
This string is exactly what is used in the
standard&nbsp;C function <code>fopen</code>.




</p><p>
</p><hr><h3><a name="pdf-io.output"><code>io.output ([file])</code></a></h3>


<p>
Similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.input"><code>io.input</code></a>, but operates over the default output file.




</p><p>
</p><hr><h3><a name="pdf-io.popen"><code>io.popen (prog [, mode])</code></a></h3>


<p>
Starts program <code>prog</code> in a separated process and returns
a file handle that you can use to read data from this program
(if <code>mode</code> is <code>"r"</code>, the default)
or to write data to this program
(if <code>mode</code> is <code>"w"</code>).


</p><p>
This function is system dependent and is not available
on all platforms.




</p><p>
</p><hr><h3><a name="pdf-io.read"><code>io.read (···)</code></a></h3>


<p>
Equivalent to <code>io.input():read</code>.




</p><p>
</p><hr><h3><a name="pdf-io.tmpfile"><code>io.tmpfile ()</code></a></h3>


<p>
Returns a handle for a temporary file.
This file is opened in update mode
and it is automatically removed when the program ends.




</p><p>
</p><hr><h3><a name="pdf-io.type"><code>io.type (obj)</code></a></h3>


<p>
Checks whether <code>obj</code> is a valid file handle.
Returns the string <code>"file"</code> if <code>obj</code> is an open file handle,
<code>"closed file"</code> if <code>obj</code> is a closed file handle,
or <b>nil</b> if <code>obj</code> is not a file handle.




</p><p>
</p><hr><h3><a name="pdf-io.write"><code>io.write (···)</code></a></h3>


<p>
Equivalent to <code>io.output():write</code>.




</p><p>
</p><hr><h3><a name="pdf-file:close"><code>file:close ()</code></a></h3>


<p>
Closes <code>file</code>.
Note that files are automatically closed when
their handles are garbage collected,
but that takes an unpredictable amount of time to happen.




</p><p>
</p><hr><h3><a name="pdf-file:flush"><code>file:flush ()</code></a></h3>


<p>
Saves any written data to <code>file</code>.




</p><p>
</p><hr><h3><a name="pdf-file:lines"><code>file:lines ()</code></a></h3>


<p>
Returns an iterator function that,
each time it is called,
returns a new line from the file.
Therefore, the construction

</p><pre>     for line in file:lines() do <em>body</em> end
</pre><p>
will iterate over all lines of the file.
(Unlike <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.lines"><code>io.lines</code></a>, this function does not close the file
when the loop ends.)




</p><p>
</p><hr><h3><a name="pdf-file:read"><code>file:read (···)</code></a></h3>


<p>
Reads the file <code>file</code>,
according to the given formats, which specify what to read.
For each format,
the function returns a string (or a number) with the characters read,
or <b>nil</b> if it cannot read data with the specified format.
When called without formats,
it uses a default format that reads the entire next line
(see below).


</p><p>
The available formats are

</p><ul>

<li><b>"*n":</b>
reads a number;
this is the only format that returns a number instead of a string.
</li>

<li><b>"*a":</b>
reads the whole file, starting at the current position.
On end of file, it returns the empty string.
</li>

<li><b>"*l":</b>
reads the next line (skipping the end of line),
returning <b>nil</b> on end of file.
This is the default format.
</li>

<li><b><em>number</em>:</b>
reads a string with up to this number of characters,
returning <b>nil</b> on end of file.
If number is zero,
it reads nothing and returns an empty string,
or <b>nil</b> on end of file.
</li>

</ul>



<p>
</p><hr><h3><a name="pdf-file:seek"><code>file:seek ([whence] [, offset])</code></a></h3>


<p>
Sets and gets the file position,
measured from the beginning of the file,
to the position given by <code>offset</code> plus a base
specified by the string <code>whence</code>, as follows:

</p><ul>
<li><b>"set":</b> base is position 0 (beginning of the file);</li>
<li><b>"cur":</b> base is current position;</li>
<li><b>"end":</b> base is end of file;</li>
</ul><p>
In case of success, function <code>seek</code> returns the final file position,
measured in bytes from the beginning of the file.
If this function fails, it returns <b>nil</b>,
plus a string describing the error.


</p><p>
The default value for <code>whence</code> is <code>"cur"</code>,
and for <code>offset</code> is 0.
Therefore, the call <code>file:seek()</code> returns the current
file position, without changing it;
the call <code>file:seek("set")</code> sets the position to the
beginning of the file (and returns 0);
and the call <code>file:seek("end")</code> sets the position to the
end of the file, and returns its size.




</p><p>
</p><hr><h3><a name="pdf-file:setvbuf"><code>file:setvbuf (mode [, size])</code></a></h3>


<p>
Sets the buffering mode for an output file.
There are three available modes:

</p><ul>

<li><b>"no":</b>
no buffering; the result of any output operation appears immediately.
</li>

<li><b>"full":</b>
full buffering; output operation is performed only
when the buffer is full (or when you explicitly <code>flush</code> the file
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.flush"><code>io.flush</code></a>)).
</li>

<li><b>"line":</b>
line buffering; output is buffered until a newline is output
or there is any input from some special files
(such as a terminal device).
</li>

</ul><p>
For the last two cases, <code>sizes</code>
specifies the size of the buffer, in bytes.
The default is an appropriate size.




</p><p>
</p><hr><h3><a name="pdf-file:write"><code>file:write (···)</code></a></h3>


<p>
Writes the value of each of its arguments to
the <code>file</code>.
The arguments must be strings or numbers.
To write other values,
use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-tostring"><code>tostring</code></a> or <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a> before <code>write</code>.







</p><h2>5.8 - <a name="5.8">Operating System Facilities</a></h2>

<p>
This library is implemented through table <a name="pdf-os"><code>os</code></a>.


</p><p>
</p><hr><h3><a name="pdf-os.clock"><code>os.clock ()</code></a></h3>


<p>
Returns an approximation of the amount in seconds of CPU time
used by the program.




</p><p>
</p><hr><h3><a name="pdf-os.date"><code>os.date ([format [, time]])</code></a></h3>


<p>
Returns a string or a table containing date and time,
formatted according to the given string <code>format</code>.


</p><p>
If the <code>time</code> argument is present,
this is the time to be formatted
(see the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-os.time"><code>os.time</code></a> function for a description of this value).
Otherwise, <code>date</code> formats the current time.


</p><p>
If <code>format</code> starts with '<code>!</code>',
then the date is formatted in Coordinated Universal Time.
After this optional character,
if <code>format</code> is the string "<code>*t</code>",
then <code>date</code> returns a table with the following fields:
<code>year</code> (four digits), <code>month</code> (1--12), <code>day</code> (1--31),
<code>hour</code> (0--23), <code>min</code> (0--59), <code>sec</code> (0--61),
<code>wday</code> (weekday, Sunday is&nbsp;1),
<code>yday</code> (day of the year),
and <code>isdst</code> (daylight saving flag, a boolean).


</p><p>
If <code>format</code> is not "<code>*t</code>",
then <code>date</code> returns the date as a string,
formatted according to the same rules as the C&nbsp;function <code>strftime</code>.


</p><p>
When called without arguments,
<code>date</code> returns a reasonable date and time representation that depends on
the host system and on the current locale
(that is, <code>os.date()</code> is equivalent to <code>os.date("%c")</code>).




</p><p>
</p><hr><h3><a name="pdf-os.difftime"><code>os.difftime (t2, t1)</code></a></h3>


<p>
Returns the number of seconds from time <code>t1</code> to time <code>t2</code>.
In POSIX, Windows, and some other systems,
this value is exactly <code>t2</code><em>-</em><code>t1</code>.




</p><p>
</p><hr><h3><a name="pdf-os.execute"><code>os.execute ([command])</code></a></h3>


<p>
This function is equivalent to the C&nbsp;function <code>system</code>.
It passes <code>command</code> to be executed by an operating system shell.
It returns a status code, which is system-dependent.
If <code>command</code> is absent, then it returns nonzero if a shell is available
and zero otherwise.




</p><p>
</p><hr><h3><a name="pdf-os.exit"><code>os.exit ([code])</code></a></h3>


<p>
Calls the C&nbsp;function <code>exit</code>,
with an optional <code>code</code>,
to terminate the host program.
The default value for <code>code</code> is the success code.




</p><p>
</p><hr><h3><a name="pdf-os.getenv"><code>os.getenv (varname)</code></a></h3>


<p>
Returns the value of the process environment variable <code>varname</code>,
or <b>nil</b> if the variable is not defined.




</p><p>
</p><hr><h3><a name="pdf-os.remove"><code>os.remove (filename)</code></a></h3>


<p>
Deletes the file or directory with the given name.
Directories must be empty to be removed.
If this function fails, it returns <b>nil</b>,
plus a string describing the error.




</p><p>
</p><hr><h3><a name="pdf-os.rename"><code>os.rename (oldname, newname)</code></a></h3>


<p>
Renames file or directory named <code>oldname</code> to <code>newname</code>.
If this function fails, it returns <b>nil</b>,
plus a string describing the error.




</p><p>
</p><hr><h3><a name="pdf-os.setlocale"><code>os.setlocale (locale [, category])</code></a></h3>


<p>
Sets the current locale of the program.
<code>locale</code> is a string specifying a locale;
<code>category</code> is an optional string describing which category to change:
<code>"all"</code>, <code>"collate"</code>, <code>"ctype"</code>,
<code>"monetary"</code>, <code>"numeric"</code>, or <code>"time"</code>;
the default category is <code>"all"</code>.
The function returns the name of the new locale,
or <b>nil</b> if the request cannot be honored.


</p><p>
When called with <b>nil</b> as the first argument,
this function only returns the name of the current locale
for the given category.




</p><p>
</p><hr><h3><a name="pdf-os.time"><code>os.time ([table])</code></a></h3>


<p>
Returns the current time when called without arguments,
or a time representing the date and time specified by the given table.
This table must have fields <code>year</code>, <code>month</code>, and <code>day</code>,
and may have fields <code>hour</code>, <code>min</code>, <code>sec</code>, and <code>isdst</code>
(for a description of these fields, see the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-os.date"><code>os.date</code></a> function).


</p><p>
The returned value is a number, whose meaning depends on your system.
In POSIX, Windows, and some other systems, this number counts the number
of seconds since some given start time (the "epoch").
In other systems, the meaning is not specified,
and the number returned by <code>time</code> can be used only as an argument to
<code>date</code> and <code>difftime</code>.




</p><p>
</p><hr><h3><a name="pdf-os.tmpname"><code>os.tmpname ()</code></a></h3>


<p>
Returns a string with a file name that can
be used for a temporary file.
The file must be explicitly opened before its use
and explicitly removed when no longer needed.







</p><h2>5.9 - <a name="5.9">The Debug Library</a></h2>

<p>
This library provides
the functionality of the debug interface to Lua programs.
You should exert care when using this library.
The functions provided here should be used exclusively for debugging
and similar tasks, such as profiling.
Please resist the temptation to use them as a
usual programming tool:
they can be very slow.
Moreover, several of its functions
violate some assumptions about Lua code
(e.g., that variables local to a function
cannot be accessed from outside or
that userdata metatables cannot be changed by Lua code)
and therefore can compromise otherwise secure code.


</p><p>
All functions in this library are provided
inside the <a name="pdf-debug"><code>debug</code></a> table.
All functions that operate over a thread
have an optional first argument which is the
thread to operate over.
The default is always the current thread.


</p><p>
</p><hr><h3><a name="pdf-debug.debug"><code>debug.debug ()</code></a></h3>


<p>
Enters an interactive mode with the user,
running each string that the user enters.
Using simple commands and other debug facilities,
the user can inspect global and local variables,
change their values, evaluate expressions, and so on.
A line containing only the word <code>cont</code> finishes this function,
so that the caller continues its execution.


</p><p>
Note that commands for <code>debug.debug</code> are not lexically nested
within any function, and so have no direct access to local variables.




</p><p>
</p><hr><h3><a name="pdf-debug.getfenv"><code>debug.getfenv (o)</code></a></h3>
Returns the environment of object <code>o</code>.




<p>
</p><hr><h3><a name="pdf-debug.gethook"><code>debug.gethook ([thread])</code></a></h3>


<p>
Returns the current hook settings of the thread, as three values:
the current hook function, the current hook mask,
and the current hook count
(as set by the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-debug.sethook"><code>debug.sethook</code></a> function).




</p><p>
</p><hr><h3><a name="pdf-debug.getinfo"><code>debug.getinfo ([thread,] function [, what])</code></a></h3>


<p>
Returns a table with information about a function.
You can give the function directly,
or you can give a number as the value of <code>function</code>,
which means the function running at level <code>function</code> of the call stack
of the given thread:
level&nbsp;0 is the current function (<code>getinfo</code> itself);
level&nbsp;1 is the function that called <code>getinfo</code>;
and so on.
If <code>function</code> is a number larger than the number of active functions,
then <code>getinfo</code> returns <b>nil</b>.


</p><p>
The returned table may contain all the fields returned by <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a>,
with the string <code>what</code> describing which fields to fill in.
The default for <code>what</code> is to get all information available,
except the table of valid lines.
If present,
the option '<code>f</code>'
adds a field named <code>func</code> with the function itself.
If present,
the option '<code>L</code>'
adds a field named <code>activelines</code> with the table of
valid lines.


</p><p>
For instance, the expression <code>debug.getinfo(1,"n").name</code> returns
a name of the current function, if a reasonable name can be found,
and the expression <code>debug.getinfo(print)</code>
returns a table with all available information
about the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-print"><code>print</code></a> function.




</p><p>
</p><hr><h3><a name="pdf-debug.getlocal"><code>debug.getlocal ([thread,] level, local)</code></a></h3>


<p>
This function returns the name and the value of the local variable
with index <code>local</code> of the function at level <code>level</code> of the stack.
(The first parameter or local variable has index&nbsp;1, and so on,
until the last active local variable.)
The function returns <b>nil</b> if there is no local
variable with the given index,
and raises an error when called with a <code>level</code> out of range.
(You can call <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-debug.getinfo"><code>debug.getinfo</code></a> to check whether the level is valid.)


</p><p>
Variable names starting with '<code>(</code>' (open parentheses)
represent internal variables
(loop control variables, temporaries, and C&nbsp;function locals).




</p><p>
</p><hr><h3><a name="pdf-debug.getmetatable"><code>debug.getmetatable (object)</code></a></h3>


<p>
Returns the metatable of the given <code>object</code>
or <b>nil</b> if it does not have a metatable.




</p><p>
</p><hr><h3><a name="pdf-debug.getregistry"><code>debug.getregistry ()</code></a></h3>


<p>
Returns the registry table (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.5">§3.5</a>).




</p><p>
</p><hr><h3><a name="pdf-debug.getupvalue"><code>debug.getupvalue (func, up)</code></a></h3>


<p>
This function returns the name and the value of the upvalue
with index <code>up</code> of the function <code>func</code>.
The function returns <b>nil</b> if there is no upvalue with the given index.




</p><p>
</p><hr><h3><a name="pdf-debug.setfenv"><code>debug.setfenv (object, table)</code></a></h3>


<p>
Sets the environment of the given <code>object</code> to the given <code>table</code>.
Returns <code>object</code>.




</p><p>
</p><hr><h3><a name="pdf-debug.sethook"><code>debug.sethook ([thread,] hook, mask [, count])</code></a></h3>


<p>
Sets the given function as a hook.
The string <code>mask</code> and the number <code>count</code> describe
when the hook will be called.
The string mask may have the following characters,
with the given meaning:

</p><ul>
<li><b><code>"c"</code>:</b> The hook is called every time Lua calls a function;</li>
<li><b><code>"r"</code>:</b> The hook is called every time Lua returns from a function;</li>
<li><b><code>"l"</code>:</b> The hook is called every time Lua enters a new line of code.</li>
</ul><p>
With a <code>count</code> different from zero,
the hook is called after every <code>count</code> instructions.


</p><p>
When called without arguments,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-debug.sethook"><code>debug.sethook</code></a> turns off the hook.


</p><p>
When the hook is called, its first parameter is a string
describing the event that has triggered its call:
<code>"call"</code>, <code>"return"</code> (or <code>"tail return"</code>),
<code>"line"</code>, and <code>"count"</code>.
For line events,
the hook also gets the new line number as its second parameter.
Inside a hook,
you can call <code>getinfo</code> with level&nbsp;2 to get more information about
the running function
(level&nbsp;0 is the <code>getinfo</code> function,
and level&nbsp;1 is the hook function),
unless the event is <code>"tail return"</code>.
In this case, Lua is only simulating the return,
and a call to <code>getinfo</code> will return invalid data.




</p><p>
</p><hr><h3><a name="pdf-debug.setlocal"><code>debug.setlocal ([thread,] level, local, value)</code></a></h3>


<p>
This function assigns the value <code>value</code> to the local variable
with index <code>local</code> of the function at level <code>level</code> of the stack.
The function returns <b>nil</b> if there is no local
variable with the given index,
and raises an error when called with a <code>level</code> out of range.
(You can call <code>getinfo</code> to check whether the level is valid.)
Otherwise, it returns the name of the local variable.




</p><p>
</p><hr><h3><a name="pdf-debug.setmetatable"><code>debug.setmetatable (object, table)</code></a></h3>


<p>
Sets the metatable for the given <code>object</code> to the given <code>table</code>
(which can be <b>nil</b>).




</p><p>
</p><hr><h3><a name="pdf-debug.setupvalue"><code>debug.setupvalue (func, up, value)</code></a></h3>


<p>
This function assigns the value <code>value</code> to the upvalue
with index <code>up</code> of the function <code>func</code>.
The function returns <b>nil</b> if there is no upvalue
with the given index.
Otherwise, it returns the name of the upvalue.




</p><p>
</p><hr><h3><a name="pdf-debug.traceback"><code>debug.traceback ([thread,] [message] [, level])</code></a></h3>


<p>
Returns a string with a traceback of the call stack.
An optional <code>message</code> string is appended
at the beginning of the traceback.
An optional <code>level</code> number tells at which level
to start the traceback
(default is 1, the function calling <code>traceback</code>).







</p><h1>6 - <a name="6">Lua Stand-alone</a></h1>

<p>
Although Lua has been designed as an extension language,
to be embedded in a host C&nbsp;program,
it is also frequently used as a stand-alone language.
An interpreter for Lua as a stand-alone language,
called simply <code>lua</code>,
is provided with the standard distribution.
The stand-alone interpreter includes
all standard libraries, including the debug library.
Its usage is:

</p><pre>     lua [options] [script [args]]
</pre><p>
The options are:

</p><ul>
<li><b><code>-e <em>stat</em></code>:</b> executes string <em>stat</em>;</li>
<li><b><code>-l <em>mod</em></code>:</b> "requires" <em>mod</em>;</li>
<li><b><code>-i</code>:</b> enters interactive mode after running <em>script</em>;</li>
<li><b><code>-v</code>:</b> prints version information;</li>
<li><b><code>--</code>:</b> stops handling options;</li>
<li><b><code>-</code>:</b> executes <code>stdin</code> as a file and stops handling options.</li>
</ul><p>
After handling its options, <code>lua</code> runs the given <em>script</em>,
passing to it the given <em>args</em> as string arguments.
When called without arguments,
<code>lua</code> behaves as <code>lua -v -i</code>
when the standard input (<code>stdin</code>) is a terminal,
and as <code>lua -</code> otherwise.


</p><p>
Before running any argument,
the interpreter checks for an environment variable <a name="pdf-LUA_INIT"><code>LUA_INIT</code></a>.
If its format is <code>@<em>filename</em></code>,
then <code>lua</code> executes the file.
Otherwise, <code>lua</code> executes the string itself.


</p><p>
All options are handled in order, except <code>-i</code>.
For instance, an invocation like

</p><pre>     $ lua -e'a=1' -e 'print(a)' script.lua
</pre><p>
will first set <code>a</code> to 1, then print the value of <code>a</code> (which is '<code>1</code>'),
and finally run the file <code>script.lua</code> with no arguments.
(Here <code>$</code> is the shell prompt. Your prompt may be different.)


</p><p>
Before starting to run the script,
<code>lua</code> collects all arguments in the command line
in a global table called <code>arg</code>.
The script name is stored at index 0,
the first argument after the script name goes to index 1,
and so on.
Any arguments before the script name
(that is, the interpreter name plus the options)
go to negative indices.
For instance, in the call

</p><pre>     $ lua -la b.lua t1 t2
</pre><p>
the interpreter first runs the file <code>a.lua</code>,
then creates a table

</p><pre>     arg = { [-2] = "lua", [-1] = "-la",
             [0] = "b.lua",
             [1] = "t1", [2] = "t2" }
</pre><p>
and finally runs the file <code>b.lua</code>.
The script is called with <code>arg[1]</code>, <code>arg[2]</code>, ···
as arguments;
it can also access these arguments with the vararg expression '<code>...</code>'.


</p><p>
In interactive mode,
if you write an incomplete statement,
the interpreter waits for its completion
by issuing a different prompt.


</p><p>
If the global variable <a name="pdf-_PROMPT"><code>_PROMPT</code></a> contains a string,
then its value is used as the prompt.
Similarly, if the global variable <a name="pdf-_PROMPT2"><code>_PROMPT2</code></a> contains a string,
its value is used as the secondary prompt
(issued during incomplete statements).
Therefore, both prompts can be changed directly on the command line.
For instance,

</p><pre>     $ lua -e"_PROMPT='myprompt&gt; '" -i
</pre><p>
(the outer pair of quotes is for the shell,
the inner pair is for Lua),
or in any Lua programs by assigning to <code>_PROMPT</code>.
Note the use of <code>-i</code> to enter interactive mode; otherwise,
the program would just end silently right after the assignment to <code>_PROMPT</code>.


</p><p>
To allow the use of Lua as a
script interpreter in Unix systems,
the stand-alone interpreter skips
the first line of a chunk if it starts with <code>#</code>.
Therefore, Lua scripts can be made into executable programs
by using <code>chmod +x</code> and the&nbsp;<code>#!</code> form,
as in

</p><pre>     #!/usr/local/bin/lua
</pre><p>
(Of course,
the location of the Lua interpreter may be different in your machine.
If <code>lua</code> is in your <code>PATH</code>,
then 

</p><pre>     #!/usr/bin/env lua
</pre><p>
is a more portable solution.) 



</p><h1>7 - <a name="7">Incompatibilities with the Previous Version</a></h1>

<p>
Here we list the incompatibilities that you may found when moving a program
from Lua&nbsp;5.0 to Lua&nbsp;5.1.
You can avoid most of the incompatibilities compiling Lua with
appropriate options (see file <code>luaconf.h</code>).
However,
all these compatibility options will be removed in the next version of Lua.



</p><h2>7.1 - <a name="7.1">Changes in the Language</a></h2>
<ul>

<li>
The vararg system changed from the pseudo-argument <code>arg</code> with a
table with the extra arguments to the vararg expression.
(See compile-time option <code>LUA_COMPAT_VARARG</code> in <code>luaconf.h</code>.)
</li>

<li>
There was a subtle change in the scope of the implicit
variables of the <b>for</b> statement and for the <b>repeat</b> statement.
</li>

<li>
The long string/long comment syntax (<code>[[<em>string</em>]]</code>)
does not allow nesting.
You can use the new syntax (<code>[=[<em>string</em>]=]</code>) in these cases.
(See compile-time option <code>LUA_COMPAT_LSTR</code> in <code>luaconf.h</code>.)
</li>

</ul>




<h2>7.2 - <a name="7.2">Changes in the Libraries</a></h2>
<ul>

<li>
Function <code>string.gfind</code> was renamed <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.gmatch"><code>string.gmatch</code></a>.
(See compile-time option <code>LUA_COMPAT_GFIND</code> in <code>luaconf.h</code>.)
</li>

<li>
When <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.gsub"><code>string.gsub</code></a> is called with a function as its
third argument,
whenever this function returns <b>nil</b> or <b>false</b> the
replacement string is the whole match,
instead of the empty string.
</li>

<li>
Function <code>table.setn</code> was deprecated.
Function <code>table.getn</code> corresponds
to the new length operator (<code>#</code>);
use the operator instead of the function.
(See compile-time option <code>LUA_COMPAT_GETN</code> in <code>luaconf.h</code>.)
</li>

<li>
Function <code>loadlib</code> was renamed <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.loadlib"><code>package.loadlib</code></a>.
(See compile-time option <code>LUA_COMPAT_LOADLIB</code> in <code>luaconf.h</code>.)
</li>

<li>
Function <code>math.mod</code> was renamed <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-math.fmod"><code>math.fmod</code></a>.
(See compile-time option <code>LUA_COMPAT_MOD</code> in <code>luaconf.h</code>.)
</li>

<li>
Functions <code>table.foreach</code> and <code>table.foreachi</code> are deprecated.
You can use a for loop with <code>pairs</code> or <code>ipairs</code> instead.
</li>

<li>
There were substantial changes in function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> due to
the new module system.
However, the new behavior is mostly compatible with the old,
but <code>require</code> gets the path from <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.path"><code>package.path</code></a> instead
of from <code>LUA_PATH</code>.
</li>

<li>
Function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-collectgarbage"><code>collectgarbage</code></a> has different arguments.
Function <code>gcinfo</code> is deprecated;
use <code>collectgarbage("count")</code> instead.
</li>

</ul>




<h2>7.3 - <a name="7.3">Changes in the API</a></h2>
<ul>

<li>
The <code>luaopen_*</code> functions (to open libraries)
cannot be called directly,
like a regular C function.
They must be called through Lua,
like a Lua function.
</li>

<li>
Function <code>lua_open</code> was replaced by <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> to
allow the user to set a memory-allocation function.
You can use <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newstate"><code>luaL_newstate</code></a> from the standard library to
create a state with a standard allocation function
(based on <code>realloc</code>).
</li>

<li>
Functions <code>luaL_getn</code> and <code>luaL_setn</code>
(from the auxiliary library) are deprecated.
Use <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_objlen"><code>lua_objlen</code></a> instead of <code>luaL_getn</code>
and nothing instead of <code>luaL_setn</code>.
</li>

<li>
Function <code>luaL_openlib</code> was replaced by <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_register"><code>luaL_register</code></a>.
</li>

<li>
Function <code>luaL_checkudata</code> now throws an error when the given value
is not a userdata of the expected type.
(In Lua&nbsp;5.0 it returned <code>NULL</code>.)
</li>

</ul>




<h1>8 - <a name="8">The Complete Syntax of Lua</a></h1>

<p>
Here is the complete syntax of Lua in extended BNF.
(It does not describe operator precedences.)




</p><pre>
	chunk ::= {stat [`<b>;</b>′]} [laststat [`<b>;</b>′]]

	block ::= chunk

	stat ::=  varlist1 `<b>=</b>′ explist1 | 
		 functioncall | 
		 <b>do</b> block <b>end</b> | 
		 <b>while</b> exp <b>do</b> block <b>end</b> | 
		 <b>repeat</b> block <b>until</b> exp | 
		 <b>if</b> exp <b>then</b> block {<b>elseif</b> exp <b>then</b> block} [<b>else</b> block] <b>end</b> | 
		 <b>for</b> Name `<b>=</b>′ exp `<b>,</b>′ exp [`<b>,</b>′ exp] <b>do</b> block <b>end</b> | 
		 <b>for</b> namelist <b>in</b> explist1 <b>do</b> block <b>end</b> | 
		 <b>function</b> funcname funcbody | 
		 <b>local</b> <b>function</b> Name funcbody | 
		 <b>local</b> namelist [`<b>=</b>′ explist1] 

	laststat ::= <b>return</b> [explist1] | <b>break</b>

	funcname ::= Name {`<b>.</b>′ Name} [`<b>:</b>′ Name]

	varlist1 ::= var {`<b>,</b>′ var}

	var ::=  Name | prefixexp `<b>[</b>′ exp `<b>]</b>′ | prefixexp `<b>.</b>′ Name 

	namelist ::= Name {`<b>,</b>′ Name}

	explist1 ::= {exp `<b>,</b>′} exp

	exp ::=  <b>nil</b> | <b>false</b> | <b>true</b> | Number | String | `<b>...</b>′ | function | 
		 prefixexp | tableconstructor | exp binop exp | unop exp 

	prefixexp ::= var | functioncall | `<b>(</b>′ exp `<b>)</b>′

	functioncall ::=  prefixexp args | prefixexp `<b>:</b>′ Name args 

	args ::=  `<b>(</b>′ [explist1] `<b>)</b>′ | tableconstructor | String 

	function ::= <b>function</b> funcbody

	funcbody ::= `<b>(</b>′ [parlist1] `<b>)</b>′ block <b>end</b>

	parlist1 ::= namelist [`<b>,</b>′ `<b>...</b>′] | `<b>...</b>′

	tableconstructor ::= `<b>{</b>′ [fieldlist] `<b>}</b>′

	fieldlist ::= field {fieldsep field} [fieldsep]

	field ::= `<b>[</b>′ exp `<b>]</b>′ `<b>=</b>′ exp | Name `<b>=</b>′ exp | exp

	fieldsep ::= `<b>,</b>′ | `<b>;</b>′

	binop ::= `<b>+</b>′ | `<b>-</b>′ | `<b>*</b>′ | `<b>/</b>′ | `<b>^</b>′ | `<b>%</b>′ | `<b>..</b>′ | 
		 `<b>&lt;</b>′ | `<b>&lt;=</b>′ | `<b>&gt;</b>′ | `<b>&gt;=</b>′ | `<b>==</b>′ | `<b>~=</b>′ | 
		 <b>and</b> | <b>or</b>

	unop ::= `<b>-</b>′ | <b>not</b> | `<b>#</b>′

</pre>

<p>






</p><hr>
<small>
Last update:
Tue Oct  3 21:27:28 BRT 2006
<br>
译文最后更新：修改几处别字
2009年4月7日
</small>
<!--
Last change: minor edit
-->



<div id="feedly-mini" title="feedly Mini tookit"></div>

<!--
</body>
<div></div>
</html>
-->
