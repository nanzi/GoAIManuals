# validation

validation 是leelaz提供的围棋AI竞赛编排工具，用于测试特定引擎下特定权重的棋力。

## 使用 Usage

```bash
# leelaz引擎: leelaz 权重内战
$ cd leelez-0.17
$ ./validation -g 2 -k lz_lz_match_sgf -n path_to_first_lz_weight.gz -o "-g -v 400 -r 5 -w" -n path_to_second_lz_weight.gz -o "-g -v 400 -r 5 -w" --leelaz --leelaz

# sai 引擎+权重 vs leelaz 引擎+权重
$ cp sai-0.17.5/sai.exe leelaz-0.17/
$ cp sai-0.17.5/networks/abc.gz leelaz-0.17

$ cd leelez-0.17
$ ./validation -g 2 -k sai_lz_match_sgf -n abc.gz -o "-g -v 400 -r 5 -w" -n path_to_lz_weight.gz -o "-g -v 400 -r 5 -w" --sai --leelaz

# sai引擎 : sai权重 vs leelaz权重
$ ./validation -g 2 -k sai_sailoadlz_match_sgf -n abc.gz -o "-g -v 400 -r 5 -w" -n path_to_lz_weight.gz -o "-g -v 400 -r 5 -w" --sai --sai
```

* -g 2 : 同时跑2个比赛
* -k path_to_folder : 保存比赛棋谱的文件夹
* -n path_to_weight : 权重（与-o连用，前后区分2个引擎）
* -o "args line" : 引擎参数（与-n连用，前后区分2个引擎）
* --path_to_engine : 引擎程序（2个引擎）不同版本的alidation可能需要增加空格(-- program)

> 一个使用绝对路径的colab实例
```bash
!/content/sai_in_colab/validation -g 2 -k /content/sai_in_colab/sai_vs_lz -n /content/sai_in_colab/networks/d351f06e446ba10697bfd2977b4be52c3de148032865eaaf9efc9796aea95a0c.gz -o "-g -p1600 --noponder -t 1 -q -d -r 0 -w" -n /content/sai_in_colab/networks/b03edd5216a19ac79033e74214799c3c1d9d91d2077bab121783a398c865c38a.gz -o "-g -p1600 --noponder -t 1 -q -d -r 0 -w" -- /content/sai_in_colab/sai -- /content/sai_in_colab/sai 
```

## 比赛结果的置信度表

validation会自动计算置信度，在确定两个权重在当前引擎、参数和硬件下的强弱后，将自动结束对战编排。

因此依照程序自动结束，赛程可能短至几十局，长至千局。

|    \\    | 90%置信度 | 99%置信度 | 99.9%置信度 | 99.99%置信度 |
| ------- | -------- | -------- | ---------- | ----------- |
| 比赛总数 | 获胜次数  | 获胜次数  | 获胜次数    | 获胜次数     |
| 3       | 3        | -        | -          | -           |
| 5       | 4        | -        | -          | -           |
| 7       | 6        | 7        | -          | -           |
| 10      | 8        | 9        | 10         | -           |
| 30      | 19       | 22       | 24         | 25          |
| 50      | 30       | 34       | 37         | 39          |
| 100     | 57       | 62       | 66         | 69          |
| 200     | 110      | 117      | 123        | 127         |
| 400     | 214      | 224      | 232        | 238         |
| 800     | 419      | 433      | 444        | 453         |
| 1600    | 826      | 847      | 862        | 875         |
