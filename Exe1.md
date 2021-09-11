# Chapter 3
1. 使用gcc -c命令生成hello.c，再使用readelf -h hello.o 查看elf信息：
```
  Magic：  7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  类别:                              ELF64
  数据:                              2 补码，小端序 (little endian)
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI 版本:                          0
  类型:                              REL (可重定位文件)
  系统架构:                          Advanced Micro Devices X86-64
  版本:                              0x1
  入口点地址：              0x0
  程序头起点：              0 (bytes into file)
  Start of section headers:          640 (bytes into file)
  标志：             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           64 (bytes)
  Number of section headers:         14
  Section header string table index: 13
  ```
使用readelf -SW hello.o 查看 Section Header Table:
```
节头：
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .text             PROGBITS        0000000000000000 000040 00001a 00  AX  0   0  1
  [ 2] .rela.text        RELA            0000000000000000 0001c0 000030 18   I 11   1  8
  [ 3] .data             PROGBITS        0000000000000000 00005a 000000 00  WA  0   0  1
  [ 4] .bss              NOBITS          0000000000000000 00005a 000000 00  WA  0   0  1
  [ 5] .rodata           PROGBITS        0000000000000000 00005a 00000c 00   A  0   0  1
  [ 6] .comment          PROGBITS        0000000000000000 000066 000013 01  MS  0   0  1
  [ 7] .note.GNU-stack   PROGBITS        0000000000000000 000079 000000 00      0   0  1
  [ 8] .note.gnu.property NOTE            0000000000000000 000080 000030 00   A  0   0  8
  [ 9] .eh_frame         PROGBITS        0000000000000000 0000b0 000038 00   A  0   0  8
  [10] .rela.eh_frame    RELA            0000000000000000 0001f0 000018 18   I 11   9  8
  [11] .symtab           SYMTAB          0000000000000000 0000e8 0000a8 18     12   4  8
  [12] .strtab           STRTAB          0000000000000000 000190 000029 00      0   0  1
  [13] .shstrtab         STRTAB          0000000000000000 000208 000074 00      0   0  1
```
使用objdump -S hello.o反汇编:
```
hello.o：     文件格式 elf64-x86-64


Disassembly of section .text:

0000000000000000 <main>:
#include <stdio.h>
int main( ) {
   0:   55                      push   %rbp
   1:   48 89 e5                mov    %rsp,%rbp
        printf("hello world\n");
   4:   48 8d 05 00 00 00 00    lea    0x0(%rip),%rax        # b <main+0xb>
   b:   48 89 c7                mov    %rax,%rdi
   e:   e8 00 00 00 00          call   13 <main+0x13>
        return 0;
  13:   b8 00 00 00 00          mov    $0x0,%eax
}
  18:   5d                      pop    %rbp
  19:   c3                      ret  
```
在完成链接后生成a.out再次使用readelf -SW 查看Section Header Table:
```
节头：
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .note.gnu.property NOTE            0000000000400270 000270 000040 00   A  0   0  8
  [ 2] .note.gnu.build-id NOTE            00000000004002b0 0002b0 000024 00   A  0   0  4
  [ 3] .note.ABI-tag     NOTE            00000000004002d4 0002d4 000020 00   A  0   0  4
  [ 4] .rela.plt         RELA            00000000004002f8 0002f8 000240 18  AI  0  20  8
  [ 5] .init             PROGBITS        0000000000401000 001000 00001b 00  AX  0   0  4
  [ 6] .plt              PROGBITS        0000000000401020 001020 0000c0 00  AX  0   0  8
  [ 7] .text             PROGBITS        00000000004010e0 0010e0 07fff0 00  AX  0   0 16
  [ 8] __libc_freeres_fn PROGBITS        00000000004810d0 0810d0 000ac0 00  AX  0   0 16
  [ 9] .fini             PROGBITS        0000000000481b90 081b90 00000d 00  AX  0   0  4
  [10] .rodata           PROGBITS        0000000000482000 082000 01c124 00   A  0   0 32
  [11] .stapsdt.base     PROGBITS        000000000049e124 09e124 000001 00   A  0   0  1
  [12] .eh_frame         PROGBITS        000000000049e128 09e128 00a96c 00   A  0   0  8
  [13] .gcc_except_table PROGBITS        00000000004a8a94 0a8a94 0000cf 00   A  0   0  1
  [14] .tdata            PROGBITS        00000000004aa908 0a9908 000020 00 WAT  0   0  8
  [15] .tbss             NOBITS          00000000004aa928 0a9928 000040 00 WAT  0   0  8
  [16] .init_array       INIT_ARRAY      00000000004aa928 0a9928 000008 08  WA  0   0  8
  [17] .fini_array       FINI_ARRAY      00000000004aa930 0a9930 000010 08  WA  0   0  8
  [18] .data.rel.ro      PROGBITS        00000000004aa940 0a9940 0035b4 00  WA  0   0 32
  [19] .got              PROGBITS        00000000004adef8 0acef8 0000f0 00  WA  0   0  8
  [20] .got.plt          PROGBITS        00000000004ae000 0ad000 0000d8 08  WA  0   0  8
  [21] .data             PROGBITS        00000000004ae0e0 0ad0e0 001a50 00  WA  0   0 32
  [22] __libc_subfreeres PROGBITS        00000000004afb30 0aeb30 000048 00  WA  0   0  8
  [23] __libc_IO_vtables PROGBITS        00000000004afb80 0aeb80 000768 00  WA  0   0 32
  [24] __libc_atexit     PROGBITS        00000000004b02e8 0af2e8 000008 00  WA  0   0  8
  [25] .bss              NOBITS          00000000004b0300 0af2f0 0018a0 00  WA  0   0 32
  [26] __libc_freeres_ptrs NOBITS          00000000004b1ba0 0af2f0 000020 00  WA  0   0  8
  [27] .comment          PROGBITS        0000000000000000 0af2f0 000012 01  MS  0   0  1
  [28] .note.stapsdt     NOTE            0000000000000000 0af304 0011c4 00      0   0  4
  [29] .debug_aranges    PROGBITS        0000000000000000 0b04c8 000030 00      0   0  1
  [30] .debug_info       PROGBITS        0000000000000000 0b04f8 00008c 00      0   0  1
  [31] .debug_abbrev     PROGBITS        0000000000000000 0b0584 000043 00      0   0  1
  [32] .debug_line       PROGBITS        0000000000000000 0b05c7 000052 00      0   0  1
  [33] .debug_str        PROGBITS        0000000000000000 0b0619 00007a 01  MS  0   0  1
  [34] .debug_line_str   PROGBITS        0000000000000000 0b0693 000026 01  MS  0   0  1
  [35] .symtab           SYMTAB          0000000000000000 0b06c0 00b280 18     36 732  8
  [36] .strtab           STRTAB          0000000000000000 0bb940 006921 00      0   0  1
  [37] .shstrtab         STRTAB          0000000000000000 0c2261 0001a7 00      0   0  1

```
可以看出：
可重定位的文件是不可执行的，因为入口地址是0。需要在链接的过程中重定位

使用objdump -t 命令查看符号表：
```
SYMBOL TABLE:
0000000000000000 l    df *ABS*  0000000000000000 hello.c
0000000000000000 l    d  .text  0000000000000000 .text
0000000000000000 l    d  .rodata        0000000000000000 .rodata
0000000000000000 l     O .bss   0000000000000004 static_var_uninit.1
0000000000000004 l     O .data  0000000000000004 static_var.0
0000000000000000 g     O .data  0000000000000004 global_int
0000000000000000 g     O .rodata        0000000000000004 global_const
0000000000000000 g     F .text  0000000000000025 main
0000000000000000         *UND*  0000000000000000 _GLOBAL_OFFSET_TABLE_
0000000000000000         *UND*  0000000000000000 puts
```
可以看出：
1. static_var_uninit.1 位于.bss段
2. static_var.0 和 global_int 位于.data段
3. global_const 和 "hello world" 位于.rodata段

使用objdump -s 命令也可以印证这一点:
```
Contents of section .text:
 0000 554889e5 4883ec10 c745fc44 44444448  UH..H....E.DDDDH
 0010 8d050000 00004889 c7e80000 0000b800  ......H.........
 0020 000000c9 c3                          .....           
Contents of section .data:
 0000 11111111 33333333                    ....3333        
Contents of section .rodata:
 0000 22222222 68656c6c 6f20776f 726c6400  """"hello world.
Contents of section .comment:
 0000 00474343 3a202847 4e552920 31312e31  .GCC: (GNU) 11.1
 0010 2e3000                               .0.             
Contents of section .note.gnu.property:
 0000 04000000 20000000 05000000 474e5500  .... .......GNU.
 0010 020001c0 04000000 00000000 00000000  ................
 0020 010001c0 04000000 01000000 00000000  ................
Contents of section .eh_frame:
 0000 14000000 00000000 017a5200 01781001  .........zR..x..
 0010 1b0c0708 90010000 1c000000 1c000000  ................
 0020 00000000 25000000 00410e10 8602430d  ....%....A....C.
 0030 06600c07 08000000                    .`......
```
