---
title: 系统调用
draft: true
---

# 系统调用

到目前为止，如果我们不调用系统库的函数，我们写出来的绝大部分的程序都是**无状态的**。也就是说，无论我们调用多少次这个程序，程序的结果都永远相同（当然也有例外，大家不妨想想有怎样的程序，不调用外部函数的情况下，每次调用的输出不同）。事实上，如果想要程序变成有状态的，包括读取用户输入、读写文件、发送网络请求等等，都需要内核的配合。

但是，我们在用户态的程序不能直接通过`bl`来调用内核的函数。我们在[操作系统](4_Operating_system.md)中提到，AArch64有不同的异常级别。一般来说，用户态程序的异常级别是EL0，内核处于EL1。低异常级别的程序是不能调用高异常级别的函数的。

为了调用内核的函数，我们需要使用特殊的指令，切换异常等级。这就是`svc`（Supervisor Call）指令。其使用方法类似于：

```armasm
svc    #0x80
``` 

这个命令会向EL1生成一个异常，系统将根据后面跟着的数，这里就是`0x80`，来判断怎样处理这个异常。在macOS中，大部分的系统调用都是可以通过`0x80`这个数来调用。

操作系统内核提供的系统调用有非常多，比如说`read`、`write`等。这里的`0x80`只是告诉内核，我发起的异常是为了调用系统调用。那么具体是哪个系统调用，则需要使用系统调用号。

系统调用号我们可以在[xnu源码](https://github.com/apple-oss-distributions/xnu)的`bsd/kern/syscalls.master`文件中查看。例如：

```c
3	AUE_NULL	ALL	{ user_ssize_t read(int fd, user_addr_t cbuf, user_size_t nbyte); }
4	AUE_NULL	ALL	{ user_ssize_t write(int fd, user_addr_t cbuf, user_size_t nbyte); }
```

就代表：`read`系统调用的系统调用号是3，`write`是4。

也就是说，我们在使用`svc`进行系统调用的时候，通过某些途径让内核知道我们的系统调用号，就可以执行相应的系统调用了。

但是，通过什么途径能让内核知道我们想要的系统调用号呢？不仅如此，正如上面的代码片段所显示的，大部分系统调用也都有参数，我们不能使用`bl`，只能使用`svc`，那又如何传参获取返回值呢？

这些其实也是一种ABI，但这种ABI并没有稳定，也就是说并没有什么官方文档中规定了这种ABI。只是目前采用了这种ABI，之后会不会变并没有给出保证。

macOS的xnu内核规定，系统调用号传入`r16`寄存器（位于xnu源码的`osfmk/arm64/proc_reg.h`的`ARM64_SYSCALL_CODE_REG_NUM`宏）。而参数传递则和普通函数的类似，传入对应的`r0`到`r7`的寄存器即可。

因此，我们终于可以用C语言写一个Hello world了（源代码位于[codes/13-hello-world.s](https://github.com/Evian-Zhang/learn-assembly-on-Apple-Silicon-Mac/blob/master/codes/13-hello-world.s)）：

```armasm
    .text
    .globl  _main
    .p2align    2
_main:
    sub    sp, sp, #16
    stp    x29, x30, [sp]

    mov    w0, #0                       ; fd: STDOUT_FILENO
    adrp   x1, my_str@PAGE
    add    x1, x1, my_str@PAGEOFF       ; cbuf: "Hello world"
    mov    w2, #12                      ; nbyte: 12
    mov    w16, #4                      ; Syscall number: write
    svc    #0x80                        ; write(STDOUT_FILENO, "Hello world", 12);

    ldp    x29, x30, [sp]
    add    sp, sp, #16
    ret

    .data
my_str:
    .asciz    "Hello world"
```

我们刚才提到，系统调用的ABI并不稳定。并且，系统调用号事实上也没有保证是不变的。因此，我们如果像上面一样，写出的代码就不具有可移植性。事实上，libc会对绝大多数常用的系统调用做一个封装，我们也可以直接调用libc对应的函数。也就是说，上面的`mov   w16, #4`和`svc    #0x80`两行，可以换成`bl    _write`，其中`_write`是libc提供的函数。
