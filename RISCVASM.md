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

## RISCV 汇编指令操作的对象
### 寄存器：
- 32个通用寄存器，x0 - x31( RV32I ) 
- Hart在执行算数逻辑运算时所进行的操作必须直接来自于寄存器。
### 内存：
- Hart可以执行寄存器和内存之间的数据读写操作
- 读写操作使用byte作为基本单位进行寻址
- RV32最多可以访问 1 << 32 个字节的内存空间

x0是readonly寄存器，[ x0 ] 恒等于 0  
RISC-V 汇编指令一共有6种格式：RISBUJ型  
指令长度：ILEN1 = 32bits ( RV32I )  
指令对齐：IALIGN = 32bits   
32个bit划分为不同的field  
funct3/7和opcode共同决定指令的类型
小端序排列  

指令格式:
- R-type( Register )
- I-type( Immediate )
- S-type( Store )
- B-type( Branch )
- U-type( Upper )
- J-type( Jump )