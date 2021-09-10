# Introduction of RISCV ASM
[ label: ] [ oepration ] [ comment ]

operation 有以下几种类型：
- 指令( instruction ) : 直接生成对应二进制指令
- 伪指令( pseudo-instruction )：一条伪指令可能指示汇编器产生多条实际的指令
- 指示/伪操作( derective ): 以.开头，类似指令控制汇编器控制代码的产生，不对应具体指令
- 宏( .macro/.endm )
```asm
.macro do_nothing
  nop
  nop
.endm

  .text
  .global _start

_start:
  li x6, 5
  li x7, 4
  add x5, x6, x7
  do_nothing

stop:
  j stop
  .end

mov

```