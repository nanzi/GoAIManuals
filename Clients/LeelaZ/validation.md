# validation

validation 是AI竞赛编排工具，可用于测试特定引擎下特定权重的棋力。

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



## 比赛结果的置信度表

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