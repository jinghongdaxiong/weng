#怎样使用Markdown?

##1:markdown是为那些使用者设计的
首先要确定你是否真的需要markdown,使用某种
工具是为了提高效率或者某种体验的,如果这种
工具并不能显著帮你改善体验,那就让它见鬼去
吧,哪怕这个工具学起来简单.
Markdown是为那些需要经常码字或者进行文字
排版的.对码字手速和排版顺畅度有要求的人群
设计的,他们希望用键盘把文字内容啪啪啪地打
出来后就已经排版好了,最好从头到尾都不要
使用鼠标.这些人包括经常需要写文档的码农.
博客写手 网站编辑 出版业人士等等.
通常情况下,网络上需要进行大量文字输入的
地方都可以通过所见即所得的方式排版(比如
知乎的答案编辑模式),本地写作的话则可以使
用Word这类常用的文本编辑软件,当然你也可
以蛋疼地手工使用html标签实现排版效果--
而Markdown只是使这一切更方便了一点而已,
所以如果你觉得现有文本编辑方式完全够用
了,就别费神折腾了(除非你在使用像github
这样Markdown作为主流编辑方式的网站).

##2:Markdown语法

###段落 标题 区块代码
一个段落是由一个以上的连接的行句组成,而一个以上的空行则会划分出不同的段落(
空行的定义是显示上看起来像空行,就被视为空行,例如有一行只有空白和tab,那该行
也会被视为空行),一般的段落不需要用空白或换行缩进.

Markdown支持两种标题的语法,Setext和atx形式.Setext形式是用底线的形式,利用
= (最高阶标题)和 -(第二阶标题),

区块引用则使用email形式的'>'角括号.
####markdown语法:
A First Level Header
====================
A Second Level Header
---------------------

Now is the time for all good men to come to 
the aid of their country .this is just a
regular paragraph.

the quick brown fox jumped over the lazy
dog's back.
### Header 3

>This is a blockquote.
>
>This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote

##修饰和强调

Markdown使用星号和底线来标记需要强调的区段.
Markdown语法:

Some of these words *are emphasized*.
Some of these words _are emphasized also_.
Use two asterisks for **strong emphasis**.
Or,if you perfer,__use two underscores instead__.

##列表
###无序列表使用星号 加号和减号来作为列表的项目标记,这些符号都是可以使用的
####使用星号:
* Candy.
* Gum.
* Booze
####加号
+ Candy.
+ Gum.
+ Booze
####减号
- Candy.
- Gum.
- Booze
###有序列表则是使用一般的数字接着一个英文句点作为项目标记:
1. Red
2. Green
3. Blue
##如果你在项目之间插入空行,那项目的内容就会用<p>包起来,你也可以在一个项目内放上多个段落,只要在它前面缩排4个空白或1个tab.

#链接
Markdown支持两种形式的链接语法:行内和参考两种形式,两种都是使用角括号来把文字转成连结.
行内形式是直接形式是直接在后面用括号直接接上链接:
This is an [example link](http://example.com/)

输出 HTML 为：

<p>This is an <a href="http://example.com/">
example link</a>.</p>

你也可以选择性的加上 title 属性：

This is an [example link](http://example.com/ "With a Title").
输出 HTML 为：

<p>This is an <a href="http://example.com/" title="With a Title">
example link</a>.</p>

参考形式的链接让你可以为链接定一个名称，之后你可以在文件的其他地方定义该链接的内容：

I get 10 times more traffic from [Google][1] than from
[Yahoo][2] or [MSN][3].

[1]: http://google.com/ "Google"
[2]: http://search.yahoo.com/ "Yahoo Search"
[3]: http://search.msn.com/ "MSN Search"

输出 HTML 为：

<p>I get 10 times more traffic from <a href="http://google.com/"
title="Google">Google</a> than from <a href="http://search.yahoo.com/"
title="Yahoo Search">Yahoo</a> or <a href="http://search.msn.com/"
title="MSN Search">MSN</a>.</p>

title 属性是选择性的，链接名称可以用字母、数字和空格，但是不分大小写：

I start my morning with a cup of coffee and
[The New York Times][NY Times].

[ny times]: http://www.nytimes.com/
输出 HTML 为：

<p>I start my morning with a cup of coffee and
<a href="http://www.nytimes.com/">The New York Times</a>.</p>

#图片
图片的语法跟链接很像.
行内形式(title是选择性的):
![alt text](/path/to/img.jpg "Title")
参考形式:
![alt text][id]
[id]:/path/to/img.jpg"Title"
上面两种方法都会输出HTML为:
<img src="/path/to/img.jpg" alt="alt text" title="Title" />

#代码
在一般的段落文字中,你可以使用反引号` 来标记代码区段,区段内的&、< 和 > 都
会被自动的转换为HTML实体,这项特性让你可以很容易的在代码区段内插入HTML码:

I strongly recommend against using any `<blink>` tags.

I wish SmartyPants used named entities like `&mdash;`
instead of decimal-encoded entites like `&#8212;`.


