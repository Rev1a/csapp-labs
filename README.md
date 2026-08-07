# CSAPP Labs

![Language](https://img.shields.io/badge/language-C-blue)
![Platform](https://img.shields.io/badge/platform-WSL%20%2F%20Linux-green)
![Progress](https://img.shields.io/badge/progress-BombLab%20Complete-green)

> 《深入理解计算机系统》（CSAPP）课程实验的个人实现与学习记录。

## 目录

- [项目简介](#项目简介)
- [目录结构](#目录结构)
- [环境要求](#环境要求)
- [快速开始](#快速开始)
- [实验进度](#实验进度)

## 项目简介

本仓库用于记录 CSAPP 课程配套实验的解题思路与代码实现，包含：

- **DataLab**：已完成
- **BombLab**：已完成
- **AttackLab**：未开始

代码仅供个人学习使用。

## 目录结构

```text
csapp-labs/
├── DataLab/                 # DataLab 实验
│   ├── datalab-handout/     # 实验代码与测试程序
│   │   ├── bits.c           # 待实现函数（主要修改文件）
│   │   ├── btest.c          # 自动评测源码
│   │   ├── driver.pl        # 驱动脚本
│   │   └── Makefile
│   └── datalab.pdf          # 实验说明
├── BombLab/                 # BombLab 实验
│   ├── bomb                 # 炸弹可执行文件
│   ├── bomb.c               # 主程序源码
│   ├── bomb.asm             # 反汇编
│   ├── solution.md          # 解题记录
│   ├── bomblab.pdf          # 实验说明
│   └── README               # 实验自带说明
├── AttackLab/               # AttackLab 实验
│   └── target1/             # 目标程序
│       ├── ctarget          # 代码注入攻击目标
│       ├── rtarget          # ROP 攻击目标
│       ├── hex2raw          # 字节串转输入工具
│       ├── farm.c           # gadget farm 源码
│       └── cookie.txt       # 个人 cookie
├── datalab.pdf              # 实验说明（根目录副本）
├── README.md
└── .gitignore
```

## 环境要求

- Ubuntu 24.04（WSL 或其他 Linux 发行版）
- GCC 与 GNU Make
- gdb、objdump（BombLab 调试用）

## 快速开始

### DataLab

```bash
cd DataLab/datalab-handout
make
./btest
```

### BombLab

```bash
cd BombLab
./bomb              # 交互式输入
./bomb solution.txt # 从答案文件逐行读取
```

### AttackLab

```bash
cd AttackLab/target1
./ctarget -q        # 自学版跳过服务器；具体参数见 README.txt
./rtarget -q
```

## 实验进度

| 实验 | 目录 | 状态 |
| --- | --- | --- |
| DataLab | `DataLab/datalab-handout/` | 已完成 |
| BombLab | `BombLab/` | 已完成 |
| AttackLab | `AttackLab/target1/` | 未开始 |
