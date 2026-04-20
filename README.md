
## 1. 小组成员

- 邹毅2025303110076      [@zy076](https://github.com/zy076)
- 王东浩2025303110072    [@Fuguiera11y](https://github.com/Fuguiera11y)
- 刘谦2025303110050      [@Liuqian615](https://github.com/Liuqian615)
- 李飒2025303120111      [@kajolliangeliki857-cpu]( https://github.com/kajolliangeliki857-cpu)              
- 赵俊然2025303110075    [@Zhao2002jun](https://github.com/Zhao2002jun)

## 2. 论文与代码

- 论文：Estimating soil redistribution rates with the RadEro model: A physically based compartmental model for 137Cs analysis in an R package
- 论文doi：https://doi.org/10.1016/j.envsoft.2025.106551
- 代码仓库：https://github.com/eead-csic-eesa/RadEro

## 3. 复现环境

- OS：Windows
- R：R version 4.5.2 (2025-10-31 ucrt)
- renv：1.1.8
- 项目目录：`D:/D2RS/RadEro-main`
- 输出目录：`D:/D2RS/RadEro-output`

## 4. 复现内容

运行仓库提供的 `Radero_QuickStart_v1.0.8.R` 示例，成功完成多个 profile 的模拟并生成结果文件与图像。

生成的结果（输出目录 `D:/D2RS/RadEro-output/results`）包括：
- results.txt
- Ref_plot.png
- profile1_plot.png … profile6_plot.png（及对应 tempFiles 文件夹）

## 5. 可复制的复现步骤

1) 下载仓库 ZIP 并解压到 `D:/D2RS/RadEro-main`
2) 初始化/恢复环境：
```r
install.packages("renv")
renv::restore()
```

3) Windows 安装并配置 Rtools（确保能找到 gcc/make），用于从源码安装
4) 从源码安装 RadEro（避免二进制安装导致 rdb 损坏）
```r
setwd("D:/D2RS/RadEro-main")
# 使用最底层安装方式（本次复现成功）：
system("D:/D2RS/R-4.5.2/bin/x64/Rcmd.exe INSTALL .")
library(RadEro)
```
5) 修改并运行 QuickStart：
- 注释掉脚本中的 install.packages(...)（避免触发二进制安装）
- 将输出目录 direct 改为本机存在目录：D:/D2RS/RadEro-output
- 读取结果文件改为绝对路径：file.path(direct, "results", "results.txt")
- 运行：
 ```r
source("Radero_QuickStart_v1.0.8.R")
```

6) 锁定环境：
```r
setwd("D:/D2RS/RadEro-main")
renv::snapshot()
```

## 6. 遇到的问题与解决

- QuickStart 默认占位路径 C:\your\own\working\directory 导致 target_dir 不存在 → 改为 D:/D2RS/RadEro-output
- QuickStart 内部包含 install.packages(...)，触发二进制安装导致 RadEro.rdb is corrupt (libdeflate) → 注释 install.packages，改为源码安装
- 读取 results\results.txt 使用相对路径导致找不到文件 → 改为 file.path(direct, "results", "results.txt")


