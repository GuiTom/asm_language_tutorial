## x86 汇编语言基础知识

### 1.汇编语言能够操作的寄存器
  
#### A.16 个通用寄存器(8位、16位、32位的 cpu 都没有 R8~R15寄存器)
#####  RAX RBX RCX RDX 
#####  RSI RDI RBP RSP
#####  R8 R9 R10 R11
#####  R12 R13 R14 R15

#### B. 1个 标志寄存器
##### RFlag 

#### C.6个段寄存器
##### CS (code Segment)
##### DS (data Segment)
##### SS (stack Segment)
##### ES (Extra Segment)
##### GS (Extra Segment)
##### SS (Extra Segment)

##### D. 5个控制寄存器 CR0 CR1 CR2 CR3 CR4 CR5
##### E. 8个调试寄存器 DR0~7
##### F. 4个系统地址寄存器 CDTR、IDTR、LDTR、TR
##### G. 其他寄存器 EIP、TSC
