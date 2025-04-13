Latex

# 一、前言

### 1.环境配置

- 方法1：直接用latex自带的texworks上写
- 方法2：安装好latex后，配置vscode

### 2.命令行基础

掌握cd

# latex语法

一般语法：

```latex
\documentclass[11pt,a4paper,oneside]{article} 
\usepackage[utf8]{inputenc} %设置编码，默认utf8
\usepackage{amsmath, amsthm, amssymb, graphicx} % 宏包的导入

%相当于head部分
\title{这是标题}
\author{作者}
\date{2022} 

%相当于body部分
\begin{document}
\maketitle   %用于使上述的head部分生效，如果有则必要
\chapter{}
\section{First section}
Your text goes here.
\subsection{A subsection}

More text.

\end{document}
```

> **命令都以反斜杠\开头**，{}是必选项，[]是可选项。其中命令为以下两种形式之一： 
>
> - 反斜线和后面的一串字母，如 \LaTeX。它们以任意非字母符号（空格、数字、标点等）为 界限。
> -  反斜线和后面的单个非字母符号，如 \$。
>
> **对大小写敏感**
>
> **单行注释通过百分号 `%`** 进行；多行的注释，你需要使用 `\begin{comment}` 和 `\end{comment}`

## 1.文档类型

- 对于英文，可以用`book`、**article**和`beamer`；
- 对于中文，可以用`ctexbook`、**ctexart**和`ctexbeamer`，这些类型自带了对中文的支持。

```latex
%在编辑框第一行，输入如下内容来设置文件类型：
\documentclass[xx px,...]{ctexart}
```

## 正文

加空格来所见也没用，默认只当作一个空格，文档默认会进行首行缩进。相邻的两行在编译时仍然会视为同一段。

**另起一段的方式是使用一行相隔**

**另起一页的方式是：**

```tex
\newpage
```

在正文中，还可以设置局部的特殊字体：

| 字体     | 命令      |
| -------- | --------- |
| 直立     | \textup{} |
| 意大利   | \textit{} |
| 倾斜     | \textsl{} |
| 小型大写 | \textsc{} |
| 加宽加粗 | \textbf{} |

> bold font

## 章节

对于`ctexart`文件类型，章节可以用`\section{}`和`\subsection{}`命令来标记，例如：

```tex
\begin{document}

\section{一级标题}

\subsection{二级标题}

这里是正文. 

\subsection{二级标题}

这里是正文. 

\end{document}
```

## 目录

在有了章节的结构之后，使用`\tableofcontents`命令就可以在指定位置**生成目录**。通常带有目录的文件需要编译两次，因为需要先在目录中生成.toc文件，再据此生成目录。

```tex
\begin{document}

\tableofcontents

\end{document}
```

## 图片

插入图片需要使用`graphicx`宏包，建议使用如下方式：

```tex
\usepackage{graphicx}
\begin{figure}[htbp]
    \centering
    \includegraphics[width=8cm]{图片.jpg}
    \caption{图片标题}
\end{figure}
```

> 其中，`[htbp]`的作用是自动选择插入图片的最优位置，`\centering`设置让图片居中，`[width=8cm]`设置了图片的宽度为8cm，`\caption{}`用于设置图片的标题。

## 表格

LaTeX中表格的插入较为麻烦，可以直接使用[Create LaTeX tables online – TablesGenerator.com](https://link.zhihu.com/?target=https%3A//www.tablesgenerator.com/%23)来生成。建议使用如下方式：

```tex
\begin{table}[htbp]
    \centering
    \caption{表格标题}
    \begin{tabular}{ccc}
    \hline  %表示下面一行的上边框有一条线
        1 & 2 & 3 \\    \hline   %表示这一行的下边框有一条线
        4 & 5 & 6 \\    %\\是换行
        7 & 8 & 9
    \end{tabular}
\end{table}
```

## 列表

LaTeX中的列表环境包含无序列表`itemize`、有序列表`enumerate`和描述`description`，以`enumerate`为例，用法如下：

```tex
\begin{enumerate}
    \item 这是第一点; 
    \item 这是第二点;
    \item 这是第三点. 
\end{enumerate}
```

> 有序列表无序列表都是用的\item表示一项

另外，也可以自定义`\item`的样式：

```tex
\begin{enumerate}
    \item[(1)] 这是第一点; 
    \item[(2)] 这是第二点;
    \item[(3)] 这是第三点. 
\end{enumerate}
```

## 定理环境

定理环境需要使用`amsthm`宏包，首先在导言区加入：

```text
\newtheorem{theorem}{定理}[section]
```

其中`{theorem}`是环境的名称，`{定理}`设置了该环境显示的名称是“定理”，`[section]`的作用是让`theorem`环境在每个section中单独编号。在正文中，用如下方式来加入一条定理：

```tex
\begin{theorem}[定理名称]
    这里是定理的内容. 
\end{theorem}
```

其中`[定理名称]`不是必须的。另外，我们还可以建立新的环境，如果要让新的环境和`theorem`环境一起计数的话，可以用如下方式：

```tex
\newtheorem{theorem}{定理}[section]
\newtheorem{definition}[theorem]{定义}
\newtheorem{lemma}[theorem]{引理}
\newtheorem{corollary}[theorem]{推论}
\newtheorem{example}[theorem]{例}
\newtheorem{proposition}[theorem]{命题}
```

另外，定理的证明可以直接用`proof`环境。

## 页面

最开始选择文件类型时，我们设置的页面大小是a4paper，除此之外，我们也可以修改页面大小为b5paper等等。

一般情况下，LaTeX默认的页边距很大，为了让每一页显示的内容更多一些，我们可以使用`geometry`宏包，并在导言区加入以下代码：

```tex
\usepackage{geometry}
\geometry{left=2.54cm, right=2.54cm, top=3.18cm, bottom=3.18cm}
```

另外，为了设置行间距，可以使用如下代码：

```tex
\linespread{1.5}
```

## 页码

默认的页码编码方式是阿拉伯数字，用户也可以自己设置为小写罗马数字：

```tex
\pagenumbering{roman}
```

另外，`aiph`表示小写字母，`Aiph`表示大写字母，`Roman`表示大写罗马数字，`arabic`表示默认的阿拉伯数字。如果要设置页码的话，可以用如下代码来设置页码从0开始：

```tex
\setcounter{page}{0}
```

# 数学公式的输入方式

## 行内公式

**行内公式通常使用`$..$`来输入**，这通常被称为公式环境，例如：

```tex
若$a>0$, $b>0$, 则$a+b>0$.
```

公式环境通常使用特殊的字体，并且默认为斜体。需要注意的是，只要是公式，就需要放入公式环境中。如果需要在行内公式中展现出行间公式的效果，可以在前面加入`\displaystyle`，例如

```tex
设$\displaystyle\lim_{n\to\infty}x_n=x$.
```

## 行间公式

**行间公式需要用`$$..$$`来输入**，笔者习惯的输入方式如下：

```tex
若$a>0$, $b>0$, 则
$$
a+b>0.
$$
```

这种输入方式的一个好处是，这同时也是Markdown的语法。需要注意的是，**行间公式也是正文的一部分，需要与正文连贯，并且加入标点符号。**

关于具体的输入方式，可以参考[在线LaTeX公式编辑器-编辑器 (latexlive.com)](https://link.zhihu.com/?target=https%3A//www.latexlive.com/)，在这里只列举一些需要注意的。

## 上下标

上标可以用`^`输入，例如`a^n`，效果为 an ；下标可以用`_`来输入，例如`a_1`，效果为 a1 。上下标只会读取第一个字符，如果**上下标的内容较多的话，需要改成`^{}`或`_{}`。**

## 分式

分式可以用`\dfrac{}{}`来输入，例如`\dfrac{a}{b}`，效果为 ab 。为了在行间、分子、分母或者指数上输入较小的分式，可以改用`\frac{}{}`，例如`a^\frac{1}{n}`，效果为 a1n 。

## 括号

括号可以直接用`(..)`输入，但是需要注意的是，有时候括号内的内容高度较大，需要改用`\left(..\right)`。例如`\left(1+\dfrac{1}{n}\right)^n`，效果是 (1+1n)n 。

在中间需要隔开时，可以用`\left(..\middle|..\right)`。

另外，输入大括号{}时需要用`\{..\}`，其中`\`起到了转义作用。

## 加粗

对于加粗的公式，建议使用`bm`宏包，并且用命令`\bm{}`来加粗，这可以保留公式的斜体。

## 大括号

在这里可以使用`cases`环境，可以用于分段函数或者方程组，例如

```tex
$$
f(x)=\begin{cases}
    x, & x>0, \\
    -x, & x\leq 0.
\end{cases}
$$
```

效果为

f(x)={x,x>0,−x,x≤0.

## 多行公式

多行公式通常使用`aligned`环境，例如

```tex
$$
\begin{aligned}
a & =b+c \\
& =d+e
\end{aligned}
$$
```

效果为

a=b+c=d+e

## 矩阵和行列式

矩阵可以用`bmatrix`环境和`pmatrix`环境，分别为方括号和圆括号，例如

```tex
$$
\begin{bmatrix}
    a & b \\
    c & d
\end{bmatrix}
$$
```

效果为 [abcd] 。如果要输入行列式的话，可以使用`vmatrix`环境，用法同上。

[TOC]

# 常用数学符号

## 高等数学

| 符号                                                         | MathJax                   |
| ------------------------------------------------------------ | ------------------------- |
| 积分: ∫ $\int$                                               | `\int`                    |
| $\iint$                                                      | `\iint`                   |
| ∮ $\oint$                                                    | `\oint`                   |
| ∏ $\prod$                                                    | `\prod`                   |
| ∑ $\sum$ $\displaystyle\sum_{i=1}^n \textstyle\sum_{i=1}^n$  | `\sum`                    |
| $\lim$ $\lim\limits_{n \to \infty}{1 \over n} \lim\nolimits_x$ | `\lim`                    |
| $\frac{1+a}{4+b}$                                            | `\frac{1+a}{4+b}`         |
| ${1+a}\over{4+b}$                                            | `${1+a}\over{4+b}$`       |
| $\sqrt{x}$                                                   | `\sqrt{x}`                |
| $\sqrt[3]{x}$                                                | `\sqrt[3]{x}`             |
| 求导：′ ″ $\prime$                                           | `\prime`                  |
| ‰ ％ $\%$                                                    | `\%`                      |
| ㏒ ㏑$\log \lg \ln$                                          | `\log`                    |
| 内积：$\braket{\phi,\psi}$                                   | `\braket{\phi,\psi}`      |
| 任意: ∀ $\forall$                                            | `\forall`                 |
| 存在: ∃ $\exists \nexists$                                   | `\exists`                 |
| $\because$                                                   | `\because`                |
| $\therefore$                                                 | `\therefore`              |
| 偏导：$\partial$                                             | `\partial`                |
| $\nabla$                                                     | `\nabla`                  |
| △ $\vartriangle$                                             | `\vartriangle`            |
| ∞ $\infty$                                                   | `\infty`                  |
| 正比：∝ $\propto \varpropto$                                 | `\propto` or `\varpropto` |
| ￡ $\pounds \mathsterling \text{\textsterling}$              | `\pounds`                 |

## 其它符号

| 符号                    | MathJax                  |
| ----------------------- | ------------------------ |
| ${n+1 \choose 2k}$      | `{n+1 \choose 2k}`       |
| $\binom{n+1}{2k}$       | `\binom{n+1}{2k}`        |
| 求导$\nabla$            | `\nabla`                 |
| 偏导$\partial$          | `\partial`               |
| 复数的虚数部分$\image $ | `\image or \Im`          |
| 复数的实数部分$\real$   | `\real or \Re`           |
| 复数$\Complex$          | `\Complex or \cnums`     |
| 实数$\Reals$            | `\Reals or \reals or \R` |
| 自然数$\natnums$        | `\natnums or \N`         |
| 范数$\ell$              | `\ell`                   |
| 损失函数$\cal L$        | `\cal L` or `\mathcal L` |

[更多参见 Other Letters](https://katex.org/docs/supported.html)

## 特殊符号

| 符号                       | MathJax                 |
| -------------------------- | ----------------------- |
| ∽ $\backsim$               | `\backsim`              |
| ～ $\thicksim$             | `\thicksim`             |
| ⋆ $\star$                  | `\star`                 |
| ∗ $\ast$                   | `\ast`                  |
| $\bullet$                  | `\bullet`               |
| $\cdot$                    | `\cdot`                 |
| $\circ$                    | `\circ`                 |
| ∧ $\land$                  | `\land`                 |
| ∨ $\lor$                   | `\lor`                  |
| ⊙ $\odot \oplus \otimes $  | `\odot`                 |
| $\copyright$               | `\copyright`            |
| $\text{\textcircled a}$    | `\text{\textcircled a}` |
| 〒                         |                         |
| ¤                          |                         |
| ○                          |                         |
| ⌒                          |                         |
| ⊥ $\bot \top$              | `\bot`                  |
| ∥                          |                         |
| ∠                          |                         |
| √ $\checkmark$             | `\checkmark`            |
| ﹙﹚                       |                         |
| ﹛﹜                       |                         |
| ‖                          |                         |
| ∶                          |                         |
| ï                          |                         |
| ＄ $\$ \text{\textdollar}$ | `\text{\textdollar}`    |
| ￥ $\yen$                  | `\yen`                  |
| $\cdots$                   | `\cdots`                |
| $\ddots$                   | `\ddots`                |
| $\vdots$                   | `\vdots`                |

## 特殊数字

| 符号                                                         | MathJax |
| ------------------------------------------------------------ | ------- |
| º                                                            |         |
| ¹ ₁ 壹                                                       |         |
| ²₂ 贰                                                        |         |
| ³₃ ·∶ ∴ ∵ 叁                                                 |         |
| ⁴₄ ∷ 肆                                                      |         |
| ½ ⅓ ⅔ ¼ ¾ ⅛ ⅜ ⅝ ⅞ ⁵∕₁₈ º¹²³⁴ⁿ ₁₂₃₄                           |         |
| 壹贰叁肆伍陆柒捌玖拾 微毫厘分 百千万亿兆吉                   |         |
| ⁿ   ₀₁₂₃₄₅₆₇₈₉ ᵢₙ                                            | 下标    |
| ₀ ₁ ₂ ₃ ₄ ₅ ₆ ₇ ₈ ₉ ₊ ₋ ₌ ₍ ₎ ₐ ₑ ₒ ₓ ₔ ₕ ₖ ₗ ₘ ₙ ₚ ₛ ₜ      | 下标    |
| ₐ ₔ ₑ ₕ ᵢ ⱼ ₖ ₗ ₘ ₙ ₒ ₚ ᵣ ₛ ₜ ᵤ ᵥ ₓ ᙮ ᵤ ᵩ ᵦ ₗ ˪ ៳ ៷ ₒ ᵨ ₛ ៴ ᵤ ᵪ ᵧ | 下标    |
| ⁰ ¹ ² ³ ⁴ ⁵ ⁶ ⁷ ⁸ ⁹ ⁺ ⁻ ⁼ ⁽ ⁾ ⁿ º ˙ ™                        | 上标    |
| ㆒㆓㆔㆕㆖㆗㆘㆙㆚㆛㆜㆝㆞㆟                                 | 上标    |
| ᵃ ᵇ ᶜ ᵈ ᵉ ᵍ ʰ ⁱ ʲ ᵏ ˡ ᵐ ⁿ ᵒ ᵖ ᵒ⃒ ʳ ˢ ᵗ ᵘ ᵛ ʷ ˣ ʸ ᙆ ᴬ ᴮ ᒼ ᴰ ᴱ ᴳ ᴴ ᴵ ᴶ ᴷ ᴸ ᴹ ᴺ ᴼ ᴾ ᴼ̴ ᴿ ˢ ᵀ ᵁ ᵂ ˣ ᵞ ᙆ ꝰ ˀ ˁ ˤ ꟸ ꭜ ʱ ꭝ ꭞ ʴ ʵ ʶ ꭟ ˠ ꟹ ᴭ ᴯ ᴲ ᴻ ᴽ ᵄ ᵅ ᵆ ᵊ ᵋ ᵌ ᵑ ᵓ ᵚ ᵝ ᵞ ᵟ ᵠ ᵡ ᵎ ᵔ ᵕ ᵙ ᵜ ᶛ ᶜ ᶝ ᶞ ᶟ ᶡ ᶣ ᶤ ᶥ ᶦ ᶧ ᶨ ᶩ ᶪ ᶫ ᶬ ᶭ ᶮ ᶯ ᶰ ᶱ ᶲ ᶳ ᶴ ᶵ ᶶ ᶷ ᶸ ᶹ ᶺ ᶼ ᶽ ᶾ ᶿ ꚜ ꚝ ჼ ᒃ ᕻ ᑦ ᒄ ᕪ ᑋ ᑊ ᔿ ᐢ ᣕ ᐤ ᣖ ᣴ ᣗ ᔆ ᙚ ᐡ ᘁ ᐜ ᕽ ᙆ ᙇ ᒼ ᣳ ᒢ ᒻ ᔿ ᐤ ᣖ ᣵ ᙚ ᐪ ᓑ ᘁ ᐜ ᕽ ᙆ ᙇ ⁰ ¹ ² ³ ⁴ ⁵ ⁶ ⁷ ⁸ ⁹ ⁺ ⁻ ⁼ ˂ ˃ ⁽ ⁾ ˙ * º | 上标    |

> https://unicode-table.com/cn/2080/ 
> 下标从U+2080到U+2089
> [上標和下標數字](https://unicode-table.com/cn/sets/superscript-and-subscript-numbers/)
> [上標和下標字母](https://unicode-table.com/cn/sets/superscript-and-subscript-letters/)

## 顶部符号（向量）

| 符号                    | MathJax                 |
| ----------------------- | ----------------------- |
| $\hat X$                | `\hat X`                |
| $\widehat {XY}$         | `\widehat {XY}`         |
| $\dot a$                | `\dot a`                |
| $\ddot a$               | `\ddot a`               |
| $\overline {xyz}$       | `\overline {xyz}`       |
| $\vec {AB}$             | `\vec {AB}`             |
| $\overrightarrow{abcd}$ | `\overrightarrow{abcd}` |

## 箭头符号

| 符号              | MathJax           |
| ----------------- | ----------------- |
| $x \to f(x)$      | `x \to f(x)`      |
| → $\rightarrow$   | `\rightarrow`     |
| ← $\leftarrow$    | `\leftarrow`      |
| ↑ $\uparrow$      | `\uparrow`        |
| ↓ $\downarrow$    | `\downarrow`      |
| $\mapsto$         | `\mapsto`         |
| $\Rightarrow$     | `\Rightarrow`     |
| $\Leftarrow$      | `\Leftarrow`      |
| $\leftrightarrow$ | `\leftrightarrow` |
| $\Leftrightarrow$ | `\Leftrightarrow` |
| ↖                 |                   |
| ↗                 |                   |
| ↘                 |                   |
| ↙                 |                   |

## 集合符号

| 符号          | MathJax       |
| ------------- | ------------- |
| ∪ $\cup$      | `\cup`        |
| ∩ $\cap$      | `\cap`        |
| ⊂ $\subset$   | `\subset`     |
| ⊆ $\subseteq$ | `\subseteq`   |
| $\subsetneq$  | `\subsetneq`  |
| ⊃ $\supset$   | `\supset`     |
| ⊇ $\supseteq$ | `\supseteq`   |
| $\supsetneq$  | `\supsetneq`  |
| ∈ $\in$       | `\in`         |
| $\notin$      | `\notin`      |
| $\emptyset$   | `\emptyset`   |
| $\varnothing$ | `\varnothing` |

## 数学运算 - 关系比较符

| 符号                                | MathJax        |
| ----------------------------------- | -------------- |
| ＜ $\lt$                            | `\lt`          |
| ≤ $\le$                             | `\le`          |
| ＞ $\gt$                            | `\gt`          |
| ≥ $\ge$                             | `\ge`          |
| ≠ $\neq$                            | `\neq`         |
| ≈ $\approx$                         | `\approx`      |
| ＝ $\equalscolon \eqqcolon$         | `\equalscolon` |
| ≡ $\equiv$                          | `\equiv`       |
| ≌ $\cong \backsimeq \approxeq$      | `\cong`        |
| ∽ $\backsim$                        | `\backsim`     |
| ≮≯∧                                 |                |
| 正定，半正定$\succeq \succcurlyeq $ | `\succeq`      |
| 负定，半负定$\preceq  \preccurlyeq$ | `\preceq`      |

## 数学运算 - 算术操作符

| 符号                   | MathJax                |
| ---------------------- | ---------------------- |
| × $\times$             | `\times`               |
| ／ ÷ $\div$            | `\div`                 |
| ± $\pm$                | `\pm`                  |
| $\mp$                  | `\mp`                  |
| $\lvert x \rvert$      | `\lvert x \rvert`      |
| $\lVert \vec a \rVert$ | `\lVert \vec a \rVert` |
| － ﹣                  |                        |
| ＋ ﹢                  |                        |

## 希腊字母

http://www.cella.cn/zzzl/zs/03.htm

| 大写                     | 小写                             | 中文名               | 英文    |
| ------------------------ | -------------------------------- | -------------------- | ------- |
| A $\Alpha$               | α $\alpha$                       | 阿尔法 /'ælfə/       | Alpha   |
| B $\Beta$                | β $\beta$                        | 贝塔 /'beɪtə/        | Beta    |
| Γ $\Gamma \varGamma$     | γ $\gamma \digamma$              | 伽玛 /'gæmə/         | Gamma   |
| Δ $\Delta \varDelta$     | δ $\delta$                       | 德尔塔 /'deltə/      | Delta   |
| Ε $\Epsilon$             | ε $\epsilon$ $\varepsilon$       | 伊普西隆 /'epsɪlɒn/  | Epsilon |
| Ζ $\Zeta$                | ζ $\zeta$                        | 泽塔　/'zi:tə/       | Zeta    |
| Η $\Eta$                 | η $\eta$                         | 伊塔 /'i:tə/         | Eta     |
| Θ $\Theta \varTheta$     | θ $\theta$ $\vartheta \thetasym$ | 西塔 /'θi:tə/        | Theta   |
| Ι $\Iota$                | ι $\iota$                        | 约塔 /aɪ'əʊtə/       | Iota    |
| Κ $\Kappa$               | κ $\kappa$ $\varkappa$           | 卡帕 /'kæpə/         | Kappa   |
| Λ $\Lambda \varLambda$   | λ $\lambda$                      | 兰姆达 /'læmdə/      | Lambda  |
| Μ $\Mu$                  | μ $\mu$                          | 米欧　/mju:/         | Mu      |
| Ν $\Nu$                  | ν $\nu$                          | 纽　 /nju:/          | nu      |
| Ξ $\Xi \varXi$           | ξ $\xi$                          | 克西　 /ksi/         | xi      |
| Ο $\Omicron$             | ο $\omicron$                     | 欧米克隆 /ˈɑmɪˌkrɑn/ | omicron |
| ∏ $\Pi \varPi$           | π $\pi$ $\varpi$                 | 派　 /paɪ/           | pi      |
| Ρ $\Rho$                 | ρ $\rho$ $\varrho$               | 柔　 /rəʊ/           | rho     |
| ∑ $\Sigma \varSigma$     | σ $\sigma$ $\varsigma$           | 西格玛　/'sɪɡmə/     | sigma   |
| Τ $\Tau$                 | τ $\tau$                         | 陶　 /taʊ/           | Tau     |
| Υ $\Upsilon \varUpsilon$ | υ $\upsilon$                     | 阿普西隆　/ˈipsilon/ | Upsilon |
| Φ $\Phi \varPhi$         | φ $\phi$ $\varphi$               | 弗爱　 /faɪ/         | Phi     |
| Χ $\Chi$                 | χ $\chi$                         | 凯　 /kaɪ/           | Chi     |
| Ψ $\Psi \varPsi$         | ψ $\psi$                         | 普赛　 /psaɪ/        | Psi     |
| Ω $\Omega \varOmega $    | ω $\omega$                       | 奥米伽 /oʊ'meɡə/     | Omega   |

## demo

- 三角函数

  $$
  \sin 30^\circ \quad
  \cos 30^\circ \quad
  \tan 30^\circ \quad
  \cot 30^\circ \quad
  \sec 30^\circ \quad
  \csc 30^\circ \quad
  \arcsin 1/2 \quad
  \arccos 1/2 \quad
  \arctan 1/2
  $$

- 多行公式

  $$
  \begin{align}
  D(x) &= \int_{x_0}^x P(x^{\prime})\,\mathrm{dx^{\prime}}  \\
  &= C\int_{x_0}^x x^{\prime n}\,\mathrm{dx^{\prime}} \\
  &= \frac{C}{n+1}(x^{n+1}-x_0^{n+1}) \\
  &\equiv  y
  \end{align}
  $$

- 表格

$$\begin{array}{c|lcr}
  	n & \text{Left} & \text{Center} & \text{Right}\\
  	\hline
  	1 & 0.24 & 1 & 125\\
  	2 & -1 & 189 & -8 \\
  	3 & 20 & 2000& 1+10i\\
  \end{array}$$

- 矩阵

  - matrix

    $$\begin{matrix}
    	1&x&x^2\\
    	1&y&y^2\\
    	1&z&z^2\\
    \end{matrix}$$

  - pmatrix

    $$\begin{pmatrix}
    	1&2\\
    	3&4\\
    	\end{pmatrix}$$

  - bmatrix

    $$\begin{bmatrix}
    	1&2\\
    	3&4\\
    	\end{bmatrix}$$

  - Bmatrix

    $$\begin{Bmatrix}
    	1&2\\
    	3&4\\
    	\end{Bmatrix}$$

  - vmatrix

    $$\begin{vmatrix}
    	1&2\\
    	3&4\\
    	\end{vmatrix}$$

  - Vmatrix

    $$\begin{Vmatrix}
    	1&2\\
    	3&4\\
    	\end{Vmatrix}$$

  - 增广矩阵

    $$\left[
        \begin{array}{cc|c}
            1&2&3\\
            4&5&6\\
        \end{array}
    \right]$$

  - 行内矩阵$\bigl[\begin{smallmatrix} a & b \\ c & d \end{smallmatrix}\bigr]$

  - 省略矩阵

    $$\begin{pmatrix}
    	1 & a_1 & a_1^2 & \cdots & a_1^n\\
    	1 & a_2 & a_2^2 & \cdots & a_2^n \\
    	\vdots & \vdots & \ddots & \vdots \\
    	1 & a_n & a_n^2 & \cdots & a_n^n  \\
    	\end{pmatrix}$$

- 方程组

$$f(n)=\begin{cases}
  	n/2,  & \text{if n is even}\\
  	3n+1, & \text{if n is odd}
  	\end{cases}$$

$$f(n)=\begin{cases}
	n/2,  & \text{if $n$ is even} \\[2ex]
	3n+1, & \text{if $n$ is odd}
	\end{cases}$$

- 高亮与框线

  - mathjax

    $$\bbox[yellow]{
    	e^x=\lim_{n\to\infty} \left( 1+\frac{x}{n} \right)^n
    	\qquad (1)
    }$$

  - mathjax

    $$\bbox[border:2px solid red]{
    	e^x=\lim_{n\to\infty} \left( 1+\frac{x}{n} \right)^n
    	\qquad (2)
    }$$

  - katex

$$\boxed{
    	e^x=\lim_{n\to\infty} \left( 1+\frac{x}{n} \right)^n
    	\qquad (2)
    }$$

- Katex 颜色 &字体

$$\textcolor{blue}{F=ma}\newline
\textcolor{#228B22}{F=ma}\newline
\colorbox{aqua}{$F=ma$}\\
\fcolorbox{red}{aqua}{$F=ma$}\\
\mathcal{AB0}\\
\color{blue} F=ma\\
\bold{Ab0}$$

> 换行`\newline` or `\\`
> color 后面的跟 color 一个颜色，否则使用 textcolor

- KaTeX Options macros(宏指令设置)
  Latex 可以使用两类命令来定义新命令：

  - 一类是 Latex（Lamport Tex）命令，包括 \newcommand、\renewcommand 和 \providecommand，
  - 一类是更基本的 Tex 原始（primitive）命令，包括 \def、\gdef、\edef 和 \xdef。
    [探究 latex 中的\def 和\edef](https://blog.csdn.net/u014713475/article/details/80651662/)
    [Latex 定义新命令](https://zhuanlan.zhihu.com/p/383336622)
    [官网 macros 参考](https://katex.org/docs/supported.html#macros)
  - 不需要配置 - 自定义新命令（newcommand、def、edef、xdef、gdef、global）

$$\def\oneover{\frac{1}}
    \oneover{x}\\
    \newcommand\twoover{\frac{2}}
    \twoover{x}$$

```latex
> newcommand 和 def 的区别是 newcommand 必须定义不存的命令（包括系统命令），而 def 会覆盖
```

  - 带参数

$$\def\bar#1{#1^2}
      \bar{y}\\
      \newcommand{\bac}[1]{#1^2}
      \bac{y}$$

  - 多个参数

$$\def\bar#1#2{#1^#2}
    \bar{y}{x}\\
    \newcommand{\avec}[3]{(#1_{#2},\cdots,#1_{#3})}
    \avec{\alpha}{s}{t}$$

```latex
> - `\newcommand{name}[num][opt]{deﬁnition}`第一个 name 是你想要建立的命令的名称，第二个 definition 是命令的定义，num 是可选的，用于指定新命令所需的参数数目（最多 9 个）。如果不给出这个参数，默认就是 0；opt 是可选参数的默认值（测试好像会出错）；

> \gdef, \xdef, \global\def, \global\edef, \global\let, and \global\futurelet 都是全局的
>
> - `\def\⟨name⟩<parameter text>{⟨definition⟩}`;
> - \gdef：与 \def 几乎完全相同，唯一的区别是 \gdef 是全局的，不受分组{}的影响。相当于\global \def;
> - \edef：与 \def 几乎完全相同，唯一的区别是 \edef 的定义中如果嵌套了命令，会首先展开命令， 然后再定义新命令。
> - \xdef：相当于 \gdef 加 \edef，全局的展开定义。

> - \newcommand defines a new command, and makes an error if it is already defined. 定义不存在的（新增）
> - \renewcommand redefines a predefined command, and makes an error if it is not yet defined. 覆盖存在的
> - \providecommand defines a new command if it isn't already defined, or does nothing if it exists. 如果存在则忽略该定义
> - \def 新增和覆盖
```

  - 需要配置 - macros

$$\f\relax{x} = \int_{-\infty}^\infty \f\hat\xi\,e^{2 \pi i \xi x}  \,d\xi$$

> macros{ "\\f": "#1f(#2)"}

- TAG&标签

$$e^x=\lim_{n\to\infty} \left( 1+\frac{x}{n} \right)^n	\tag{1}$$

$$e^x=\lim_{n\to\infty} \left( 1+\frac{x}{n} \right)^n
	\label{2}\tag{2}$$

$$\begin{align} \label{eqn:1} (\mathbf{A}\mathbf{B})^{-1} &= \mathbf{B}^{-1}\mathbf{A}^{-1} \\ \label{eqn:2} (\mathbf{ABC\ldots})^{-1} &= \ldots\mathbf{C}^{-1}\mathbf{B}^{-1}\mathbf{A}^{-1} \\ \label{eqn:3} (\mathbf{A}^{T})^{-1} &= (\mathbf{A}^{-1})^{T} \\ \label{eqn:4} (\mathbf{A} + \mathbf{B})^{T} &= \mathbf{A}^{T} + \mathbf{B}^{T} \\ \label{eqn:5} (\mathbf{AB})^{T} &= \mathbf{B}^{T}\mathbf{A}^{T} \\ \label{eqn:6} (\mathbf{ABC\ldots})^{T} &= \ldots\mathbf{C}^{T}\mathbf{B}^{T}\mathbf{A}^{T} \\ \label{eqn:7} (\mathbf{A}^{H})^{-1} &= (\mathbf{A}^{-1})^{H} \\ \label{eqn:8} (\mathbf{A} + \mathbf{B})^{H} &= \mathbf{B}^{H} + \mathbf{A}^{H} \\ \label{eqn:9} (\mathbf{AB})^{H} &= \mathbf{B}^{H}\mathbf{A}^{H} \\ \label{eqn:10} (\mathbf{ABC\ldots})^{H} &= \ldots\mathbf{C}^{H}\mathbf{B}^{H}\mathbf{A}^{H} \\ \end{align}$$

$$a := x^2-y^3 \tag{2-1}\label{2-1}$$

$$a+y^3 \stackrel{\eqref{2-1}}= x^2$$

$$a+y^3 \stackrel{\ref{2-1}}= x^2$$

$$\begin{aligned} \sin 2\theta = 2\sin \theta \cos \theta \\ = \cfrac{2 \tan \theta}{1+\tan^2 \theta} \end{aligned} \label{1-1}\tag{1-1}$$

转跳： $\eqref{1-1}$ or $\ref{1-1}$ or $\ref{eqn:1}$.

> label 是用来跳转的，tag 是用来显示的
> https://github.com/KaTeX/KaTeX/issues/2003

```latex
module.exports = {
  trust: ["\\htmlId"],
  macros: {
    "\\eqref": "\\href{###1}{(\\text{#1})}",
    "\\ref": "\\href{###1}{\\text{#1}}",
    "\\label": "\\htmlId{#1}{}",
    "\\f": "#1f(#2)"
  }
}
```

## Unicode Latex & latex-input 插件

> Ctrl+Shift+P: Unicode: Insert Math Symbol
> 当输入`\`时会提示

```latex
α \alpha	β \beta	χ \chi	δ \delta	ϝ \digamma	ε \epsilon
η \eta	γ \gamma	ι \iota	κ \kappa	λ \lambda	μ \mu
ν \nu	ω \omega	ϕ \phi	π \pi	ψ \psi	ρ \rho
σ \sigma	τ \tau	θ \theta	υ \upsilon	ε \varepsilon	ϰ \varkappa
φ \varphi	ϖ \varpi	ϱ \varrho	ς \varsigma	ϑ \vartheta	ξ \xi
ζ \zeta
Upper-case Greek
Δ \Delta	Γ \Gamma	Λ \Lambda	Ω \Omega	Φ \Phi	Π \Pi	Ψ \Psi	Σ \Sigma
Θ \Theta	Υ \Upsilon	Ξ \Xi	℧ \mho	∇ \nabla
Hebrew
ℵ \aleph	ℶ \beth	ℸ \daleth	ℷ \gimel
Delimiters
/ /	[ [	⇓ \Downarrow	⇑ \Uparrow	‖ \Vert	\backslash
↓ \downarrow	⟨ \langle	⌈ \lceil	⌊ \lfloor	⌞ \llcorner	⌟ \lrcorner
⟩ \rangle	⌉ \rceil	⌋ \rfloor	⌜ \ulcorner	↑ \uparrow	⌝ \urcorner
\vert
{ \{
\|
} \}	] ]
|
Big symbols
⋂ \bigcap	⋃ \bigcup	⨀ \bigodot	⨁ \bigoplus	⨂ \bigotimes	⨄ \biguplus
⋁ \bigvee	⋀ \bigwedge	∐ \coprod	∫ \int	∮ \oint	∏ \prod
∑ \sum
Standard function names
Pr \Pr	arccos \arccos	arcsin \arcsin	arctan \arctan	arg \arg	cos \cos
cosh \cosh	cot \cot	coth \coth	csc \csc	deg \deg	det \det
dim \dim	exp \exp	gcd \gcd	hom \hom	inf \inf	ker \ker
lg \lg	lim \lim	liminf \liminf	limsup \limsup	ln \ln	log \log
max \max	min \min	sec \sec	sin \sin	sinh \sinh	sup \sup
tan \tan	tanh \tanh
Binary operation and relation symbols
≎ \Bumpeq	⋒ \Cap	⋓ \Cup	≑ \Doteq
⨝ \Join	⋐ \Subset	⋑ \Supset	⊩ \Vdash
⊪ \Vvdash	≈ \approx	≊ \approxeq	∗ \ast
≍ \asymp	϶ \backepsilon	∽ \backsim	⋍ \backsimeq
⊼ \barwedge	∵ \because	≬ \between	○ \bigcirc
▽ \bigtriangledown	△ \bigtriangleup	◀ \blacktriangleleft	▶ \blacktriangleright
⊥ \bot	⋈ \bowtie	⊡ \boxdot	⊟ \boxminus
⊞ \boxplus	⊠ \boxtimes	∙ \bullet	≏ \bumpeq
∩ \cap	⋅ \cdot	∘ \circ	≗ \circeq
≔ \coloneq	≅ \cong	∪ \cup	⋞ \curlyeqprec
⋟ \curlyeqsucc	⋎ \curlyvee	⋏ \curlywedge	† \dag
⊣ \dashv	‡ \ddag	⋄ \diamond	÷ \div
⋇ \divideontimes	≐ \doteq	≑ \doteqdot	∔ \dotplus
⌆ \doublebarwedge	≖ \eqcirc	≕ \eqcolon	≂ \eqsim
⪖ \eqslantgtr	⪕ \eqslantless	≡ \equiv	≒ \fallingdotseq
⌢ \frown	≥ \geq	≧ \geqq	⩾ \geqslant
≫ \gg	⋙ \ggg	⪺ \gnapprox	≩ \gneqq
⋧ \gnsim	⪆ \gtrapprox	⋗ \gtrdot	⋛ \gtreqless
⪌ \gtreqqless	≷ \gtrless	≳ \gtrsim	∈ \in
⊺ \intercal	⋋ \leftthreetimes	≤ \leq	≦ \leqq
⩽ \leqslant	⪅ \lessapprox	⋖ \lessdot	⋚ \lesseqgtr
⪋ \lesseqqgtr	≶ \lessgtr	≲ \lesssim	≪ \ll
⋘ \lll	⪹ \lnapprox	≨ \lneqq	⋦ \lnsim
⋉ \ltimes	∣ \mid	⊧ \models	∓ \mp
⊯ \nVDash	⊮ \nVdash	≉ \napprox	≇ \ncong
≠ \ne	≠ \neq	≠ \neq	≢ \nequiv
≱ \ngeq	≯ \ngtr	∋ \ni	≰ \nleq
≮ \nless	∤ \nmid	∉ \notin	∦ \nparallel
⊀ \nprec	≁ \nsim	⊄ \nsubset	⊈ \nsubseteq
⊁ \nsucc	⊅ \nsupset	⊉ \nsupseteq	⋪ \ntriangleleft
⋬ \ntrianglelefteq	⋫ \ntriangleright	⋭ \ntrianglerighteq	⊭ \nvDash
⊬ \nvdash	⊙ \odot	⊖ \ominus	⊕ \oplus
⊘ \oslash	⊗ \otimes	∥ \parallel	⟂ \perp
⋔ \pitchfork	± \pm	≺ \prec	⪷ \precapprox
≼ \preccurlyeq	≼ \preceq	⪹ \precnapprox	⋨ \precnsim
≾ \precsim	∝ \propto	⋌ \rightthreetimes	≓ \risingdotseq
⋊ \rtimes	∼ \sim	≃ \simeq	∕ \slash
⌣ \smile	⊓ \sqcap	⊔ \sqcup	⊏ \sqsubset
⊏ \sqsubset	⊑ \sqsubseteq	⊐ \sqsupset	⊐ \sqsupset
⊒ \sqsupseteq	⋆ \star	⊂ \subset	⊆ \subseteq
⫅ \subseteqq	⊊ \subsetneq	⫋ \subsetneqq	≻ \succ
⪸ \succapprox	≽ \succcurlyeq	≽ \succeq	⪺ \succnapprox
⋩ \succnsim	≿ \succsim	⊃ \supset	⊇ \supseteq
⫆ \supseteqq	⊋ \supsetneq	⫌ \supsetneqq	∴ \therefore
× \times	⊤ \top	◁ \triangleleft	⊴ \trianglelefteq
≜ \triangleq	▷ \triangleright	⊵ \trianglerighteq	⊎ \uplus
⊨ \vDash	∝ \varpropto	⊲ \vartriangleleft	⊳ \vartriangleright
⊢ \vdash	∨ \vee	⊻ \veebar	∧ \wedge
≀ \wr
Arrow symbols
⇓ \Downarrow	⇐ \Leftarrow	⇔ \Leftrightarrow	⇚ \Lleftarrow
⟸ \Longleftarrow	⟺ \Longleftrightarrow	⟹ \Longrightarrow	↰ \Lsh
⇗ \Nearrow	⇖ \Nwarrow	⇒ \Rightarrow	⇛ \Rrightarrow
↱ \Rsh	⇘ \Searrow	⇙ \Swarrow	⇑ \Uparrow
⇕ \Updownarrow	↺ \circlearrowleft	↻ \circlearrowright	↶ \curvearrowleft
↷ \curvearrowright	⤎ \dashleftarrow	⤏ \dashrightarrow	↓ \downarrow
⇊ \downdownarrows	⇃ \downharpoonleft	⇂ \downharpoonright	↩ \hookleftarrow
↪ \hookrightarrow	⇝ \leadsto	← \leftarrow	↢ \leftarrowtail
↽ \leftharpoondown	↼ \leftharpoonup	⇇ \leftleftarrows	↔ \leftrightarrow
⇆ \leftrightarrows	⇋ \leftrightharpoons	↭ \leftrightsquigarrow	↜ \leftsquigarrow
⟵ \longleftarrow	⟷ \longleftrightarrow	⟼ \longmapsto	⟶ \longrightarrow
↫ \looparrowleft	↬ \looparrowright	↦ \mapsto	⊸ \multimap
⇍ \nLeftarrow	⇎ \nLeftrightarrow	⇏ \nRightarrow	↗ \nearrow
↚ \nleftarrow	↮ \nleftrightarrow	↛ \nrightarrow	↖ \nwarrow
→ \rightarrow	↣ \rightarrowtail	⇁ \rightharpoondown	⇀ \rightharpoonup
⇄ \rightleftarrows	⇄ \rightleftarrows	⇌ \rightleftharpoons	⇌ \rightleftharpoons
⇉ \rightrightarrows	⇉ \rightrightarrows	↝ \rightsquigarrow	↘ \searrow
↙ \swarrow	→ \to	↞ \twoheadleftarrow	↠ \twoheadrightarrow
↑ \uparrow	↕ \updownarrow	↕ \updownarrow	↿ \upharpoonleft
↾ \upharpoonright	⇈ \upuparrows
Miscellaneous symbols
$ \$	Å \AA	Ⅎ \Finv	⅁ \Game
ℑ \Im	¶ \P	ℜ \Re	§ \S
∠ \angle	‵ \backprime	★ \bigstar	■ \blacksquare
▴ \blacktriangle	▾ \blacktriangledown	⋯ \cdots	✓ \checkmark
® \circledR	Ⓢ \circledS	♣ \clubsuit	∁ \complement
© \copyright	⋱ \ddots	♢ \diamondsuit	ℓ \ell
∅ \emptyset	ð \eth	∃ \exists	♭ \flat
∀ \forall	ħ \hbar	♡ \heartsuit	ℏ \hslash
∭ \iiint	∬ \iint	ı \imath	∞ \infty
ȷ \jmath	… \ldots	∡ \measuredangle	♮ \natural
¬ \neg	∄ \nexists	∰ \oiiint	∂ \partial
′ \prime	♯ \sharp	♠ \spadesuit	∢ \sphericalangle
ß \ss	▿ \triangledown	∅ \varnothing	▵ \vartriangle
⋮ \vdots	℘ \wp	¥ \yen
```

## 参考

> 插件：Latex Sympy Calculator；根据表达式自动计算等号右边的表达式

### TEX绘图demo

[绘图demo源码](https://github.com/zclab/tikz)
[绘图demo演示](https://zclab.github.io/tikz/)

### LaTex(数学公式排版系统)

[一份不太简短的 LATEX2e 介绍](http://www.mohu.org/info/lshort-cn.pdf)

[latex](https://www.latex-project.org/help/documentation/)
[Arbitrary LaTeX reference](https://latex.knobs-dials.com/)
[Begin LaTeX in minutes](https://github.com/luong-komorebi/Begin-Latex-in-minutes)
[LaTeX](https://www.overleaf.com/learn/latex/Picture_environment)
[Help:MATH](https://en.jinzhao.wiki/wiki/Help:Displaying_a_formula)

> LATEX 使用 TEX 做为格式化引擎，当前的版本是 LATEX2ϵ
> MathJax & KaTeX 是用来渲染 LaTex 格式的数学公式
> LaTex 可以用来写 PDF
> TikZ 宏包是一个十分强大的绘图宏包

### itex2MML

https://golem.ph.utexas.edu/~distler/blog/itex2MML.html

### MathJax(数学公式渲染器)

[MathJax 官网](https://www.mathjax.org/)
[Mathjax 常用语法 - 推荐](https://blog.csdn.net/fly0202/article/details/82534854)
[MathJax 基本语法](https://blog.csdn.net/qq_40871466/article/details/96328967)
[基本数学公式语法(of MathJax)](https://blog.csdn.net/ethmery/article/details/50670297)
[Markdown 语法中输入数学公式（MathJax）及特殊符号](https://www.jianshu.com/p/8363e3815b92)
[MathJax 数学公式 - 推荐](http://devgou.com/article/MathJax/)

[KaTeX and MathJax Comparison Demo](https://www.intmath.com/cg5/katex-mathjax-comparison.php)

### KaTeX(数学公式渲染器)

> KaTeX 是一个快速，易于使用的 JavaScript 库 TeX 数学渲染在 web 上。
> KaTeX 支持大部分(但不是全部)LaTeX 和许多 LaTeX 包。

KaTeX 拥有比 MathJax 更快的性能，但是它却少了很多 MathJax 拥有的特性。[KaTeX supported functions/symbols](https://katex.org/docs/supported.html) 来了解 KaTeX 支持那些符号和函数
[katex](https://katex.org/)

`$...$` 或者 `\(...\)` 中的数学表达式将会在行内显示。
`$$...$$` 或者 `\[...\]` 或者 ```math 中的数学表达式将会在块内显示。

[Latex/MathJax/Katex 数学公式手册](https://fivecakes.com/p/5b1bd56d2392ec23b91bab2e)

### AsciiMath 或 JLaTeXMath

[AsciiMath](http://asciimath.org/)
[JLaTeXMath ](https://github.com/opencollab/jlatexmath)

### sympy 表达式转换为 latex

```latex
import sympy
x = symbols("x")
y = symbols("y")
s = "1+2**(x+y)"
sympy.latex(eval(s))   # prints '$1 + {2}^{x + y}$'
```

### 图片识别latex(手写公式转换为 LaTeX)

[image-to-latex](https://github.com/kingyiusuen/image-to-latex)

[Mathpix Snip](https://mathpix.com/)


### Python 函数表达式转换为 latex

#### latexify-py

https://github.com/google/latexify_py
从 Python 函数生成 LaTeX 数学描述。
`pip install latexify-py`

```latex
import math
import latexify

# 写pi而不是math.pi，就可以了

@latexify.with_latex
def f_1(x):
    if x==1:
        return 1
    elif x==2:
        return 2
    else:
        return f_1(x-1) + f_1(x-2)

print(f_1)
```

#### handcalcs

Latex 公式/python代码输出数学公式
https://github.com/connorferster/handcalcs

### www.overleaf.com

online LaTeX


### github latex 公式渲染

TeX All the Things 插件

### jupyter notebook

markdown 的 cell 配置显示 mathjax,修改 jupyter 配置文件，linux 系统配置文件路径为`~/.jupyter/jupyter_notebook_config.py`，windows 系统配置文件路径为`C:\Users\User\.jupyter\jupyter_notebook_config.py`，如果没有这个文件，可以使用下面命令生成，

`$ jupyter notebook --generate-config`
`c.NotebookApp.enable_mathjax = True `

python 代码的 cell 在 print 中显示 mathjax
jupyter 输出渲染 latex 公式

```latex
# display(Math(latex_s))和display(Latex(latex_s))输出的是latex类型，
# display(Markdown(latex_s))输出的是markdown
# 推荐markdown和Latex；而Math只支持纯latex
from IPython.display import display,Latex, SVG, Math, Markdown

s1 = r"$\frac{{\partial {}}}{{\partial {}}}$".format(1, 2)
display(Math(s1))
```

matplotlib 输出渲染 latex 公式

```latex
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon
from matplotlib.collections import PatchCollection
import seaborn as sns
plt.rcParams['text.usetex'] = True
plt.rcParams['text.latex.preamble'] = r'\usepackage{amsmath} \usepackage{amsfonts}'
# plt.rcParams.update({
#     #'font.size': 8,
#     #'text.usetex': True,
#     'text.latex.preamble':  [r'\usepackage{amsmath}', #for \text command
#                             r'\usepackage{amsfonts}', # \mathbb is provided by the LaTeX package amsfonts
#                             ]
# })
# 参数'text.latex.preamble' or 'pgf.preamble'（这两个不是同一个参数） 以前是用数组，现在用字符串
# 罗马体 operatorname -> mbox or mathrm

# https://matplotlib.org/stable/tutorials/text/mathtext.html

# matplotlib.rcParams['text.latex.unicode'] = True
# matplotlib.rcParams['text.latex.preamble'] = [
#        '\\usepackage{CJK}',
#        r'\AtBeginDocument{\begin{CJK}{UTF8}{gbsn}}',
#        r'\AtEndDocument{\end{CJK}}',
# ]

# Matplotlib中文显示和Latex
#import matplotlib.font_manager as mf # 导入字体管理器
#my_font= mf.FontProperties(fname='C://Windows//Fonts/simsun.ttc') # 加载字体


def show_latex(eqn:int, latex_s:str , validated:bool):
    fig, ax = plt.subplots(figsize=(20, 0.7))
    #latex_s = r"$\alpha _ { 1 } ^ { r } \gamma _ { 1 } + \dots + \alpha _ { N } ^ { r } \gamma _ { N } = 0 \quad ( r = 1 , . . . , R ) ,$"
    plt.text(0.01, 0.5, "({})".format(eqn), ha='left', va='center', fontsize=20)
    #水平和垂直方向居中对齐
    plt.text(0.5, 0.5, latex_s, ha='center', va='center', fontsize=20)
    if validated:
        plt.text(0.97, 0.5, r"ok", ha='right', va='center', fontsize=20, color = "g")
    else:
        plt.text(0.97, 0.5, r"error", ha='right', va='center', fontsize=20, color = "r")
    # 隐藏框线
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    ax.spines['bottom'].set_visible(False)
    ax.spines['left'].set_visible(False)
    # 隐藏坐标轴的刻度信息
    plt.xticks([])
    plt.yticks([])

show_latex(1,s_1,True)
```

### 数学Math

[在线计算矩阵微积分](http://www.matrixcalculus.org/)

#### wolframalpha

数学图形/数学工具
https://www.wolframalpha.com/ 这个网站其实是一个计算知识引擎

- 在线积分计算器
- 逆矩阵、行列式、利息、房贷等

#### gnuplot

交互式绘图工具
http://www.gnuplot.info/

你可以在c#程序中编写数据文件，从c#调用gnuplot可执行文件，并在c#图片框中显示生成的图像。

#### GeoGebra

GeoGebra是适用于各级教育的最佳开源免费绘图软件之一，它将电子表格、绘图、几何、代数、统计、数学和微积分集成在一个易于使用的工具中。

GeoGebra是全球领先的数学软件提供商，支持科学、统计、技术、工程和数学教育。 您可以轻松地求解方程、创建构造、图形函数、分析数据和探索三维数学！您可以在线使用该程序，也可以将其下载到您的计算机上。
https://www.geogebra.org

#### 将数学公式转化成 LaTeX 代码

https://github.com/lukas-blecher/LaTeX-OCR
该项目可以将图片、剪贴板中的图片和屏幕截图，转化成对应的 LaTeX 代码，提供了命令行、库、GUI、Docker 多种使用方式。

