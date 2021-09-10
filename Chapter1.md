# 计算机的硬件组成
## CPU ( Central Processing Unit )
ALU: Arithmetic Logic Unit  
CU: Control Unit  
Register
### Von Neumamm Architecture ( Princeton Architecture )
指令和数据不加区别地存储在存储器中，经同一个总线传输，总线开销小，控制器逻辑简单，执行效率低
### Harvard Architecture
指令和数据分开存储，执行效率高，总线开销更大，控制逻辑更加复杂
# 程序的存储和执行
Fetch Decode Execute
# RISCV ISA ( Instruction Set Architecture )
是底层硬件电路面向上层软件程序提供的接口规范，ISA定义了基本数据类型、寄存器、指令、寻址模式、异常或中断的处理 ( form Microarchitecture to OS )。最早由IBM提出。  
ISA的宽度指CPU中通用寄存器的宽度，决定了寻址范围的大小。  
常用ISA:   
X86 ---- Intel  
SPARC ---- SUN  
Power ---- IBM  
ARM ---- ARM  
MIPS ---- MIPS tech  
RISC-V  