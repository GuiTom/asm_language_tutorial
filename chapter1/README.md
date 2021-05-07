### 我们知道，C 语言 编译到执行的流程是 1.编译c 文件为目标文件,一般扩展名为.o 或.obj(c 语法分解为与汇编语言一一对应的机器指令)->2.链接多个目标文件(如果是单个c文件的话省略这一步)和调用的系统库函数(没调用的话则省略)，生成可执行文件
#### 这里先从我们比较熟悉的c 语言入手，看看编译器是怎样用汇编语言实现c语言的功能的。
```c
//file 1.c
int sum(int a,int b,int c){
    return a + b + c;
}
int main(void){
    int result = sum(a,b,c);
    return result;
}
```
#### 上面的文件为 1.c,我们在 macos 上执行 gcc -S 1.c 会在同目录下面生成一个名为1.s 的汇编文件(linux 环境下编译成的汇编文件略有不同,可能是 gcc 版本的问题,未证实)
```asm
    # 以下是 1.c 对应的汇编文件
    # 以下的以.开头的，不以冒号结尾的标号都可以省略，不会影响功能（.globl main 这行除外，否则会找不到入口函数）
	.section	__TEXT,__text,regular,pure_instructions
	.build_version macos, 10, 15	sdk_version 10, 15, 6
	.globl	_sum                    ## -- Begin function sum
	.p2align	4, 0x90
_sum:                                   ## @sum
	.cfi_startproc
## %bb.0:
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset %rbp, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register %rbp
	movl	%edi, -4(%rbp)
	movl	%esi, -8(%rbp)
	movl	%edx, -12(%rbp)
	movl	-4(%rbp), %eax
	addl	-8(%rbp), %eax
	addl	-12(%rbp), %eax
	popq	%rbp
	retq
	.cfi_endproc
                                        ## -- End function
	.globl	_main                   ## -- Begin function main
	.p2align	4, 0x90
_main:                                  ## @main
	.cfi_startproc
## %bb.0:
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset %rbp, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register %rbp
	subq	$16, %rsp
	movl	$0, -4(%rbp)
	movl	$1, -8(%rbp)
	movl	$2, -12(%rbp)
	movl	$5, -16(%rbp)
	movl	-8(%rbp), %edi
	movl	-12(%rbp), %esi
	movl	-16(%rbp), %edx
	callq	_sum
	addq	$16, %rsp
	popq	%rbp
	retq
	.cfi_endproc
                                        ## -- End function
.subsections_via_symbols
```
#### 我们可以看到,汇编程序终生成了两个冒号表记的函数，一个是 sum 函数，一个是 main 函数.
#### 接下来更进一将对汇编代码编译成可执行文件 gcc -o 1 1.s,输入./1 回车运行，发现什么也没打印，然后我们输入 echo $? ,屏幕上输入了6，这便是 main 函数的返回值，验证了汇编语言的跟 c 语言是一致的，逆向的过程，就是要能通过汇编语言，还原出对应的 C 语言.第二章开始我们学习一些汇编语言的基础知识，并进一步解释本例的汇编是如何实现三个数想加的功能的。


