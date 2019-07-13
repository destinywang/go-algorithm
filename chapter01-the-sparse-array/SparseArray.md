# 1. 实际场景


    假设有一个五子棋游戏, 棋盘容量为 11 * 11, 有三颗棋子, 如果想将棋盘保存下来, 需要如下方式
    0   0   0   0   0   0   0   0   0   0   0
    0   0   0   0   0   0   2   0   0   0   0
    0   0   0   0   0   1   0   0   0   0   0
    0   0   0   0   0   2   0   0   0   0   0
    0   0   0   0   0   1   0   0   0   0   0
    0   0   0   0   0   1   2   0   0   0   0
    0   0   0   0   0   0   0   0   0   0   0
    0   0   1   0   0   0   0   0   0   0   0
    0   0   0   0   0   0   0   0   0   0   0
    0   0   0   2   0   0   0   0   0   0   0
    0   0   0   0   0   0   0   0   0   0   0
    其中 0 代表空, 1 代表白棋, 2 代表黑棋
    由于该二维数组记录了很多默认值, 大部分都是没有实际意义的数据, 因此面对这种场景, 我们可以考虑使用稀疏数组来处理.

# 2. 概念

当一个数组大部分元素为 0, 或者同一个值时, 可以使用稀疏数组来保存该数组:

1. 记录数组一共有几行几列, 有多少个不同的值
2. 把具有不同值的元素的行列及值记录在一个小规模数组中, 从而缩小存储的规模

如果使用稀疏数组, 上面的棋盘就可以保存为如下的形式

| 行 | 列 | 值 |
| :-: | :-: | :-: |
| 11 | 11 | 0 |
| 1 | 6 | 2 |
| 2 | 5 | 1 |
| 3 | 5 | 2 |
| 4 | 5 | 1 |
| 5 | 5 | 1 |
| 5 | 6 | 2 |
| 7 | 2 | 1 |
| 9 | 3 | 2 |

# 3. 转化思路

二维数组转稀疏数组的思路:

1. 遍历原始二维数组, 得到有效数据的个数 sum
2. 根据 sum 就可以创建稀疏数组 sparseArr [][]int
3. 将二维数组的有效数据存储到稀疏数组

还原思路:

1. 先读取稀疏数组的第一行, 根据第一行的数组创建原始的二维数组
2. 在读取稀疏数组的后几行数据, 并赋给原始的二维数组即可