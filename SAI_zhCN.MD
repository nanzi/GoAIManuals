# SAI

New networks Leela Zero, a Sensible Artificial Intelligence

里拉元的新网络，一个敏锐的围棋人工智能：SAI

## 获取SAI

[官方网址](http://sai.unich.it)：可获取最新的官方权重文件

[项目网址](https://github.com/sai-dev/sai/releases/)：可获取最新的引擎源代码和官方程序


## 编译/安装SAI
colab环境

```colab
//安装编译工具
!apt install cmake g++ libboost-dev libboost-program-options-dev libboost-filesystem-dev opencl-headers ocl-icd-libopencl1 ocl-icd-opencl-dev zlib1g-dev

//克隆项目源代码
!rm -rf sai
!git clone --recursive https://github.com/sai-dev/sai
!cd sai

//编译
!cd sai && mkdir build
!cd sai/build && cmake ..
!cd sai/build && cmake --build .

//测试
!cd sai/build/&& ./tests

//复制sai程序至子文件夹autogtp下
!cd sai/build && cp sai autogtp

//运行
!cd sai/build/autogtp/ && ./autogtp --url http://sai.unich.it/ --username $username --password $passwd -g2 -m100| grep minute
```

## 运行SAI

### 命令行方式

从项目网址下载的官方程序/或自行编译好的程序，可以通过命令行方式，配合权重文件，直接调用。
略
### 客户端加载

Lizzie客户端代码：用于本地棋谱分析与人机对弈自测
```bash
sai-0.17.4-gpu\sai.exe -g --weights sai-0.17.4-gpu\networks\$Hash值.gz --noponder -b0 -p0 -v0 -r3 -m0 --gpu0 --gpu1 --lambda0.5 --mu0 --komi7.5 --nrsymm --timemanage auto
```

* --lambda0 --mu0 = LeelaZ/AlphaZ风格，退让目数争取更稳定的胜率
* --lambda0.5 --mu0.5 = 使用虚拟贴目，在AI优势下产生贴目负担，形成不退让风格；AI劣势的时候产生贴目补贴，不致棋招变形。
    * SAI需要获得 虚拟贴目 = [领先目数 * 递减函数(mu参数)] 的额外目数才可胜利
    * SAI需要失去 虚拟贴目 = [落后目数 * 递减函数(mu参数)] 的额外目数才会失败
    * lambda参数0.5可变
    * mu参数0.5可变
* --lambda0.5 --mu0 = SAI默认设置
    * SAI自动在追求更高胜率招法的同时，兼顾了目数的胜利，但不额外产生虚拟贴目，造成行棋负担和补贴
    * lambda参数0.5
* --komi7.5 调整任意贴目，是SAI较LeelaZ更优胜的地方，7.5可变（+-361.5，步长0.5）
* --nrsymm 利用镜像方法剪枝（同--symm），兼顾棋盘行棋礼仪（下手方第一手行在右上角）
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
            * 如果你的电脑够强，可以尝试在参数列填写 -g2
            * 如果你只想跑50张谱就结束，可以在参数列填写 -m50
            * AutoGTP.exe会自动下载权重并开始跑谱了
            * 如果网络不佳，你最好去官方网址用下载工具先把权重下好
            * 如果提示权重文件hash值不符，那就是网络不佳导致权重下载不完整，删除并重新运行sai.hta吧。
    * 如果你是 a Linux or macOS user, follow this link: https://github.com/sai-dev/sai#macos-and-linux
