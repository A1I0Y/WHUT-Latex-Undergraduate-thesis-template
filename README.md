# 注意

本文件是对GitHub中前辈文件[WHUT-Bachelor-Degree-Thesis-LaTeX-Template](https://github.com/GuangtaoLyu/WHUT-Bachelor-Degree-Thesis-LaTeX-Template)的改进。

## 之前文件的read me

对于已有论文写作经验的人来说，Latex无疑是一个更好更方便的工具，特别是对于理工科学生而言，Latex能更方便地插入公式、论文、图片等多种形式的内容，并且可以在一定程度上减少排版的工作量。特别在这种有了前人做好的模板的基础上，我们就可以专注于内容，不太需要考虑各种格式问题。当然，如果有前人的word模板，也能很方便地完成毕业论文。

**这是曹宇学长做的latex模板，非官方的。感谢曹宇前辈的工作和分享**

原始链接：https://github.com/tsaoyu/WHUT-LaTeX-bachelor。感谢曹宇前辈的工作和分享。我是在https://www.latexstudio.net/archives/6530.html  这个链接上下载的。

我在使用的过程中，遇到了一点点的小问题，特在此记录且分享出来。我本人也只是简单的使用Latex，对Latex的各种原理也不了解，以下的分享仅仅是我自己在搜集整理后，在自己的条件下可行的解决方法。不保证完全正确，仅仅是分享出来，为后来者节约一些时间。答辩完，修改时间比较短，都是一些能用就行的方案，没有仔细看。

### 参考文献引用问题

问题：latex参考文献出现[S.1.]或[S.1.s.n.]等问题。

原因：通过多方搜索，看起来是缺少了address、doi等信息。默认替换成了S.1 S.n等。

解决方法：一个轻松能用的解决方法，在对应的bst文件中，搜索s.1 s.n等，然后替换成""空字符串。

首先我在thesis.tex中明确使用 gbt7714-numerical。个人猜测这样他就使用了gbt7714-numerical.bst。 原始只写了gbt7714。 \usepackage{gbt7714}                 %配置gb7714引用格式

我在此基础上指定了对应的文件。这个我粗略理解为用了空着bib引用信息的。答辩完，修改时间比较短，没有深究。 \bibliographystyle{gbt7714-numerical}

然后，在gbt7714-numerical.bst 中搜索s.1 s.n等信息，替换为空字符串。 "[S.l.]" -> ""

会有多种S.xxx信息，不放心的可以都替换掉。

### 手写签名以及日期

这个如果需要，直接搜索就行。

```
\begin{minipage}{2cm}
\includegraphics[height=2\baselineskip]{figure/吕光涛_手写签名.png}
\end{minipage} \quad\quad\quad\quad \\
 
\begin{minipage}{2cm}
\includegraphics[height=2\baselineskip]{figure/吕光涛_手写签名.png} 
\end{minipage} \quad\quad 2023 年 6 月  10  日\\

     
以及是否保密 打勾
$ \CheckedBox $ 

%\usepackage{wasysym} %保密那里打勾用得上 这个命令的位置放在靠后一些的地方，放的靠前会冲突。
```

 ### 总结

这是我在使用过程中，以及答辩之后，老师觉得格式不合理的地方。我经过多方搜索，以及自己的尝试，最终解决了问题。特此记录一下，给后来者提供一定的参考。

由于我本身只是在以往写论文过程中使用到了latex，但是对latex本身了解也不多，加上时间紧迫，很多解决方法可能不是那么合理，搜集整理和猜测的原因也不一定准确，只能说勉强可行。如果不可行，请自行使用关键词搜索，很多都是经典问题。

至于模板的使用方式可以参考前文链接，原始链接：https://github.com/tsaoyu/WHUT-LaTeX-bachelor。感谢曹宇前辈的工作和分享。我是在https://www.latexstudio.net/archives/6530.html  这个链接上下载的。

我本身的环境是 Win10， 使用Textstudio， 默认编译器：Xelatex。



## 新的修改和补充

在我的修改之后，本文件已经完美符合本科毕业论文的要求，本人已通过答辩。

我的环境是win10+Textstudio

### 运行前注意

首先在全文开头加一个`% !TeX program = xelatex`，这样使用xelatex进行编译

其次，安装一个华文中宋字体，我已放入文件夹font

### 新加入的宏包和作用

1、存在一个链接出现红色方框的问题（无论是外部链接 还是内部链接），解决方法是先导入宏包`\usepackage{hyperref}`调用宏包中的如下代码：

``` latex
\hypersetup{
	colorlinks=true,
	linkcolor=black,
	filecolor=black,      
	urlcolor=black,
	citecolor=black,
}
```



2、插入浮动图片格式，在前文导入宏包`\usepackage{float} %浮动图片`

在thbp！的位置选用H



3、原始的有序列表使用的是小写数字1.2.3. 不符合论文要求，应该使用(1)(2)(3)

调用宏包`\usepackage{enumitem}`,可以让有序列表换成其他形式

```latex
\begin{enumerate}[label=(\arabic*)]      %括号加小写数字
    \item Apple is a kind of fruit.
    \item Cat is a kind of animal.
    \item Butterfly is a kind of insect.
\end{enumerate}


[label=\alph*.]                          %小写字母
[label=$(\mathbf{\arabic*})$]            %粗体+小写数字+括号
[label=\Alph*.]							 %大写字母
[label=\roman*.]						 %罗马字母，也可以大写
```



### 引用文献报错问题

当前文献用的是gbt7714宏包，Miktex+Texstudio，设置默认使用xetex+bibtex运行建议所有的关于引用文献的东西不要动，动了就寄

引入新的文献的时候，要开始以下的操作：

1、清空当前所有辅助文件，剪切移走当前的pdf。

2、用命令中运行xelatex，看看aux文件是否完整。

3、如果完整，运行bibtex，看看bbl文件是否完整。

4、两个文件都完整了，直接构建，即可。

注意！！有一些pdf图片放进去，可能会导致bibtex报错，需要换成png格式。