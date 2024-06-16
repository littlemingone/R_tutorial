# R 语言教程

## R 语言解释器以及 IDE 的安装与配置

<font color=#FF0000 >⚠️ 注意：本部分主要针对 Windows 平台用户，mac 与 linux 用户请参照 windows 的内容自行解决。</font>

### 安装过程中可能用到的网站：

- R 语言官网 CRAN([清华镜像](https://mirrors.tuna.tsinghua.edu.cn/CRAN/))
- [Rstudio 官网 Posit](https://posit.co/products/open-source/rstudio/)
  > 注：它曾经是www.rstudio.com，但后来已被Posit公司收购，软件的下载和社区都迁移到了posit.co上。

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
  > Rtools 本质是一些 C/C++和 Fortran 的编译器，用于将这些语言的代码编译成二进制文件。base 和大部分 R 包安装时是直接安装编译好的二进制文件，因此其实并不需要编译步骤，也用不到 Rtools。所以理论上来说 Rtools 并不是必须安装的。但根据我的经验，大部分需要从 github 直接安装的包都需要 Rtools 编译。这种包虽然不多，但你总有用到的一天，因此建议把 Rtools 装上。
  >
  > ⚠️Rtools 版本需与 R 版本匹配，要求不是很严格但最起码大版本需要匹配。不知道装哪个就都装最新的。

- R 语言集成开发环境(IDE)：Rstudio
  > IDE 对于 R 语言的使用也不是必须的。但是它提供了美观，便于使用的界面和方便配置的 gui 菜单界面。总之没必要折磨自己裸奔用 R。
  >
  > R 语言有多种其他可选 IDE，比如 Vscode，jupyter notebook 等。尽管 Rstudio 也有很多缺点，但对于新手来说 Rstudio 永远是功能最完善最好用的 IDE，因此<span style="color:red;">新手请一定要无脑选择 Rstudio。</span>
  >
  > Rstudio 的版本与 base 版本相互独立，更新时互不干涉。Rstudio 只是一个壳子。

### Rstudio 的开箱设置

- 设置镜像源：

  默认的 R 包安装会从国外服务器下载 R 包，容易出现网络连接不上或者速度慢的情况。国内很多高校都架设了公用的国内镜像站，自动同步国外服务器的资源。从国内镜像站下载会快很多。  

  注：除了CRAN，即官方镜像之外，我们还经常需要使用Bioconductor网站上的R包。因此Bioconductor的软件源也是有镜像的。不过一般来说使用Bioconductor安装的时候会自动套用CRAN镜像或者在命令行提示询问你要使用哪个镜像站，所以一般可以不管。

  - Rstduio 设置步骤如下：
    ![](/assets/img/tutorial/69aea78628e983e2a6c60687a989bd22e8fb29a27ac1c55130ad5c95028aaab0.png)

  - 使用命令行设置：  
  此配置重启R后失效，因此需要将它们写到R的启动脚本里，每次打开R的时候自动加载。
    ```R
    options("repos" = c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/"))
    options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
    ```
- 打开Rstudio的语法高亮
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
  > 如`Sys.setenv(all_proxy='socks5://127.0.0.1:10808')`会让 R 中的流量全部通过本机的 10808 端口 socks5 代理(重启 Rstudio 后失效)。偶尔安装 github 上的包时网络连接不上或者特别慢时可以启用代理加速。

- R 语言解释器级别：使用`options()`查看与修改。
  > options()实际上是查看并修改 globalEnv 中的`.Options`对象。options 中的变量很多很杂，一些 R 包的设置项也会写进这里。`options()`主要指定了 R 语言的一些默认行为，比如控制台终端一次最多打印多少行输出，`read.table()`时是否自动讲字符串变量转换成`factor`类型，R 包安装时使用的镜像站地址等等。

## R语言的常见数据类型

### 一维对象
