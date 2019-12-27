# SAI

New networks Leela Zero, a Sensible Artificial Intelligence

里拉元的新网络，一个敏锐的围棋人工智能：SAI

## 获取SAI

[官方网址](http://sai.unich.it)：可获取最新的官方权重文件

[项目网址](https://github.com/sai-dev/sai/releases/)：可获取最新的引擎源代码和官方程序


## 编译/安装SAI

本节提供私有编译SAI的方法，如果已获取官方提供的版本，可跳过本节。

colab环境

```colab
# 安装编译工具
!apt install cmake g++ libboost-dev libboost-program-options-dev libboost-filesystem-dev opencl-headers ocl-icd-libopencl1 ocl-icd-opencl-dev zlib1g-dev

# 克隆项目源代码
!rm -rf sai
!git clone --recursive https://github.com/sai-dev/sai
!cd sai && git branch
!cd sai && git shortlog

# 编译
!cd sai && mkdir build
!cd sai/build && cmake ..
!cd sai/build && cmake --build .

# 测试
!cd sai/build/&& ./tests

# 复制sai程序至子文件夹autogtp下
!cd sai/build && cp sai autogtp

# 运行
!cd sai/build/autogtp/ && ./autogtp --url http://sai.unich.it/ --username $username --password $passwd -g2 -m100| grep minute
```

## 运行SAI

### 命令行方式

从项目网址下载的官方程序/或自行编译好的程序，可以通过命令行方式，配合权重文件，直接调用。
略
### 客户端加载

Lizzie客户端设置：

```bash
$Path路径\sai-0.17.4-gpu\sai.exe -g --weights $Path路径\sai-0.17.4-gpu\networks\$Hash值.gz --noponder -b 0 -p 0 -v 0 -r 3 -m 0 --gpu 0 --gpu 1 --lambda 0.5 --mu 0 --komi 7.5 --nrsymm --timemanage auto
```

* Lizzie客户端设置说明（对弈必看）
    * 该示例可以用于本地棋谱分析，空格开启或暂停，无限计算
    * lizzie的对弈设置中，自带限时、限计算量设置，可用于人机对弈自测
        1. genmove模式
        2. 分析模式
        3. [time_settings](https://www.gnu.org/software/gnugo/gnugo_19.html)
            * 该参数基于比赛用时规则设计而来
            * 不能在Lizzie客户端设置中直接写入该参数
            * 通过对弈面板设置以上#a、#b模式的用时、用计算量方法
            * Lizzie的对弈面板设置较该参数更强大
    * 网棋需要修改 -b 网络延迟参数、删除--noponder开启全程思考模式、以及棋风调整--lambda 0


Sabaki客户端设置

```bash
# Path 引擎路径
$Path路径\sai-0.17.4-gpu\sai.exe

# Arguments 参数设置
-g --weights $Path路径\sai-0.17.4-gpu\networks\$Hash值.gz --noponder -b 0 -p 0 -v 0 -r 3 -m 0 --gpu 0 --gpu 1 --lambda 0.5 --mu 0 --komi 7.5 --nrsymm --timemanage auto

# Initial commands 初始化参数
time_settings 0 1 0

```

 time_settings 需具体参考比赛规则设置([设置方法](https://www.gnu.org/software/gnugo/gnugo_19.html))


### SAI引擎特有参数说明（必读）

[官方Wiki](https://github.com/sai-dev/sai/wiki/Features)

* --lambda 0 --mu 0 = LeelaZ/AlphaZ风格，退让目数争取更稳定的胜率
* --lambda 0.5 --mu 0.5 = 使用虚拟贴目
    * SAI优势下产生贴目负担，形成不退让风格
    * SAI需要获得 虚拟贴目 = [领先目数 * 递减函数(mu参数)] 的额外目数才可胜利
    * SAI劣势的时候产生贴目补贴，不致棋招变形。
    * SAI需要失去 虚拟贴目 = [落后目数 * 递减函数(mu参数)] 的额外目数才会失败
    * lambda参数0.5可变，mu参数0.5可变
* --lambda 0.5 --mu 0 = SAI默认设置
    * SAI自动在追求更高胜率招法的同时，兼顾了目数的胜利(lambda)
    * SAI不额外产生虚拟贴目，造成行棋负担和补贴(mu)
    * lambda参数0.5可变
* --komi7.5 调整任意贴目，是SAI较LeelaZ更优胜的地方，7.5可变（+-361.5，步长0.5）
   * 部分引擎需要在棋盘参数上额外说明贴目，其优先级为最高，如lizzie
* --symm 利用镜像方法剪枝 （示例中未使用，与--nrsymm冲突）
* --nrsymm 利用镜像方法剪枝（同--symm），兼顾棋盘行棋礼仪（下手方第一手行在右上角）
* --noladdercode 关闭启发式征子探索（示例中未添加），默认开启设置，极大提升征子判断
* -j 支持日本数目规则（示例中未添加）


## 支持SAI

Would you like to contribute? If you have a computer with a recent GPU and updated drivers, and are willing to let it run for some hours per day, please do as follows:

1. 在 [这里](http://sai.unich.it/user-request) 注册用户名和密码
2. 如果
    * 你是 Windows user
        * 首先看看 <获取SAI> 那一节的内容
        * 双击sai.hta，这是一个表单提交程序
            * 给予运行权限
            * 填写第一步注册的用户名密码
            * 如果你的电脑够强，可以尝试在参数列(包括前端空格)填写 -g2
            * 如果你只想跑50张谱就结束，可以在参数列(包括前端空格)填写 -m50
            * AutoGTP.exe会自动下载权重并开始跑谱了
            * 如果网络不佳，你最好去官方网址用下载工具先把权重下好
            * 如果提示权重文件hash值不符，那就是网络不佳导致权重下载不完整，删除并重新运行sai.hta吧。
    * 如果你是 a Linux or macOS user, follow this link: https://github.com/sai-dev/sai#macos-and-linux
