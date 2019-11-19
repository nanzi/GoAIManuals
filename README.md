# GoAIManuals
go,baduk,weiqi,manuals,command line



## Leela Zero

### autogtp.exe

[Download Engine](https://github.com/leela-zero/leela-zero/releases)

[Download Weight Files](https://zero.sjeng.org)


Contribute to leelazero: Run **autogtp.exe** directly. 

If there were some issues on downloading weight files, You can download them from link above.

Then make a subfolder named "networks" in leelazero, and move weight files in it.

```bash
./autogtp -h
  -?, -h, --help                        #Displays this help.
  -v, --version                         #Displays version information.
  -g, --gamesNum <num>                  #Play 'gamesNum' games on one device
                                        #(GPU/CPU) at the same time.
  -u, --gpus <num>                      #Index of the device(s) to use for
                                        #multiple devices support.
  -k, --keepSgf <output directory>      #Save SGF files after each self-play
                                        #game.
  -d, --debug <output directory>        #Save training and extra debug files
                                        #after each self-play game.
  -t, --timeout <time in minutes>       #Save running games after the timeout
                                        #(in minutes) is passed and then exit.
  -s, --single                          #Exit after the first game is completed.
  -m, --maxgames <max number of games>  #Exit after the given number of games is
                                        #completed.
  -e, --erase                           #Erase old networks when new ones are
                                        #available.
  # with <> parameter, we need to provide them to arguments, like numbers or file paths.
  # But don't use "<>" when providing real information. We can use space to help reading.
  #
  # e.g.:
  # ./autogtp -g2 -u0 -u1 -k c:\sgfs\ -m 10 -e
  #
  # It says 2 games played on 1 device as "-g2", and use 2 devices which are "-u0" and "-u1",
  # which also means 4 games are played in the same time. 
  # You really need to have two GPUs to run this command correctly.
  # save selfplayed games to blockdevice driver c, subfolder sgfs:"-k c:\sgfs\", 
  # and end contribute with 10 selfplays "-m 10".
  # "-m10" also correct，"-u 0 - u 1 " also correct，choose a style as you like.
  # -e without parameters told autogtp.exe clear old networks automatically.
```

***

[引擎地址](https://github.com/leela-zero/leela-zero/releases)

[权重地址](https://zero.sjeng.org)

参加分布式计算(跑谱)： 直接运行 **autogtp.exe**

如果下载权重遇到问题，你可以访问上面的权重地址，提前下载好它们。

然后在leelazero文件夹下建立子文件夹“networks”，这个子文件夹与autogtp.exe程序同在leelazero文件夹里面，是同级的。

之后将下载好的最新权重或其他权重放到networks文件夹下面，运行 autogtp.exe 即可进行自对弈比赛和晋升比赛了。

```bash
./autogtp -h
  -?, -h, --help                        #显示 autogtp 程序的帮助信息.
  -v, --version                         #显示 autogtp 程序的版本信息.
  -g, --gamesNum <num>                  #同时在一个硬件设备(GPU或CPU)上运行 'gamesNum' 数量的游戏.
                                        
  -u, --gpus <num>                      #启用多个硬件设备的序号.
                                        
  -k, --keepSgf <output directory>      #每一局自对弈结束后，保存弈谱.
                                        
  -d, --debug <output directory>        #每一局自对弈结束后，保存训练文件和调试信息文件.
                                        
  -t, --timeout <time in minutes>       #经过<以分钟数计算的整数时间>，保存游戏并退出 autogtp 程序.
                                        
  -s, --single                          #第一局游戏结束后，退出 autogtp 程序.
  -m, --maxgames <max number of games>  #给定数量的游戏完成后，退出 autogtp 程序.
                                        
  -e, --erase                           #启用后自动删除陈旧权重.
  
  # 带有<>变量的参数，需要提供所需变量信息，如数量、文件夹路径等信息。
  # 提供实际信息时，无需添加<>符号。空格可以适当添加，帮助阅读不影响程序使用。
  #
  # 例子： ./autogtp -g2 -u0 -u1 -k c:\sgfs\ -m 10 -e
  #
  # 即 1个设备同时运行2个游戏-g2，调用两个计算卡-u0/-u1，（同时共运行4个游戏）
  # 保存自对弈谱到c盘sgfs文件夹下面-k c:\sgfs\, 自对弈10局就结束跑谱-m 10。
  # -m10同样是正确的写法，-u 0 - u 1 同样正确，选择适合自己阅读的参数写法即可。
  # -e 无参变量告诉程序开启自动清理旧权重的功能。
```

### leelaz.exe

```bash
.\leelaz.exe -h
Leela Zero 0.17  Copyright (C) 2017-2019  Gian-Carlo Pascutto and contributors
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions; see the COPYING file for details.


Generic options:
  -h [ --help ]                         #Show commandline options.
  -g [ --gtp ]                          #Enable GTP mode.
  -t [ --threads ] arg (=0)             #Number of threads to use. Select 0 to
                                        #let leela-zero pick a reasonable
                                        #default.
  -p [ --playouts ] arg                 #Weaken engine by limiting the number of
                                        #playouts. Requires --noponder.
  -v [ --visits ] arg                   #Weaken engine by limiting the number of
                                        #visits.
  -b [ --lagbuffer ] arg (=100)         #Safety margin for time usage in
                                        #centiseconds.
  -r [ --resignpct ] arg (=-1)          #Resign when winrate is less than x%.
                                        #-1 uses 10% but scales for handicap.
  -w [ --weights ] arg (=$Path\best-network)
                                        #File with network weights.
  -l [ --logfile ] arg                  #File to log input/output to.
  -q [ --quiet ]                        #Disable all diagnostic output.
  --timemanage arg (=auto)              #[auto|on|off|fast|no_pruning] Enable
                                        #time management features.
                                        #auto = no_pruning when using -n,
                                        #otherwise on.
                                        #on = Cut off search when the best move
                                        #can't change, but use full time if
                                        #moving faster doesn't save time.
                                        #fast = Same as on but always plays
                                        #faster.
                                        #no_pruning = For self play training
                                        #use.

  --noponder                            #Disable thinking on opponent's time.
  --benchmark                           #Test network and exit. Default args:
                                        #-v3200 --noponder -m0 -t1 -s1.
  --cpu-only                            #Use CPU-only implementation and do not
                                        #use OpenCL device(s).

OpenCL device options:
  --gpu arg                             #ID of the OpenCL device(s) to use
                                        #(disables autodetection).
  --full-tuner                          #Try harder to find an optimal OpenCL
                                        #tuning.
  --tune-only                           #Tune OpenCL only and then exit.
  --batchsize arg (=0)                  #Max batch size.  Select 0 to let
                                        #leela-zero pick a reasonable default.
  --precision arg                       #Floating-point precision
                                        #(single/half/auto).
                                        #Default is to auto which automatically
                                        #determines which one to use.

Self-play options:
  -n [ --noise ]                        #Enable policy network randomization.
  -s [ --seed ] arg                     #Random number generation seed.
  -d [ --dumbpass ]                     #Don't use heuristics for smarter
                                        #passing.
  -m [ --randomcnt ] arg (=0)           #Play more randomly the first x moves.
  --randomvisits arg (=1)               #Don't play random moves if they have <=
                                        #x visits.
  --randomtemp arg (=1)                 #Temperature to use for random move
                                        #selection.
```

在lizzie/sabaki的调用中，可以使用：

```bash
路径/leelaz.exe -g -w 路径/权重文件 -p0 -v0 -b0 -m0 -r1 --noponder --gpu0 --gpu1 -l 路径/日志文件 --timemanage auto

 # -g 通过客户端 gtp 命令控制leelaz的行为。必要的参数，否则只是后台计算，无法与用户交互。
 # -p(playouts)是模拟计算量,-v(visits)是节点计算量，0代表无限制。
 # 同数量的v参数产生的playout往往大于同数量的p参数（1600v的playout平均后大于1600p）。
 # 但两者差距不大，没有数量级上的差距。1600p和1600v都是常用的参数。
 #
 # -b0 忽略网络延迟。我们一般是自己的电脑，不用考虑远程计算带来的网络延迟问题。使用ai对弈平台需要这个参数，-b200是给予200毫秒延迟。
 # -r1 胜率1%以下就认输。
 # --noponder 对手回合不进行局面计算。分析模式下不要开启这个参数。公平对弈时开启（人机对弈/ai对弈）。
 # 
 #  --gpu N 如果只有1张显卡，或没有显卡，可以不使用这个参数，默认使用独立显卡。
 # -l记录输出日志，可以不用。有些客户端可以把日志输出记录在棋谱注释里。
 # --timemanage auto 启用自动时间管理模式，如果最佳选点无变化则停止搜索。but use full time if moving faster doesn't save time.
 #
 
有用的GTP命令


time_settings是GTP协议提供的命令，leelaz支持这个设置。这个命令提供了"设置比赛用时规定"的参数。

time_settings 0 1 0   是指 总思考时间无限秒 1次读秒 每步限时无限秒
time_settings 0 1 120 是指 总思考时间无限秒 1次读秒 每步限时120秒

Sabaki中在 "Manage Engines" 选项页中，"Initial commands" 行内填入time_settings参数
其他开启分析、genmove等都是通过客户端发送gtp命令给 leelaz 实现的。

```
## SAI


```bash
SAI 0.17 release 4 (19x19) is a fork of Leela Zero.
Leela Zero Copyright (C) 2017-2019  Gian-Carlo Pascutto and contributors.
SAI Copyright (C) 2018-2019 SAI Team.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions; see the COPYING file for details.


Generic options:
  -h [ --help ]                         #Show commandline options.
  -g [ --gtp ]                          #Enable GTP mode.
  -j [ --japanese ]                     #Enable Japanese scoring mode.
  -t [ --threads ] arg (=0)             #Number of threads to use. Select 0 to
                                        #let SAI pick a reasonable default.
  -p [ --playouts ] arg                 #Weaken engine by limiting the number of
                                        #playouts. Requires --noponder.
  -v [ --visits ] arg                   #Weaken engine by limiting the number of
                                        #visits.
  --komi arg (=7.5)                     #Komi
  --lambda arg (=0.5)                   #Lambda value
  --mu arg (=0)                         #Mu value
  --symm                                #Exploit symmetries by collapsing policy
                                        #values of equivalent moves to a single
                                        #one, chosen randomly. When writing
                                        #training data, split the visit count
                                        #evenly among equivalent moves.
  --nrsymm                              #Same as --symm, but the move is chosen
                                        #to be in the general direction of the
                                        #'polite' eightth of the board, instead
                                        #of randomly.
  -b [ --lagbuffer ] arg (=100)         #Safety margin for time usage in
                                        #centiseconds.
  -r [ --resignpct ] arg (=-1)          #Resign when winrate is less than x%.
                                        #-1 uses 10% but scales for handicap.
  -w [ --weights ] arg (=$Path\best-network)
                                        #File with network weights.
  -l [ --logfile ] arg                  #File to log input/output to.
  -q [ --quiet ]                        #Disable all diagnostic output.
  --timemanage arg (=auto)              #[auto|on|off|fast|no_pruning] Enable
                                        #time management features.
                                        #auto = no_pruning when using -n,
                                        #otherwise on.
                                        #on = Cut off search when the best move
                                        #can't change, but use full time if
                                        #moving faster doesn't save time.
                                        #fast = Same as on but always plays
                                        #faster.
                                        #no_pruning = For self play training
                                        #use.

  --noponder                            #Disable thinking on opponent's time.
  --benchmark                           #Test network and exit. Default args:
                                        #-v3200 --noponder -m0 -t1 -s1.
  --nocache                             #Disable neural network cache.
  --cpu-only                            #Use CPU-only implementation and do not
                                        #use OpenCL device(s).

OpenCL device options:
  --gpu arg                             #ID of the OpenCL device(s) to use
                                        #(disables autodetection).
  --full-tuner                          #Try harder to find an optimal OpenCL
                                        #tuning.
  --tune-only                           #Tune OpenCL only and then exit.
  --batchsize arg (=0)                  #Max batch size.  Select 0 to let SAI
                                        #pick a reasonable default.
  --precision arg                       #Floating-point precision
                                        #(single/half/auto).
                                        #Default is to auto which automatically
                                        #determines which one to use.

Self-play options:
  -n [ --noise ]                        #Enable policy network randomization.
  --noise-value arg (=0.03)             #Dirichilet noise for network
                                        #randomization.
  -s [ --seed ] arg                     #Random number generation seed.
  -d [ --dumbpass ]                     #Don't use heuristics for smarter
                                        #passing.
  --restrict_tt                         #Restrict use of Tromp-Taylor score in
                                        #search.
  -m [ --randomcnt ] arg (=0)           #Play more randomly the first x moves.
  --randomvisits arg (=1)               #Don't play random moves if they have <=
                                        #x visits.
  --randomtemp arg (=1)                 #Temperature to use for random move
                                        #selection.
  --blunderthr arg (=1)                 #Moves with winrate drop higher than
                                        #this, are blunders. Don't save training
                                        #data for moves before last blunder.
  --blunder_maxavg arg (=1.38629436)    #Blunders number is bounded by a Poisson
                                        #r.v. with this mean.
  --recordvisits                        #Don't normalize visits to probabilities
                                        #when writing training info.

Tuning options:
  --puct arg
  --policy_temp arg
  --logpuct arg
  --logconst arg
  --softmax_temp arg
  --fpu_reduction arg
  --fpu_zero                            #Use constant fpu=0.0 (AlphaGoZero). The
                                        #default is reduced parent's value
                                        #(LeelaZero).
  --adv_features                        #Include advanced features (legal moves,
                                        #last liberty intersections) when saving
                                        #training data. Shorten history from 8
                                        #past moves to last 4.
  --chainlibs_feat                      #Include 4 chain liberties feature plane
                                        #when saving training data. Shorten
                                        #history to 1 move.
  --chainsize_feat                      #Include 4 chain size feature plane when
                                        #saving training data. Shorten history
                                        #to 1 move.
  --ci_alpha arg




```

```bash
./sai.exe -g -w 路径/权重文件 -p0 -v0 -b0 -m0 -r1 --noponder --gpu0 --gpu1 -l 路径/日志文件 --timemanage auto --nrsymm --komi7.5 --lambda0.5
  --mu0
```

--lambda0   --mu0   = leela/alphagozero style，退让目数争取更稳定的胜率
--lambda0.5 --mu0.5 = 使用虚拟贴目产生不退让风格，SAI需要获得领先目数\*参数=虚拟贴目的额外目数才可胜利
--lambda0.5 --mu0   = SAI默认设置，SAI自动在追求更高胜率招法的同时，兼顾了目数的胜利，但不额外增加优势方的贴目负担 
