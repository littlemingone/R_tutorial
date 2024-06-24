# R 语言教程

## R 语言解释器以及 IDE 的安装与配置

<font color=#FF0000 >⚠️ 注意：本部分主要针对 Windows 平台用户，mac 与 linux 用户请参照 windows 的内容自行解决。</font>

### 安装过程中可能用到的网站：

- R 语言官网 CRAN([清华镜像](https://mirrors.tuna.tsinghua.edu.cn/CRAN/))
- [Rstudio 官网 Posit](https://posit.co/products/open-source/rstudio/)
  > 注：它曾经是 www.rstudio.com，但后来已被 Posit 公司收购，软件的下载和社区都迁移到了 posit.co 上。

### 作为一个 R 语言初学者，你需要安装以下软件：

- R 语言本体：base / r-base(conda 库中的名字)

  > base 可通过两种途径安装，对于新手我建议直接使用 CRAN 官方提供的[R 语言安装器](https://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/windows/base/)像一般 windows 软件一样安装。
  >
  > 后文中大部分的`R语言`指的就是 base。
  >
  > 熟悉命令行或者对版本控制有要求的朋友可以使用 conda 安装。但注意 conda 所有源中的 R 相关软件均有`r-`前缀，因此使用 conda 安装时，包名为 r-base。
  >
  > ⚠️<span style="color:red;">关于 conda</span>：请注意 conda 源中的 r-base 包版本比较落后，尤其是 Windows 平台的包！因此如果你想使用最新版本的 R，请谨慎考虑 conda。[我的自制的 conda r-base 包](https://github.com/littlemingone/handmake_r-base_conda_channel)可以部分解决该问题，但更新未必足够勤且目前只有 windows 版本。

- R 语言的 windows 平台编译工具包：Rtools

  > Rtools 只需要安装，其他什么都不用管，用到的时候会自动调用。
  >
  > mac 平台没有打包好的整套工具包，需要在 R 语言官网[CRAN](https://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/macosx/tools)分别安装。
  >
  > Rtools 本质是一些 C/C++ 和 Fortran 的编译器，用于将这些语言的代码编译成二进制文件。base 和大部分 R 包安装时是直接安装编译好的二进制文件，因此其实并不需要编译步骤，也用不到 Rtools。所以理论上来说 Rtools 并不是必须安装的。但根据我的经验，大部分需要从 github 直接安装的包都需要 Rtools 编译。这种包虽然不多，但你总有用到的一天，因此建议把 Rtools 装上。
  >
  > ⚠️Rtools 版本需与 R 版本匹配，要求不是很严格但最起码大版本需要匹配。不知道装哪个就都装最新的。

- R 语言集成开发环境 (IDE)：Rstudio
  > IDE 对于 R 语言的使用也不是必须的。但是它提供了美观，便于使用的界面和方便配置的 gui 菜单界面。总之没必要折磨自己裸奔用 R。
  >
  > R 语言有多种其他可选 IDE，比如 Vscode，jupyter notebook 等。尽管 Rstudio 也有很多缺点，但对于新手来说 Rstudio 永远是功能最完善最好用的 IDE，因此<span style="color:red;">新手请一定要无脑选择 Rstudio。</span>
  >
  > Rstudio 的版本与 base 版本相互独立，更新时互不干涉。Rstudio 只是一个壳子。

### Rstudio 的开箱设置

- 设置镜像源：

  默认的 R 包安装会从国外服务器下载 R 包，容易出现网络连接不上或者速度慢的情况。国内很多高校都架设了公用的国内镜像站，自动同步国外服务器的资源。从国内镜像站下载会快很多。

  注：除了 CRAN，即官方镜像之外，我们还经常需要使用 Bioconductor 网站上的 R 包。因此 Bioconductor 的软件源也是有镜像的。不过一般来说使用 Bioconductor 安装的时候会自动套用 CRAN 镜像或者在命令行提示询问你要使用哪个镜像站，所以一般可以不管。

  - Rstduio 设置步骤如下：
    ![](/assets/img/tutorial/69aea78628e983e2a6c60687a989bd22e8fb29a27ac1c55130ad5c95028aaab0.png)

  - 使用命令行设置：  
    此配置重启 R 后失效，因此需要将它们写到 R 的启动脚本里，每次打开 R 的时候自动加载。
    ```R
    options("repos" = c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/"))
    options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
    ```

- 打开 Rstudio 的语法高亮
  ![](/assets/img/tutorial/984927dd9a5e0490d4513324b9f3c8260e91afdc7f1320fb04b2fe9a74059d6b.png)

### 设置 Rstudio 使用的 R 版本

正常安装后，Rstudio 会自动找到系统中 R 的路径并调用。但如果你同时安装了多个 R 版本，可以在 Rstudio 的设置菜单中选择你要使用的 R 版本。

![](/assets/img/tutorial/6779cc9733064a70229fefc60103c0cb5dcd2a5813562046802bd3059eda0a8b.png)

> <span style="color:red;">如果设置版本自定义 R 路径时设置了错误路径</span>  
> 由于 Rstudio 的大部分功能基于 R 语言，一旦指定了错误的 R 语言路径会导致 Rstudio 无法启动，也无法再次回到这个设置界面更改。需要手动修正在配置文件`C:/User/xxx/AppData/Roaming/Rstudio/config.json`中的 R 语言路径值`rExecutablePath`。⚠️ 记得将路径中的`xxx`换成自己的用户名。

### 环境变量的查看与修改

R 语言中主要有 2 种环境变量。里面都包含了大量的设置项，一些 Rstudio 设置中没有出现的设置选项可以在这里修改。

- 系统级别：使用`Sys.getenv()`与`Sys.setenv()`查看与修改。

  > ![](/assets/img/tutorial/2f7f5a5da1d968cff3ffb358b450ec3c5a843eca0e17e292c2651b7aac568786.png)
  >
  > 这些环境变量主要包括一些默认目录的位置，如 Rtools 所在路径`RTOOLS<版本号>_HOME`。
  > ![](/assets/img/tutorial/27883ed9c714a4d02967de1d6837f76046705d991ecc1e531257848ccfde7ea8.png)
  >
  > 安装了多个版本的 Rtools 或者在 conda 中使用 R 导致 R 无法自动获取 Rtools 路径时可以通过该设置项指定正确的 Rtools 路径。
  >
  > 另外，网络代理的设置也在此处修改。常见的全局代理对 Rstudio 中的 R 终端不起作用。
  > 如`Sys.setenv(all_proxy='socks5://127.0.0.1:10808')`会让 R 中的流量全部通过本机的 10808 端口 socks5 代理 (重启 Rstudio 后失效)。偶尔安装 github 上的包时网络连接不上或者特别慢时可以启用代理加速。

- R 语言解释器级别：使用`options()`查看与修改。
  > options() 实际上是查看并修改 globalEnv 中的`.Options`对象。options 中的变量很多很杂，一些 R 包的设置项也会写进这里。`options()`主要指定了 R 语言的一些默认行为，比如控制台终端一次最多打印多少行输出，`read.table()`时是否自动讲字符串变量转换成`factor`类型，R 包安装时使用的镜像站地址等等。

## R 语言的常见数据类型

### R 语言的一些基础知识

#### 命令提示符

首先需要知道，所有运算和操作，都是需要时间的。一些简单的运算时间很短，瞬间就能完成。但是有的运算耗时相对比较长，而在它运算完成之前，R 命令行会处于忙碌状态，无法接受新的命令并执行。因此为了提示使用者现在是否可以输入命令，有一个叫`命令提示符`的东西。Rstudio 中的命令提示符为`>`。只有在控制台最下端显示`>`的时候你才能输入命令。

> 没用小知识：
>
> 命令提示符其实是可以改的。控制台中输入`options(prompt='新的命令提示符')`可以修改你的命令提示符。
> 比如：
>
> ![](/assets/img/tutorial/62dd2663ff975e032068a6dfab73cd0169e25056f2d67cd0ad0d7939c096c4e1.png)

然后，你必须能了解与分辨编程语言中的一些常见的基础数据类型：

- 字符串：  
  字符串可以简单理解为文本。

  ```R
  >example='hello world'
  >print(example)
  输出：
  [1] "hello world"

  >example2="1.14"
  >print(example2)
  输出:
  [1] "1.14"

  >example+1
  输出：
  Error in example + 1 : 二进列运算符中有非数值参数
  ```

  解释器区分字符串与非字符串的主要依据是有没有使用引号将文本括起来。有的编程语言中双引号`"`与单引号`'`有细微区别，但在 R 语言中两种引号的功能完全相同，挑选一个喜欢的用就可以。遇到需要在引号中使用引号的场合，可以结合两种引号一起使用以区分，比如`text='He said "Hello!"'`。

  注意，字符串是可以有数字的。字符的 1 和数值的 1 并不相同！如上面代码中的"1.14"没有任何大小上的意义，无法进行加减乘除等运算。

- 数值：

  如 1234 等，数值型的对象代表数值大小，可以进行加减乘除等运算。

  ```R
  >example=1.14
  >print(example)
  输出：
  [1] 1.14

  >example+1
  输出：
  [1] 2.14
  ```

  其他一些编程语言中会需要区分整数，浮点数等不同种类的数值，但在 R 语言中一般不需要关注这个。

  - 空值与特殊值

  R 语言中的空值或者说与空值类似的值一共有三种。

  - `NA`  
    `NA`的意义为空，是"Not Available"是缩写，但是它会占位 (长度为 1)。比如一个表格：
    位置|1|2|3
    ---|---|-|-
    内容|'a'|`NA`|'c'

    NA 代表此处为空，但是有个空格子。  
    ⚠️`NA`无法用常规的等于判断语句识别。比如`NA==NA`的结果为`F`。
    必须使用`is.na()`函数判断。

  - `NULL`  
    `NULL`是真正意义上的空，代表连格子也不存在 (长度为 0)。
    位置|1|不存在|2
    ---|---|-|-
    内容|'a'|`NULL`|'c'

    上表为了便于理解画出了 NULL 的位置，但实际上它长这样：
    位置|1|2
    ---|--|-
    内容|'a'|'c'

    在 R 中将一个值赋值为`NULL`等于删除这个值。  
    与`NA`类似，

  - `logical(0)`,`numeric(0)`,`character(0)`等  
    这几个值都是分别属于逻辑值，数值，字符串。但它们的长度都是零，类似于有类型的`NULL`。它们的出现大多是`NULL`经过运算的产物，一般不会主动创建。具体见下文`逻辑值(布尔值) `部分。

  - `NaN`  
    `NaN`其实并非空值。`NaN`是"Not a Number"的缩写，代表该值为数学上不存在的值，比如`log(-1)`，是一种数学运算的产物。  
    ⚠️ 正数除以 0 的结果并不是`NaN`，而是无限`Inf`。0 除以 0 的结果是`NaN`。

    ```R
    >log(-1)
    输出：
    [1] NaN
    Warning message:
    In log(-1) : NaNs produced

    >10/0
    输出：
    [1] Inf

    >0/0
    输出：
    [1] NaN
    ```

- 逻辑值 (布尔值)

  逻辑值其实就是`TRUE`和`FALSE`,也可以简写成`T`和`F`。一般用于判断语句。  
  ⚠️`True`是错误的写法，必须全大写。  
  除了`T`和`F`，其实还有一种`logical(0)`的值也是逻辑值。`logical(0)`是一种长度为 0 的逻辑值，它没有值，但是使用类型判断函数`is.logical()`判断的时候结果为`T`。这种值的出现一般与`NULL`有关，判断语句或函数中出现`NULL`常常会导致结果为`logical(0)`。而`NULL`出现在这种地方的最常见原因是使用函数的时候没写参数，参数使用了默认值`NULL`。

  ```R
  >age <- NULL
  >18 > age
  输出：
  logical(0)

  >is.logical(logical(0))
  输出：
  [1] TRUE
  ```

  > 没什么用的小知识：
  >
  > 严格来说，只有`TRUE`和`FALSE`算是 R 语言中的逻辑关键字。`T`和`F`其实只是两个初始设置好的变量，其值分别为`TRUE`和`FALSE`。因此其实`T`和`F`是可以被重新赋值的，而`TRUE`和`FALSE`则因为是关键字，不能被赋值。
  >
  > ```R
  > >T <- FALSE
  > >print(T)
  > 输出：
  > [1] FALSE
  >
  > >TRUE <- FALSE
  > 输出：
  > Error in TRUE <- FALSE : invalid (do_set) left-hand side to assignment
  > ```
  >
  > 因此，如果你的同学和你有仇，你可以偷偷打开他的电脑，在他的用户目录下新建或修改 R 每次启动自动运行的脚本`.Rprofile`，在其中加入
  >
  > > ```R
  > > T <- FALSE
  > > F <- TRUE
  > > ```
  > >
  > > 😈😈😈 让他在使用简写逻辑值的时候享受一个逆反的 R 语言解释器。

还有一些其他的数据类型，后面提到再说。暂时你只需要了解这些。

### 一维对象

R 语言中常见的一维数据类型有:

- `vector` (向量)
- `factor` (矢量)
- `list` (列表)

#### `vector`

##### 使用`c()`创建 vector

最常见的创建 vector 的方法为使用`c()`函数。  
可以在 vector 后面接`[]`，对 vector 取子集。

```R
# 创建vector
>example1 <- c(1,'2','a',NA)
>print(example1)
输出：
[1] "1" "2" "a" NA

# 对vector取子集
>example1[2]
输出：
[1] "2"

# 使用vector对vector取子集
>example1[c(2,4)]
输出：
[1] "2" NA
```

example1 结构示意图：
index|1|2|3|4
---|---|-|-|--
name|NULL|NULL|NULL|NULL
value|"1"|"2"|"a"|NA

⚠️ 大部分编程语言的索引从 0 开始递增，而 R 语言的索引从 1 开始。  
⚠️vector 中的值必须为同一数据类型。如 example1，由于第二、三元素为`"2"`,`"a"`,是字符串类型，因此第一位的数值 1 也被转换成了字符串的`"1"`。`NA`代表此处为空，不会被转换类型。

```
# vector中的元素可以有名字
>example2 <- c(a=1,b=2,c=3)
>print(example2)
输出：
a b c
1 2 3

# 使用名字(字符串索引)对vector取子集
>example2["b"]
输出：
b
2

# ⚠️错误示范
>example2[b]
输出：
Error: object 'b' not found

# ⚠️挽救错误示范
>b<-'c'
>example2[b] # 等价于example2["c"]
输出：
c
3
```

example2 结构示意图：
index|1|2|3
---|---|-|-
name|"a"|"b"|"c"
value|1|2|3

一个 vector 主要由它的值，索引，名字 (字符串索引) 组成。
其中值和索引是必定会有的，名字可以不指定，默认为`NULL`，即不存在。

使用`:`可以快速生成连续数字向量。该方法得到的向量没有名字。

```R
>1:10 # 等价于c(1,2,3,4,5,6,7,8,9,10)
输出：
[1]  1  2  3  4  5  6  7  8  9 10

>5:2 # 逆序也可以
输出：
[1] 5 4 3 2
```

##### 修改 vector

使用数值索引与字符串索引对 vector 取子集在前面的示例代码中已经示范过了。
除此之外，还有一种使用逻辑值 vector 对 vector 进行子集操作的方法。

```R
example1[c(T,F,T,F)] #使用一个长度与被取子集的vector一致的逻辑值向量作为索引
输出：
[1] "1" "a"
# 只返回了位置为T的值
```

⚠️ 对向量取子集时，如果使用了不存在的索引或字符串索引，并不会报错，而是会返回`NA`。

```R
>example1[99]
输出：
<NA>
  NA
```

⚠️R 语言的索引中，负号`-`的意义与 python 中不一样，不能使用如`example1[-1]`这样的方式取`example1`的最后一位元素。在 R 语言中，在**数字**索引 vector 前面带负号代表删除索引对应位置的元素的意思。比如：

```R
example1[-1]
输出：
[1] "2" "a" NA

example1[-c(1:2)] #可以一次删多个
输出：
[1] "a" NA

example2[-c('a','b')]
输出：
Error in -c("a", "b") : invalid argument to unary operator
# 只有数字索引能这么干，因为实际上这个操作是先计算-c(1:2)的值,其结果为c(-1,-2),然后R解释器认为负号代表删除，删掉了1,2号位置的元素。而-c('a','b')本质是对字符串进行四则运算操作，于是在这一步报错。
```

**合并向量**或**给向量增加元素**可以使用`c()`。

```R
>example3<-c(114514,example1,example2)
>print(example3)
输出：
                                                    a        b        c
"114514"      "1"      "2"      "a"       NA      "1"      "2"      "3"
# 页面宽度不够的话此处会换行
```

> ⚠️ 重要小知识：关于 R 语言的打印函数`print()`与`cat()`以及 R 命令行的默认打印行为
>
> 想必你已经注意到了，前文的示例代码中多次出现了`print()`这个函数。
>
> `print()`函数的功能是**输出**传递给它的`对象`(或者说`变量`).其中这个具体的**输出**方式，根据具体的变量类型会有所变化，这个变化的具体实现是依赖于 R 语言的 S3 面向对象编程方式，这个后面再细讲。
>
> 但是所有的输出方式都是根据这个对象本身的类型来设计的，主旨都是为了能给更好地让使用者能够直观地了解到这个对象是什么样子。比如对于一个字符串，数值，向量或者表格这种存贮数据的对象类型，`print()`的输出方式是将它们的内容直接在控制台用文本的方式打印出来。而对于函数(**是的，函数也是一种对象**)，`print()`的输出方式则是将函数的代码在控制台中打印出来。而对于一个 `ggplot2`绘图包生成的`ggplot2`图象对象，`print()`的输出方式是在绘图窗口中把这个图片画出来。
>
> 而如果你在**R 的命令行中**只输入一个对象的名字，没有指定任何的函数来对这个对象进行操作，R 语言解释器会**自动**为该对象使用`print()`函数。比如前文中的对向量取子集的示例代码：
>
> ```R
> # 使用名字(字符串索引)对vector取子集
> example2["b"]
> 输出：
> b
> 2
> ```
>
> 此处的`example2["b"]`完全等价于`print(example2["b"])`,而且后者才是它的真实情况。
>
> ⚠️ 这个 R 解释器默认`print()`的行为，只会发生在用户直接在命令行/控制台中输入对象名的情况。与之不同的是，在循环或者函数的代码块中，是不会发生默认`print()`的行为的。比如：
>
> ```R
> library(ggplot2)
> # 此处，变量p为一张ggplot2图像，print(p)会画出它的内容。
> p<-ggplot(data=data.frame(x=1:3,y=1:3))+geom_point(aes(x=x,y=y))
> #直接p
> p
> 输出：右下角画出了图
>
> #在循环中p
> for (i in 1:3){
>  p
> }
> 输出：什么也没有发生
> ```
>
> 使用 R 绘图的时候经常会遇到需要通过`print()`输出图片以保存的情况，如果是使用循环批量存图记得循环体中一定要`print()`哦。

#### `list`

##### 什么是`list`

`list`的结构与特点与`vector`十分相似，其区别在于`list`中每个元素的内容可以是 R 语言中的任何对象，也不要求它们的类型同一。而`vector`中的元素只能是字符串，数值，逻辑值空值等`原子型数据`。

##### 创建`list`

创建`list`的方法与向量类似，只是把`c()`换成了`list()`

```R
example_list<-list(ex1=example1,ex2=example2,example3)
print(example_list)
输出： #多行
$ex1
[1] "1" "2" "a" NA

$ex2
a b c
1 2 3

[[3]]
                                                    a        b        c
"114514"      "1"      "2"      "a"       NA      "1"      "2"      "3"


# 使用数字索引取list的子集
example_list[1]
输出： #注意，此处返回的对象类型为list,是一个只有一个元素的list。
$ex1
[1] "1" "2" "a" NA

# 使用字符串索引取list的子集
example_list['ex2']
输出：#注意，此处返回的对象类型为list,是一个只有一个元素的list。
$ex2
a b c
1 2 3

# 使用逻辑值取list的子集
example_list[c(T,T,F)]
输出：
$ex1
[1] "1" "2" "a" NA

$ex2
a b c
1 2 3
```

通过上面的例子，我们可以发现，list 同样可以使用数字索引，字符串以及逻辑值来进行取子集的操作，与向量十分类似。对 list 中的元素进行删除操作也是一样的，可以通过负号`-`删除 list 中的部分元素。

> ⚠️ 重要小知识：查看对象类型  
> 对象可以被分成不同的种类，如`vector`,`list`,`data.frame`,`function`等。这些是 R 语言本身就有的`class`。还可以在这些的基础上自己定义新的`class`，如`ggplot2`包的`ggplot2`对象。由于不同的数据类型有着不同的行为，输入给同一个函数以后也有可能会触发完全不同的函数代码，因此弄清楚一个对象到底是什么类型是十分重要的。
>
> ```R
> #使用class()查看对象的类型
> class(example_list[1])
> ```
>
> > 输出：  
> > [1] "list"

##### 取出 list 中的元素

通过前面的例子我们可以发现，单纯的使用`[]`对`list`取子集，无论怎么取最终得到的始终是一个`list`，哪怕它的长度只有 1.
要打开`list`这个盒子，得到里面的对象，有两种办法：

- 双中括号`[[]]`

```R
example_list[[1]]
```

> 输出：  
> [1] "1" "2" "a" NA

在原本对`list`取子集的基础上，把一个
