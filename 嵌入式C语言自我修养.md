<h4 id="d303267a">问题：</h4>
<h5 id="44ab7fe4">内存泄漏与防范</h5>
**<font style="color:#d1a300;">什么是内存泄露？代码举例说明？如何预防内存泄露？如何检测内存泄露（代码示例）？广义上的内存泄露是什么，如何预防？常见的内存错误有哪些？如何调试？</font>**

<h5 id="ffbda940">**GNU C拓展**</h5>
**<font style="color:#d1a300;">常见的GNU（G-N-U）C拓展语法有哪些？结构体指定初始化是什么？有哪些应用场景？typeof是什么？有哪些应用场景？contaniner of宏是什么？有什么哪些应用场景？</font>**

**<font style="color:#d1a300;">变长数组是什么？有哪些应用场景？为什么不使用指针代替？</font>**

**<font style="color:#d1a300;">__attribute__属性有哪些？</font>**

**<font style="color:#d1a300;">aligned属性有什么用？为什么要用aligned？packed?section?可变参数?weak？oninline和always_inline？什么是内联函数？linux内核中的likely和unlikely？</font>**

<h5 id="7e788260">**C语言面向对象编程思想**</h5>
**<font style="color:#58a401;">什么是代码复用？什么是分层？C语言如何模拟类？C语言如何模拟继承？linux内核链表如何体现面向对象的特性的？C语言如何实现多态的？</font>**

<h5 id="af303e94">**C语言模块化编程思想**</h5>
**<font style="color:#58a401;">不同模块如何链接成一个文件？面向对象编程和模块化编程有什么区别？头文件有什么用？头文件重复包含是什么？变量声明和定义有什么区别? extern变量怎么用？goto关键字有什么用？模块设计原则是什么?模块直接耦合的方式有哪些？模块间如何进行通信？</font>**

<h4 id="40185fb0">思考：</h4>
<h5 id="5a34ad07">**思考：C++编译的时候可以使用GNU C的规则吗？如noinline或者always_inline？**</h5>
+ C++ 编译时可以使用 GNU C 的规则（如 `noinline` 和 `always_inline`），因为这些是 GCC 提供的扩展特性。
+ 如果代码需要跨平台或跨编译器，建议使用条件编译或避免依赖 GNU 扩展特性。
+ 性能关键代码中，可以合理使用 `always_inline` 和 `noinline` 来优化或调试代码。

<h1 id="9f065cce">ARM体系结构与汇编语言</h1>
<h4 id="0b4a806d">ARM体系结构</h4>
⭐

关联知识点：指令集

计算机的指令集一般可分为4种：复杂指令集(CISC)、精简指令集(RISC) 、显式并行指令集 (EPIC)和超长 指 令 字 指 令 集(VLIW)。嵌入式用的是RISC指令集，RISC指令集相对于CISC指令集，主要有以下特点

●Load/Store架构，CPU不能直接处理内存中的数据，要先将内存中的数据Load（加载）到寄存器中才能操作，然后将处理结果Store(存储)到内存中。

●固定的指令长度，单周期指令。

●倾向于使用更多的寄存器来存储数据，而不是使用内存中的堆栈，效率更高。ARM指令集虽然属于RISC，但是和RISC相比，有一些差异如下：

●ARM有桶型移位寄存器，单周期内可以完成数据的各种移位操作。

●并不是所有的ARM指令都是单周期的。

●ARM有16位的Thumb指令集，是32位ARM指令集的压缩形式，提

高了代码密度。

●条件执行：通过指令组合，减少了分支指令数目，提高了代码

密度。

●增加了DSP、SIMD/NEON等指令。

⭐

关联知识点：用户态、内核态、中断

ARM处理器有多种工作模式，应用程序正常运行时，ARM处理器工作在用户模式，当程序运行出错或有中断发生时，ARM处理器就会切换到对应的特权工作模式。用户模式运行不了特权指令，需要切换到特权模式下才能运行。在ARM处理器中，除了用户模式是普通模式，剩下的几种工作模式都属于特权模式。

在ARM处理器内部，除了基本的算术运算单元、逻辑运算单元、浮点运算单元和控制单元，还有一系列寄存器，包括各种通用寄存器、状态寄存器、控制寄存器，用来控制处理器的运行，保存程序运行时

的各种状态和临时结果。

ARM处理器中的寄存器可分为通用寄存器和专用寄存器两种。

寄存器R0～R12属于通用寄存器，除了FIQ工作模式，在其他工作模式下这些寄存器都是共用、共享的：

1. R0～R3通常用来传递函数参数
2. R4～R11用来保存程序运算的中间结果或函数的局部变量等，R12常用来作为函数调用过程中的临时寄存器。

ARM处理器有多种工作模式，除了这些在各个模式下通用的寄存器，还有一些寄存器在各自的工作模式下是独立存在的，如R13、R14、R15、CPSP、SPSR寄存器，在每个工作模式下都有自己单独的寄存器。

1. R13寄存器又称为堆栈指针寄存器，用来维护和管理函数调用过程中的栈帧变化，R13总是指向当前正在运行的函数的栈帧，一般不能再用作其他用途。
2. R14寄存器又称为链接寄存器，在函数调用过程中主要用来保存上一级函数调用者的返回地址。
3. 寄存器R15又称为程序计数器(PC)，保存的地址中取的，每取一次指令，PC寄存器的地址值自动增加。CPU一条一条不停地取指令，程序也就源源不断地一直运行下去。在ARM三级流水线中，PC指针的值等于当前正在运行的指令地址+8，后续的32位处理器虽然流水线的级数不断增加，但为了简化编程，PC指针的值继续延续了这种计算方式。
4. 当前处理器状态寄存器（Current Processor State Register CPSR）主要用来表征当前处理器的运行状态。除了各种状态位、标志位，CPSR寄存器里也有一些控制位，用来切换处理器的工作模式和中断使能控制。

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443196-f1c8c17c-9023-4081-961d-7787a1ba0c5d.png)

在每种工作模式下，都有一个单独的程序状态保存寄存器（Saved Processor State Register，SPSR）。当ARM处理器切换工作模式或发生异常时，SPSR用来保存当前工作模式下的处理器现场，即将CPSR寄存器的值保存到当前工作模式下的SPSR寄存器。当ARM处理器从异常返回时，就可以从SPSR寄存器中恢复原先的处理器状态，切换到原来的工作模式继续运行。

在ARM所有的工作模式中，有一种工作模式比较特殊，即FIQ模式。为了快速响应中断，减少中断现场保护带来的时间开销，在FIQ工作模式下，ARM处理器有自己独享的R8～R12寄存器。

<h4 id="739693b7">ARM汇编指令</h4>
一个完整的ARM指令通常由操作码+操作数组成，指令的编码格式如下。

```cpp
<opcode>{<cond>{s} <Rd>,<Rn>{,<operand2>}}
```

● 使用<>标起来的是必选项,使用{}标起来的是可选项。

● <opcode>是二进制机器指令的操作码助记符，如MOV、ADD这些

汇编指令都是操作码的指令助记符。

● cond：执行条件，ARM为减少分支跳转指令个数，允许类似BEQ、BNE等形式的组合指令。

● S：是否影响CPSR寄存器中的标志位，如SUBS指令会影响CPSR寄存器中的N、Z、C、V标志位，而SUB指令不会。

● Rd：目标寄存器。

● Rn：第一个操作数的寄存器。

● operand2：第二个可选操作数，灵活使用第二个操作数可以提

高代码效率。

<h5 id="7d7c4b8f">存储访问指令</h5>
ARM指令集属于RISC指令集，RISC处理器采用典型的加载/存储体系结构，CPU无法对内存里的数据直接操作，只能通过Load/Store指令来实现：当需要对内存中的数据进行操作时，要首先将这个数据从内存加载到寄存器，然后在寄存器中对数据进行处理，最后将结果重新存储到内存中。

ARM处理器属于冯·诺依曼架构，程序和数据都存储在同一存储器上，内存空间和I/O空间统一编址，ARM处理器对程序指令、数据、I/O空间中外设寄存器的访问都要通过Load/Store指令来完成。

```cpp
LDR R1,[RO]; 将R中的值作为地址，将该地址上的数据保存到R1
STR R1,[RO];  将R中的值作为地址，将R1中的值存储到这个内存地址;每次读写一字节，LDR/STR默认每次读写4字节
    LDRB/STRB;  批量加载/存储指令，在一组寄存器和一片内存之间传输数据
SWPR1,R1,[R0];  将R1与R中地址指向的内存单元中的数据进行交换
SWPR1,R2,[R0];  将[R0]存储到R1，将R2写入[R0]这个内存存储单元LDM/STM
```

LDR/STR、LDM/STM两对指令经常使用。

LDR/STR指令是ARM汇编程序中使用频率最高的一对指令。

LDM/STM指令常用来加载或存储一组寄存器到一片连续的内存，通过和堆栈格式符组合使用，LDM/STM指令还可以用来模拟堆栈操作。

将一组寄存器入栈，或者从栈中弹出一组寄存器。

```cpp
LDMFD SP!,{R0-R2,R14}; 将内存栈中的数据依次弹出到R14，R2，R1，RO
STMFD SP!{RO-R2,R14}; 将R，R1，R2，R14依次压入内存栈
```

ARM还专门提供了PUSH和POP指令来执行栈元素的入栈和出栈操作。

```cpp
PUSH {R0-R2,R14} ；将 R0、R1、R2、R14依次压入栈
    POP {R0-R2,R14}   ；将栈中的数据依次弹出到R14、R2、R1、R0
```

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443232-a2e27edc-8db7-4e28-943a-11620df67fb7.png)

在一个堆栈内存结构中，如果堆栈指针SP总是指向栈顶元素，那么这个栈就是满栈；如果堆栈指针SP指向的是栈顶元素的下一个空闲的存储单元，那么这个栈就是空栈。

每入栈一个元素，栈指针SP都会往栈增长的方向移动一个存储单元。如果栈指针SP从高地址往低地址移动，那么这个栈就是递减栈；如果栈指针SP从低地址往高地址移动，那么这个栈就是递增栈。

<h5 id="7cbb7c6f">数据传送指令</h5>
LDR/STR指令用来在寄存器和内存之间输送数据。想要在寄存器之间传送数据，则可以使用MOV指令。

```cpp
MOV {cond} {s} Rd, operand2
    MVN {cond} {S} Rd, operand2
```

如果想要在寄存器之间传送数据，则可以使用MOV指令。MVN指令用来将操作数operand2按位取反后传送到目标寄存器Rd。

```cpp
MOV R1，#1   ;将立即数1传送到寄存器R1中
    MOV R1, RO   ;将R寄存器中的值传送到R1寄存器中
MOV PC, LR   ;子程序返回
MVN RO，#xFF ;将立即数 0xFF 取反后赋值给 R
MVN RO, R1   ;将R1寄存器的值取反后赋值给R
```

<h5 id="ea0a7a48">算术逻辑运算指令</h5>
算术运算指令包括基本的加、减、乘、除，逻辑运算指令包括与、或、非、异或、清除等

```cpp
ADD {cond} {S} Rd, Rn, operand2 ;加法
ADC {cond} {S} Rd, Rn, operand2 ;带进位加法
SUB {cond} {S} Rd, Rn, operand2 ;减法
AND {cond} {S} Rd, Rn, operand2 ;逻辑与运算
ORR {cond} {S} Rd, Rn, operand2 ;逻辑或运算
EOR {cond} {S} Rd, Rn, operand2 ;异或运算
BIC {cond} {S} Rd, Rn, operand2 ;位清除指令
```

算术逻辑运算指令的基本使用方法及说明如下

```cpp
ADD R2，R1，#1 ; R2=R1+1
    ADC R1，R1，#1 ; R1=R1+1+C(其中C为CPSR寄存器中进位)
    SUB R1, R1, R2 ; R1=R1-R2 
    SBC R1,R1,R2 ;R1=R1-R2-C
    AND RO,RO,#3 ; 保留 R的 bit0和 1，其余位清除
    ORR RO,RO,#3 ; 置位 R0的 bit0 和 bit1
EOR RO,RO,#3 ; 反转 R0中的 bit 和 bit1
    BIC RO,RO,#3 ;  清除 R0中的 bit0和 bit1
```

操作数：operand2详解

.......

<h4 id="7e602460">ARM寻址方式</h4>
不同的ARM指令又有不同的寻址方式，比较常见的寻址方式有寄存器寻址、立即寻址、寄存器偏移寻址、寄存器间接寻址、基址寻址、多寄存器寻址、相对寻址等.

<h5 id="e56c99ce">寄存器寻址</h5>
寄存器寻址比较简单，操作数保存在寄存器中，通过寄存器名就可以直接对寄存器中的数据进行读写.

```cpp
MOV R1, R2 ;将寄存器R2中的值传送到R1
ADD R1，R2，R3 ;运行减法运算R2-R3，并将结果保存到R1中
```

<h5 id="835a4c76">立即数寻址</h5>
```cpp
ADD R1，R1，#1 ;将R1寄存器中的值加1，并将结果保存到R1中
ADDR1，R1，#16，20; R1=R1+立即数16循环右移20位
    MOV R1，#xFF ;将十六进制常数0xFF写到R1寄存器中
    MOV R1，#12 ; 将十进制常数12放到R1寄存器中
```

<h5 id="37f0bd84">寄存器偏移寻址</h5>
<h5 id="05c60d27">寄存器间接寻址</h5>
寄存器间接寻址主要用来在内存和寄存器之间传输数据。寄存器中保存的是数据在内存中的存储地址，通过这个地址就可以在寄存器和内存之间传输数据。C语言中的指针操作，在汇编层次其实就是使用寄存器间接寻址实现的。

```cpp
LDRR1,[R2]; 将R2中的值作为地址，取该内存地址上的数据，保存到R1
STRR1,[R2]; 将R2中的值作为地址，将R1寄存器的值写入该内存地址
```

<h5 id="a39803d3">基址寻址</h5>
基址寻址其实也属于寄存器间接寻址。两者的不同之处在于,基址寻址将寄存器中的地址与一个偏移量相加，生成一个新地址，然后基于这个新地址去访问内存.

```cpp
LDRR1，[FP，#2]     ;将FP中的值加2作为新地址，取该地址上的值保存到R1
LDR R1，[FP，#2]!   ; FP=FP+2，然后将FP指定的内存单元数据保存到R1中
    LDRR1，[FP，R0]     ;将FP+R0作为新地址，取该地址上的值保存到 R1
    LDR R1，[FP,RO,LSL#2];将FP+R0<<2作为新地址，读取该内存地址上的值保存到 R1
    LDR R1，[FP]，#2   ;将FP中的值作为地址，读取该地址上的值保存到R1，然后 FP 中的值加 2
    STRR1，[FP，#-2]   ;将FP中的值减 2，作为新地址，将 R1中的值写入该地址
STR R1，[FP]，#-2] ;将FP中的值作为地址，将R1中的值写入此地址，然后FP中的值减2
```

基址寻址一般用在查表、数组访问、函数的栈帧管理等场合。根据偏移量的正负，基址寻址又可以分为向前索引寻址和向后索引寻址.

<h5 id="6181dbb1">多寄存器寻址</h5>
STM/LDM指令就属于多寄存器寻址，一次可以传输多个寄存器的值。

```cpp
LDMIA SP!,{R0-R2,R14};将内存栈中的数据依次弹出到 R14、R2、R1、RO
STMDB SP!,{RO-R2,R14};将RO、R1、R2、R14 依次压入栈
LDMFD SP!,{R0-R2,R14};将内存栈中的数据依次弹出到 R14、R2、R1、R0
STMFDSP!,{RO-R2,R14};将R、R1、R2、R14 依次压入栈
```

在多寄存器寻址中，用大括号{}括起来的是寄存器列表，寄存器之间用逗号隔开，如果是连续的寄存器，还可以使用连接符连接，如R0-R3，就表示R0、R1、R2、R3这4个寄存器。LDM/STM指令一般和IA、IB、DA、DB组合使用，分别表示Increase After、Increase Before、Decrease After、Decrease Before。LDM/STM指令也可以和FD、ED、FA、EA组合使用，用于堆栈操作。

<h5 id="d13304f4">相对寻址</h5>
相对寻址属于基址寻址，只不过是基址寻址的一种特殊情况。

以PC指针作为基地址进行寻址，以指令中的地址差作为偏移，两者相加后得到的就是一个新地址，然后可以对这个地址进行读写操作。

ARM中的B、BL、ADR指令都是采用相对寻址的。

很多与位置无关的代码，如动态链接共享库，其在汇编代码层次的实现其实也是采用相对寻址的。程序中使用相对寻址访问的好处是不需要重定位，将代码加载到内存中的任何地址都可以直接运行。

<h4 id="08496b2c">ARM伪指令</h4>
ARM伪指令不是ARM指令集中定义的标准指令，而是为了编程方便，编译器厂商自定义的一些辅助指令。在程序编译时，这些伪指令会被翻译为一条或多条ARM标准指令。常见的ARM伪指令主要有4个：ADR、ADRL、LDR、NOP。

<h5 id="8dbead99">LDR伪指令</h5>
LDR伪指令的主要用途是将一个32位的内存地址保存到寄存器中 。

RISC指令的特点是单周期指令，指令的长度固定。在一个32位的系统中，一条指令通常是32位的，指令中包括操作码和操作数。

指令中的操作码和操作数共享32位的存储空间：一般前面的操作码要占据几个比特位，剩下来的留给操作数的编码空间就小于32位。当编译器遇到MOV R0，＃0x30008000这条指令时，后面的操作数是32位，编译器就无法对这条指令进行编码了。为了解决这个难题，编译器提供了一个LDR伪指令来完成上面的功能。

LDR不是普通的ARM加载指令，而是一个伪指令。为了与ARM指令集中的加载指令LDR区别开来，LDR伪指令中的操作数前一般会有一个等于号=，用来表示该指令是个伪指令。通过LDR伪指令，编译器就解决了向一个寄存器传送32位的立即数时指令无法编码的难题。

```cpp
LDR R，=0x30008000;  有=号的就是伪指令，将立即数x30008000送到R0
LDR RO， =LOOP ；将标号LOOP表示的地址送到R0
LDR RO，[R1] ；R1中的值作为地址，将该地址上的值送到R0
LDR RO，LOOP ；将标号LOOP表示的内存地址上的数据送到R0
```

<h5 id="c8a651bd">ADR伪指令</h5>
```cpp
START
ADR R0, LOOP     ; 将标号 LOOP 对应的地址加载到寄存器 R0 中
B END            ; 跳转到 END 标签，结束程序
LOOP
NOP              ; 一个空操作，作为示例使用
B LOOP           ; 无限循环
```

**ADR R0, LOOP**：这一行使用了 `ADR` 伪指令，它将标号 `LOOP` 的地址加载到寄存器 `R0` 中。`ADR` 指令会计算当前指令地址与标号 `LOOP` 之间的偏移量，然后通过相对寻址将 `LOOP` 的地址加载到 `R0` 中。ADR伪指令的功能与LDR伪指令类似，将基于PC相对偏移的地址值读取到寄存器中。ADR为小范围的地址读取伪指令，底层使用相对寻址来实现，因此可以做到代码与位置无关。

编译器在编译ADR伪指令时，会首先计算出当前正在执行的ADR伪指令地址与标号LOOP之间的地址偏移OFFSET，然后使用ARM指令集中的一条标准指令代替。

<h4 id="ad9c46b4">ARM汇编程序设计</h4>
<h5 id="97f4e266">ARM汇编程序格式</h5>
ARM汇编程序是以段（section）为单位进行组织的。在一个汇编文件中，可以有不同的section，分为代码段、数据段等，各个段之间相互独立，一个ARM汇编程序至少要有一个代码段。可以使用AREA伪操作来标识一个段的起始、段名和段的读写属性。

```cpp
AREA COPY, CODE, READONLY   ; 当前段属性为代码段，只读，段名为 COPY
ENTRY
START
LDR R0, =SRC            ; 将源地址 SRC 加载到寄存器 R0 中
LDR R1, =DST            ; 将目标地址 DST 加载到寄存器 R1 中
MOV R2, #10             ; 将值 10 加载到寄存器 R2 中
    LOOP
    LDR R3, [R0], #4        ; 从 R0 地址加载一个字到 R3 中，并将 R0 增加 4
    STR R3, [R1], #4        ; 将 R3 中的值存储到 R1 指向的地址，并将 R1 增加 4
    SUBS R2, R2, #1         ; 将 R2 减 1，并设置条件标志
BNE LOOP                ; 如果 R2 不为 0，则跳转回 LOOP
AREA COPYDATA, DATA, READWRITE ; 数据段，读写权限，段名为 COPYDATA
SRC DCD 1,2,3,4,5,6,7,8,9,0  ; 源数据数组
DST DCD 0,0,0,0,0,0,0,0,0,0  ; 目标数据数组，用于存放复制后的数据
END
```

在汇编程序中，使用分号；来注释代码

<h5 id="eb089208">符号与标号</h5>
使用符号来标识一个地址、变量或数字常量。当用符号来标识一个地址时，这个符号通常又被称为标号。符号的命名规则和C语言的标识符命名规则一样：由字母、数字和下画线组成，符号的开头不能使用数字，但标号除外。标号比较任性，标号的开头不仅可以是数字，甚至整个标号可以是一个纯数字。

**局部标号**

局部标号用于标记程序中的特定位置，以便在该位置附近进行跳转或引用。与全局标号不同，局部标号的作用域通常仅限于当前段或当前范围内，不会影响到其他代码段。局部标号常常使用数字（如 `0`, `1`, `2` 等）来命名，并通过特定的格式来引用。

**作用域有限:**局部标号的作用域只在当前段内有效。这意味着同一个局部标号可以在不同的段中重复使用，而不会产生冲突。

**命名方式简单:**局部标号通常使用数字命名，如 `0`, `1`, `2` 等，这使得它们在短距离跳转和循环结构中非常方便。

**引用格式**：引用局部标号时，使用 `%` 符号加上 `B`（向后搜索）或 `F`（向前搜索）来确定跳转方向。

如果未指定 `F` 或 `B`，编译器会默认先向后搜索，如果找不到，再向前搜索。

```cpp
MOV R0, #10       ; 将值 10 存入寄存器 R0 中
0   SUBS R0, R0, #1   ; 将 R0 减 1，并设置条件标志
    BNE %B0           ; 如果 R0 不为零，则跳转回局部标号 0
```

<h5 id="2826c859">伪操作</h5>
伪操作（也称为伪指令）是在汇编语言中使用的一类特殊指令，用来辅助编写和组织汇编代码。与真正的机器指令不同，伪操作并不会直接转换为机器码，而是为汇编器提供了指示，用于控制汇编过程、数据定义、段定义以及程序结构管理等功能。伪操作主要用于提高代码的可读性和结构化，让程序员更方便地编写和管理汇编程序。

**符号定义：**使用伪操作定义变量、常量或符号。例如，可以使用 `EQU` 指令将一个符号绑定到一个数值或表达式上。

**数据定义**：用于定义数据段中的变量和常量。例如，`DCD`、`DCB`、`SPACE` 等伪操作用来在内存中分配特定的数据空间。

**程序结构控制**：用于控制汇编程序的流程和组织。例如，`AREA` 用于定义段（section），`ENTRY` 用于指定程序的入口点，`EXPORT` 和 `IMPORT` 用于声明全局符号和导入其他模块中的符号。

**模块化编程**：伪操作可以用于定义汇编子程序，并通过伪操作声明全局符号，以便在主程序或其他程序中调用这些子程序。

以下是一些常用的伪操作及其使用方法：

**AREA**：定义一个段或区域。

```cpp
AREA MyCode, CODE, READONLY
```

**DCD**：定义一个32位常量。

```cpp
DCD 1, 2, 3, 4
```

**DCB**：定义一个字节常量。

```cpp
DCB 'A', 'B', 'C'
```

**EQU**：定义一个符号常量。

```cpp
MyValue EQU 10
```

**EXPORT**：将符号声明为全局符号，允许其他模块访问。

```cpp
EXPORT MyFunction
```

**IMPORT**：导入外部模块中的符号。

```cpp
IMPORT ExternalFunction
```

**ENTRY**：指定程序的入口点。

```cpp
ENTRY
```

**SPACE：**在内存中分配一定数量的字节。

```cpp
SPACE 16 ;分配16字节
```

伪操作的作用

伪操作的主要作用是帮助汇编器组织和处理汇编代码，而不是转换成机器码。它们在汇编代码的预处理中起到重要作用，使代码更加灵活和易于维护。例如，使用 `EXPORT` 和 `IMPORT` 伪操作，可以轻松实现模块化编程，使得不同的汇编程序模块可以相互调用。

<h4 id="5c4718f8">C语言和汇编语言混合编程</h4>
<h5 id="b44ecbb7">ATPCS规则</h5>
ATPCS的全称是ARM-Thumb Procedure Call Standard，核心内容就是定义ARM子程序调用的基本规则及堆栈的使用约定等。

如ATPCS规定了ARM程序要使用满递减堆栈，入栈/出栈操作要使用STMFD/LDMFD指令，只要所有的程序都遵循这个约定，ARM程序的格式也就统一了，编写的ARM程序也就可以在各种各样的ARM处理器上运行。

子程序间要通过寄存器R0～R3（可记作a0～a3）传递参数，当参数个数大于4时，剩余的参数使用堆栈来传递。

●子程序通过R0～R1返回结果。

●子程序中使用R4～R11（可记作v1～v8）来保存局部变量。

●R12作为调用过程中的临时寄存器，一般用来保存函数的栈帧

基址，记作FP。

●R13作为堆栈指针寄存器，一般记作SP。

●R14作为链接寄存器，用来保存函数调用者的返回地址，记作LR。

●R15作为程序计数器，总是指向当前正在运行的指令，记作PC。

在ARM平台下，无论是C程序，还是汇编程序，只要大家遵守ARM子程序之间的参数传递和调用规则，就可以很方便地在一个C程序中调用汇编子程序，或者在一个汇编程序中调用C程序。

```cpp
AREA    SumFunc, CODE, READONLY
EXPORT  sum           ; 声明sum为全局函数，使其可以被C代码调用
sum     PROC
;输入：R0 和 R1 为两个加数
;输出：R0 为和
ADD     R0, R0, R1    ; 执行加法操作，将结果存储到R0中
BX      LR            ; 返回调用者
ENDP
END

#include <stdio.h>
extern int sum(int a, int b);  // 声明汇编函数

int main() {
    int result = sum(5, 7);    // 调用汇编函数sum
    printf("The result is: %d\n", result);  // 打印结果
    return 0;
}
```

**无条件跳转:**`BX`指令将控制权转移到指定的地址(寄存器中的值)。

<h5 id="c0d02cf2">在C程序中内嵌汇编代码</h5>
为了能在C程序中内嵌汇编代码，ARM编译器在ANSI C标准的基础上扩展了一个关键字__asm。通过这个关键字,可以在C程序中内嵌ARM汇编代码。

```cpp
int src[10] = {1,2,3,4,5,6,7,8,9};
int dst[10] = {0};
int data_copy_c(void){
    for(int i = 0; i < 10; i++)
        dst[i] = src[i];
    return 0;
}
int data_copy_asm(void){
__asm
{
LDR R0, =src
LDR R1, =dst
MOV R2, #10
LOOP:
LDR R3, [R0], #4
STR R3, [R1], #4
SUBS R2, R2, #1
BNE LOOP
}
}
```

<h5 id="dead88c3">在汇编程序中调用C程序</h5>
在汇编程序中同样也可以调用C程序。在调用的时候，我们要注意根据ATPCS规则来完成参数的传递，并配置好C程序传递参数和保存局部变量所依赖的堆栈环境，然后使用BL指令直接跳转即可。

<h4 id="96481fc6">GNU ARM汇编语言</h4>
........

<h1 id="d855463b">内存堆栈管理</h1>
👋

关联知识点：

程序地址空间：[https://kdocs.cn/l/cjeGfIOJleoy?linkname=ZoO9Iu52pZ](https://kdocs.cn/l/cjeGfIOJleoy?linkname=ZoO9Iu52pZ)

malloc原理：[https://kdocs.cn/l/cjeGfIOJleoy?linkname=SxljDaCa3X](https://kdocs.cn/l/cjeGfIOJleoy?linkname=SxljDaCa3X)

垃圾回收：[https://kdocs.cn/l/cjeGfIOJleoy?linkname=sTJaIsjKQl](https://kdocs.cn/l/cjeGfIOJleoy?linkname=sTJaIsjKQl)

<h4 id="44ab7fe4-1">内存泄漏与防范</h4>
**<font style="color:#d1a300;">什么是内存泄露？代码举例说明？如何预防内存泄露？如何检测内存泄露（代码示例）？广义上的内存泄露是什么，如何预防？</font>**

**<font style="color:#d1a300;">常见的内存错误有哪些？如何调试？</font>**

内存泄漏

<u>如果使用malloc()申请的内存在使用结束后没有及时被释放，则C标准库中的内存分配器ptmalloc和内核中的内存管理子系统都失去了对这块内存的追踪和管理。</u>

<u>这里的使用结束指的是程序不需要访问这段内存，长期运行的程序可能会因为内存泄露导致程序崩溃，但是程序结束后操作系统会回收该进程的所有资源。</u>  
<u>操作系统为每个进程分配独立的虚拟地址空间，进程结束时，（内存、文件描述符、网络连接等）。</u>

```cpp
char *p;
p=(char *)malloc(32);
strcpy(p,“hello");
没有free p
```

在函数退出之前，如果我们没有使用free()函数及时 将 这 块 内 存 归 还 给 内 存 分 配 器 ptmalloc或内存管理子系统，ptmalloc和内存管理子系统就失去了对这块内存的控制权，它们可能认为用户还在使用这片内存。等下次去申请内存时，内存分配器和内存管理子系统都没有这块内存的信息，所以不可能把这块内存再分配给用户使用。

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443211-39694f20-3a2c-4d5b-96fe-0066d866ccb0.png)

 图中有大小为548 Byte和504 Byte的两个内存块，一开始这两个内存块是在空闲链表中的，当用户使用malloc()申请内存时，内存分配器ptmalloc将这两个内存块节点从空闲链表中摘除，并把内存块的地址返给用户使用。如果用户使用后忘了归还，那么空闲链表中就没有这两个内存块的信息，这两块内存也就无法继续使用了，在内存中就产生了两个漏洞,即发生内存泄漏。

<h5 id="baf6e9d9">预防内存泄漏</h5>
<u>预防内存泄漏：内存申请后及时地释放，两者要配对使用，内存释放后要及时将指针设置为NULL，使用内存指针前要进行非空判断。</u>

<h5 id="42aa7655">内存泄漏检测：MTrace</h5>
MTrace，Valgrind，Dmalloc，purify，KCachegrind，MallocDebug

```cpp
#include <mcheck.h>
void mtrace(void);
void muntrace(void);
```

如果想检测一段代码是否有内存泄漏，则可以把mtrace和muntrace两个函数添加到要检测的程序代码中。

```cpp
...
    #include <mcheck.h>
    int main (void){
        mtrace();//开启跟踪
        char *p,*q;
        p =(char *)malloc(8); q =(char *)malloc(8);
        strcpy(p, “hello”);
        strcpy(q,“world”);
        free(p);
        muntrace();//关闭跟踪
        return 0;
    }
```

根据动态内存的使用记录，我们可以很快定位到内存泄漏发生在mcheck.c文件中的第11行代码。

```cpp
#mtrace a.out mtrace.log
Memory not freed:
address Size Caller
0x0901a380 0x8 at /home/c/mem leak/mcheck.c:11
```

<h5 id="abb24acc">广义上的内存泄漏</h5>
<u>广义上的内存泄漏指系统频繁地进行内存申请和释放，导致内存碎片越来越多，无法再申请一片连续的大块内存。如fast bins，主要用来保存用户释放的小于80 Bytes(M_MXFAST)的内存，在提高内存分配效率的同时，带来了大量的内存碎片。</u>

<u>为了最大化地提高系统性能，我们可以通过一些参数对glibc的内存分配器进行调整，使之与实际业务需求达到更大的匹配度,更高效地应对实际业务的需求。</u>

glibc底层实现了一个<u>mallopt()函数，可以通过这个函数对上面的各种参数进行调整。</u>

```cpp
#include <malloc.h>
int mallopt(int param, int value);
```

<h4 id="37d8d958">常见的内存错误及检测</h4>
<u>处理器引入MMU后，操作系统接管了内存管理的工作，负责虚拟空间和物理空间的地址映射和权限管理。操作系统的内存管理子系统将一个进程的虚拟空间划分为不同的区域，如代码段、数据段、BSS段、堆、栈、mmap映射区域、内核空间等，每个区域都有不同的读、写、执行权限。(见内存管理)</u>

对于应用程序来说，常见的内存错误一般主要分为以下几种类型：<u>段错误，内存越界、内存踩踏、多次释放、非法指针。</u>

<h5 id="ef86f028">段错误</h5>
<u>通过内存管理，每个区域都有具体的访问权限，如只读、读写、禁止访问等。数据段、BSS段、堆栈区域都属于读写区，而代码段则属于只读区,如果往代码段的地址空间上写数据,就会发生一个段错误。</u>

<u>当我们往一个只读区域的地址空间执行写操作时，或者访问一个禁止访问的地址（如零地址）时，都会发生段错误。内核空间、零地址、堆和mmap区域之间的内存空间，这部分地址空间要么被内核占用，要么还处于“未开发”状态，需要申请才能使用。</u>

（1）<u>在调试链表时，通常通过指针来操作每一个节点。如果指针在遍历链表时已经指向链表的末尾或头部，指针已经指向NULL了，此时再通过该指针去访问节点的成员，就相当于访问零地址了，也会发生一个段错误，这个指针也就变成了非法指针。</u>

（2）<u>每一个用户进程默认有8MB大小的栈空间，如果在函数内定义大容量的数组或局部变量，就可能造成栈溢出，会引发一个段错误。内核中的线程也是如此，每一个内核线程只有8KB的内核栈，在实际使用中也要非常小心，防止堆栈溢出。</u>

（3）<u>使用malloc()申请的堆内存，如果不小心多次使用free()进行释放，通常也会触发一个段错误。</u>

由于C语言语法检查的宽松性，程序中对内存访问的各种操作并不报错，或者给一个警告信息，这会导致程序在运行期间出现段错误时很难定位。此时我们可以借助一些第三方工具来快速定位段错误。

<h6 id="a0862672">使用core dump调试段错误</h6>
在Linux环境下运行的应用程序，由于各种异常或Bug，会导致程序退出或被终止运行。<u>此时系统会将该程序运行时的内存、寄存器状态、堆栈指针、内存管理信息、各种函数的堆栈调用信息保存到一个core文件中。</u>

<u>core dump功能开启后运行a.out，发生段错误后就会在当前目录下生成一个core文件，然后我们就可以使用gdb来解析这个core文件来定位程序到底出错在哪里。在GDB交互环境下，我们通过bt查看调用栈信息，可以查看错误的具体行数。</u>

<h5 id="a8b2c649">内存踩踏</h5>
<u>比如申请两块动态内存，对其中的一块内存写数据时产生了溢出，就会把溢出的数据写到另一块缓冲区里。在缓冲区释放之前，系统是不会发现任何错误的，也不会报任何提示信息，但是程序却可能因为误操作，覆盖了另一块缓冲区的数据，造成程序莫名其妙的错误</u>。

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main (void){
    char *p,*q;
    p= malloc(16);
    9= malloc(16);
    strcpy(p, "hello world! hello zhaixue.cc!\n");
    printf("%s\n",p);
    printf("%s\n"，q);
    while (1);
    free(q);
    free(p);
    return 0;
}
```

如果一个进程中有多个线程，多个线程都申请堆内存，这些堆内存就可能彼此相邻，使用时需要谨慎，提防越界。在内核驱动开发中，驱动代码运行在特权状态，对内存访问比较自由，多个驱动程序申请的物理内存也可能彼此相邻。

<h6 id="375ec59b">内存踩踏监测：mprotect</h6>
<u>mprotect()是Linux环境下一个用来保护内存非法写入的函数，它会监测要保护的内存的使用情况，一旦遇到非法访问就立即终止当前。</u>进程的运行，并产生一个core dump。

```cpp
#include <sys/mman.h>
int mprotect(void *addr, size t len, int prot);
```

mprotect()函数的第一个参数为要保护的内存的起始地址，len表示内存的长度，第三个参数prot表示要设置的内存访问权限。

<h6 id="49da9439">内存检测神器：Valgrind</h6>
<u>Valgrind包含一套工具集，其中一个内存检测工具Memcheck可以对我们的内存进行内存覆盖、内存泄漏、内存越界检测。</u>

<h1 id="ad88bede">GNU C编译器扩展语法</h1>
<font style="color:#078654;">👋</font>

**<font style="color:#078654;">关联知识点：</font>**

**<font style="color:#078654;">驱动开发file_operation</font>**

**<font style="color:#078654;">C++11类型推导(auto，decltype)</font>**

**<font style="color:#078654;">套接字缓冲区(Socket Buffer)</font>**

**<font style="color:#078654;">USB驱动usb request block</font>**

**<font style="color:#d1a300;">常见的GNU（G-N-U）C拓展语法有哪些？结构体指定初始化是什么？有哪些应用场景？typeof是什么？有哪些应用场景？contaniner of宏是什么？有什么哪些应用场景？</font>**

**<font style="color:#d1a300;">变长数组是什么？有哪些应用场景？为什么不使用指针代替？</font>**

**<font style="color:#d1a300;">__attribute__属性有哪些？</font>**

**<font style="color:#d1a300;">aligned属性有什么用？为什么要用aligned？packed?section?可变参数?weak？oninline和always_inline？什么是内联函数？linux内核中的likely和unlikely？</font>**

<h4 id="f58aeb5b">C语言标准和编译器</h4>
C语言标准因为是在1989年发布的，所以人们一般称其为C89或C90标准，或者叫作ANSI C标准。

<h5 id="3472fc62">C语言标准的内容</h5>
C语言编程的一些语法惯例、约定规则，在C语言标准里：

● 定义各种关键字、数据类型。

● 定义各种运算规则、各种运算符的优先级和结合性。

● 数据类型转换。

● 变量的作用域。

● 函数原型、函数嵌套层数、函数参数个数限制。

● 标准库函数接口。

程序员开发程序时，按照这种标准规定的语法规则编写程序；编译器厂商开发编译

器工具时，也按照这种标准去解析、翻译程序。

<h5 id="d24cde93">C语言标准的发展过程</h5>
ANSI C统一了各大编译器厂商的不同标准，并对C语言的语法和特性做了一些扩展，在1989年发布的一个标准。这个标准一般也叫作C89/C90标准，也是目前各种编译器默认支持的C语言标准。

C99标准是ANSI在1999年基于C89标准发布的一个新标准。

C11标准是ANSI在2011年发布的最新C语言标准，C11标准修改了C语言标准的一些bug，增加了一些新特性。目前绝大多数编译器还不支持，暂时还用不到。

<h5 id="b3cf843e">编译器对C语言标准的支持</h5>
目前对C99标准支持最好的是GNU C编译器。 

<h5 id="d0405b9e">编译器对C语言标准的扩展</h5>
不同编译器，出于开发环境、硬件平台、性能优化的需要，除了支持C语言标准，还会自己做一些扩展。

如GCC编译器也对C语言标准做了很多扩展。零长度数组，语句表达式，内建函数，__attribute__特殊属性声明.....这些新增的特性，C语言标准目前是不支持的，其他编译器也不支持。

<h4 id="aa9ce2ef">指定初始化</h4>
<h5 id="f0b12b67">指定初始化数组</h5>
C语言标准初始化数组

```cpp
int a[10]={0,1,2,3,4,5,6,7,8};
```

a[9]默认为0.

```cpp
int b[100]={[10]=1,[30]=2};
```

通过数组元素索引，我们可以直接给指定的数组元素赋值。在GNU C中，通过数组元素索引，可以直接给指定的几个元素赋值。

给数组中某一个索引范围的数组元素初始化

```cpp
int main(void)
{
    int b[100] = {[10...30] = 1, [50...60] = 2};
    for(int i = 0; i < 100; i++)
        {
            printf("%d", a[i]);
            if (i % 10 == 0)
                printf("\n");
        }
    return 0;
}
```

使用[10...30]表示一个索引范围，给a[10]到a[30]之间的20个数组元素赋值为1。

GNU C支持使用...表示范围扩展，这个特性不仅可以使用在数组初始化中，也可以使用在switch-case语句中。

```cpp
#include <stdio.h>
int main(void)
{
    int i = 4;
    switch(i){
        switch(i){
            case 1:
                printf("1\n");
                break;
            case 2...8:
                printf("%d\n", i);
                break;
            case 9:
                printf("9\n");
                break;
            default:
                printf("default!\n");
                break;
        }
    }
    return 0;
}
```

<h5 id="693d989c"><u>指定初始化结构体成员()</u></h5>
<u>在GNU C中我们可以通过结构域来指定初始化某个成员。</u>

```cpp
#include <stdio.h>
struct student {
char name[20]; // 假设名字不超过19个字符
int age;
};
int main(void) {
    struct student stu2 = {
    .name = "wanglitao", 
    .age = 28
};
    printf("%s:%d\n", stu2.name, stu2.age);
    return 0;
}
```

通过<u>结构域名.name和.age，可以给结构体变量的某一个指定成员直接赋值。</u>

<h5 id="be465f12">Linux内核驱动注册</h5>
<u>驱动程序中，经常使用file_operations这个结构体来注册我们开发的驱动，然后系统会以回调的方式来执行驱动实现的具体功能。</u>

```cpp
#include <linux/fs.h>
static const struct file_operations ab3100_otp_operations = {
.open=ab3100_otp_open,
.read=seq_read,
.llseek=seq_lseek,
.release=single_release,
};
```

flie_operations结构体中有很多函数，使用.指定可以减少代码量。

```cpp
#include <linux/fs.h>
struct file_operations {
struct module *owner;
loff_t (*llseek)(struct file *, loff_t, int);
ssize_t (*read)(struct file *, char __user *, size_t, loff_t *);
ssize_t (*write)(struct file *, const char __user *, size_t, loff_t *);
ssize_t (*read_iter)(struct kiocb *, struct iov_iter *);
ssize_t (*write_iter)(struct kiocb *, struct iov_iter *);
int (*iterate)(struct file *, struct dir_context *);
unsigned int (*poll)(struct file *, struct poll_table_struct *);
long (*unlocked_ioctl)(struct file *, unsigned int, unsigned long);
long (*compat_ioctl)(struct file *, unsigned int, unsigned long);
int (*mmap)(struct file *, struct vm_area_struct *);
int (*open)(struct inode *, struct file *);
int (*flush)(struct file *, fl_owner_t id);
int (*release)(struct inode *, struct file *);
int (*fsync)(struct file *, loff_t, loff_t, int datasync);
int (*aio_fsync)(struct kiocb *, int datasync);
int (*fasync)(int, struct file *, int);
int (*lock)(struct file *, int, struct file_lock *);
ssize_t (*sendpage)(struct file *, struct page *, int, size_t, loff_t *, int);
unsigned long (*get_unmapped_area)(struct file *, unsigned long, unsigned long, unsigned long, unsigned long);
int (*check_flags)(int);
int (*flock)(struct file *, int, struct file_lock *);
ssize_t (*splice_write)(struct pipe_inode_info *, struct file *, loff_t *, size_t, unsigned int);
ssize_t (*splice_read)(struct file *, loff_t *, struct pipe_inode_info *, size_t, unsigned int);
int (*setlease)(struct file *, long, struct file_lock **, void **);
long (*fallocate)(struct file *file, int mode, loff_t offset, loff_t len);
void (*show_fdinfo)(struct seq_file *m, struct file *f);
#ifdef CONFIG_MMU
unsigned (*mmap_capabilities)(struct file *);
#endif
};
```

<u>当成百上千个文件都使用file_operations这个结构体类型来定义变量并初始化时，如果采用C标准按照固定顺序赋值，当file_operations结构体类型发生变化时，如添加了一个成员、删除了一个成员、调整了成员顺序，那么使用该结构体类型定义变量的大量C文件都需要重新调整初始化顺序，牵一发而动全</u>

<u>身。我们通过指定初始化方式，就可以避免这个问题。无论file_operations结构体类型如何变化，添加成员也好、删除成员也好、调整成员顺序也好，都不会影响其他文件的使用。</u>

<h4 id="f09ce65c">宏构造“利器”：语句表达式</h4>
<h5 id="5439b835">表达式、语句和代码块</h5>
略

<h5 id="c0e93eae">在宏定义中使用语句表达式</h5>
使用简单的宏定义做文本替换后会因为括号出现优先级的问题，所以需要进行调整，如linux中min和max的宏定义如下：

```cpp
#define min(x, y) ({ \
typeof(x) _min1 = x; \
typeof(y) _min2 = y; \
(void) (&_min1 == &_min2); \
_min1 < _min2 ? _min1 ： _min2; })

#define max(x, y) ({ \
typeof(x) _max1 = x; \
typeof(y) _max2 = y; \
(void) (&_max1 == &_max2); \
_max1 > _max2 ? _max1 : _max2; }
```

`(void)` 是一个类型转换，它将后面的表达式转换为 `void` 类型，这意味着表达式的结果被丢弃。而 `&_min1 == &_min2` 是一个比较两个变量地址是否相同的表达式，这个表达式的结果是一个布尔值，但通过将其转换为 `void` 类型，这个结果就被忽略了。void这一行代码的目的是让编译器认为 `_min1` 和 `_min2`（或 `_max1` 和 `_max2`）这两个变量被使用了，从而避免编译器发出未使用变量的警告。

<h4 id="27a08cc3">typeof与container_of宏</h4>
<h5 id="5f3b6348"><u>typeof关键字</u></h5>
ANSI C定义了sizeof关键字，用来获取一个变量或数据类型在内存中所占的字节数<u>。GNU C扩展了一个关键字typeof，用来获取一个变量或表达式的类型。</u>typeof没有被纳入C标准，是GCC扩展的一个关键字。

```cpp
int i ;
typeof(i)j= 20;
typeof(int *)a;
    int f();
    typeof(f())k;
```

变量i的类型为int，所以typeof(i)就等于int，typeof(i) j=20就相当于int j=20，typeof(int*) a；

相当于int*a，f()函数的返回值类型是int，所以typeof(f()) k；就相当于int k;

```cpp
typeof(int*) y;
```

定义了一个类型为`int*`的变量 `y`,等价于`int* y;`

```cpp
typeof (int) *y;
```

等价于int *y;

```cpp
typeof(*x) y;
```

定义了一个变量 `y`，其类型是 指针`x` 指向的类型。如果 `x` 是一个指针，`y` 将是 `x` 所指向类型的变量。

```cpp
typeof(int) y[4];
```

等价于 `int y[4];`

```cpp
typeof ( typeof(char *)[4] ) y；
```

等价于char *y[4]；

```cpp
typeof(int x[4]) y;
```

等价于int y[4]；

<h5 id="e200d7ed">Linux内核中的container_of宏</h5>
`<u>container_of</u>`<u>是 Linux 内核中一个非常常用的宏，用于通过结构体成员的指针来获取整个结构体的指针。它在内核实现链表、设备驱动等场景时非常有用。假设有一个结构体，其中包含多个成员。如果只有一个成员的指针，也可以获取整个结构体的指针。</u>

`<u>container_of</u>`<u> 通过结构体成员的指针，减去该成员在结构体中的偏移量，得到整个结构体的起始地址，然后使用强制类型转换可以获取结构体成员的指针。</u>

`**container_of**`** 的原型**

```cpp
#define container_of(ptr, type, member)(
{\
    const typeof(((type *)0)->member)*__mptr=(ptr);
    \(type *)((char*)__mptr -offsetof(type, member));\
})
```

`**ptr**`：结构体成员的指针。`**type**`：结构体的类型。`**member**`：结构体中成员的名称。

`**container_of**`** 的工作原理**

`**typeof(((type *)0)->member)**`:获取 `member` 成员的类型。例如，如果 `member` 是 `int` 类型，则 `typeof` 会推导出 `int`。`**offsetof(type, member)**`：计算 `member` 在结构体 `type` 中的偏移量。`offsetof` 是标准库中的一个宏，用于获取结构体成员的偏移量。`**(char *)__mptr - offsetof(type, member)**`：将 `member` 的指针转换为 `char *`（因为 `char` 的大小是 1 字节，方便计算偏移量）。减去 `member` 在结构体中的偏移量，得到结构体的起始地址。`**(type *)**`：将计算出的地址转换为结构体类型的指针。

`container_of`（会用不要求手写）

```cpp
#include <stdio.h>
#include <stddef.h>
// 定义结构体
struct my_struct {
int data1; int data2; char data3;
};
// 定义 container_of 宏
#define container_of(ptr, type, member) ({              \
const typeof(((type *)0)->member) *__mptr = (ptr);   \
(type *)((char *)__mptr - offsetof(type, member));   \
})
int main() {
    // 创建一个结构体实例
    struct my_struct my_instance = {10, 20, 'A'};
    // 获取 data2 的指针
    int *data2_ptr = &my_instance.data2;
    // 使用 container_of 获取整个结构体的指针
    struct my_struct *parent_struct = container_of(data2_ptr, struct my_struct, 
    data2);
    // 打印结果
    printf("data1: %d, data2: %d, data3: %c\n",
        parent_struct->data1, parent_struct->data2, parent_struct->data3);
    return 0;
}
```

<h3 id="26b4c4b4">`**container_of**`** 的典型应用场景**</h3>
**链表**：

    - <u>Linux 内核中的链表实现广泛使用 </u>`<u>container_of</u>`<u>。</u>
    - <u>链表节点通常嵌入到结构体中，通过节点的指针可以获取整个结构体的指针。</u>

**设备驱动**：

    - <u>在设备驱动中，通常需要从某个成员的指针获取设备结构体的指针。</u>

**回调函数**：

    - <u>在回调函数中，通常只能访问某些特定数据，通过 </u>`<u>container_of</u>`<u> 可以获取更多上下文信息。</u>

<h4 id="15bb9cb1">零长度数组和变长结构体</h4>
💡

**关联知识点：**

**class和struct的区别 **[https://kdocs.cn/l/cuSTtRAG1IvG?linkname=b15pVlL5k0](https://kdocs.cn/l/cuSTtRAG1IvG?linkname=b15pVlL5k0)

零长度数组、变长数组都是GNU C编译器支持的数组类型

<h5 id="23b8c340">什么是零长度数组</h5>
长度为0的数组

```cpp
int a[0];
```

<u>零长度数组有一个特点，就是不占用内存存储空间。</u><u>零长度数组一般单独使用的机会很少，它常常作为结构 体的一个成员，构成一个变长结构体。</u>

```cpp
struct buffer{
int len;
int a[0];
}
```

使用变长数组实现buffer。

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct buffer {
int len;
int a[0]; // 一个零长度的数组，表示后面可以追加任意长度的数据
};
int main(void) {
    struct buffer *buf;
    buf = (struct buffer *)malloc(sizeof(struct buffer) + 20);
    if (buf == NULL) {
        // 内存分配失败的处理
        perror("malloc failed");
        return 1;
    }
    buf->len = 20;
    strcpy(buf->a, "hello zhaixue.cc!\n");
    puts(buf->a);
    free(buf);
    return 0;
}
```

<h5 id="c9ec18d7">linux内核中的零长度数组</h5>
网卡驱动中的套接字缓冲区(Socket Buffer)，USB驱动中的usb request block.......

<h5 id="db62e792">指针与零长度数组</h5>
<u>为什么不使用指针来代替零长度数组？</u>如果使用指针，指针本身占用存储空间不说，远远没有零长度数组用得巧妙：<u>零长度数组不会对结构体定义造成冗余，而且使用起来很方便。</u>

<h4 id="4aa080a3">属性声明</h4>
<h5 id="83f4287c">GNU C编译器扩展关键字：<u>__attribute__</u></h5>
GNU C增加了一个__attribute__关键字用来声明一个函数、变量或类型的特殊属性。

```cpp
atttribute((ATTRIBUTE))
```

目前__attribute__支持十几种属性声明。

section，aligned，packed，format，weak，alias，noinline，always_inline...

<h5 id="19128465"><u>aligned属性</u></h5>
<u>aligned和packed用来显式指定一个变量的存储对齐方式。使用__atttribute__这个属性声明，可以告诉编译器，按照指定的边界对齐方式去给这个变量分配存储空间。</u>

```cpp
char c __attribute__((aligned(8))) = 4;
```

<u>代码声明一个字符变量 </u>`<u>c</u>`<u>，使用 </u>`<u>__attribute__((aligned(8)))</u>`<u> 指定该变量的对齐方式，表示c应该被对齐到8字节的边界，c在内存中的地址应该是8的倍数。</u>

aligned有一个参数，表示要按几字节对齐，使用时要注意，地址对齐的字节数必须是2的幂次方，否则编译就会出错。<u>aligned只是建议编译器按照这种大小地址对齐，但不能超过编译器允许的最大值。 </u>

当定义一个变量时，编译器会按照默认的地址对齐方式，来给该变量分配一个存储空间地址。如果该变量是一个int型数据，那么编译器就会按4字节或4字节的整数倍地址对齐；如果该变量是一个short型数据，那么编译器就会按2字节或2字节的整数倍地址对齐；如果是一个char类型的变量，那么编译器就会按照1字节地址对齐。

<u>地址对齐会造成一定的内存空洞，但是这种对齐设置可以简化CPU读取数据。</u>一个32位的计算机系统，在CPU读取内存时，硬件设计上可能只支持4字节或4字节倍数对齐的地址访问，CPU每次向内存RAM读写数据时，一个周期可以读写4字节。<u>如果我们把一个int型数据放在4字节对齐的地址上，那么CPU一次就可以把数据读写完毕；如果我们把一个int型数据放在一个非4字节对齐的地址上，那么CPU可能就要分两次才能把这个4字节大小的数据读写完毕。</u>

<h5 id="bbabd5dd">结构体的对齐</h5>
char 1字节对齐，short 2 字节对齐，int 4字节对齐，结构体的整体对齐要按结构体所有成员中最大对齐字节数或其整数倍对齐。

```cpp
struct data{
char a;
int b ;
short c ;
}
```

1+3+4+2+2(结构体)=12

结构体成员按不同的顺序排放，可能会导致结构体的整体长度不一样。

```cpp
struct data{
char a;
short b ;
int c;
}
```

1+1(short 2字节对齐)+2+4=8

<h5 id="76199bd0">packed属性</h5>
packed属性则与之相反，一般用来减少地址对齐，指定变量或类型使用最可能小的地址对齐方式。

```cpp
struct data{
char a;
short battribute ((packed));
int c_attribute_((packed));
}
```

1+2+4=7

在ARM芯片中，每一个控制器的寄存器地址空间一般都是连续存在的。如果考虑数据对齐，则结构体内就可能有空洞，就和实际连续的寄存器地址不一致。<u>使用packed可以避免这个问题，结构体的每个成员都紧挨着，依次分配存储地址，这样就避免了各个成员因地址对齐而造成的内存空洞。</u>

在Linux内核源码中，经常看到aligned和packed一起使用，对一个变量或类型同时使用aligned和packed属性声明。这样避免了结构体内各成员因地址对齐产生内存空洞，又指定了整个结构体的对齐方式。

```cpp
struct data {
char a;
short b;
int c;
}_attribute_((packed,aligned(8)));
```

<h5 id="add83441">属性声明：<u>section</u></h5>
<u>可以使用__attribute__来声明一个section属性，section属性的主要作用是：在程序编译时，将一个函数或变量放到指定的段，放到指定的section中。（程序地址空间）</u>

```cpp
int global_val __attribute__((section(".data")));
```

代码声明一个全局整型变量 `global_val`，并使用 `__attribute__((section(".data")))` 指定该变量应该被放置在程序的哪个段中。

`section(".data")` 表示 `global_val` 应该被放置在名为 ".data" 的段中。全局变量默认被放置在 ".data" 段 或者在需要的情况下将其放置在其他段中。

<u>一个可执行文件主要由代码段、数据段、BSS段构成。代码段主要存放编译生成的可执行指令代码，数据段和BSS段用来存放全局变量、未初始化的全局变量。代码段、数据段和BSS段构成了一个可执行文件的主要部分。</u>

<u>编译器在编译程序时，以源文件为单位，将一个个源文件编译生成一个个目标文件。在编译过程中，编译器都会按照这个默认规则，将函数、变量分别放在不同的section中，最后将各个section组成一个目标文件。编译过程结束后，链接器会将各个目标文件组装合并、重定位，生成一个可执行文件。（编译链接)。</u>

<h5 id="9e538193">U-boot镜像自复制分析</h5>
U-boot在启动过程中，是如何将自身代码加载的RAM中的。U-boot的用途主要是加载Linux内核镜像到内存，给内核传递启动参数，然后引导Linux操作系统启动。

U-boot是怎样将自身代码从Flash复制到内存的呢？.....（如果以后投嵌入式的岗位，再看这部分的内容。）

<h5 id="4f8f64c8">属性声明format</h5>
<h5 id="b0f8125a">变参函数的格式检查</h5>
GNU通过__attribute__扩展的format属性，来指定变参函数的参数格式检查。

```cpp
#include <stdio.h>
#include <stdarg.h>
void myprintf(const char *format, ...) __attribute__((format(printf, 1, 2)));
void myprintf(const char *format, ...){
    va_list args;
    va_start(args, format);
    vprintf(format, args);
    va_end(args);
}
int main() {
    myprintf("%s %d %f\n", "The answer is", 42, 3.14);
    return 0;
}
```

va_list:定 义 在 编 译 器 头 文 件 stdarg.h 中,如typedef char * va_list(所以va_list是一个char指针)

va_start(fmt，args):根据参数args的地址，获取args后面参数的地址，并保存在fmt指针变量中。

va_end(args):释放args指针，将其赋值为NULL。

`__attribute__((format(printf, 1, 2)))`

`myprintf` 函数的参数应该按照 `printf`函数的参数格式来检查

格式字符串是第一个参数，从第二个参数开始的参数需要与格式字符串相匹配。

如果调用 `myprintf` 时提供的参数与格式字符串不匹配，编译器将会发出警告。

```cpp
void LOG(int num,char *fmt,...) __attribute__((format(printf,2,3)));
```

<h6 id="5c977fb1">变参函数初体验</h6>
```cpp
#include <stdio.h>
void print_num(int count,...) {
    int *args = (int *) &count + 1;
    for (int i = 0; i < count; i++) {
        printf("*args: %d\n", *args);
        args++;
    }
}
int main(void) {
    print_num(5, 1, 2, 3, 4, 5);
    return 0;
}
```

在print_num()函数中，首先获取count参数地址，然后使用&count+1就可以获取下一个参数的地址，使用指针变量args保存这个地址，并依次访问下一个地址，就可以直接打印传进来的各个实参值。

<h6 id="26a53b1b">变参函数改进版</h6>
```cpp
#include <stdio.h>
#include <stdarg.h>
void print_num(int count, ...) {
    va_list args;
    va_start(args, count);
    for (int i = 0；i < count；i++) printf("%d\n", va_arg(args, int));
    va_end(args);
}
int main(void) {
    print_num(5, 1, 2, 3, 4, 5);
    return 0;
}
```

va_arg(args, int)相当于args指针加4后解引用(取出一个整数)。

实现不同等级的日志打印：

```cpp
#include <stdio.h>
#include <stdarg.h>
#define LOG_LEVEL_INFO  1
#define LOG_LEVEL_WARN  2
#define LOG_LEVEL_ERR   3
int current_log_level = LOG_LEVEL_INFO; // 默认日志等级为INFO
void log_info(const char *format, ...) {
    if (current_log_level <= LOG_LEVEL_INFO) {
        va_list args;
        va_start(args, format);
        printf("INFO: ");
        vprintf(format, args);
        va_end(args);
    }
}
void log_warn(const char *format, ...) {
    if (current_log_level <= LOG_LEVEL_WARN) {
        va_list args;
        va_start(args, format);
        printf("WARN: ");
        vprintf(format, args);
        va_end(args);
    }
}
void log_err(const char *format, ...) {
    if (current_log_level <= LOG_LEVEL_ERR) {
        va_list args;
        va_start(args, format);
        printf("ERROR: ");
        vprintf(format, args);
        va_end(args);
    }
}
int main() {
    log_info("This is an info message: %d", 42);
    log_warn("This is a warning message: %s", "Be careful!");
    log_err("This is an error message: %d", -1);
    return 0;
}
```

<h5 id="41fbcbbf"><u>属性声明：weak</u></h5>
<u>GNU C通过weak属性声明，可以将一个强符号转换为弱符号。程序中变量名/函数名,在编译器的眼里，就是一个符号而已。符号可以分为强符号和弱符号。</u>

<u>●强符号：函数名，初始化的全局变量名 ●弱符号：未初始化的全局变量名</u>

<u>对于相同的全局变量名、函数名</u>

<u>●强符号+强符号 ●强符号+弱符号 ●弱符号+弱符号。</u>

<u>强符号和弱符号主要用来解决在程序链接过程中，出现多个同名全局变量、同名函数的冲突问题。一般遵循下面3个规则：</u>

<u>不能同时存在两个强符号：</u><u>两个同名的函数或全局变量，那么链接器在链接时就会报重定义错误。</u>

<u>强弱可以共处：可以同时定义一个初始化的全局变量和一个未初始化的全局变量。</u>

<u>体积大者胜出：当同名的符号都是弱符号时，那么编译器该选择哪个呢？谁的体积大，即谁在内存中的存储空间大，就选谁。</u>

<u>弱符号的这个特性，在库函数中应用得很广泛。在开发一个库时，基础功能已经实现，有些高级功能还没实现，那么可以将这些函数通过weak属性声明转换为一个弱符号</u>。<u>通过这样设置，即使还没有定义函数，我们在应用程序中只要在调用之前做一个非零的判断就可以了，并不影响程序的正常运行。等以后发布新的库版本，实现了这些高级功能，应用程序也不需要进行任何修改，直接运行就可以调用这些高级功能。</u>

`**<u>static</u>**`**<u> 变量的作用域</u>**<u>：在 C 语言中，</u>`<u>static</u>`<u> 关键字用于修饰变量或函数时，会将它们的作用域限制在当前即编译单元内。即使不同文件中的 </u>`<u>static</u>`<u> 变量同名，它们也是相互独立的，不会相互干扰。</u>`<u>static</u>`<u> 变量在编译时会被标记为</u>**<u>局部符号，</u>**<u>不会暴露给链接器。因此，链接器不会处理这些 </u>`<u>static</u>`<u> 变量，也不会认为它们是冲突的。</u>

结合命名空间。

```cpp
#include <stdio.h>
//基础功能
void basic_function() {
    printf("Basic function is implemented.\n");
}
// 高级功能（声明为弱符号）
__attribute__((weak)) void advanced_function() {
    printf("Advanced function is not implemented yet.\n");
}


#include <stdio.h>

// 声明库中的函数
void basic_function();
void advanced_function();

int main() {
    // 调用基础功能
    basic_function();
    // 判断高级功能是否已实现
    if (advanced_function) {
        printf("Advanced function is available.\n");
        advanced_function();  // 调用高级功能
    } else {
        printf("Advanced function is not available.\n");
    }

    return 0;
}
```

`**__attribute__((weak))**`：将 `advanced_function` 声明为弱符号。如果应用程序中没有实现 `advanced_function`，则调用库中的默认实现。如果应用程序中实现了 `advanced_function`，则调用应用程序中的实现。

<h5 id="56944ee6">属性声明：alias</h5>
GNU C扩展了一个alias属性，用来给函数定义一个别名。

```cpp
#include <stdio.h>
//定义_f函数
void _f(void) {
    printf("_f\n");
}

//为_f函数创建别名 f
void f(void) __attribute__ ((alias("_f")));
int main(void) {
    // 调用 f 函数，实际上调用的是 _f 函数
    f();
    return 0;
}
```

<h4 id="63d3d3b0">内联函数</h4>
<h5 id="cbbc3597">属性声明：noinline</h5>
noinline和always_inline，两个属性的用途是告诉编译器，在编译时，对指定的函数内联展开或不展开。声明一个静态内联函数，使用 always inline 属性强制编译器内联。

```cpp
static inline int func2() __attribute__((no_inline));
static inline int func2() __attribute__((always_inline));
```

<u>使用inline声明一个内联函数，和使用关键字register声明一个寄存器变量一样，只是建议编译器在编译时内联展开。使用关键字register修饰一个变量，只是建议编译器在为变量分配存储空间时，将这个变量放到寄存器里，这会使程序的运行效</u>率更高。那么编译器会不会放呢？得视具体情况而定，编译器要根据寄存器资源是否紧张、这个变量的类型及是否频繁使用来做权衡。

<u>当一个函数使用inline关键字修饰时，编译器在编译时一定会内联展开吗？也不一定。编译器也会根据实际情况，如函数体大小、函数体内是否有循环结构、是否有指针、是否有递归、函数调用是否频繁来做决定。使用noinline和always_inline对一个内联函数作显式属性声明后，编译器的编译行为就变得确定。</u>

<h5 id="46053ba8">什么是内联函数</h5>
<u>内联函数在调用的时候插入的调用的位置，省去了压栈和出栈的操作。与宏相比，内联函数有以下优势：</u>

<u>● 参数类型检查：内联函数虽然具有宏的展开特性，但其本质仍是函数，在编译过程中，编译器仍可以对其进行参数检查，而宏不具备这个功能。</u>

<u>● 便于调试：函数支持的调试功能有断点、单步等，内联函数同样支持。</u>

<u>● 返回值：内联函数有返回值，返回一个结果给调用者。这个优势是相对于ANSI C说的，因为现在宏也可以有返回值和类型了，如前面使用语句表达式定义的宏。</u>

<u>● 接口封装：有些内联函数可以用来封装一个接口，而宏不具备这个特性。</u>

内联函数并不是完美无瑕的，也有一些缺点。<u>内联函数会增大程序的体积，如果在一个文件中多次调用内联函数，多次展开，那么整个程序的体积就会变大，在一定程度上会降低程序的执行效率。函数的作用之一就是提高代码的复用性。我们将常用的一些代码或代码块封装成函数，进行模块化编程，可以减轻软件开发工作量。内联函数往往又降低了函数的复用性。编译器在对内联函数做展开时，除了检测用户定义的内联函数内部是否有指针、循环、递归，还会在函数执行效率和函数调用开销之间进行权衡。</u>

<u>当函数体积小，函数体内无指针赋值、递归、循环等语句，调用频繁，就可以使用static inline关键字修饰它。但编译器不一定会做内联展开，如果你想明确告诉编译器一定要展开，或者不展开，就可以使用noinline或always_inline对函数做一个属性声明。</u>

<h5 id="2a97bae3">思考：内联函数为什么定义在头文件中</h5>
内联函数为什么要定义在头文件中呢？因为它是一个内联函数，可以像宏一样使用，任何想使用这个内联函数的源文件，都不必亲自再去定义一遍，直接包含这个头文件，即可像宏一样使用。<u>那么为什么还要用static修饰呢？</u>因为我们使用inline定义的内联函数，编译器不一定会内联展开<u>，那么当一个工程中多个文件都包含这个内联函数的定义时，编译时就有可能报重定义错误。使用static关键字修饰，则可以将这个函数的作用域限制在各自的文件内，避免重定义错误的发生。</u>

<h4 id="cc6c5b78">内建函数</h4>
（暂时不看）

内建函数，就是编译器内部实现的函数。函数和关键字一样，可以直接调用，无须像标准库函数那样，要先声明后使用。

内建函数的函数命名，通常以__builtin开头。这些函数主要在编译器内部使用，主要是为编译器服务的。内建函数的主要用途如下。

●用来处理变长参数列表。

●用来处理程序运行异常、编译优化、性能优化。

●查看函数运行时的底层信息、堆栈信息等。

●实现C标准库的常用函数。

<h5 id="79d16311">常用的内建函数</h5>
<h6 id="47ab34bf">__builtin_return_address()</h6>
这个函数用来返回当前函数或调用者的返回地址。函数的参数LEVEL表示函数调用链中不同层级的函数。

● 0：获取当前函数的返回地址。

● 1：获取上一级函数的返回地址。

● 2：获取上二级函数的返回地址。

```cpp
#include <stdio.h>
void f(void) {
    int *p;
    p = __builtin_return_address(0);
    printf("f return address: %p\n", (void*)p);
    p = __builtin_return_address(1);
    printf("func return address: %p\n", (void*)p);
    p = __builtin_return_address(2);
    printf("main return address: %p\n", (void*)p);
    printf("\n");
}
void func(void) {
    int *p;
    p = __builtin_return_address(0);
    printf("func return address: %p\n", (void*)p);
    p = __builtin_return_address(1);
    printf("main return address: %p\n", (void*)p);
    printf("\n");
}
int main(void) {
    int *p;
    p = __builtin_return_address(0);
    printf("main return address: %p\n", (void*)p);
    printf("\n");
    func();
    printf("goodbye!\n");
    return 0;
}
```

<h6 id="d18674e7">__builtin_frame_address()</h6>
函数每调用一次，都会将当前函数的现场（返回地址、寄存器、临时变量等）保存在栈中，每一层函数调用都会将各自的现场信息保存在各自的栈中。这个栈就是当前函数的栈帧，每一个栈帧都有起始地址和结束地址，多层函数调用就会有多个栈帧，每个栈帧都会保存上一层栈帧的起始地址，这样各个栈帧就形成了一个调用链。很多调试器其实都是通过回溯函数的栈帧调用链来获取函数底层的各种信息的，如返回地址、调用关系等。

通过内建函数__builtin_frame_address(LEVEL)查看函数的栈帧地址。

●0：查看当前函数的栈帧地址。

●1：查看上一级函数的栈帧地址。

```cpp
#include <stdio.h>
void func(void) {
    int *p;
    p = __builtin_frame_address(0);
    printf("func frame: %p\n", (void*)p);
    p = __builtin_frame_address(1);
    printf("main frame: %p\n", (void*)p);
}
int main(void) {
    int *p;
    p = __builtin_frame_address(0);
    printf("main frame: %p\n", (void*)p);
    func();
    return 0;
}
```

<h6 id="89921a7f">__builtin_constant_p(n)</h6>
编译器内部还有一些内建函数主要用来编译优化、性能优化，如__builtin_constant_p(n) 函数。该函数主要用来判断参数n在编译时是否为常量。如果是常量，则函数返回1，否则函数返回0。

该函数常用于宏定义中，用来编译优化。一个宏定义，根据宏的参数是常量还

是变量，可能实现的方法不一样。

<h6 id="2f65f43e">__builtin_expect(exp，c)</h6>
内建函数__builtin_expect()也常常用来编译优化，函数有2个参数，返回值就是其中一个参数，仍是exp。这个函数的意义主要是告诉编译器：参数exp的值为c的可能性很大，然后编译器可以根据这个提示信息，做一些分支预测上的代码优化。 

那么Cache如何缓存内存数据呢？空间局部性。如CPU正在执行一条指令，那么在下一个时钟周期里，CPU一般会大概率执行当前指令的下一条指令。如果此时Cache将下面的几条指令都缓存到Cache里，则下一个时钟周期里，CPU就可以直接000到Cache里取指、译指和执行，从而使运算效率大大提高。 

如程序在执行过程中遇到函数调用、if 分支、goto跳转等程序结构，会跳到其他地方执行，原先缓存到Cache 里的指令不是CPU要执行的指令。此时，就说Cache没有命中， Cache会重新缓存正确的指令代码供CPU读取。

遇到if/switch这种选择 分支的程序结构，一般建议将大概率发生的分支写在前面。当程序运 行时，因为大概率发生，所以大部分时间就不需要跳转，程序就相当 于一个顺序结构。

<h5 id="dead6789"><u>Linux内核中的likely和unlikely</u></h5>
<u>这两个宏的主要作用就是告诉编译器：某一个分支发生的概率很高，或者很低，基本不可能发生。</u>

```cpp
int main(void)
{
    int a; scanf("%d",&a); if (unlikely(a==0)) {
        {
            printf("%d", 1);
            printf("%d", 2);
            printf("\n");
        }
        else {
        printf("%d", 5); printf("%d", 6);
        printf("%d", 6); printf("\n");
    }
}
return 0;
}
```

<h4 id="d0f019a6"><u>可变参数宏</u></h4>
<u>变参函数基本套路就是使用va_list、va_start、va_end等宏，去解析那些可变参数列表。</u>只有GNU C标准支持这个功能，所以有时候我们也把这个可变参数宏看作GNU C标准的一个语法扩展。

```cpp
#include <stdio.h>
#define LOG(fmt, ...) printf(fmt, ##__VA_ARGS__)
#define DEBUG(...) printf(__VA_ARGS__)
int main(void) {
    LOG("Hello! I'm %s\n", "Wanglitao");
    DEBUG("Hello! I'm %s\n", "Wanglitao");
    return 0;
    _}
```

可变参数宏的实现形式其实和变参函数差不多：用...表示变参列表，变参列表由不确定的参数组成，各个参数之间用逗号隔开。可变参数宏使用C99标准新增加的一个__VA_ARGS__预定义标识符来表示前面的变参列表，而不是像变参函数一样，使用va_list、va_start、va_end这些宏去解析变参列表。预处理器在将宏展开时，会用变参列表替换掉宏定义中的所有__VA_ARGS__标识符。

标识符__VA_ARGS__前面加上了宏连接符＃＃，这样做的好处是：当变参列表非空时，＃＃的作用是连接fmt和变参列表，各个参数之间用逗号隔开，宏可以正常使用；当变参列表为空时，＃＃还有一个特殊的用处，它会将固定参数fmt后面的逗号删除掉，这样宏就可以正常使用了。

<h1 id="8c815d30">C语言的面向对象编程思想</h1>
⭐

关联知识点：

C和C++的区别

操作系统的顶层设计

C++的封装，继承，多态

**<font style="color:#58a401;">什么是代码复用？什么是分层？C语言如何模拟类？C语言如何模拟继承？</font>**

**<font style="color:#58a401;">linux内核链表如何体现面向对象的特性的？C语言如何实现多态的？</font>**

<h4 id="660b2cd7">代码复用与分层思想</h4>
<u>什么是代码复用？</u>

<u>（1）函数级代码复用：定义一个函数实现某个功能，所有的程序都可以调用这个函数，不用自己再单独实现一遍，函数级的代码复用。</u>

<u>（2）将一些通用的函数打包封装成库，并引出API供程序调用，实现了库级的代码复用；</u>

<u>（3）将一些类似的应用程序抽象成应用骨架，然后进一步迭代成框架，实现框架级的代码复用；</u>

<u>如果从代码复用的角度看操作系统，操作系统其实也是对任务调度、任务间通信等功能实现，并引出API供应用程序调用，相当于实现了操作系统级的代码复用。</u>

<u>通常将要复用的具有某种特定功能的代码封装成一个模块，各个模块之间相互独立，使用的时候可以以模块为单位集成到系统中。随着系统越来越复杂，集成的模块越来越多，模块之间会产生依赖关系。为了便于系统的管理和维护，又开始出现分层思想，可以把一个计算机系统分为应用层、系统层、硬件层。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443143-425e5ae9-48cd-45da-836a-88920b536aad.png)

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443183-fc3f912c-1d8c-476b-ab76-c046a8f7ce5b.png)

在Linux内核中，往往包含很多模块和子系统，如文件系统、内存管理子系统、进程调度等。每一个模块或子系统也包含着分层的思想。如Linux文件系统，就包括虚拟文件系统VFS和各种类型的文件系统Ext、Fat、NFS等。底层的磁盘、文件系统、虚拟文件系统及应用层的API读写接口也可以实现分层。

一个系统通过分层设计，各层实现各自的功能，各层之间通过接口通信。每一层都是对其下面一层的封装，并留出API，为上一层提供服务，实现代码复用。

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443697-d6afc7e2-ff74-4789-b2df-221dba82e6d4.png)

<h4 id="21042c4e">面向对象编程基础</h4>
面向过程编程中函数是程序的基本单元，可以把一个问题分解成多个步骤来解决，每

一步或每一个功能都可以使用函数来实现。

在面向对象编程中，对象是程序的基本单元，对象是类的实例化，类则是对客观事物抽象而成的一种数据类型，其内部包括属性和方法。

面向对象编程则侧重于将问题抽象、封装成一个个类，然后通过继承来实现代码复用，面向对象编程一般用于复杂系统的软件分层和架构设计。

<h4 id="5aea40fc">Linux内核中的OOP思想：封装</h4>
内核中的很多子系统、模块在实现过程中处处体现了面向对象编程思想。

<h5 id="010c2f8b">类的C语言模拟实现</h5>
<u>C语言中没有class关键字，但是可以使用struct模拟一个类，C++类中的属性类似结构体的各个成员。虽然结构体内部不能像类一样可以直接定义函数，但可以在结构体中内嵌函数指针来模拟类中的方法。</u>

```cpp
struct animal{
int age;
int weight;
void (*fp)(void);
}
```

<u>如果一个结构体中需要内嵌多个函数指针，可以把这些函数指针进一步封装到一个结构体内。</u>

```cpp
struct func operations{
    void(*fp1)(void);
    void (*fp2)(void);
    void (*fp3)(void);
    void (*fp4)(void);
}
struct animal{
int age;
int weight;
struct func operations fp;
}
```

<u>通过把函数封装在结构体中，然后嵌入该结构体，可以把一个类的属性和方法都封装在一个结构体里。</u>

如何继承？

```cpp
struct cat{
struct animal *p;
struct animal ani;
char sex;
void (*eat)(void);
}
```

<u>C语言可以通过在结构体中内嵌另一个结构体或结构体指针来模拟类的继承。</u>

在结构体类型cat里内嵌结构体类型animal，此时结构体cat就相当于模拟了一个子类cat，而结构体animal相当于一个父类。

C语言中,内嵌结构体或内嵌指向结构体的指针，可以看作对“继承”的模拟。

<h5 id="992e5734">链表的抽象与封装</h5>
Linux内核中为了实现对链表操作的代码复用，定义了一个通用的链表及相关操作.

```cpp
struct list head{
    struct list head *next, *prev;
}
void INIT LIST HEAD(struct list head *list);
int list empty(const struct list head *head);
void list add(struct list head *new, struct list head *head);
    void list del(struct list head *entry);
    void list replace(struct list head *old,struct list head *new),
        void list move(struct list head *list, struct list head *head);
```

如果想复用Linux内核中的通用链表及相关操作，就可以通过内嵌结构体来继承list_head的属性和方法。

```cpp
struct my_list node{
    int data;
    struct list head list;
}
```

<h5 id="6f1008f6">设备管理模型</h5>
Linux如何管理和维护这些设备的信息呢？

Linux的设备管理模型说起。Linux内核中定义了一个非常重要的结构体类型。

```cpp
struct kobject{
const char *name;
struct list head entry;
struct kobject *parent;
struct kernfs node *sd;
struct kset *kset;
struct kobj_type *ktype;
struct kref kref;
unsigned int state initialized:1;
unsigned int state_in_sysfs:1;
unsigned int state add uevent sent:1;
unsigned int state_remove_uevent sent:1;
unsigned int uevent suppress:1;
}
```

所有设备在系统中的树结构,kobject结构体用来表示Linux系统中的一个设备，相同类型的kobject通过其内嵌的list_head链成一个链表，然后使用另外一个结构体kset来指向和管理这个列表。

以后再说。

以字符设备为例，我们可以看到字符设备结构体cdev在内核中的定义。

```cpp
struct cdev {
struct kobject      kobj;          // 内嵌kobject结构体
struct module       *owner;
const struct file_operations *ops;
struct list_head    list;
dev_t               dev;
unsigned int        count;
};
```

在结构类型cdev中，通过内嵌结构体kobject来模拟对基类kobject的继承，字符设备的注册与注销，都可以通过继承基类的kobject_add()/kobject_del()方法来完成。与此同时，字符设备在继承基类的基础上，也完成了自己的扩展：实 现 了 自 己的read/write/open/close接口，并把这些接口以函数指针的形式封装在结构体file_operations中。

```cpp
struct file_operations {
struct module *owner;
loff_t (*llseek) (struct file *, loff_t, int);
ssize_t (*read) (struct file *, char __user *, size_t, loff_t *)；
ssize_t (*write) (struct file *, const char __user *, size_t, loff_t *);
ssize_t (*read_iter) (struct kiocb *, struct iov_iter *)；
ssize_t (*write_iter) (struct kiocb *, struct iov_iter *);
int (*iterate) (struct file *, struct dir_context *);
unsigned int (*poll) (struct file *, struct poll_table_struct *);
long (*unlocked_ioctl) (struct file *, unsigned int, unsigned long);
long (*compat_ioctl) (struct file *, unsigned int, unsigned long); 
int (*mmap) (struct file *, struct vm_area_struct *);
int (*open) (struct inode *, struct file *);
int (*flush) (struct file *, fl_owner_t id);
int (*release) (struct inode *, struct file *);
int (*fsync) (struct file *, loff_t, loff_t, int datasync);
int (*aio_fsync) (struct kiocb *, int datasync);
int (*fasync) (int, struct file *, int);
int (*lock) (struct file *, int, struct file_lock *);
...
};
```

不同的字符设备，会根据自己的硬件逻辑实现各自的read()、write()函数，并注册到系统中。当用户程序读写这些字符设备时，通过这些接口，就可以找到对应设备的读写函数，对字符设备进行打开、读写、关闭等各种操作。

<h5 id="236e6db1">总线设备模型</h5>
Linux每一个设备都要有一个对应的驱动程序，否则就

无法对这个设备进行读写。每一个字符设备都对应的字符设备驱动程序；每一个块设备都有对应的块设备驱动程序。对于一些总线型的设备，如鼠标、键盘、U盘等USB设备，设备通信是按照USB标准协议进行的。

Linux系统为了实现最大化的驱动代码复用，设计了设备-总线-驱动模型：用总线提供的一些方法来管理设备的插拔信息，所有的设备都挂到总线上，总线会根据设备的类型选择合适的驱动与之匹配。通过这种设计，相同类型的设备可以共享同一个总线驱动，实现了驱动级的代码复用。

总线设备模型相关的3个结构体分别为device、bus、driver，它们可以看成基类kobject的子类。

```cpp
struct device {
struct device         *parent;     // 父设备
struct device_private *p;          // 内嵌私有数据
struct kobject        kobj;        // 内嵌kobject结构体
const struct device_type *type;    // 设备类型
struct bus_type       *bus;        // 总线类型
struct device_driver  *driver;     // 驱动程序
void                 *platform_data;
void                 *driver_data;
dev_t                devt;
u32                  id;
struct klist_node     knode_class;
struct class         *class;
void (*release)(struct device *dev);
};
```

与字符设备cdev类似，在结构体类型device的定义里，也通过内嵌kobject结构体来完成对基类kobject的继承。但其与字符设备不同之处在于，device结构体内部还内嵌了bus_type和device_driver，用来表示其挂载的总线和与其匹配的设备驱动。

device结构体可以看成一个抽象类，我们无法使用它去创建一个

具体的设备。其他具体的总线型设备，如USB设备、I2C设备等可以通

过内嵌device结构体来完成对device类属性和方法的继承。

```cpp
struct usb_device {
int      devnum;
char     devpath[16];
u32      route;
enum usb_device_state    state;
enum usb_device_speed   speed;
struct usb_tt           *tt;
int                     ttport;
unsigned int            toggle[2];
struct usb_device       *parent;
struct usb_bus          *bus;
struct usb_host_endpoint ep0;
struct device           dev;             // 内嵌device 结构体
...
};
```

<h4 id="ed61f047">Linux内核中的OOP思想：继承</h4>
<h5 id="167d5d3e">继承与私有指针</h5>
<u>除了内嵌结构体，C语言还可以有其他方法来模拟类的继承，如通过私有指针。我们可以把使用结构体类型定义各个不同的结构体变量，也可以看作继承，各个结构体变量就是子类，然后各个子类通过私有指针扩展各自的属性或方法。这种继承方法主要适用于父类和子类差别不大的场合。</u>

如Linux内核中的网卡设备，不同厂家的网卡、不同速度的网卡，以及相同厂家不同品牌的网卡，它们的读写操作基本上都是一样的，都通过标准的网络协议传输数据，唯一不同的就是不同网卡之间存在一些差异，如I/O寄存器、I/O内存地址、中断号等硬件资源不相同。

遇到可以将各个网卡一些相同的属性抽取出来，构建一个通用的结构体net_device，然后通过一个私有指针，指向每个网卡各自不同的属性和方法，这样可以最大程度地实现代码复用。

```cpp
struct net_device {
char name[IFNAMSIZ];                   // 网络设备名称
const struct net_device_ops *netdev_ops; // 网络设备操作
const struct ethtool_ops *ethool_ops;    // Ethtool操作
void *ml_priv;                       // 中间层私有数据
struct device dev;                   // 内嵌device结构体
};
```

当我们使用该结构体类型定义不同的变量来表示不同型号的网卡设备时，这个私有指针就会指向各个网卡自身扩展的一些属性。

<h5 id="0f512396">继承与抽象类</h5>
含有纯虚函数的类，称之为抽象类。抽象类不能被实例化，实例化也没有意义，如animal类，它只能被子类继承。抽象类的作用，主要就是实现分层：实现抽象层。当父类和子类之间的差别太大时，很难通过继承来实现代码复用，如生物类和狗

类，我们可以在它们之间添加一个animal抽象类。抽象类主要用来管理父类和子类的继承关系，通过分层来提高代码的复用性。

如上面设备模型中的device类，位于kobj类和usb_device类之间，通过分层，

可以更好地实现代码复用。

<h4 id="a37ce137">Linux内核中的OOP思想：多态</h4>
可以使用C语言来模拟多态：<u>如果把使用同一个结构体类型定义的不同结构体变量看成这个结构体类型的各个子类，那么在初始化各个结构体变量时，如果基类是抽象类，类成员中包含纯虚函数，则为函数指针成员赋予不同的具体函数，然后通过指针调用各个结构体变量的具体函数即可实现多态。</u>

```cpp
#include <stdio.h>
// 文件操作结构体
typedef struct file_operation {
void(*read)(void);  // 读取操作
void(*write)(void); // 写入操作
} FileOperation;
// 文件系统结构体
typedef struct file_system {
char name[20];      // 文件系统名称
FileOperation fops; // 文件操作
} FileSystem;

// 扩展文件系统的读操作
void ext_read(void) {
    printf("ext read...\n");
}
// 扩展文件系统的写操作
void ext_write(void) {
    printf("ext write...\n");
}
// FAT文件系统的读操作
void fat_read(void) {
    printf("fat read...\n");
}

// FAT文件系统的写操作
void fat_write(void) {
    printf("fat write...\n");
}
int main(void) {
    // 初始化扩展文件系统
    FileSystem ext = {"ext3", {ext_read, ext_write}};
    // 初始化FAT文件系统
    FileSystem fat = {"fat32", {fat_read, fat_write}};

    // 文件系统指针
    FileSystem *fs_ptr;

    // 指向扩展文件系统
    fs_ptr = &ext;
    fs_ptr->fops.read(); // 调用扩展文件系统的读操作
    // 指向FAT文件系统
    fs_ptr = &fat;
    fs_ptr->fops.read(); // 调用FAT文件系统的读操作
    return 0;
}
```

<h1 id="4c3fadc4">C语言的模块化编程思想</h1>
**<font style="color:#58a401;">不同模块如何链接成一个文件？面向对象编程和模块化编程有什么区别？</font>**

**<font style="color:#58a401;">头文件有什么用？头文件重复包含是什么？</font>**

**<font style="color:#58a401;">变量声明和定义有什么区别?extern变量怎么用？</font>**

**<font style="color:#58a401;">goto关键字有什么用？</font>**

**<font style="color:#58a401;">模块设计原则是什么?模块直接耦合的方式有哪些？模块间如何进行通信？</font>**

<h4 id="959c3af8"><u>模块的编译和链接</u></h4>
<u>一个C语言项目划分成不同的模块，通常由多个文件来实现。在项目编译过程中，编译器是以C源文件为单位进行编译的，每一个C源文件都会被编译器翻译成对应的一个目标文件。链接器对每一个目标文件进行解析，将文件中的代码段、数据段分别组装，生成一个可执行的目标文件。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443786-b4858761-e3ef-4d89-9974-69b6242be598.png)

<u>如果程序调用了库函数，则链接器也会找到对应的库文件，将程序中引用的库代码一同链接到可执行文件中。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443749-7ad9e0e7-e7bc-43a4-86ab-924878e8c534.png)

<u>在链接过程中，如果多个目标文件定义了重名的函数或全局变量，就会发生符号冲突，报重定义错误。这时候链接器就要对这些重复定义的符号做符号决议，决定哪些留下，哪些丢弃。</u>

<u>在一个多文件项目中，不允许有多个强符号。</u>

<u>若存在一个强符号和多个弱符号，则选择强符号。</u>

<u>若存在多个弱符号，则选择占用空间最大的那一个。</u>

<u>初始化的全局变量和函数是强符号，未初始化的全局变量。默认属于弱符号。</u>

<u>可以通过__attribute__属性声明显式更改符号的属性，将一个强符号显式转换为弱符号。</u>

和强符号、弱符号对应的，还有强引用、弱引用的概念。在一个程序中，我们可以定义多个函数和变量，变量名和函数名都是符号，这些符号的本质，或者说这些符号值，其实就是地址。在另一个文件中，我们可以通过函数名去调用该函数，通过变量名去访问该变量。我们通过符号去调用一个函数或访问一个变量，通常称之为引用

强符号对应强引用，弱符号对应弱引用。在程序链接过程中，若对一个符号的引用为强引用，链接时找不到其定义，链接器将会报未定义错误；若对一个符号的引用为弱引用，链接时找不到其定义，则链接器不会报错，不会影响最终可执行文件的生成。可执行文件在运行时如果没有找到该符号的定义才会报错。

利用链接器对弱引用的处理规则，我们在引用一个符号之前可以先判断该符号是否存在（定义）。这样做的好处是：当我们引用一个未定义符号时，在链接阶段不会报错，在运行阶段通过判断运行，也可以避免运行错误。

```cpp
void log_message(const char* message) __attribute__((weak));
void some_function() {
    if (log_message) {
        log_message("Starting some_function");
    } // 如果log_message未定义，这里不会执行，也不会报错
    // 执行some_function的其他逻辑
}
```

<u>整个项目编译过程中，可以通过编译控制参数来控制编译流程：预处理、编译、汇编、链接，也可以指定多个文件的编译顺序。</u>

<u>通常使用自动化编译工具make来编译项目，make自动编译工具依赖项目的Makefile文件。</u>

<u>Makefile文件主要用来描述各个模块文件的依赖关系，要生成的可执行文件，需要编译哪些源文件。</u>

<u>make在编译项目时，会首先解析Makefile，分析需要编译哪些源文件，构建一个完整的依赖关系树，然后调用具体的命令一步步去生成各个目标文件和最终的可执行文件。</u>

<h4 id="aa208c3a">系统模块划分</h4>
根据系统的目标、实现的功能进行划分；当系统比较复杂时，对系统进行分层。

<u>面向对象编程和系统的模块化设计侧重点不同。模块化设计的思想</u>

<u>内核是分而治之，重点在于抽象的对象之间的关联，而不是内容；面向对象编程思想主要是为了代码复用，重点在于内容实现。两者还有一个重要的区别是：两者不在同一个层面上。模块化设计是最高原则，先有系统定义，然后有模块和模块的实现，最后才有代码复用。一个系统不仅仅是模块的实现，还有各个模块之间的相互作用、相互关联，以及由它们构成的一个有机整体。面向对象编程，通过类的封装和继承实现了代码复用，减少了开发工作量，这是面向对象编程的长处。</u>

<h4 id="cc220b99">模块的封装</h4>
<u>在C语言中一个模块一般对应一个C文件和一个头文件。模块的实现在C源文件中，头文件主要用来存放函数声明，留出模块的API，供其他模块调用。</u>

变量的定义和声明有什么区别？

<h4 id="8534e893">头文件深度剖析</h4>
<u>编译器在编译各个C源文件的过程中，如果该C文件引用了其他文件中定义的函数或变量，编译器也不会报错，链接器在链接的时候会到这个文件里查找你引用的函数，如果没有找到才会报错。但是编译器为了检查你的函数调用格式是否存在语法错误，形参实参的类型是否一致，会要求程序员在引用其他文件的全局符号之前必须先声明，如变量的类型、函数的类型等，编译器会根据你声明的类型对编写的程序语句进行语法、语义上的检查。为了方便，将函数的声明直接放到头文件里，作为本模块封装的API，供其他模块使用。程序员在其他文件中如果想引用这些API函数，则直接＃include这个头文件，然后直接调用。</u>

<u>变量的声明和定义的区别：</u><u><font style="background-color:#fbf5b3;">是否分配内存是区分定义和声明的唯一标准。</font></u>

<u>一个变量的定义最终会生成与具体平台相关的内存分配汇编指令。</u>

<u>变量的声明则告诉编译器，该变量可能在其他文件中定义，编译时先不要报错，等链接的时候可以到指定的文件里去看看有没有，如果有就直接链接，如果没有则再报错也不迟。一个变量只能定义一次，即只能分配一次存储空间，但是可以多次声明。一般变量的定义要放到C文件中，不放到头文件中，因为头文件可能被多人使用，被多个文件包含，头文件经过预处理器多次展开之后也就变成了多次定义。</u>

**<u>头文件重复包含</u>**

<u>如果在一个项目中多次包含相同头文件，编译器也不会报错，因为预处理器在预处理阶段已经将头文件展开了：一个变量或函数可以有多次声明，这是编译器允许的。如果在头文件里定义了宏或一种新的数据类型，头文件再多次包含展开，编译器在编译时可能会报重定义错误。为了防止这种错误产生，可以在头文件中使用条件编译来预防头文件的多次包含。</u>

<h5 id="d1ca11e6">隐式声明</h5>
（ANSI C标准支持，<font style="background-color:#fbf5b3;">但C99/C11/C++标准已禁止</font>)

如果一个C程序引用了在其他文件中定义的函数而没有在本文件中声明，编译器也不会报错，编译器会认为这个函数可能会在其他文件中定义，等链接的时候找不到其定义才会报错，而是会给一个警告信息并自动添加一个默认的函数声明。这个声明我们称为隐式声明。

函数的隐式声明可能与自定义函数冲突，如果我们引用库函数而没有包含对应的头文件，也有可能与库函数发生类型冲突。这些函数类型冲突虽然不影响程序的正常运行，但是会给程序带来很多无法预料的深层次bug，在不同的编译环境下，函数的运行结果甚至可能都不一样。为了编写高质量稳定运行的程序，我们要养成“先声明后使用”的良好编程习惯。

<h5 id="11b77f39">变量的声明与定义</h5>
<u>extern关键字对</u><u>外部文件的符号进行声明</u>

```cpp
extern int i;
extern int a[20],
extern struct student stu;
extern int function();
extern“c” int function();
```

<u>extern声明的变量或函数在别的文件里定义，在本文件使用，告诉编译器不要报错。</u>

```cpp
//i.c
int i = 10;
int a[10]={1,2,3,4,5,6,7,8,9};
struct student
int age;
int num;
```

```cpp
//main.c
#include <stdio.h>
extern int i;
extern int a[10];
struct student{
int age;
int num;
extern struct student stu;
extern int k;
int main(void)
printf("%s:i =%d\n",_func_,i);
for(int j=0;j<10;j++)
    printf("a[%d]:%d\n"，j，a[j]);
        printf("stu.age =%d,num = %d\n",stu.age, stu.num);
printf("%s:k=%d\n",_func_,k);
return 0;
```

<h5 id="1b027d90">如何区分定义和声明</h5>
定义的本质就是为对象分配存储空间，声明则将一个标识符与某个C语言对象相关联(函数、变量等)。

声明函数原型为了提供给编译器做函数参数格式检查，声明一个变量，是为了告诉编译器，这个变量已经在别的文件里定义，我们想在本文件里使用它。在C语言中，我们可以声明各种各样的标识符：变量名、函数名、类型、类型标志、结构体、联合、枚举常量、语句标号、预处理器宏等。

<u>（1）从extern的角度区别定义和声明：</u>

<u>如果省略了extern且具有初始化语句，则为定义语句。如int i=10。</u>

<u>如果使用了extern，无初始化语句，则为声明语句。如extern int i；。</u>

<u>如果省略了extern且无初始化语句，则为试探性定义。如int i；。</u>

试探性定义(int i)。该变量可能在别的文件里有定义，所以先暂时定为声明。若别的文件里没有定义，则按照语法规则初始化该变量i，并将该语句定性为定义。一般这些变量会初始化为一些默认值：NULL、0、undefined values等。

<u>（2）编译链接的角度去分析int i：</u>

<u>对于未初始化的全局变量，它是一个弱符号，先定性为声明。如果其他文件里存在同名的强符号，那么这个强符号就是定义，把这个弱符号看作声明没毛病；如果其他文件里没有强符号，那么只能将这个弱符号当作定义，为它分配存储空间，初始化为默认值。</u>

<h5 id="c320c78e">前向引用和前向声明</h5>
<u>无论声明什么类型的标识符，先声明后使用。</u>

因为早期的编译器鉴于计算机内存资源限制，不可能同时编译多个文件，所以只能采取单独编译。编译器为了简化设计，采用了one-pass compiler设计，每个源文件只编译一次，这也决定了C语言“先声明后使用”的使用原则。

"先声明后使用"指一个标识符要在声明完成之后才能使用，在声明完成之前不能使用。

**什么是声明完成呢？**

<u>一个变量的声明无非就是声明其类型，声明是给编译器看的，是为了应付编译器语法检查的。如果已经让编译器知道了这个标识符的类型，那么就认为声明完成了。</u>

在C语言中，并不是所有的标识符都需要先声明后使用。

如果一个标识符在未声明完成之前就引用，被称为前向引用。

在C语言中，有3个可以前向引用的特例。

● 隐式声明

● 语句标号：跳转向后的标号时，不需要声明，可以直接使用。

● 不完全类型：在被定义完整之前用于某些特定用途。

<font style="background-color:#fbf5b3;">语句标号</font>：使用C语言的goto关键字可以往前跳，也可以往后跳，不需要对语句标号进行事先声明。

不完全类型是 指 那些尚未提供完整信息的类型。这种类型的对象或指针可以被声明和使用，但它们不能被定义（即分配存储空间。

（1）数组类型未知大小：

当数组声明时没有指定大小，例如 `int a[];` 这样一个数组就是一个不完全类型。在这种情况下，编译器不知道数组的确切大小，因此无法为它分配具体的内存空间。但是你可以有一个指向该数组类型的指针，比如 `int *p = a;` 只要之后通过其他方式明确了数组的大小，就可以正常使用了。

（2）结构体或联合体类型未知内容：如果结构体或联合体只被命名而没有给出其成员的定义，那么这个结构体或联合体就是一个不完全类型。

<h5 id="3f21e90c">定义与声明的一致性</h5>
```cpp
//add.h
int add(int a, int b);
//add.c
#include"add.h"
int add(int a, int b)
return a+b;
//main.c
#include "add.h"
int main(void){
    int sum; 
    sum = add(1,2);
    return 0;
}
```

<font style="background-color:#fbf5b3;">在模块里包含自己的头文件</font>，可以使用头文件中定义的宏或数据类型，还有一个好处就是可以让编译器检查定义与声明的一致性。在模块的封装中，接口函数的声明和定义是在不同的文件里分别完成的，很多人在编程时可能比较粗心，一个函

数在声明和定义时的类型可能不一致，但是编译器又是以文件为单位进行编译的，无法检测到这个错误，那该怎么办？很简单，我们把一个函数的声明和定义放到一个文件中，编译器在编译时就会帮我们进行自检：检查一个函数的定义和声明是否一致，避免出现低级错误。

<h5 id="8ffe4389">头文件路径</h5>
头文件两种包含方法

```cpp
#include <stdio.h>
#include“module.h”
```

<>表示引用标准库的头文件

如果你使用的头文件是自定义的或项目中的头文件，一般使用双引号""包含。头文件路径一般分为绝对路径和相对路径：绝对路径以根目录“/”

编译器在编译过程中会按照这些路径信息到指定的位置查找头文件，然后通过预处理器做展开处理。在查找头文件的过程中，编译器会按照默认的搜索顺序到不同的路径下去搜索。

使用<>包含头文件：

GCC参数gcc-I指定的目录->环境变量CINCLUDEPATH指定的目录->GCC的内定目录。当不同目录下存在相同的头文件时，先搜到哪个就使用哪个，搜索到头文件后不再往下搜索。

在程序编译时，如果头文件没有放到官方路径下面，那么可以通过gcc-I来指定头文件路径，编译器在编译程序时，就会到用户指定的路径目录下面去搜索该头文件。如果你不想通过这种方式，也可以通过环境变量来添加头文件的搜索路径。

用双引号""来包含头文件路径：

编译器会首先在项目当前目录搜索需要的头文件，如果在当前项目目录下搜不到，则再到其他指定的路径下去搜索。

项目当前目录->通过GCC参数gcc-I指定的目录->环境变量CINCLUDEPATH指定的目录->GCC的内定目录.

常见的内定目录

```cpp
/usr/include
    /usr/local/include
    /usr/include/i386-linux-gnu
    /usr/lib/gcc/i686-linux-gnu/5/include
    /usr/lib/gcc/i686-linux-gnu/5/include-fixed
    /usr/lib/gcc-cross/arm-linux-gnueabi/5/include
```

<h5 id="13636dbe">头文件中的内联函数</h5>
使用inline关键字修饰的函数称为内联函数。内联函数也是函数，它和普通函数的不同之处在于，编译器在编译内联函数时，会根据需要在调用处直接展开，从而省去了函数调用开销。对于一些频繁调用而又短小精悍的函数，如果我们将其声明为内联函数，编译器编译时像宏一样展开，可以提升程序的运行效率。内联函数和宏相比，除了能像宏一样在调用处直接展开，在参数传递、参数检查、返回值等方面比宏更有优势。正是这种优势，内联函数在C语言中被广泛使用。但是函数虽然变成了内联函数，但是在编译的时候会不会展开还得由编译器决定。

内联函数一般定义在.C文件中，但是内联函数也可以定义在头文件中。一般来讲，变量和函数是不能在头文件中定义的，因为该头文件可能被多个C文件包含，当被预处理器展开后就变成了多次定义，很可能报重定义错误。当多个模块引用该头文件时，内联函数在编译时已经在多个调用处展开，不复存在了，不存在重定义问题。即使编译器没有对内联函数展开，也可以在内联函数前通过添加一个static关键字将该函数的作用域限制在本文件内，从而避免了重定义错误的发生。

```cpp
static inline void func(int a, int b);
```

<h4 id="f7f62564">模块设计原则</h4>
<font style="background-color:#fbf5b3;">高内聚低耦合</font>是模块设计的基本原则。

高内聚：各个模块在实现各自功能的时候，要自己的事自己做，自己的功能自己实现，尽量不麻烦其他模块。一个模块要想实现高内聚，首先模块的功能要尽可能单一，一个功能由一个模块实现，这样才能体现模块的独立性，进而实现高内聚。要尽量调用本模块实现的函数，减少对外部函数的依赖，这样可以进一步提高模块的独立性，提高模块的内聚度。

与模块内聚对应的是模块耦合。

模块耦合指的是模块间的关联和依赖，包括调用关系、控制关系、数据传递等。模块间的关联越强，耦合度就越高，模块的独立性越差，内聚度也就随之越低。

不同模块之间有不同的耦合方式。

●非直接耦合：两个模块之间没有直接联系。

●数据耦合：通过参数来交换数据。

●标记耦合：通过参数传递记录信息。

●控制耦合：通过标志、开关、名字等，控制另一个模块。

●外部耦合：所有模块访问同一个全局变量。

我们在设计模块时，要尽量降低模块的耦合度。

低耦合有很多好处，如可以让系统的结构层次更加清晰，升级维护起来更加方便。在C语言程序中，我们可以通过下面的常用方法降低模块的耦合度。

● 接口设计：隐藏不必要的接口和内部数据类型，模块的API封装在头文件中，其余函数使用static修饰。

● 全局变量：尽量少使用，可改为通过API访问以减少外部耦合。

● 模块设计：尽可能独立存在，功能单一明确，接口少而简单。

● 模块依赖：模块之间最好全是单向调用，上下依赖，禁止相互调用。

<h4 id="88b7b1a3">被误解的关键字：goto</h4>
goto不是一无是处，其无条件跳转的特性有时候会大大简化程序的设计。如有多个出错出口的函数，我们可以使用goto将函数内的出错指定一个统一的出口，统一处理，反而会使函数的结构更加清晰。

```cpp
int func(void){
    dosomething;
    if(expr1) goto err;
    do sth;
        if(expr2)
        goto err;
    return @;
    err:
    return -1
        }
```

通过代码复用，将一个函数多个出口归并为一个总出口，然后在总出口处对出错统一处理，释放malloc() 申请的动态内存、释放锁、文件句柄等资源。通过函数内部这种模块化的设计，既提高了效率，又不会破坏程序原来的结构。

在一个多重循环程序中，如果我们想从最内层的循环直接跳出，则需要多次使用break和return，层层退出才能达到预期目的,使用goto无条件跳转，简单粗暴,一步到位。

```cpp
for(cxpr1){
    for(expr2){
        for(expr3){
            for(expr4){
                if(expr5)
                    goto endloop;
            }}}}
return @;
endloop:
return -1;
```

注意事项：goto在使用的过程中，也有一些需要注意的地方，如只能往下跳，不能往上跳。使用goto只能在同一函数内跳转，函数内goto标签的位置也有一定的讲究，goto标签一般在函数体内两段不同逻辑功能代码的交界处，用来区分函数内的模块化设计和逻辑关系。

<h4 id="d77d0157">模块间通信</h4>
系统内的各个模块可以通过各种耦合方式进行通信

<h5 id="fcfffbf5">全局变量</h5>
各个模块共享全局变量是各个模块之间进行数据通信最简单直接的方式。一个全局变量具有文件作用域，但是我们可以通过extern关键字将全局变量的作用域扩展到不同的文件中，然后各个模块可以通过全局变量进行通信了。

但是这样耦合度比较高，改进的方法：对全局变量的直接访问修改为通过函数接口间接访问。就像类的私有成员一样，该全局变量只能在一个模块中创建或直接修改，如果其他模块想要访问这个全局变量，则只能通过引出的函数读写接口进行访问。

```cpp
//module.h
void val set(int value)；
int val_get(void)；
//module.c
int global val = 10；
void val set(int value){
    global_val = value；
        }
int val_get(void){
    return global _val；
        }
```

linux内核模块1：

```cpp
#include <linux/init.h>
#include <linux/module.h>
MODULE_LICENSE("GPL");
int global_val = 10;
EXPORT_SYMBOL(global_val);
int get_global_val_value(void){
    return global_val;
}
void set_global_val_value(int a){
    global_val = a;
}
static int __init module1_init(void){
    printk(KERN_INFO "hello module1!\n");
    printk(KERN_INFO "module1:global_val = %d\n", global_val);
    return 0;
}
static void __exit module1_exit(void)
{
    printk(KERN_INFO "goodbye, module1!\n");
}
module_init(module1_init);
module_exit(module1_exit);
```

linux内核模块2:

```cpp
#include <linux/init.h>
#include <linux/module.h>
#include <asm-generic/errno.h>
MODULE_LICENSE("GPL");
extern int global_val;
static int __init module2_init(void){
    printk(KERN_INFO "hello module2!\n");
    printk(KERN_INFO "module2:global_val = %d\n", global_val);
    return 0;
}
static void __exit module2_exit(void){
    printk(KERN_INFO "goodbye, module2!\n");
}
module_init(module2_init);
module_exit(module2_exit);
```

两个模块编译后insmod到内核中，模块2可以访问到模块1的全局变量。

通过共享全局变量进行模块间通信，实现最简单，也最容易理解，因此在各个项目中被广泛使用，包括在生产者-消费者模型中常用的共享缓冲区，其实也是基于这个思想设计的。

<h5 id="3b485447"><u>回调函数</u></h5>
<u>一个系统的不同模块还可以通过数据耦合、标记耦合的方式进行通信，即通过函数调用过程中的参数传递、返回值来实现模块间通信。</u>

```cpp
// module.c
#include <stdio.h>
int send_data(char *buf, int len) {
    char data[100];
    int i;
    for(i = 0; i < len; i++)
        data[i] = buf[i];
    for(i = 0; i < len; i++)
        printf("received data[%d] = %d\n", i, data[i]);
    return len;
}
// main.c
#include <stdio.h>
#include "module.h"
int main(void) {
    char buffer[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
    int return_data;
    return_data = send_data(buffer, 10);
    printf("send data len:%d\n", return_data);
    return 0;
}
```

通过send_data()函数将main.c模块buffer 中 的 数 据 传 递 到 module.c 模 块 并 进 行 打 印 ， 同 时 通 过send_data()函数的返回值将数据传递的长度信息从module.c模块反馈给main.c模块。

这种通信方式是单向调用的，无法实现双向通信。一个系统通过模块化设计，各个模块之间最理想的关系是一种上下依赖的关系，每一层的模块都是对下一层的封装，并留出API供上一层调用。每一层的模块只能主动调用下一层模块提供的API，然后自己封装成API供上一层的模块调用。但是当底层的模块想主动与上一层的模块进行通信时，该如何实现？

model.h

```cpp
#ifndef RUNCALLBACK_H
#define RUNCALLBACK_H
// 声明回调函数类型
typedef void (*callback_func)(void);
// 声明运行回调函数的函数
void runcallback(callback_func fp);
#endif // RUNCALLBACK_H
```

model.c

```cpp
#include <stdio.h>
#include "module.h"
// 定义运行回调函数的函数
void runcallback(callback_func fp){
    // 调用传入的回调函数
    fp();
}
```

main.c

```cpp
#include <stdio.h>
#include "module.h"
// 定义两个回调函数
void func1(void)
{
    printf("func1...\n");
}
void func2(void)
{
    printf("func2...\n");
}
// 主函数
int main(void)
{
    // 运行回调函数
    runcallback(func1);
    runcallback(func2);
    return 0;
}
```

通过回调函数的设计，两个模块之间可以实现双向通信。模块之间通过函数调用或变量引用产生了耦合，也就有了依赖关系。因此为了 减少模块间的耦合性，我们可以在两个模块之间定义一个抽象接口。

**device_manager.h**

```cpp
#ifndef STORAGE_DEVICE_H
#define STORAGE_DEVICE_H
typedef int (*read_fp)(void);
struct storage_device {
char name[20];
read_fp read;
};
extern int register_device(struct storage_device dev);
extern int read_device(const char* device_name);
#endif // STORAGE_DEVICE_H
```

**device_manager.c**

```cpp
#include <stdio.h>
#include <string.h>
#include "device_manager.h"
struct storage_device device_list[100] = {0};
unsigned char num = 0;
int register_device(struct storage_device dev) {
    device_list[num++] = dev;
    return 0;
}
int read_device(const char* device_name) {
    int i;
    for (i = 0; i < 100; i++) {
        if (!strcmp(device_name, device_list[i].name)) {
            return device_list[i].read();
        }
    }
    printf("Error! Can't find device: %s\n", device_name);
    return -1;
}
```

main.c

```cpp
#include <stdio.h>
#include "device_manager.h"
int sd_read(void) {
    printf("SD read data...\n");
    return 10;
}
int udisk_read(void) {
    printf("Udisk read data...\n");
    return 20;
}
int main(void) {
    struct storage_device sd = {"sdcard", sd_read};
    struct storage_device udisk = {"udisk", udisk_read};
    register_device(sd); // 高层模块函数注册，以便回调
    register_device(udisk);
    read_device("udisk"); // 实现回调, 控制反转
    read_device("sdcard");
    return 0;
}
```

`device_manager.h` 中，我们定义了一个抽象接口 `read_fp`，它是一个函数指针类型，指向一个没有参数并返回 `int` 类型的函数。这个接口允许任何设备实现自己的 `read` 函数，而主模块不需要知道具体的实现细节。

同一个头文件中，我们定义了一个 `struct storage_device` 结构体，它包含一个设备名称和一个指向 `read_fp` 类型函数的指针。这个结构体就是模块间通信的接口。

在 `device_manager.c` 中，实现了 `register_device` 和 `read_device` 函数。`register_device` 函数允许设备注册自己的 `read` 函数，而 `read_device` 函数通过设备名称查找并调用相应的 `read` 函数

<h4 id="30f9829f"><u>异步通信</u></h4>
<u>函数调用，回调函数都是同步阻塞式调用。</u>

CPU在访问一个资源时，如果资源没有准备好需要等待，CPU什 么也不干，原地打转干等就是同步通信，CPU去干其他事情，等资源准 备好了通知CPU，CPU再来访问就是异步通信。

<u>常用的异步通信如下。</u>

<u>● 消息机制：具体实现与平台相关。</u>

<u>● 事件驱动机制：状态机、GUI、前端编程等。</u>

<u>● 中断。</u>

<u>● 异步回调。</u>

<u>在Linux操作系统中，各个模块间也会采用不同的异步通信方式进行通信：Linux内核模块之间可以使用notify机制进行通信；内核和用户之间可以通过AIO、netlink进行通信；用户模块之间异步通信的方</u>

<u>式更多，除了操作系统支持的管道、信号、信号量、消息队列，还可以使用socket、PIPE、FIFO等方式进行异步通信(?)</u>

<h4 id="YFiAQ"><u>问题：</u></h4>
<h5 id="oG7FS"><u>内存泄漏与防范</u></h5>
**<font style="color:#d1a300;">什么是内存泄露？代码举例说明？如何预防内存泄露？如何检测内存泄露（代码示例）？广义上的内存泄露是什么，如何预防？常见的内存错误有哪些？如何调试？</font>**

<h5 id="YVMtQ">**GNU C拓展**</h5>
**<font style="color:#d1a300;">常见的GNU（G-N-U）C拓展语法有哪些？结构体指定初始化是什么？有哪些应用场景？typeof是什么？有哪些应用场景？contaniner of宏是什么？有什么哪些应用场景？</font>**

**<font style="color:#d1a300;">变长数组是什么？有哪些应用场景？为什么不使用指针代替？</font>**

**<font style="color:#d1a300;">__attribute__属性有哪些？</font>**

**<font style="color:#d1a300;">aligned属性有什么用？为什么要用aligned？packed?section?可变参数?weak？oninline和always_inline？什么是内联函数？linux内核中的likely和unlikely？</font>**

<h5 id="bIXpw">**C语言面向对象编程思想**</h5>
**<font style="color:#58a401;">什么是代码复用？什么是分层？C语言如何模拟类？C语言如何模拟继承？linux内核链表如何体现面向对象的特性的？C语言如何实现多态的？</font>**

<h5 id="qqQgL">**C语言模块化编程思想**</h5>
**<font style="color:#58a401;">不同模块如何链接成一个文件？面向对象编程和模块化编程有什么区别？头文件有什么用？头文件重复包含是什么？变量声明和定义有什么区别? extern变量怎么用？goto关键字有什么用？模块设计原则是什么?模块直接耦合的方式有哪些？模块间如何进行通信？</font>**

<h4 id="blP17"><u>思考：</u></h4>
<h5 id="qS5rh">**思考：C++编译的时候可以使用GNU C的规则吗？如noinline或者always_inline？**</h5>
+ <u>C++ 编译时可以使用 GNU C 的规则（如 </u>`noinline`<u> 和 </u>`always_inline`<u>），因为这些是 GCC 提供的扩展特性。</u>
+ <u>如果代码需要跨平台或跨编译器，建议使用条件编译或避免依赖 GNU 扩展特性。</u>
+ <u>性能关键代码中，可以合理使用 </u>`always_inline`<u> 和 </u>`noinline`<u> 来优化或调试代码。</u>

<h1 id="fuRwD"><u>ARM体系结构与汇编语言</u></h1>
<h4 id="qgYty"><u>ARM体系结构</u></h4>
⭐

<u>关联知识点：指令集</u>

<u>计算机的指令集一般可分为4种：复杂指令集(CISC)、精简指令集(RISC) 、显式并行指令集 (EPIC)和超长 指 令 字 指 令 集(VLIW)。嵌入式用的是RISC指令集，RISC指令集相对于CISC指令集，主要有以下特点</u>

<u>●Load/Store架构，CPU不能直接处理内存中的数据，要先将内存中的数据Load（加载）到寄存器中才能操作，然后将处理结果Store(存储)到内存中。</u>

<u>●固定的指令长度，单周期指令。</u>

<u>●倾向于使用更多的寄存器来存储数据，而不是使用内存中的堆栈，效率更高。ARM指令集虽然属于RISC，但是和RISC相比，有一些差异如下：</u>

<u>●ARM有桶型移位寄存器，单周期内可以完成数据的各种移位操作。</u>

<u>●并不是所有的ARM指令都是单周期的。</u>

<u>●ARM有16位的Thumb指令集，是32位ARM指令集的压缩形式，提</u>

<u>高了代码密度。</u>

<u>●条件执行：通过指令组合，减少了分支指令数目，提高了代码</u>

<u>密度。</u>

<u>●增加了DSP、SIMD/NEON等指令。</u>

⭐

<u>关联知识点：用户态、内核态、中断</u>

<u>ARM处理器有多种工作模式，应用程序正常运行时，ARM处理器工作在用户模式，当程序运行出错或有中断发生时，ARM处理器就会切换到对应的特权工作模式。用户模式运行不了特权指令，需要切换到特权模式下才能运行。在ARM处理器中，除了用户模式是普通模式，剩下的几种工作模式都属于特权模式。</u>

<u>在ARM处理器内部，除了基本的算术运算单元、逻辑运算单元、浮点运算单元和控制单元，还有一系列寄存器，包括各种通用寄存器、状态寄存器、控制寄存器，用来控制处理器的运行，保存程序运行时</u>

<u>的各种状态和临时结果。</u>

<u>ARM处理器中的寄存器可分为通用寄存器和专用寄存器两种。</u>

<u>寄存器R0～R12属于通用寄存器，除了FIQ工作模式，在其他工作模式下这些寄存器都是共用、共享的：</u>

1. <u>R0～R3通常用来传递函数参数</u>
2. <u>R4～R11用来保存程序运算的中间结果或函数的局部变量等，R12常用来作为函数调用过程中的临时寄存器。</u>

<u>ARM处理器有多种工作模式，除了这些在各个模式下通用的寄存器，还有一些寄存器在各自的工作模式下是独立存在的，如R13、R14、R15、CPSP、SPSR寄存器，在每个工作模式下都有自己单独的寄存器。</u>

1. <u>R13寄存器又称为堆栈指针寄存器，用来维护和管理函数调用过程中的栈帧变化，R13总是指向当前正在运行的函数的栈帧，一般不能再用作其他用途。</u>
2. <u>R14寄存器又称为链接寄存器，在函数调用过程中主要用来保存上一级函数调用者的返回地址。</u>
3. <u>寄存器R15又称为程序计数器(PC)，保存的地址中取的，每取一次指令，PC寄存器的地址值自动增加。CPU一条一条不停地取指令，程序也就源源不断地一直运行下去。在ARM三级流水线中，PC指针的值等于当前正在运行的指令地址+8，后续的32位处理器虽然流水线的级数不断增加，但为了简化编程，PC指针的值继续延续了这种计算方式。</u>
4. <u>当前处理器状态寄存器（Current Processor State Register CPSR）主要用来表征当前处理器的运行状态。除了各种状态位、标志位，CPSR寄存器里也有一些控制位，用来切换处理器的工作模式和中断使能控制。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443827-030c6f89-7866-4463-af9a-d0d5f661265e.png)

<u>在每种工作模式下，都有一个单独的程序状态保存寄存器（Saved Processor State Register，SPSR）。当ARM处理器切换工作模式或发生异常时，SPSR用来保存当前工作模式下的处理器现场，即将CPSR寄存器的值保存到当前工作模式下的SPSR寄存器。当ARM处理器从异常返回时，就可以从SPSR寄存器中恢复原先的处理器状态，切换到原来的工作模式继续运行。</u>

<u>在ARM所有的工作模式中，有一种工作模式比较特殊，即FIQ模式。为了快速响应中断，减少中断现场保护带来的时间开销，在FIQ工作模式下，ARM处理器有自己独享的R8～R12寄存器。</u>

<h4 id="MeiIy"><u>ARM汇编指令</u></h4>
一个完整的ARM指令通常由操作码+操作数组成，指令的编码格式如下。

```cpp
<opcode>{<cond>{s} <Rd>,<Rn>{,<operand2>}}
```

<u>● 使用<>标起来的是必选项,使用{}标起来的是可选项。</u>

<u>● <opcode>是二进制机器指令的操作码助记符，如MOV、ADD这些</u>

<u>汇编指令都是操作码的指令助记符。</u>

<u>● cond：执行条件，ARM为减少分支跳转指令个数，允许类似BEQ、BNE等形式的组合指令。</u>

<u>● S：是否影响CPSR寄存器中的标志位，如SUBS指令会影响CPSR寄存器中的N、Z、C、V标志位，而SUB指令不会。</u>

<u>● Rd：目标寄存器。</u>

<u>● Rn：第一个操作数的寄存器。</u>

<u>● operand2：第二个可选操作数，灵活使用第二个操作数可以提</u>

<u>高代码效率。</u>

<h5 id="p3dw3"><u>存储访问指令</u></h5>
<u>ARM指令集属于RISC指令集，RISC处理器采用典型的加载/存储体系结构，CPU无法对内存里的数据直接操作，只能通过Load/Store指令来实现：当需要对内存中的数据进行操作时，要首先将这个数据从内存加载到寄存器，然后在寄存器中对数据进行处理，最后将结果重新存储到内存中。</u>

<u>ARM处理器属于冯·诺依曼架构，程序和数据都存储在同一存储器上，内存空间和I/O空间统一编址，ARM处理器对程序指令、数据、I/O空间中外设寄存器的访问都要通过Load/Store指令来完成。</u>

```cpp
LDR R1,[RO]; 将R中的值作为地址，将该地址上的数据保存到R1
STR R1,[RO];  将R中的值作为地址，将R1中的值存储到这个内存地址;每次读写一字节，LDR/STR默认每次读写4字节
    LDRB/STRB;  批量加载/存储指令，在一组寄存器和一片内存之间传输数据
SWPR1,R1,[R0];  将R1与R中地址指向的内存单元中的数据进行交换
SWPR1,R2,[R0];  将[R0]存储到R1，将R2写入[R0]这个内存存储单元LDM/STM
```

<u>LDR/STR、LDM/STM两对指令经常使用。</u>

<u>LDR/STR指令是ARM汇编程序中使用频率最高的一对指令。</u>

<u>LDM/STM指令常用来加载或存储一组寄存器到一片连续的内存，通过和堆栈格式符组合使用，LDM/STM指令还可以用来模拟堆栈操作。</u>

<u>将一组寄存器入栈，或者从栈中弹出一组寄存器。</u>

```cpp
LDMFD SP!,{R0-R2,R14}; 将内存栈中的数据依次弹出到R14，R2，R1，RO
STMFD SP!{RO-R2,R14}; 将R，R1，R2，R14依次压入内存栈
```

<u>ARM还专门提供了PUSH和POP指令来执行栈元素的入栈和出栈操作。</u>

```cpp
PUSH {R0-R2,R14} ；将 R0、R1、R2、R14依次压入栈
    POP {R0-R2,R14}   ；将栈中的数据依次弹出到R14、R2、R1、R0
```

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811443876-3d269de3-4142-48cc-8d3a-4e82742f6bd2.png)

<u>在一个堆栈内存结构中，如果堆栈指针SP总是指向栈顶元素，那么这个栈就是满栈；如果堆栈指针SP指向的是栈顶元素的下一个空闲的存储单元，那么这个栈就是空栈。</u>

<u>每入栈一个元素，栈指针SP都会往栈增长的方向移动一个存储单元。如果栈指针SP从高地址往低地址移动，那么这个栈就是递减栈；如果栈指针SP从低地址往高地址移动，那么这个栈就是递增栈。</u>

<h5 id="hLLTL"><u>数据传送指令</u></h5>
<u>LDR/STR指令用来在寄存器和内存之间输送数据。想要在寄存器之间传送数据，则可以使用MOV指令。</u>

```cpp
MOV {cond} {s} Rd, operand2
    MVN {cond} {S} Rd, operand2
```

<u>如果想要在寄存器之间传送数据，则可以使用MOV指令。MVN指令用来将操作数operand2按位取反后传送到目标寄存器Rd。</u>

```cpp
MOV R1，#1   ;将立即数1传送到寄存器R1中
    MOV R1, RO   ;将R寄存器中的值传送到R1寄存器中
MOV PC, LR   ;子程序返回
MVN RO，#xFF ;将立即数 0xFF 取反后赋值给 R
MVN RO, R1   ;将R1寄存器的值取反后赋值给R
```

<h5 id="vQCzs"><u>算术逻辑运算指令</u></h5>
<u>算术运算指令包括基本的加、减、乘、除，逻辑运算指令包括与、或、非、异或、清除等</u>

```cpp
ADD {cond} {S} Rd, Rn, operand2 ;加法
ADC {cond} {S} Rd, Rn, operand2 ;带进位加法
SUB {cond} {S} Rd, Rn, operand2 ;减法
AND {cond} {S} Rd, Rn, operand2 ;逻辑与运算
ORR {cond} {S} Rd, Rn, operand2 ;逻辑或运算
EOR {cond} {S} Rd, Rn, operand2 ;异或运算
BIC {cond} {S} Rd, Rn, operand2 ;位清除指令
```

<u>算术逻辑运算指令的基本使用方法及说明如下</u>

```cpp
ADD R2，R1，#1 ; R2=R1+1
    ADC R1，R1，#1 ; R1=R1+1+C(其中C为CPSR寄存器中进位)
    SUB R1, R1, R2 ; R1=R1-R2 
    SBC R1,R1,R2 ;R1=R1-R2-C
    AND RO,RO,#3 ; 保留 R的 bit0和 1，其余位清除
    ORR RO,RO,#3 ; 置位 R0的 bit0 和 bit1
EOR RO,RO,#3 ; 反转 R0中的 bit 和 bit1
    BIC RO,RO,#3 ;  清除 R0中的 bit0和 bit1
```

<u>操作数：operand2详解</u>

<u>.......</u>

<h4 id="dDYe3"><u>ARM寻址方式</u></h4>
<u>不同的ARM指令又有不同的寻址方式，比较常见的寻址方式有寄存器寻址、立即寻址、寄存器偏移寻址、寄存器间接寻址、基址寻址、多寄存器寻址、相对寻址等.</u>

<h5 id="Yy7vi"><u>寄存器寻址</u></h5>
<u>寄存器寻址比较简单，操作数保存在寄存器中，通过寄存器名就可以直接对寄存器中的数据进行读写.</u>

```cpp
MOV R1, R2 ;将寄存器R2中的值传送到R1
ADD R1，R2，R3 ;运行减法运算R2-R3，并将结果保存到R1中
```

<h5 id="Xtxdo"><u>立即数寻址</u></h5>
```cpp
ADD R1，R1，#1 ;将R1寄存器中的值加1，并将结果保存到R1中
ADDR1，R1，#16，20; R1=R1+立即数16循环右移20位
    MOV R1，#xFF ;将十六进制常数0xFF写到R1寄存器中
    MOV R1，#12 ; 将十进制常数12放到R1寄存器中
```

<h5 id="tcy02"><u>寄存器偏移寻址</u></h5>
<h5 id="zpFOk"><u>寄存器间接寻址</u></h5>
<u>寄存器间接寻址主要用来在内存和寄存器之间传输数据。寄存器中保存的是数据在内存中的存储地址，通过这个地址就可以在寄存器和内存之间传输数据。C语言中的指针操作，在汇编层次其实就是使用寄存器间接寻址实现的。</u>

```cpp
LDRR1,[R2]; 将R2中的值作为地址，取该内存地址上的数据，保存到R1
STRR1,[R2]; 将R2中的值作为地址，将R1寄存器的值写入该内存地址
```

<h5 id="gsKnE"><u>基址寻址</u></h5>
<u>基址寻址其实也属于寄存器间接寻址。两者的不同之处在于,基址寻址将寄存器中的地址与一个偏移量相加，生成一个新地址，然后基于这个新地址去访问内存.</u>

```cpp
LDRR1，[FP，#2]     ;将FP中的值加2作为新地址，取该地址上的值保存到R1
LDR R1，[FP，#2]!   ; FP=FP+2，然后将FP指定的内存单元数据保存到R1中
    LDRR1，[FP，R0]     ;将FP+R0作为新地址，取该地址上的值保存到 R1
    LDR R1，[FP,RO,LSL#2];将FP+R0<<2作为新地址，读取该内存地址上的值保存到 R1
    LDR R1，[FP]，#2   ;将FP中的值作为地址，读取该地址上的值保存到R1，然后 FP 中的值加 2
    STRR1，[FP，#-2]   ;将FP中的值减 2，作为新地址，将 R1中的值写入该地址
STR R1，[FP]，#-2] ;将FP中的值作为地址，将R1中的值写入此地址，然后FP中的值减2
```

<u>基址寻址一般用在查表、数组访问、函数的栈帧管理等场合。根据偏移量的正负，基址寻址又可以分为向前索引寻址和向后索引寻址.</u>

<h5 id="eLNnj"><u>多寄存器寻址</u></h5>
<u>STM/LDM指令就属于多寄存器寻址，一次可以传输多个寄存器的值。</u>

```cpp
LDMIA SP!,{R0-R2,R14};将内存栈中的数据依次弹出到 R14、R2、R1、RO
STMDB SP!,{RO-R2,R14};将RO、R1、R2、R14 依次压入栈
LDMFD SP!,{R0-R2,R14};将内存栈中的数据依次弹出到 R14、R2、R1、R0
STMFDSP!,{RO-R2,R14};将R、R1、R2、R14 依次压入栈
```

<u>在多寄存器寻址中，用大括号{}括起来的是寄存器列表，寄存器之间用逗号隔开，如果是连续的寄存器，还可以使用连接符连接，如R0-R3，就表示R0、R1、R2、R3这4个寄存器。LDM/STM指令一般和IA、IB、DA、DB组合使用，分别表示Increase After、Increase Before、Decrease After、Decrease Before。LDM/STM指令也可以和FD、ED、FA、EA组合使用，用于堆栈操作。</u>

<h5 id="Uvtxk"><u>相对寻址</u></h5>
<u>相对寻址属于基址寻址，只不过是基址寻址的一种特殊情况。</u>

<u>以PC指针作为基地址进行寻址，以指令中的地址差作为偏移，两者相加后得到的就是一个新地址，然后可以对这个地址进行读写操作。</u>

<u>ARM中的B、BL、ADR指令都是采用相对寻址的。</u>

<u>很多与位置无关的代码，如动态链接共享库，其在汇编代码层次的实现其实也是采用相对寻址的。程序中使用相对寻址访问的好处是不需要重定位，将代码加载到内存中的任何地址都可以直接运行。</u>

<h4 id="gEcbn"><u>ARM伪指令</u></h4>
<u>ARM伪指令不是ARM指令集中定义的标准指令，而是为了编程方便，编译器厂商自定义的一些辅助指令。在程序编译时，这些伪指令会被翻译为一条或多条ARM标准指令。常见的ARM伪指令主要有4个：ADR、ADRL、LDR、NOP。</u>

<h5 id="swNpu"><u>LDR伪指令</u></h5>
<u>LDR伪指令的主要用途是将一个32位的内存地址保存到寄存器中 。</u>

<u>RISC指令的特点是单周期指令，指令的长度固定。在一个32位的系统中，一条指令通常是32位的，指令中包括操作码和操作数。</u>

<u>指令中的操作码和操作数共享32位的存储空间：一般前面的操作码要占据几个比特位，剩下来的留给操作数的编码空间就小于32位。当编译器遇到MOV R0，＃0x30008000这条指令时，后面的操作数是32位，编译器就无法对这条指令进行编码了。为了解决这个难题，编译器提供了一个LDR伪指令来完成上面的功能。</u>

<u>LDR不是普通的ARM加载指令，而是一个伪指令。为了与ARM指令集中的加载指令LDR区别开来，LDR伪指令中的操作数前一般会有一个等于号=，用来表示该指令是个伪指令。通过LDR伪指令，编译器就解决了向一个寄存器传送32位的立即数时指令无法编码的难题。</u>

```cpp
LDR R，=0x30008000;  有=号的就是伪指令，将立即数x30008000送到R0
LDR RO， =LOOP ；将标号LOOP表示的地址送到R0
LDR RO，[R1] ；R1中的值作为地址，将该地址上的值送到R0
LDR RO，LOOP ；将标号LOOP表示的内存地址上的数据送到R0
```

<h5 id="U1SaV"><u>ADR伪指令</u></h5>
```cpp
START
ADR R0, LOOP     ; 将标号 LOOP 对应的地址加载到寄存器 R0 中
B END            ; 跳转到 END 标签，结束程序
LOOP
NOP              ; 一个空操作，作为示例使用
B LOOP           ; 无限循环
```

**ADR R0, LOOP**<u>：这一行使用了 </u>`ADR`<u> 伪指令，它将标号 </u>`LOOP`<u> 的地址加载到寄存器 </u>`R0`<u> 中。</u>`ADR`<u> 指令会计算当前指令地址与标号 </u>`LOOP`<u> 之间的偏移量，然后通过相对寻址将 </u>`LOOP`<u> 的地址加载到 </u>`R0`<u> 中。</u><u>ADR伪指令的功能与LDR伪指令类似，将基于PC相对偏移的地址值读取到寄存器中。ADR为小范围的地址读取伪指令，底层使用相对寻址来实现，因此可以做到代码与位置无关。</u>

<u>编译器在编译ADR伪指令时，会首先计算出当前正在执行的ADR伪指令地址与标号LOOP之间的地址偏移OFFSET，然后使用ARM指令集中的一条标准指令代替。</u>

<h4 id="iRta0"><u>ARM汇编程序设计</u></h4>
<h5 id="ftOpm"><u>ARM汇编程序格式</u></h5>
<u>ARM汇编程序是以段（section）为单位进行组织的。在一个汇编文件中，可以有不同的section，分为代码段、数据段等，各个段之间相互独立，一个ARM汇编程序至少要有一个代码段。可以使用AREA伪操作来标识一个段的起始、段名和段的读写属性。</u>

```cpp
AREA COPY, CODE, READONLY   ; 当前段属性为代码段，只读，段名为 COPY
ENTRY
START
LDR R0, =SRC            ; 将源地址 SRC 加载到寄存器 R0 中
LDR R1, =DST            ; 将目标地址 DST 加载到寄存器 R1 中
MOV R2, #10             ; 将值 10 加载到寄存器 R2 中
    LOOP
    LDR R3, [R0], #4        ; 从 R0 地址加载一个字到 R3 中，并将 R0 增加 4
    STR R3, [R1], #4        ; 将 R3 中的值存储到 R1 指向的地址，并将 R1 增加 4
    SUBS R2, R2, #1         ; 将 R2 减 1，并设置条件标志
BNE LOOP                ; 如果 R2 不为 0，则跳转回 LOOP
AREA COPYDATA, DATA, READWRITE ; 数据段，读写权限，段名为 COPYDATA
SRC DCD 1,2,3,4,5,6,7,8,9,0  ; 源数据数组
DST DCD 0,0,0,0,0,0,0,0,0,0  ; 目标数据数组，用于存放复制后的数据
END
```

<u>在汇编程序中，使用分号；来注释代码</u>

<h5 id="CsbE0"><u>符号与标号</u></h5>
<u>使用符号来标识一个地址、变量或数字常量。当用符号来标识一个地址时，这个符号通常又被称为标号。符号的命名规则和C语言的标识符命名规则一样：由字母、数字和下画线组成，符号的开头不能使用数字，但标号除外。标号比较任性，标号的开头不仅可以是数字，甚至整个标号可以是一个纯数字。</u>

**局部标号**

<u>局部标号用于标记程序中的特定位置，以便在该位置附近进行跳转或引用。与全局标号不同，局部标号的作用域通常仅限于当前段或当前范围内，不会影响到其他代码段。局部标号常常使用数字（如 </u>`0`<u>, </u>`1`<u>, </u>`2`<u> 等）来命名，并通过特定的格式来引用。</u>

**作用域有限:**<u>局部标号的作用域只在当前段内有效。这意味着同一个局部标号可以在不同的段中重复使用，而不会产生冲突。</u>

**命名方式简单:**<u>局部标号通常使用数字命名，如 </u>`0`<u>, </u>`1`<u>, </u>`2`<u> 等，这使得它们在短距离跳转和循环结构中非常方便。</u>

**引用格式**<u>：引用局部标号时，使用 </u>`%`<u> 符号加上 </u>`B`<u>（向后搜索）或 </u>`F`<u>（向前搜索）来确定跳转方向。</u>

<u>如果未指定 </u>`F`<u> 或 </u>`B`<u>，编译器会默认先向后搜索，如果找不到，再向前搜索。</u>

```cpp
MOV R0, #10       ; 将值 10 存入寄存器 R0 中
0   SUBS R0, R0, #1   ; 将 R0 减 1，并设置条件标志
    BNE %B0           ; 如果 R0 不为零，则跳转回局部标号 0
```

<h5 id="qcLuW"><u>伪操作</u></h5>
<u>伪操作（也称为伪指令）是在汇编语言中使用的一类特殊指令，用来辅助编写和组织汇编代码。与真正的机器指令不同，伪操作并不会直接转换为机器码，而是为汇编器提供了指示，用于控制汇编过程、数据定义、段定义以及程序结构管理等功能。伪操作主要用于提高代码的可读性和结构化，让程序员更方便地编写和管理汇编程序。</u>

**符号定义：**<u>使用伪操作定义变量、常量或符号。例如，可以使用 </u>`EQU`<u> 指令将一个符号绑定到一个数值或表达式上。</u>

**数据定义**<u>：用于定义数据段中的变量和常量。例如，</u>`DCD`<u>、</u>`DCB`<u>、</u>`SPACE`<u> 等伪操作用来在内存中分配特定的数据空间。</u>

**程序结构控制**<u>：用于控制汇编程序的流程和组织。例如，</u>`AREA`<u> 用于定义段（section），</u>`ENTRY`<u> 用于指定程序的入口点，</u>`EXPORT`<u> 和 </u>`IMPORT`<u> 用于声明全局符号和导入其他模块中的符号。</u>

**模块化编程**<u>：伪操作可以用于定义汇编子程序，并通过伪操作声明全局符号，以便在主程序或其他程序中调用这些子程序。</u>

<u>以下是一些常用的伪操作及其使用方法：</u>

**AREA**<u>：定义一个段或区域。</u>

```cpp
AREA MyCode, CODE, READONLY
```

**DCD**<u>：定义一个32位常量。</u>

```cpp
DCD 1, 2, 3, 4
```

**DCB**<u>：定义一个字节常量。</u>

```cpp
DCB 'A', 'B', 'C'
```

**EQU**<u>：定义一个符号常量。</u>

```cpp
MyValue EQU 10
```

**EXPORT**<u>：将符号声明为全局符号，允许其他模块访问。</u>

```cpp
EXPORT MyFunction
```

**IMPORT**<u>：导入外部模块中的符号。</u>

```cpp
IMPORT ExternalFunction
```

**ENTRY**<u>：指定程序的入口点。</u>

```cpp
ENTRY
```

**SPACE：**<u>在内存中分配一定数量的字节。</u>

```cpp
SPACE 16 ;分配16字节
```

<u>伪操作的作用</u>

<u>伪操作的主要作用是帮助汇编器组织和处理汇编代码，而不是转换成机器码。它们在汇编代码的预处理中起到重要作用，使代码更加灵活和易于维护。例如，使用 </u>`EXPORT`<u> 和 </u>`IMPORT`<u> 伪操作，可以轻松实现模块化编程，使得不同的汇编程序模块可以相互调用。</u>

<h4 id="Q7kuz"><u>C语言和汇编语言混合编程</u></h4>
<h5 id="jO193"><u>ATPCS规则</u></h5>
<u>ATPCS的全称是ARM-Thumb Procedure Call Standard，核心内容就是定义ARM子程序调用的基本规则及堆栈的使用约定等。</u>

<u>如ATPCS规定了ARM程序要使用满递减堆栈，入栈/出栈操作要使用STMFD/LDMFD指令，只要所有的程序都遵循这个约定，ARM程序的格式也就统一了，编写的ARM程序也就可以在各种各样的ARM处理器上运行。</u>

<u>子程序间要通过寄存器R0～R3（可记作a0～a3）传递参数，当参数个数大于4时，剩余的参数使用堆栈来传递。</u>

<u>●子程序通过R0～R1返回结果。</u>

<u>●子程序中使用R4～R11（可记作v1～v8）来保存局部变量。</u>

<u>●R12作为调用过程中的临时寄存器，一般用来保存函数的栈帧</u>

<u>基址，记作FP。</u>

<u>●R13作为堆栈指针寄存器，一般记作SP。</u>

<u>●R14作为链接寄存器，用来保存函数调用者的返回地址，记作LR。</u>

<u>●R15作为程序计数器，总是指向当前正在运行的指令，记作PC。</u>

<u>在ARM平台下，无论是C程序，还是汇编程序，只要大家遵守ARM子程序之间的参数传递和调用规则，就可以很方便地在一个C程序中调用汇编子程序，或者在一个汇编程序中调用C程序。</u>

```cpp
AREA    SumFunc, CODE, READONLY
EXPORT  sum           ; 声明sum为全局函数，使其可以被C代码调用
sum     PROC
;输入：R0 和 R1 为两个加数
;输出：R0 为和
ADD     R0, R0, R1    ; 执行加法操作，将结果存储到R0中
BX      LR            ; 返回调用者
ENDP
END

#include <stdio.h>
extern int sum(int a, int b);  // 声明汇编函数

int main() {
    int result = sum(5, 7);    // 调用汇编函数sum
    printf("The result is: %d\n", result);  // 打印结果
    return 0;
}
```

**无条件跳转:**`BX`<u>指令将控制权转移到指定的地址(寄存器中的值)。</u>

<h5 id="PbSfC"><u>在C程序中内嵌汇编代码</u></h5>
<u>为了能在C程序中内嵌汇编代码，ARM编译器在ANSI C标准的基础上扩展了一个关键字__asm。通过这个关键字,可以在C程序中内嵌ARM汇编代码。</u>

```cpp
int src[10] = {1,2,3,4,5,6,7,8,9};
int dst[10] = {0};
int data_copy_c(void){
    for(int i = 0; i < 10; i++)
        dst[i] = src[i];
    return 0;
}
int data_copy_asm(void){
__asm
{
LDR R0, =src
LDR R1, =dst
MOV R2, #10
LOOP:
LDR R3, [R0], #4
STR R3, [R1], #4
SUBS R2, R2, #1
BNE LOOP
}
}
```

<h5 id="mFJr3"><u>在汇编程序中调用C程序</u></h5>
<u>在汇编程序中同样也可以调用C程序。在调用的时候，我们要注意根据ATPCS规则来完成参数的传递，并配置好C程序传递参数和保存局部变量所依赖的堆栈环境，然后使用BL指令直接跳转即可。</u>

<h4 id="aMPVh"><u>GNU ARM汇编语言</u></h4>
<u>........</u>

<h1 id="EFX6F"><u>内存堆栈管理</u></h1>
👋

关联知识点：

程序地址空间：[<u>https://kdocs.cn/l/cjeGfIOJleoy?linkname=ZoO9Iu52pZ</u>](https://kdocs.cn/l/cjeGfIOJleoy?linkname=ZoO9Iu52pZ)

malloc原理：[<u>https://kdocs.cn/l/cjeGfIOJleoy?linkname=SxljDaCa3X</u>](https://kdocs.cn/l/cjeGfIOJleoy?linkname=SxljDaCa3X)

垃圾回收：[<u>https://kdocs.cn/l/cjeGfIOJleoy?linkname=sTJaIsjKQl</u>](https://kdocs.cn/l/cjeGfIOJleoy?linkname=sTJaIsjKQl)

<h4 id="YJixm"><u>内存泄漏与防范</u></h4>
**<font style="color:#d1a300;">什么是内存泄露？代码举例说明？如何预防内存泄露？如何检测内存泄露（代码示例）？广义上的内存泄露是什么，如何预防？</font>**

**<font style="color:#d1a300;">常见的内存错误有哪些？如何调试？</font>**

内存泄漏

<u>如果使用malloc()申请的内存在使用结束后没有及时被释放，则C标准库中的内存分配器ptmalloc和内核中的内存管理子系统都失去了对这块内存的追踪和管理。</u>

<u>这里的使用结束指的是程序不需要访问这段内存，长期运行的程序可能会因为内存泄露导致程序崩溃，但是程序结束后操作系统会回收该进程的所有资源。</u><u>  
</u><u>操作系统为每个进程分配独立的虚拟地址空间，进程结束时，（内存、文件描述符、网络连接等）。</u>

```cpp
char *p;
p=(char *)malloc(32);
strcpy(p,“hello");
没有free p
```

<u>在函数退出之前，如果我们没有使用free()函数及时 将 这 块 内 存 归 还 给 内 存 分 配 器 ptmalloc或内存管理子系统，ptmalloc和内存管理子系统就失去了对这块内存的控制权，它们可能认为用户还在使用这片内存。等下次去申请内存时，内存分配器和内存管理子系统都没有这块内存的信息，所以不可能把这块内存再分配给用户使用。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811444197-92c65e80-5391-4927-b38d-e569a6705e20.png)

<u> 图中有大小为548 Byte和504 Byte的两个内存块，一开始这两个内存块是在空闲链表中的，当用户使用malloc()申请内存时，内存分配器ptmalloc将这两个内存块节点从空闲链表中摘除，并把内存块的地址返给用户使用。如果用户使用后忘了归还，那么空闲链表中就没有这两个内存块的信息，这两块内存也就无法继续使用了，在内存中就产生了两个漏洞,即发生内存泄漏。</u>

<h5 id="DZeUl"><u>预防内存泄漏</u></h5>
<u>预防内存泄漏：内存申请后及时地释放，两者要配对使用，内存释放后要及时将指针设置为NULL，使用内存指针前要进行非空判断。</u>

<h5 id="iOJg9"><u>内存泄漏检测：MTrace</u></h5>
<u>MTrace，Valgrind，Dmalloc，purify，KCachegrind，MallocDebug</u>

```cpp
#include <mcheck.h>
void mtrace(void);
void muntrace(void);
```

<u>如果想检测一段代码是否有内存泄漏，则可以把mtrace和muntrace两个函数添加到要检测的程序代码中。</u>

```cpp
...
    #include <mcheck.h>
    int main (void){
        mtrace();//开启跟踪
        char *p,*q;
        p =(char *)malloc(8); q =(char *)malloc(8);
        strcpy(p, “hello”);
        strcpy(q,“world”);
        free(p);
        muntrace();//关闭跟踪
        return 0;
    }
```

<u>根据动态内存的使用记录，我们可以很快定位到内存泄漏发生在mcheck.c文件中的第11行代码。</u>

```cpp
#mtrace a.out mtrace.log
Memory not freed:
address Size Caller
0x0901a380 0x8 at /home/c/mem leak/mcheck.c:11
```

<h5 id="OUqoW"><u>广义上的内存泄漏</u></h5>
<u>广义上的内存泄漏指系统频繁地进行内存申请和释放，导致内存碎片越来越多，无法再申请一片连续的大块内存。如fast bins，主要用来保存用户释放的小于80 Bytes(M_MXFAST)的内存，在提高内存分配效率的同时，带来了大量的内存碎片。</u>

<u>为了最大化地提高系统性能，我们可以通过一些参数对glibc的内存分配器进行调整，使之与实际业务需求达到更大的匹配度,更高效地应对实际业务的需求。</u>

<u>glibc底层实现了一个</u><u>mallopt()函数，可以通过这个函数对上面的各种参数进行调整。</u>

```cpp
#include <malloc.h>
int mallopt(int param, int value);
```

<h4 id="izUoV"><u>常见的内存错误及检测</u></h4>
<u>处理器引入MMU后，操作系统接管了内存管理的工作，负责虚拟空间和物理空间的地址映射和权限管理。操作系统的内存管理子系统将一个进程的虚拟空间划分为不同的区域，如代码段、数据段、BSS段、堆、栈、mmap映射区域、内核空间等，每个区域都有不同的读、写、执行权限。(见内存管理)</u>

<u>对于应用程序来说，常见的内存错误一般主要分为以下几种类型：</u><u>段错误，内存越界、内存踩踏、多次释放、非法指针。</u>

<h5 id="wNffe"><u>段错误</u></h5>
<u>通过内存管理，每个区域都有具体的访问权限，如只读、读写、禁止访问等。数据段、BSS段、堆栈区域都属于读写区，而代码段则属于只读区,如果往代码段的地址空间上写数据,就会发生一个段错误。</u>

<u>当我们往一个只读区域的地址空间执行写操作时，或者访问一个禁止访问的地址（如零地址）时，都会发生段错误。内核空间、零地址、堆和mmap区域之间的内存空间，这部分地址空间要么被内核占用，要么还处于“未开发”状态，需要申请才能使用。</u>

<u>（1）</u><u>在调试链表时，通常通过指针来操作每一个节点。如果指针在遍历链表时已经指向链表的末尾或头部，指针已经指向NULL了，此时再通过该指针去访问节点的成员，就相当于访问零地址了，也会发生一个段错误，这个指针也就变成了非法指针。</u>

<u>（2）</u><u>每一个用户进程默认有8MB大小的栈空间，如果在函数内定义大容量的数组或局部变量，就可能造成栈溢出，会引发一个段错误。内核中的线程也是如此，每一个内核线程只有8KB的内核栈，在实际使用中也要非常小心，防止堆栈溢出。</u>

<u>（3）</u><u>使用malloc()申请的堆内存，如果不小心多次使用free()进行释放，通常也会触发一个段错误。</u>

<u>由于C语言语法检查的宽松性，程序中对内存访问的各种操作并不报错，或者给一个警告信息，这会导致程序在运行期间出现段错误时很难定位。此时我们可以借助一些第三方工具来快速定位段错误。</u>

<h6 id="qPiEC"><u>使用core dump调试段错误</u></h6>
<u>在Linux环境下运行的应用程序，由于各种异常或Bug，会导致程序退出或被终止运行。</u><u>此时系统会将该程序运行时的内存、寄存器状态、堆栈指针、内存管理信息、各种函数的堆栈调用信息保存到一个core文件中。</u>

<u>core dump功能开启后运行a.out，发生段错误后就会在当前目录下生成一个core文件，然后我们就可以使用gdb来解析这个core文件来定位程序到底出错在哪里。在GDB交互环境下，我们通过bt查看调用栈信息，可以查看错误的具体行数。</u>

<h5 id="WlhF5"><u>内存踩踏</u></h5>
<u>比如申请两块动态内存，对其中的一块内存写数据时产生了溢出，就会把溢出的数据写到另一块缓冲区里。在缓冲区释放之前，系统是不会发现任何错误的，也不会报任何提示信息，但是程序却可能因为误操作，覆盖了另一块缓冲区的数据，造成程序莫名其妙的错误</u><u>。</u>

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main (void){
    char *p,*q;
    p= malloc(16);
    9= malloc(16);
    strcpy(p, "hello world! hello zhaixue.cc!\n");
    printf("%s\n",p);
    printf("%s\n"，q);
    while (1);
    free(q);
    free(p);
    return 0;
}
```

<u>如果一个进程中有多个线程，多个线程都申请堆内存，这些堆内存就可能彼此相邻，使用时需要谨慎，提防越界。在内核驱动开发中，驱动代码运行在特权状态，对内存访问比较自由，多个驱动程序申请的物理内存也可能彼此相邻。</u>

<h6 id="Oh2Cw"><u>内存踩踏监测：mprotect</u></h6>
<u>mprotect()是Linux环境下一个用来保护内存非法写入的函数，它会监测要保护的内存的使用情况，一旦遇到非法访问就立即终止当前。</u><u>进程的运行，并产生一个core dump。</u>

```cpp
#include <sys/mman.h>
int mprotect(void *addr, size t len, int prot);
```

<u>mprotect()函数的第一个参数为要保护的内存的起始地址，len表示内存的长度，第三个参数prot表示要设置的内存访问权限。</u>

<h6 id="QlhI0"><u>内存检测神器：Valgrind</u></h6>
<u>Valgrind包含一套工具集，其中一个内存检测工具Memcheck可以对我们的内存进行内存覆盖、内存泄漏、内存越界检测。</u>

<h1 id="l4FF9"><u>GNU C编译器扩展语法</u></h1>
<font style="color:#078654;">👋</font>

**<font style="color:#078654;">关联知识点：</font>**

**<font style="color:#078654;">驱动开发file_operation</font>**

**<font style="color:#078654;">C++11类型推导(auto，decltype)</font>**

**<font style="color:#078654;">套接字缓冲区(Socket Buffer)</font>**

**<font style="color:#078654;">USB驱动usb request block</font>**

**<font style="color:#d1a300;">常见的GNU（G-N-U）C拓展语法有哪些？结构体指定初始化是什么？有哪些应用场景？typeof是什么？有哪些应用场景？contaniner of宏是什么？有什么哪些应用场景？</font>**

**<font style="color:#d1a300;">变长数组是什么？有哪些应用场景？为什么不使用指针代替？</font>**

**<font style="color:#d1a300;">__attribute__属性有哪些？</font>**

**<font style="color:#d1a300;">aligned属性有什么用？为什么要用aligned？packed?section?可变参数?weak？oninline和always_inline？什么是内联函数？linux内核中的likely和unlikely？</font>**

<h4 id="caPSz"><u>C语言标准和编译器</u></h4>
<u>C语言标准因为是在1989年发布的，所以人们一般称其为C89或C90标准，或者叫作ANSI C标准。</u>

<h5 id="pEAp6"><u>C语言标准的内容</u></h5>
<u>C语言编程的一些语法惯例、约定规则，在C语言标准里：</u>

<u>● 定义各种关键字、数据类型。</u>

<u>● 定义各种运算规则、各种运算符的优先级和结合性。</u>

<u>● 数据类型转换。</u>

<u>● 变量的作用域。</u>

<u>● 函数原型、函数嵌套层数、函数参数个数限制。</u>

<u>● 标准库函数接口。</u>

<u>程序员开发程序时，按照这种标准规定的语法规则编写程序；编译器厂商开发编译</u>

<u>器工具时，也按照这种标准去解析、翻译程序。</u>

<h5 id="lzp3q"><u>C语言标准的发展过程</u></h5>
<u>ANSI C统一了各大编译器厂商的不同标准，并对C语言的语法和特性做了一些扩展，在1989年发布的一个标准。这个标准一般也叫作C89/C90标准，也是目前各种编译器默认支持的C语言标准。</u>

<u>C99标准是ANSI在1999年基于C89标准发布的一个新标准。</u>

<u>C11标准是ANSI在2011年发布的最新C语言标准，C11标准修改了C语言标准的一些bug，增加了一些新特性。目前绝大多数编译器还不支持，暂时还用不到。</u>

<h5 id="cQ93L"><u>编译器对C语言标准的支持</u></h5>
<u>目前对C99标准支持最好的是GNU C编译器。 </u>

<h5 id="I3XnT"><u>编译器对C语言标准的扩展</u></h5>
<u>不同编译器，出于开发环境、硬件平台、性能优化的需要，除了支持C语言标准，还会自己做一些扩展。</u>

<u>如GCC编译器也对C语言标准做了很多扩展。零长度数组，语句表达式，内建函数，__attribute__特殊属性声明.....这些新增的特性，C语言标准目前是不支持的，其他编译器也不支持。</u>

<h4 id="pi5yl"><u>指定初始化</u></h4>
<h5 id="OPQLO"><u>指定初始化数组</u></h5>
<u>C语言标准初始化数组</u>

```cpp
int a[10]={0,1,2,3,4,5,6,7,8};
```

<u>a[9]默认为0.</u>

```cpp
int b[100]={[10]=1,[30]=2};
```

<u>通过数组元素索引，我们可以直接给指定的数组元素赋值。在GNU C中，通过数组元素索引，可以直接给指定的几个元素赋值。</u>

<u>给数组中某一个索引范围的数组元素初始化</u>

```cpp
int main(void)
{
    int b[100] = {[10...30] = 1, [50...60] = 2};
    for(int i = 0; i < 100; i++)
        {
            printf("%d", a[i]);
            if (i % 10 == 0)
                printf("\n");
        }
    return 0;
}
```

<u>使用[10...30]表示一个索引范围，给a[10]到a[30]之间的20个数组元素赋值为1。</u>

<u>GNU C支持使用...表示范围扩展，这个特性不仅可以使用在数组初始化中，也可以使用在switch-case语句中。</u>

```cpp
#include <stdio.h>
int main(void)
{
    int i = 4;
    switch(i){
        switch(i){
            case 1:
                printf("1\n");
                break;
            case 2...8:
                printf("%d\n", i);
                break;
            case 9:
                printf("9\n");
                break;
            default:
                printf("default!\n");
                break;
        }
    }
    return 0;
}
```

<h5 id="WwiZf"><u>指定初始化结构体成员()</u></h5>
<u>在GNU C中我们可以通过结构域来指定初始化某个成员。</u>

```cpp
#include <stdio.h>
struct student {
char name[20]; // 假设名字不超过19个字符
int age;
};
int main(void) {
    struct student stu2 = {
    .name = "wanglitao", 
    .age = 28
};
    printf("%s:%d\n", stu2.name, stu2.age);
    return 0;
}
```

<u>通过</u><u>结构域名.name和.age，可以给结构体变量的某一个指定成员直接赋值。</u>

<h5 id="HdxpG"><u>Linux内核驱动注册</u></h5>
<u>驱动程序中，经常使用file_operations这个结构体来注册我们开发的驱动，然后系统会以回调的方式来执行驱动实现的具体功能。</u>

```cpp
#include <linux/fs.h>
static const struct file_operations ab3100_otp_operations = {
.open=ab3100_otp_open,
.read=seq_read,
.llseek=seq_lseek,
.release=single_release,
};
```

<u>flie_operations结构体中有很多函数，使用.指定可以减少代码量。</u>

```cpp
#include <linux/fs.h>
struct file_operations {
struct module *owner;
loff_t (*llseek)(struct file *, loff_t, int);
ssize_t (*read)(struct file *, char __user *, size_t, loff_t *);
ssize_t (*write)(struct file *, const char __user *, size_t, loff_t *);
ssize_t (*read_iter)(struct kiocb *, struct iov_iter *);
ssize_t (*write_iter)(struct kiocb *, struct iov_iter *);
int (*iterate)(struct file *, struct dir_context *);
unsigned int (*poll)(struct file *, struct poll_table_struct *);
long (*unlocked_ioctl)(struct file *, unsigned int, unsigned long);
long (*compat_ioctl)(struct file *, unsigned int, unsigned long);
int (*mmap)(struct file *, struct vm_area_struct *);
int (*open)(struct inode *, struct file *);
int (*flush)(struct file *, fl_owner_t id);
int (*release)(struct inode *, struct file *);
int (*fsync)(struct file *, loff_t, loff_t, int datasync);
int (*aio_fsync)(struct kiocb *, int datasync);
int (*fasync)(int, struct file *, int);
int (*lock)(struct file *, int, struct file_lock *);
ssize_t (*sendpage)(struct file *, struct page *, int, size_t, loff_t *, int);
unsigned long (*get_unmapped_area)(struct file *, unsigned long, unsigned long, unsigned long, unsigned long);
int (*check_flags)(int);
int (*flock)(struct file *, int, struct file_lock *);
ssize_t (*splice_write)(struct pipe_inode_info *, struct file *, loff_t *, size_t, unsigned int);
ssize_t (*splice_read)(struct file *, loff_t *, struct pipe_inode_info *, size_t, unsigned int);
int (*setlease)(struct file *, long, struct file_lock **, void **);
long (*fallocate)(struct file *file, int mode, loff_t offset, loff_t len);
void (*show_fdinfo)(struct seq_file *m, struct file *f);
#ifdef CONFIG_MMU
unsigned (*mmap_capabilities)(struct file *);
#endif
};
```

<u>当成百上千个文件都使用file_operations这个结构体类型来定义变量并初始化时，如果采用C标准按照固定顺序赋值，当file_operations结构体类型发生变化时，如添加了一个成员、删除了一个成员、调整了成员顺序，那么使用该结构体类型定义变量的大量C文件都需要重新调整初始化顺序，牵一发而动全</u>

<u>身。我们通过指定初始化方式，就可以避免这个问题。无论file_operations结构体类型如何变化，添加成员也好、删除成员也好、调整成员顺序也好，都不会影响其他文件的使用。</u>

<h4 id="J5kv2"><u>宏构造“利器”：语句表达式</u></h4>
<h5 id="AnlCI"><u>表达式、语句和代码块</u></h5>
<u>略</u>

<h5 id="xYPMw"><u>在宏定义中使用语句表达式</u></h5>
<u>使用简单的宏定义做文本替换后会因为括号出现优先级的问题，所以需要进行调整，如linux中min和max的宏定义如下：</u>

```cpp
#define min(x, y) ({ \
typeof(x) _min1 = x; \
typeof(y) _min2 = y; \
(void) (&_min1 == &_min2); \
_min1 < _min2 ? _min1 ： _min2; })

#define max(x, y) ({ \
typeof(x) _max1 = x; \
typeof(y) _max2 = y; \
(void) (&_max1 == &_max2); \
_max1 > _max2 ? _max1 : _max2; }
```

`(void)`<u> 是一个类型转换，它将后面的表达式转换为 </u>`void`<u> 类型，这意味着表达式的结果被丢弃。而 </u>`&_min1 == &_min2`<u> 是一个比较两个变量地址是否相同的表达式，这个表达式的结果是一个布尔值，但通过将其转换为 </u>`void`<u> 类型，这个结果就被忽略了。void这一行代码的目的是让编译器认为 </u>`_min1`<u> 和 </u>`_min2`<u>（或 </u>`_max1`<u> 和 </u>`_max2`<u>）这两个变量被使用了，从而避免编译器发出未使用变量的警告。</u>

<h4 id="abCD3"><u>typeof与container_of宏</u></h4>
<h5 id="YrQP4"><u>typeof关键字</u></h5>
<u>ANSI C定义了sizeof关键字，用来获取一个变量或数据类型在内存中所占的字节数</u><u>。GNU C扩展了一个关键字typeof，用来获取一个变量或表达式的类型。</u><u>typeof没有被纳入C标准，是GCC扩展的一个关键字。</u>

```cpp
int i ;
typeof(i)j= 20;
typeof(int *)a;
    int f();
    typeof(f())k;
```

<u>变量i的类型为int，所以typeof(i)就等于int，typeof(i) j=20就相当于int j=20，typeof(int*) a；</u>

<u>相当于int*a，f()函数的返回值类型是int，所以typeof(f()) k；就相当于int k;</u>

```cpp
typeof(int*) y;
```

<u>定义了一个类型为</u>`int*`<u>的变量 </u>`y`<u>,</u><u>等价于</u>`int* y;`

```cpp
typeof (int) *y;
```

<u>等价于int *y;</u>

```cpp
typeof(*x) y;
```

<u>定义了一个变量 </u>`y`<u>，其类型是 指针</u>`x`<u> 指向的类型。如果 </u>`x`<u> 是一个指针，</u>`y`<u> 将是 </u>`x`<u> 所指向类型的变量。</u>

```cpp
typeof(int) y[4];
```

<u>等价于 </u>`int y[4];`

```cpp
typeof ( typeof(char *)[4] ) y；
```

<u>等价于char *y[4]；</u>

```cpp
typeof(int x[4]) y;
```

<u>等价于int y[4]；</u>

<h5 id="flhTW"><u>Linux内核中的container_of宏</u></h5>
`<u>container_of</u>`<u>是 Linux 内核中一个非常常用的宏，用于通过结构体成员的指针来获取整个结构体的指针。它在内核实现链表、设备驱动等场景时非常有用。假设有一个结构体，其中包含多个成员。如果只有一个成员的指针，也可以获取整个结构体的指针。</u>

`<u>container_of</u>`<u> 通过结构体成员的指针，减去该成员在结构体中的偏移量，得到整个结构体的起始地址，然后使用强制类型转换可以获取结构体成员的指针。</u>

`**container_of**`** 的原型**

```cpp
#define container_of(ptr, type, member)(
{\
    const typeof(((type *)0)->member)*__mptr=(ptr);
    \(type *)((char*)__mptr -offsetof(type, member));\
})
```

`**ptr**`<u>：结构体成员的指针。</u>`**type**`<u>：结构体的类型。</u>`**member**`<u>：结构体中成员的名称。</u>

`**container_of**`** 的工作原理**

`**typeof(((type *)0)->member)**`<u>:获取 </u>`member`<u> 成员的类型。例如，如果 </u>`member`<u> 是 </u>`int`<u> 类型，则 </u>`typeof`<u> 会推导出 </u>`int`<u>。</u>`**offsetof(type, member)**`<u>：计算 </u>`member`<u> 在结构体 </u>`type`<u> 中的偏移量。</u>`offsetof`<u> 是标准库中的一个宏，用于获取结构体成员的偏移量。</u>`**(char *)__mptr - offsetof(type, member)**`<u>：将 </u>`member`<u> 的指针转换为 </u>`char *`<u>（因为 </u>`char`<u> 的大小是 1 字节，方便计算偏移量）。减去 </u>`member`<u> 在结构体中的偏移量，得到结构体的起始地址。</u>`**(type *)**`<u>：将计算出的地址转换为结构体类型的指针。</u>

`container_of`<u>（会用不要求手写）</u>

```cpp
#include <stdio.h>
#include <stddef.h>
// 定义结构体
struct my_struct {
int data1; int data2; char data3;
};
// 定义 container_of 宏
#define container_of(ptr, type, member) ({              \
const typeof(((type *)0)->member) *__mptr = (ptr);   \
(type *)((char *)__mptr - offsetof(type, member));   \
})
int main() {
    // 创建一个结构体实例
    struct my_struct my_instance = {10, 20, 'A'};
    // 获取 data2 的指针
    int *data2_ptr = &my_instance.data2;
    // 使用 container_of 获取整个结构体的指针
    struct my_struct *parent_struct = container_of(data2_ptr, struct my_struct, 
    data2);
    // 打印结果
    printf("data1: %d, data2: %d, data3: %c\n",
        parent_struct->data1, parent_struct->data2, parent_struct->data3);
    return 0;
}
```

<h3 id="Z3EwH">`**container_of**`** 的典型应用场景**</h3>
**链表**<u>：</u>

    - <u>Linux 内核中的链表实现广泛使用 </u>`<u>container_of</u>`<u>。</u>
    - <u>链表节点通常嵌入到结构体中，通过节点的指针可以获取整个结构体的指针。</u>

**设备驱动**<u>：</u>

    - <u>在设备驱动中，通常需要从某个成员的指针获取设备结构体的指针。</u>

**回调函数**<u>：</u>

    - <u>在回调函数中，通常只能访问某些特定数据，通过 </u>`<u>container_of</u>`<u> 可以获取更多上下文信息。</u>

<h4 id="wplBA"><u>零长度数组和变长结构体</u></h4>
💡

**关联知识点：**

**class和struct的区别 **[<u>https://kdocs.cn/l/cuSTtRAG1IvG?linkname=b15pVlL5k0</u>](https://kdocs.cn/l/cuSTtRAG1IvG?linkname=b15pVlL5k0)

<u>零长度数组、变长数组都是GNU C编译器支持的数组类型</u>

<h5 id="C39kh"><u>什么是零长度数组</u></h5>
<u>长度为0的数组</u>

```cpp
int a[0];
```

<u>零长度数组有一个特点，就是不占用内存存储空间。</u><u>零长度数组一般单独使用的机会很少，它常常作为结构 体的一个成员，构成一个变长结构体。</u>

```cpp
struct buffer{
int len;
int a[0];
}
```

<u>使用变长数组实现buffer。</u>

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct buffer {
int len;
int a[0]; // 一个零长度的数组，表示后面可以追加任意长度的数据
};
int main(void) {
    struct buffer *buf;
    buf = (struct buffer *)malloc(sizeof(struct buffer) + 20);
    if (buf == NULL) {
        // 内存分配失败的处理
        perror("malloc failed");
        return 1;
    }
    buf->len = 20;
    strcpy(buf->a, "hello zhaixue.cc!\n");
    puts(buf->a);
    free(buf);
    return 0;
}
```

<h5 id="n1Bcy"><u>linux内核中的零长度数组</u></h5>
<u>网卡驱动中的套接字缓冲区(Socket Buffer)，USB驱动中的usb request block.......</u>

<h5 id="vXBzd"><u>指针与零长度数组</u></h5>
<u>为什么不使用指针来代替零长度数组？</u><u>如果使用指针，指针本身占用存储空间不说，远远没有零长度数组用得巧妙：</u><u>零长度数组不会对结构体定义造成冗余，而且使用起来很方便。</u>

<h4 id="O5Q9c"><u>属性声明</u></h4>
<h5 id="OaLuE"><u>GNU C编译器扩展关键字：</u><u>__attribute__</u></h5>
<u>GNU C增加了一个__attribute__关键字用来声明一个函数、变量或类型的特殊属性。</u>

```cpp
atttribute((ATTRIBUTE))
```

<u>目前__attribute__支持十几种属性声明。</u>

<u>section，aligned，packed，format，weak，alias，noinline，always_inline...</u>

<h5 id="XjO2x"><u>aligned属性</u></h5>
<u>aligned和packed用来显式指定一个变量的存储对齐方式。使用__atttribute__这个属性声明，可以告诉编译器，按照指定的边界对齐方式去给这个变量分配存储空间。</u>

```cpp
char c __attribute__((aligned(8))) = 4;
```

<u>代码声明一个字符变量 </u>`<u>c</u>`<u>，使用 </u>`<u>__attribute__((aligned(8)))</u>`<u> 指定该变量的对齐方式，表示c应该被对齐到8字节的边界，c在内存中的地址应该是8的倍数。</u>

<u>aligned有一个参数，表示要按几字节对齐，使用时要注意，地址对齐的字节数必须是2的幂次方，否则编译就会出错。</u><u>aligned只是建议编译器按照这种大小地址对齐，但不能超过编译器允许的最大值。 </u>

<u>当定义一个变量时，编译器会按照默认的地址对齐方式，来给该变量分配一个存储空间地址。如果该变量是一个int型数据，那么编译器就会按4字节或4字节的整数倍地址对齐；如果该变量是一个short型数据，那么编译器就会按2字节或2字节的整数倍地址对齐；如果是一个char类型的变量，那么编译器就会按照1字节地址对齐。</u>

<u>地址对齐会造成一定的内存空洞，但是这种对齐设置可以简化CPU读取数据。</u><u>一个32位的计算机系统，在CPU读取内存时，硬件设计上可能只支持4字节或4字节倍数对齐的地址访问，CPU每次向内存RAM读写数据时，一个周期可以读写4字节。</u><u>如果我们把一个int型数据放在4字节对齐的地址上，那么CPU一次就可以把数据读写完毕；如果我们把一个int型数据放在一个非4字节对齐的地址上，那么CPU可能就要分两次才能把这个4字节大小的数据读写完毕。</u>

<h5 id="ee179"><u>结构体的对齐</u></h5>
<u>char 1字节对齐，short 2 字节对齐，int 4字节对齐，</u><u>结构体的整体对齐要按结构体所有成员中最大对齐字节数或其整数倍对齐。</u>

```cpp
struct data{
char a;
int b ;
short c ;
}
```

<u>1+3+4+2+2(结构体)=12</u>

<u>结构体成员按不同的顺序排放，可能会导致结构体的整体长度不一样。</u>

```cpp
struct data{
char a;
short b ;
int c;
}
```

<u>1+1(short 2字节对齐)+2+4=8</u>

<h5 id="blGWK"><u>packed属性</u></h5>
<u>packed属性则与之相反，一般用来减少地址对齐，指定变量或类型使用最可能小的地址对齐方式。</u>

```cpp
struct data{
char a;
short battribute ((packed));
int c_attribute_((packed));
}
```

<u>1+2+4=7</u>

<u>在ARM芯片中，每一个控制器的寄存器地址空间一般都是连续存在的。如果考虑数据对齐，则结构体内就可能有空洞，就和实际连续的寄存器地址不一致。</u><u>使用packed可以避免这个问题，结构体的每个成员都紧挨着，依次分配存储地址，这样就避免了各个成员因地址对齐而造成的内存空洞。</u>

<u>在Linux内核源码中，经常看到aligned和packed一起使用，对一个变量或类型同时使用aligned和packed属性声明。这样避免了结构体内各成员因地址对齐产生内存空洞，又指定了整个结构体的对齐方式。</u>

```cpp
struct data {
char a;
short b;
int c;
}_attribute_((packed,aligned(8)));
```

<h5 id="CMLSm"><u>属性声明：</u><u>section</u></h5>
<u>可以使用__attribute__来声明一个section属性，section属性的主要作用是：在程序编译时，将一个函数或变量放到指定的段，放到指定的section中。（程序地址空间）</u>

```cpp
int global_val __attribute__((section(".data")));
```

<u>代码声明一个全局整型变量 </u>`global_val`，<u>并使用 </u>`__attribute__((section(".data")))`<u> 指定该变量应该被放置在程序的哪个段中。</u>

`section(".data")`<u> 表示 </u>`global_val`<u> 应该被放置在名为 ".data" 的段中。全局变量默认被放置在 ".data" 段 或者在需要的情况下将其放置在其他段中。</u>

<u>一个可执行文件主要由代码段、数据段、BSS段构成。代码段主要存放编译生成的可执行指令代码，数据段和BSS段用来存放全局变量、未初始化的全局变量。代码段、数据段和BSS段构成了一个可执行文件的主要部分。</u>

<u>编译器在编译程序时，以源文件为单位，将一个个源文件编译生成一个个目标文件。在编译过程中，编译器都会按照这个默认规则，将函数、变量分别放在不同的section中，最后将各个section组成一个目标文件。编译过程结束后，链接器会将各个目标文件组装合并、重定位，生成一个可执行文件。（编译链接)。</u>

<h5 id="TT6Vv"><u>U-boot镜像自复制分析</u></h5>
<u>U-boot在启动过程中，是如何将自身代码加载的RAM中的。U-boot的用途主要是加载Linux内核镜像到内存，给内核传递启动参数，然后引导Linux操作系统启动。</u>

<u>U-boot是怎样将自身代码从Flash复制到内存的呢？.....（如果以后投嵌入式的岗位，再看这部分的内容。）</u>

<h5 id="fRKTD"><u>属性声明format</u></h5>
<h5 id="FfuoM"><u>变参函数的格式检查</u></h5>
<u>GNU通过__attribute__扩展的format属性，来指定变参函数的参数格式检查。</u>

```cpp
#include <stdio.h>
#include <stdarg.h>
void myprintf(const char *format, ...) __attribute__((format(printf, 1, 2)));
void myprintf(const char *format, ...){
    va_list args;
    va_start(args, format);
    vprintf(format, args);
    va_end(args);
}
int main() {
    myprintf("%s %d %f\n", "The answer is", 42, 3.14);
    return 0;
}
```

<u>va_list:定 义 在 编 译 器 头 文 件 stdarg.h 中,如typedef char * va_list(所以va_list是一个char指针)</u>

<u>va_start(fmt，args):根据参数args的地址，获取args后面参数的地址，并保存在fmt指针变量中。</u>

<u>va_end(args):释放args指针，将其赋值为NULL。</u>

`__attribute__((format(printf, 1, 2)))`

`myprintf`<u> 函数的参数应该按照 </u>`printf`<u>函数的参数格式来检查</u>

<u>格式字符串是第一个参数，从第二个参数开始的参数需要与格式字符串相匹配。</u>

<u>如果调用 </u>`myprintf`<u> 时提供的参数与格式字符串不匹配，编译器将会发出警告。</u>

```cpp
void LOG(int num,char *fmt,...) __attribute__((format(printf,2,3)));
```

<h6 id="jkV2q"><u>变参函数初体验</u></h6>
```cpp
#include <stdio.h>
void print_num(int count,...) {
    int *args = (int *) &count + 1;
    for (int i = 0; i < count; i++) {
        printf("*args: %d\n", *args);
        args++;
    }
}
int main(void) {
    print_num(5, 1, 2, 3, 4, 5);
    return 0;
}
```

<u>在print_num()函数中，首先获取count参数地址，然后使用&count+1就可以获取下一个参数的地址，使用指针变量args保存这个地址，并依次访问下一个地址，就可以直接打印传进来的各个实参值。</u>

<h6 id="QFvDG"><u>变参函数改进版</u></h6>
```cpp
#include <stdio.h>
#include <stdarg.h>
void print_num(int count, ...) {
    va_list args;
    va_start(args, count);
    for (int i = 0；i < count；i++) printf("%d\n", va_arg(args, int));
    va_end(args);
}
int main(void) {
    print_num(5, 1, 2, 3, 4, 5);
    return 0;
}
```

<u>va_arg(args, int)相当于args指针加4后解引用(取出一个整数)。</u>

<u>实现不同等级的日志打印：</u>

```cpp
#include <stdio.h>
#include <stdarg.h>
#define LOG_LEVEL_INFO  1
#define LOG_LEVEL_WARN  2
#define LOG_LEVEL_ERR   3
int current_log_level = LOG_LEVEL_INFO; // 默认日志等级为INFO
void log_info(const char *format, ...) {
    if (current_log_level <= LOG_LEVEL_INFO) {
        va_list args;
        va_start(args, format);
        printf("INFO: ");
        vprintf(format, args);
        va_end(args);
    }
}
void log_warn(const char *format, ...) {
    if (current_log_level <= LOG_LEVEL_WARN) {
        va_list args;
        va_start(args, format);
        printf("WARN: ");
        vprintf(format, args);
        va_end(args);
    }
}
void log_err(const char *format, ...) {
    if (current_log_level <= LOG_LEVEL_ERR) {
        va_list args;
        va_start(args, format);
        printf("ERROR: ");
        vprintf(format, args);
        va_end(args);
    }
}
int main() {
    log_info("This is an info message: %d", 42);
    log_warn("This is a warning message: %s", "Be careful!");
    log_err("This is an error message: %d", -1);
    return 0;
}
```

<h5 id="Sv9te"><u>属性声明：weak</u></h5>
<u>GNU C通过weak属性声明，可以将一个强符号转换为弱符号。程序中变量名/函数名,在编译器的眼里，就是一个符号而已。符号可以分为强符号和弱符号。</u>

<u>●强符号：函数名，初始化的全局变量名 ●弱符号：未初始化的全局变量名</u>

<u>对于相同的全局变量名、函数名</u>

<u>●强符号+强符号 ●强符号+弱符号 ●弱符号+弱符号。</u>

<u>强符号和弱符号主要用来解决在程序链接过程中，出现多个同名全局变量、同名函数的冲突问题。一般遵循下面3个规则：</u>

<u>不能同时存在两个强符号：</u><u>两个同名的函数或全局变量，那么链接器在链接时就会报重定义错误。</u>

<u>强弱可以共处：可以同时定义一个初始化的全局变量和一个未初始化的全局变量。</u>

<u>体积大者胜出：当同名的符号都是弱符号时，那么编译器该选择哪个呢？谁的体积大，即谁在内存中的存储空间大，就选谁。</u>

<u>弱符号的这个特性，在库函数中应用得很广泛。在开发一个库时，基础功能已经实现，有些高级功能还没实现，那么可以将这些函数通过weak属性声明转换为一个弱符号</u><u>。</u><u>通过这样设置，即使还没有定义函数，我们在应用程序中只要在调用之前做一个非零的判断就可以了，并不影响程序的正常运行。等以后发布新的库版本，实现了这些高级功能，应用程序也不需要进行任何修改，直接运行就可以调用这些高级功能。</u>

`**<u>static</u>**`**<u> 变量的作用域</u>**<u>：在 C 语言中，</u>`<u>static</u>`<u> 关键字用于修饰变量或函数时，会将它们的作用域限制在当前即编译单元内。即使不同文件中的 </u>`<u>static</u>`<u> 变量同名，它们也是相互独立的，不会相互干扰。</u>`<u>static</u>`<u> 变量在编译时会被标记为</u>**<u>局部符号，</u>**<u>不会暴露给链接器。因此，链接器不会处理这些 </u>`<u>static</u>`<u> 变量，也不会认为它们是冲突的。</u>

<u>结合命名空间。</u>

```cpp
#include <stdio.h>
//基础功能
void basic_function() {
    printf("Basic function is implemented.\n");
}
// 高级功能（声明为弱符号）
__attribute__((weak)) void advanced_function() {
    printf("Advanced function is not implemented yet.\n");
}


#include <stdio.h>

// 声明库中的函数
void basic_function();
void advanced_function();

int main() {
    // 调用基础功能
    basic_function();
    // 判断高级功能是否已实现
    if (advanced_function) {
        printf("Advanced function is available.\n");
        advanced_function();  // 调用高级功能
    } else {
        printf("Advanced function is not available.\n");
    }

    return 0;
}
```

`**__attribute__((weak))**`<u>：将 </u>`advanced_function`<u> 声明为弱符号。如果应用程序中没有实现 </u>`advanced_function`<u>，则调用库中的默认实现。如果应用程序中实现了 </u>`advanced_function`<u>，则调用应用程序中的实现。</u>

<h5 id="hw5Rr"><u>属性声明：alias</u></h5>
<u>GNU C扩展了一个alias属性，用来给函数定义一个别名。</u>

```cpp
#include <stdio.h>
//定义_f函数
void _f(void) {
    printf("_f\n");
}

//为_f函数创建别名 f
void f(void) __attribute__ ((alias("_f")));
int main(void) {
    // 调用 f 函数，实际上调用的是 _f 函数
    f();
    return 0;
}
```

<h4 id="Yl596"><u>内联函数</u></h4>
<h5 id="LnNCF"><u>属性声明：noinline</u></h5>
<u>noinline和always_inline，两个属性的用途是告诉编译器，在编译时，对指定的函数内联展开或不展开。</u><u>声明一个静态内联函数，使用 always inline 属性强制编译器内联。</u>

```cpp
static inline int func2() __attribute__((no_inline));
static inline int func2() __attribute__((always_inline));
```

<u>使用inline声明一个内联函数，和使用关键字register声明一个寄存器变量一样，只是建议编译器在编译时内联展开。使用关键字register修饰一个变量，只是建议编译器在为变量分配存储空间时，将这个变量放到寄存器里，这会使程序的运行效</u><u>率更高。那么编译器会不会放呢？得视具体情况而定，编译器要根据寄存器资源是否紧张、这个变量的类型及是否频繁使用来做权衡。</u>

<u>当一个函数使用inline关键字修饰时，编译器在编译时一定会内联展开吗？也不一定。编译器也会根据实际情况，如函数体大小、函数体内是否有循环结构、是否有指针、是否有递归、函数调用是否频繁来做决定。使用noinline和always_inline对一个内联函数作显式属性声明后，编译器的编译行为就变得确定。</u>

<h5 id="oVbA8"><u>什么是内联函数</u></h5>
<u>内联函数在调用的时候插入的调用的位置，省去了压栈和出栈的操作。与宏相比，内联函数有以下优势：</u>

<u>● 参数类型检查：内联函数虽然具有宏的展开特性，但其本质仍是函数，在编译过程中，编译器仍可以对其进行参数检查，而宏不具备这个功能。</u>

<u>● 便于调试：函数支持的调试功能有断点、单步等，内联函数同样支持。</u>

<u>● 返回值：内联函数有返回值，返回一个结果给调用者。这个优势是相对于ANSI C说的，因为现在宏也可以有返回值和类型了，如前面使用语句表达式定义的宏。</u>

<u>● 接口封装：有些内联函数可以用来封装一个接口，而宏不具备这个特性。</u>

<u>内联函数并不是完美无瑕的，也有一些缺点。</u><u>内联函数会增大程序的体积，如果在一个文件中多次调用内联函数，多次展开，那么整个程序的体积就会变大，在一定程度上会降低程序的执行效率。函数的作用之一就是提高代码的复用性。我们将常用的一些代码或代码块封装成函数，进行模块化编程，可以减轻软件开发工作量。内联函数往往又降低了函数的复用性。编译器在对内联函数做展开时，除了检测用户定义的内联函数内部是否有指针、循环、递归，还会在函数执行效率和函数调用开销之间进行权衡。</u>

<u>当函数体积小，函数体内无指针赋值、递归、循环等语句，调用频繁，就可以使用static inline关键字修饰它。但编译器不一定会做内联展开，如果你想明确告诉编译器一定要展开，或者不展开，就可以使用noinline或always_inline对函数做一个属性声明。</u>

<h5 id="m6cle"><u>思考：内联函数为什么定义在头文件中</u></h5>
<u>内联函数为什么要定义在头文件中呢？因为它是一个内联函数，可以像宏一样使用，任何想使用这个内联函数的源文件，都不必亲自再去定义一遍，直接包含这个头文件，即可像宏一样使用。</u><u>那么为什么还要用static修饰呢？</u><u>因为我们使用inline定义的内联函数，编译器不一定会内联展开</u><u>，那么当一个工程中多个文件都包含这个内联函数的定义时，编译时就有可能报重定义错误。使用static关键字修饰，则可以将这个函数的作用域限制在各自的文件内，避免重定义错误的发生。</u>

<h4 id="YR9Gk"><u>内建函数</u></h4>
<u>（暂时不看）</u>

<u>内建函数，就是编译器内部实现的函数。函数和关键字一样，可以直接调用，无须像标准库函数那样，要先声明后使用。</u>

<u>内建函数的函数命名，通常以__builtin开头。这些函数主要在编译器内部使用，主要是为编译器服务的。内建函数的主要用途如下。</u>

<u>●用来处理变长参数列表。</u>

<u>●用来处理程序运行异常、编译优化、性能优化。</u>

<u>●查看函数运行时的底层信息、堆栈信息等。</u>

<u>●实现C标准库的常用函数。</u>

<h5 id="esNBF"><u>常用的内建函数</u></h5>
<h6 id="tUeU5"><u>__builtin_return_address()</u></h6>
<u>这个函数用来返回当前函数或调用者的返回地址。函数的参数LEVEL表示函数调用链中不同层级的函数。</u>

<u>● 0：获取当前函数的返回地址。</u>

<u>● 1：获取上一级函数的返回地址。</u>

<u>● 2：获取上二级函数的返回地址。</u>

```cpp
#include <stdio.h>
void f(void) {
    int *p;
    p = __builtin_return_address(0);
    printf("f return address: %p\n", (void*)p);
    p = __builtin_return_address(1);
    printf("func return address: %p\n", (void*)p);
    p = __builtin_return_address(2);
    printf("main return address: %p\n", (void*)p);
    printf("\n");
}
void func(void) {
    int *p;
    p = __builtin_return_address(0);
    printf("func return address: %p\n", (void*)p);
    p = __builtin_return_address(1);
    printf("main return address: %p\n", (void*)p);
    printf("\n");
}
int main(void) {
    int *p;
    p = __builtin_return_address(0);
    printf("main return address: %p\n", (void*)p);
    printf("\n");
    func();
    printf("goodbye!\n");
    return 0;
}
```

<h6 id="EZdwQ"><u>__builtin_frame_address()</u></h6>
<u>函数每调用一次，都会将当前函数的现场（返回地址、寄存器、临时变量等）保存在栈中，每一层函数调用都会将各自的现场信息保存在各自的栈中。这个栈就是当前函数的栈帧，每一个栈帧都有起始地址和结束地址，多层函数调用就会有多个栈帧，每个栈帧都会保存上一层栈帧的起始地址，这样各个栈帧就形成了一个调用链。很多调试器其实都是通过回溯函数的栈帧调用链来获取函数底层的各种信息的，如返回地址、调用关系等。</u>

<u>通过内建函数__builtin_frame_address(LEVEL)查看函数的栈帧地址。</u>

<u>●0：查看当前函数的栈帧地址。</u>

<u>●1：查看上一级函数的栈帧地址。</u>

```cpp
#include <stdio.h>
void func(void) {
    int *p;
    p = __builtin_frame_address(0);
    printf("func frame: %p\n", (void*)p);
    p = __builtin_frame_address(1);
    printf("main frame: %p\n", (void*)p);
}
int main(void) {
    int *p;
    p = __builtin_frame_address(0);
    printf("main frame: %p\n", (void*)p);
    func();
    return 0;
}
```

<h6 id="IosJE"><u>__builtin_constant_p(n)</u></h6>
<u>编译器内部还有一些内建函数主要用来编译优化、性能优化，如__builtin_constant_p(n) 函数。该函数主要用来判断参数n在编译时是否为常量。如果是常量，则函数返回1，否则函数返回0。</u>

<u>该函数常用于宏定义中，用来编译优化。一个宏定义，根据宏的参数是常量还</u>

<u>是变量，可能实现的方法不一样。</u>

<h6 id="HPC2L"><u>__builtin_expect(exp，c)</u></h6>
<u>内建函数__builtin_expect()也常常用来编译优化，函数有2个参数，返回值就是其中一个参数，仍是exp。这个函数的意义主要是告诉编译器：参数exp的值为c的可能性很大，然后编译器可以根据这个提示信息，做一些分支预测上的代码优化。 </u>

<u>那么Cache如何缓存内存数据呢？空间局部性。如CPU正在执行一条指令，那么在下一个时钟周期里，CPU一般会大概率执行当前指令的下一条指令。如果此时Cache将下面的几条指令都缓存到Cache里，则下一个时钟周期里，CPU就可以直接000到Cache里取指、译指和执行，从而使运算效率大大提高。 </u>

<u>如程序在执行过程中遇到函数调用、if 分支、goto跳转等程序结构，会跳到其他地方执行，原先缓存到Cache 里的指令不是CPU要执行的指令。此时，就说Cache没有命中， Cache会重新缓存正确的指令代码供CPU读取。</u>

<u>遇到if/switch这种选择 分支的程序结构，一般建议将大概率发生的分支写在前面。当程序运 行时，因为大概率发生，所以大部分时间就不需要跳转，程序就相当 于一个顺序结构。</u>

<h5 id="D3ZaM"><u>Linux内核中的likely和unlikely</u></h5>
<u>这两个宏的主要作用就是告诉编译器：某一个分支发生的概率很高，或者很低，基本不可能发生。</u>

```cpp
int main(void)
{
    int a; scanf("%d",&a); if (unlikely(a==0)) {
        {
            printf("%d", 1);
            printf("%d", 2);
            printf("\n");
        }
        else {
        printf("%d", 5); printf("%d", 6);
        printf("%d", 6); printf("\n");
    }
}
return 0;
}
```

<h4 id="uQ1Tu"><u>可变参数宏</u></h4>
<u>变参函数基本套路就是使用va_list、va_start、va_end等宏，去解析那些可变参数列表。</u><u>只有GNU C标准支持这个功能，所以有时候我们也把这个可变参数宏看作GNU C标准的一个语法扩展。</u>

```cpp
#include <stdio.h>
#define LOG(fmt, ...) printf(fmt, ##__VA_ARGS__)
#define DEBUG(...) printf(__VA_ARGS__)
int main(void) {
    LOG("Hello! I'm %s\n", "Wanglitao");
    DEBUG("Hello! I'm %s\n", "Wanglitao");
    return 0;
    _}
```

<u>可变参数宏的实现形式其实和变参函数差不多：用...表示变参列表，变参列表由不确定的参数组成，各个参数之间用逗号隔开。可变参数宏使用C99标准新增加的一个__VA_ARGS__预定义标识符来表示前面的变参列表，而不是像变参函数一样，使用va_list、va_start、va_end这些宏去解析变参列表。预处理器在将宏展开时，会用变参列表替换掉宏定义中的所有__VA_ARGS__标识符。</u>

<u>标识符__VA_ARGS__前面加上了宏连接符＃＃，这样做的好处是：当变参列表非空时，＃＃的作用是连接fmt和变参列表，各个参数之间用逗号隔开，宏可以正常使用；当变参列表为空时，＃＃还有一个特殊的用处，它会将固定参数fmt后面的逗号删除掉，这样宏就可以正常使用了。</u>

<h1 id="rZnug"><u>C语言的面向对象编程思想</u></h1>
⭐

<u>关联知识点：</u>

<u>C和C++的区别</u>

<u>操作系统的顶层设计</u>

<u>C++的封装，继承，多态</u>

**<font style="color:#58a401;">什么是代码复用？什么是分层？C语言如何模拟类？C语言如何模拟继承？</font>**

**<font style="color:#58a401;">linux内核链表如何体现面向对象的特性的？C语言如何实现多态的？</font>**

<h4 id="hvBty"><u>代码复用与分层思想</u></h4>
<u>什么是代码复用？</u>

<u>（1）函数级代码复用：定义一个函数实现某个功能，所有的程序都可以调用这个函数，不用自己再单独实现一遍，函数级的代码复用。</u>

<u>（2）将一些通用的函数打包封装成库，并引出API供程序调用，实现了库级的代码复用；</u>

<u>（3）将一些类似的应用程序抽象成应用骨架，然后进一步迭代成框架，实现框架级的代码复用；</u>

<u>如果从代码复用的角度看操作系统，操作系统其实也是对任务调度、任务间通信等功能实现，并引出API供应用程序调用，相当于实现了操作系统级的代码复用。</u>

<u>通常将要复用的具有某种特定功能的代码封装成一个模块，各个模块之间相互独立，使用的时候可以以模块为单位集成到系统中。随着系统越来越复杂，集成的模块越来越多，模块之间会产生依赖关系。为了便于系统的管理和维护，又开始出现分层思想，可以把一个计算机系统分为应用层、系统层、硬件层。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811444379-54a37bd8-d92b-4930-8d53-fe564ffdfa5b.png)

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811444399-324e0bc1-a936-415f-861f-c823f3157333.png)

<u>在Linux内核中，往往包含很多模块和子系统，如文件系统、内存管理子系统、进程调度等。每一个模块或子系统也包含着分层的思想。如Linux文件系统，就包括虚拟文件系统VFS和各种类型的文件系统Ext、Fat、NFS等。底层的磁盘、文件系统、虚拟文件系统及应用层的API读写接口也可以实现分层。</u>

<u>一个系统通过分层设计，各层实现各自的功能，各层之间通过接口通信。每一层都是对其下面一层的封装，并留出API，为上一层提供服务，实现代码复用。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811444390-f8745231-aad2-49c1-aa18-56017d8e8239.png)

<h4 id="vL7Nt"><u>面向对象编程基础</u></h4>
<u>面向过程编程中函数是程序的基本单元，可以把一个问题分解成多个步骤来解决，每</u>

<u>一步或每一个功能都可以使用函数来实现。</u>

<u>在面向对象编程中，对象是程序的基本单元，对象是类的实例化，类则是对客观事物抽象而成的一种数据类型，其内部包括属性和方法。</u>

<u>面向对象编程则侧重于将问题抽象、封装成一个个类，然后通过继承来实现代码复用，面向对象编程一般用于复杂系统的软件分层和架构设计。</u>

<h4 id="JUjSM"><u>Linux内核中的OOP思想：封装</u></h4>
<u>内核中的很多子系统、模块在实现过程中处处体现了面向对象编程思想。</u>

<h5 id="CruR3"><u>类的C语言模拟实现</u></h5>
<u>C语言中没有class关键字，但是可以使用struct模拟一个类，C++类中的属性类似结构体的各个成员。虽然结构体内部不能像类一样可以直接定义函数，但可以在结构体中内嵌函数指针来模拟类中的方法。</u>

```cpp
struct animal{
int age;
int weight;
void (*fp)(void);
}
```

<u>如果一个结构体中需要内嵌多个函数指针，可以把这些函数指针进一步封装到一个结构体内。</u>

```cpp
struct func operations{
    void(*fp1)(void);
    void (*fp2)(void);
    void (*fp3)(void);
    void (*fp4)(void);
}
struct animal{
int age;
int weight;
struct func operations fp;
}
```

<u>通过把函数封装在结构体中，然后嵌入该结构体，可以把一个类的属性和方法都封装在一个结构体里。</u>

<u>如何继承？</u>

```cpp
struct cat{
struct animal *p;
struct animal ani;
char sex;
void (*eat)(void);
}
```

<u>C语言可以通过在结构体中内嵌另一个结构体或结构体指针来模拟类的继承。</u>

<u>在结构体类型cat里内嵌结构体类型animal，此时结构体cat就相当于模拟了一个子类cat，而结构体animal相当于一个父类。</u>

<u>C语言中,内嵌结构体或内嵌指向结构体的指针，可以看作对“继承”的模拟。</u>

<h5 id="XgMzf"><u>链表的抽象与封装</u></h5>
Linux内核中为了实现对链表操作的代码复用，定义了一个通用的链表及相关操作.

```cpp
struct list head{
    struct list head *next, *prev;
}
void INIT LIST HEAD(struct list head *list);
int list empty(const struct list head *head);
void list add(struct list head *new, struct list head *head);
    void list del(struct list head *entry);
    void list replace(struct list head *old,struct list head *new),
        void list move(struct list head *list, struct list head *head);
```

如果想复用Linux内核中的通用链表及相关操作，就可以通过内嵌结构体来继承list_head的属性和方法。

```cpp
struct my_list node{
    int data;
    struct list head list;
}
```

<h5 id="z7o2P"><u>设备管理模型</u></h5>
Linux如何管理和维护这些设备的信息呢？

Linux的设备管理模型说起。Linux内核中定义了一个非常重要的结构体类型。

```cpp
struct kobject{
const char *name;
struct list head entry;
struct kobject *parent;
struct kernfs node *sd;
struct kset *kset;
struct kobj_type *ktype;
struct kref kref;
unsigned int state initialized:1;
unsigned int state_in_sysfs:1;
unsigned int state add uevent sent:1;
unsigned int state_remove_uevent sent:1;
unsigned int uevent suppress:1;
}
```

<u>所有设备在系统中的树结构,kobject结构体用来表示Linux系统中的一个设备，相同类型的kobject通过其内嵌的list_head链成一个链表，然后使用另外一个结构体kset来指向和管理这个列表。</u>

<u>以后再说。</u>

<u>以字符设备为例，我们可以看到字符设备结构体cdev在内核中的定义。</u>

```cpp
struct cdev {
struct kobject      kobj;          // 内嵌kobject结构体
struct module       *owner;
const struct file_operations *ops;
struct list_head    list;
dev_t               dev;
unsigned int        count;
};
```

在结构类型cdev中，通过内嵌结构体kobject来模拟对基类kobject的继承，字符设备的注册与注销，都可以通过继承基类的kobject_add()/kobject_del()方法来完成。与此同时，字符设备在继承基类的基础上，也完成了自己的扩展：实 现 了 自 己的read/write/open/close接口，并把这些接口以函数指针的形式封装在结构体file_operations中。

```cpp
struct file_operations {
struct module *owner;
loff_t (*llseek) (struct file *, loff_t, int);
ssize_t (*read) (struct file *, char __user *, size_t, loff_t *)；
ssize_t (*write) (struct file *, const char __user *, size_t, loff_t *);
ssize_t (*read_iter) (struct kiocb *, struct iov_iter *)；
ssize_t (*write_iter) (struct kiocb *, struct iov_iter *);
int (*iterate) (struct file *, struct dir_context *);
unsigned int (*poll) (struct file *, struct poll_table_struct *);
long (*unlocked_ioctl) (struct file *, unsigned int, unsigned long);
long (*compat_ioctl) (struct file *, unsigned int, unsigned long); 
int (*mmap) (struct file *, struct vm_area_struct *);
int (*open) (struct inode *, struct file *);
int (*flush) (struct file *, fl_owner_t id);
int (*release) (struct inode *, struct file *);
int (*fsync) (struct file *, loff_t, loff_t, int datasync);
int (*aio_fsync) (struct kiocb *, int datasync);
int (*fasync) (int, struct file *, int);
int (*lock) (struct file *, int, struct file_lock *);
...
};
```

<u>不同的字符设备，会根据自己的硬件逻辑实现各自的read()、write()函数，并注册到系统中。当用户程序读写这些字符设备时，通过这些接口，就可以找到对应设备的读写函数，对字符设备进行打开、读写、关闭等各种操作。</u>

<h5 id="xUHcx"><u>总线设备模型</u></h5>
Linux每一个设备都要有一个对应的驱动程序，否则就

无法对这个设备进行读写。每一个字符设备都对应的字符设备驱动程序；每一个块设备都有对应的块设备驱动程序。对于一些总线型的设备，如鼠标、键盘、U盘等USB设备，设备通信是按照USB标准协议进行的。

Linux系统为了实现最大化的驱动代码复用，设计了设备-总线-驱动模型：用总线提供的一些方法来管理设备的插拔信息，所有的设备都挂到总线上，总线会根据设备的类型选择合适的驱动与之匹配。通过这种设计，相同类型的设备可以共享同一个总线驱动，实现了驱动级的代码复用。

总线设备模型相关的3个结构体分别为device、bus、driver，它们可以看成基类kobject的子类。

```cpp
struct device {
struct device         *parent;     // 父设备
struct device_private *p;          // 内嵌私有数据
struct kobject        kobj;        // 内嵌kobject结构体
const struct device_type *type;    // 设备类型
struct bus_type       *bus;        // 总线类型
struct device_driver  *driver;     // 驱动程序
void                 *platform_data;
void                 *driver_data;
dev_t                devt;
u32                  id;
struct klist_node     knode_class;
struct class         *class;
void (*release)(struct device *dev);
};
```

<u>与字符设备cdev类似，在结构体类型device的定义里，也通过内嵌kobject结构体来完成对基类kobject的继承。但其与字符设备不同之处在于，device结构体内部还内嵌了bus_type和device_driver，用来表示其挂载的总线和与其匹配的设备驱动。</u>

<u>device结构体可以看成一个抽象类，我们无法使用它去创建一个</u>

<u>具体的设备。其他具体的总线型设备，如USB设备、I2C设备等可以通</u>

<u>过内嵌device结构体来完成对device类属性和方法的继承。</u>

```cpp
struct usb_device {
int      devnum;
char     devpath[16];
u32      route;
enum usb_device_state    state;
enum usb_device_speed   speed;
struct usb_tt           *tt;
int                     ttport;
unsigned int            toggle[2];
struct usb_device       *parent;
struct usb_bus          *bus;
struct usb_host_endpoint ep0;
struct device           dev;             // 内嵌device 结构体
...
};
```

<h4 id="xYU2Z"><u>Linux内核中的OOP思想：继承</u></h4>
<h5 id="pRliS"><u>继承与私有指针</u></h5>
<u>除了内嵌结构体，C语言还可以有其他方法来模拟类的继承，如通过私有指针。我们可以把使用结构体类型定义各个不同的结构体变量，也可以看作继承，各个结构体变量就是子类，然后各个子类通过私有指针扩展各自的属性或方法。这种继承方法主要适用于父类和子类差别不大的场合。</u>

<u>如Linux内核中的网卡设备，不同厂家的网卡、不同速度的网卡，以及相同厂家不同品牌的网卡，它们的读写操作基本上都是一样的，都通过标准的网络协议传输数据，唯一不同的就是不同网卡之间存在一些差异，如I/O寄存器、I/O内存地址、中断号等硬件资源不相同。</u>

遇到可以将各个网卡一些相同的属性抽取出来，构建一个通用的结构体net_device，然后通过一个私有指针，指向每个网卡各自不同的属性和方法，这样可以最大程度地实现代码复用。

```cpp
struct net_device {
char name[IFNAMSIZ];                   // 网络设备名称
const struct net_device_ops *netdev_ops; // 网络设备操作
const struct ethtool_ops *ethool_ops;    // Ethtool操作
void *ml_priv;                       // 中间层私有数据
struct device dev;                   // 内嵌device结构体
};
```

<u>当我们使用该结构体类型定义不同的变量来表示不同型号的网卡设备时，这个私有指针就会指向各个网卡自身扩展的一些属性。</u>

<h5 id="ljMR0"><u>继承与抽象类</u></h5>
<u>含有纯虚函数的类，称之为抽象类。抽象类不能被实例化，实例化也没有意义，如animal类，它只能被子类继承。抽象类的作用，主要就是实现分层：实现抽象层。当父类和子类之间的差别太大时，很难通过继承来实现代码复用，如生物类和狗</u>

<u>类，我们可以在它们之间添加一个animal抽象类。抽象类主要用来管理父类和子类的继承关系，通过分层来提高代码的复用性。</u>

<u>如上面设备模型中的device类，位于kobj类和usb_device类之间，通过分层，</u>

<u>可以更好地实现代码复用。</u>

<h4 id="mQRyv"><u>Linux内核中的OOP思想：多态</u></h4>
<u>可以使用C语言来模拟多态：</u><u>如果把使用同一个结构体类型定义的不同结构体变量看成这个结构体类型的各个子类，那么在初始化各个结构体变量时，如果基类是抽象类，类成员中包含纯虚函数，则为函数指针成员赋予不同的具体函数，然后通过指针调用各个结构体变量的具体函数即可实现多态。</u>

```cpp
#include <stdio.h>
// 文件操作结构体
typedef struct file_operation {
void(*read)(void);  // 读取操作
void(*write)(void); // 写入操作
} FileOperation;
// 文件系统结构体
typedef struct file_system {
char name[20];      // 文件系统名称
FileOperation fops; // 文件操作
} FileSystem;

// 扩展文件系统的读操作
void ext_read(void) {
    printf("ext read...\n");
}
// 扩展文件系统的写操作
void ext_write(void) {
    printf("ext write...\n");
}
// FAT文件系统的读操作
void fat_read(void) {
    printf("fat read...\n");
}

// FAT文件系统的写操作
void fat_write(void) {
    printf("fat write...\n");
}
int main(void) {
    // 初始化扩展文件系统
    FileSystem ext = {"ext3", {ext_read, ext_write}};
    // 初始化FAT文件系统
    FileSystem fat = {"fat32", {fat_read, fat_write}};

    // 文件系统指针
    FileSystem *fs_ptr;

    // 指向扩展文件系统
    fs_ptr = &ext;
    fs_ptr->fops.read(); // 调用扩展文件系统的读操作
    // 指向FAT文件系统
    fs_ptr = &fat;
    fs_ptr->fops.read(); // 调用FAT文件系统的读操作
    return 0;
}
```

<h1 id="j0TMk"><u>C语言的模块化编程思想</u></h1>
**<font style="color:#58a401;">不同模块如何链接成一个文件？面向对象编程和模块化编程有什么区别？</font>**

**<font style="color:#58a401;">头文件有什么用？头文件重复包含是什么？</font>**

**<font style="color:#58a401;">变量声明和定义有什么区别?extern变量怎么用？</font>**

**<font style="color:#58a401;">goto关键字有什么用？</font>**

**<font style="color:#58a401;">模块设计原则是什么?模块直接耦合的方式有哪些？模块间如何进行通信？</font>**

<h4 id="eXHNo"><u>模块的编译和链接</u></h4>
<u>一个C语言项目划分成不同的模块，通常由多个文件来实现。在项目编译过程中，编译器是以C源文件为单位进行编译的，每一个C源文件都会被编译器翻译成对应的一个目标文件。链接器对每一个目标文件进行解析，将文件中的代码段、数据段分别组装，生成一个可执行的目标文件。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811444406-dc23208d-45bc-457d-9ee2-8ccb053d27ab.png)

<u>如果程序调用了库函数，则链接器也会找到对应的库文件，将程序中引用的库代码一同链接到可执行文件中。</u>

![](https://cdn.nlark.com/yuque/0/2025/png/45533403/1742811444761-615a3deb-7ddf-47c7-8cc7-e4b08684e3c1.png)

<u>在链接过程中，如果多个目标文件定义了重名的函数或全局变量，就会发生符号冲突，报重定义错误。这时候链接器就要对这些重复定义的符号做符号决议，决定哪些留下，哪些丢弃。</u>

<u>在一个多文件项目中，不允许有多个强符号。</u>

<u>若存在一个强符号和多个弱符号，则选择强符号。</u>

<u>若存在多个弱符号，则选择占用空间最大的那一个。</u>

<u>初始化的全局变量和函数是强符号，未初始化的全局变量。默认属于弱符号。</u>

<u>可以通过__attribute__属性声明显式更改符号的属性，将一个强符号显式转换为弱符号。</u>

<u>和强符号、弱符号对应的，还有强引用、弱引用的概念。在一个程序中，我们可以定义多个函数和变量，变量名和函数名都是符号，这些符号的本质，或者说这些符号值，其实就是地址。在另一个文件中，我们可以通过函数名去调用该函数，通过变量名去访问该变量。我们通过符号去调用一个函数或访问一个变量，通常称之为引用</u>

<u>强符号对应强引用，弱符号对应弱引用。在程序链接过程中，若对一个符号的引用为强引用，链接时找不到其定义，链接器将会报未定义错误；若对一个符号的引用为弱引用，链接时找不到其定义，则链接器不会报错，不会影响最终可执行文件的生成。可执行文件在运行时如果没有找到该符号的定义才会报错。</u>

<u>利用链接器对弱引用的处理规则，我们在引用一个符号之前可以先判断该符号是否存在（定义）。这样做的好处是：当我们引用一个未定义符号时，在链接阶段不会报错，在运行阶段通过判断运行，也可以避免运行错误。</u>

```cpp
void log_message(const char* message) __attribute__((weak));
void some_function() {
    if (log_message) {
        log_message("Starting some_function");
    } // 如果log_message未定义，这里不会执行，也不会报错
    // 执行some_function的其他逻辑
}
```

<u>整个项目编译过程中，可以通过编译控制参数来控制编译流程：预处理、编译、汇编、链接，也可以指定多个文件的编译顺序。</u>

<u>通常使用自动化编译工具make来编译项目，make自动编译工具依赖项目的Makefile文件。</u>

<u>Makefile文件主要用来描述各个模块文件的依赖关系，要生成的可执行文件，需要编译哪些源文件。</u>

<u>make在编译项目时，会首先解析Makefile，分析需要编译哪些源文件，构建一个完整的依赖关系树，然后调用具体的命令一步步去生成各个目标文件和最终的可执行文件。</u>

<h4 id="hQlFj"><u>系统模块划分</u></h4>
<u>根据系统的目标、实现的功能进行划分；当系统比较复杂时，对系统进行分层。</u>

<u>面向对象编程和系统的模块化设计侧重点不同。模块化设计的思想</u>

<u>内核是分而治之，重点在于抽象的对象之间的关联，而不是内容；面向对象编程思想主要是为了代码复用，重点在于内容实现。两者还有一个重要的区别是：两者不在同一个层面上。模块化设计是最高原则，先有系统定义，然后有模块和模块的实现，最后才有代码复用。一个系统不仅仅是模块的实现，还有各个模块之间的相互作用、相互关联，以及由它们构成的一个有机整体。面向对象编程，通过类的封装和继承实现了代码复用，减少了开发工作量，这是面向对象编程的长处。</u>

<h4 id="mksrq"><u>模块的封装</u></h4>
<u>在C语言中一个模块一般对应一个C文件和一个头文件。模块的实现在C源文件中，头文件主要用来存放函数声明，留出模块的API，供其他模块调用。</u>

<u>变量的定义和声明有什么区别？</u>

<h4 id="G6KFI"><u>头文件深度剖析</u></h4>
<u>编译器在编译各个C源文件的过程中，如果该C文件引用了其他文件中定义的函数或变量，编译器也不会报错，链接器在链接的时候会到这个文件里查找你引用的函数，如果没有找到才会报错。但是编译器为了检查你的函数调用格式是否存在语法错误，形参实参的类型是否一致，会要求程序员在引用其他文件的全局符号之前必须先声明，如变量的类型、函数的类型等，编译器会根据你声明的类型对编写的程序语句进行语法、语义上的检查。为了方便，将函数的声明直接放到头文件里，作为本模块封装的API，供其他模块使用。程序员在其他文件中如果想引用这些API函数，则直接＃include这个头文件，然后直接调用。</u>

<u>变量的声明和定义的区别：</u><u><font style="background-color:#fbf5b3;">是否分配内存是区分定义和声明的唯一标准。</font></u>

<u>一个变量的定义最终会生成与具体平台相关的内存分配汇编指令。</u>

<u>变量的声明则告诉编译器，该变量可能在其他文件中定义，编译时先不要报错，等链接的时候可以到指定的文件里去看看有没有，如果有就直接链接，如果没有则再报错也不迟。一个变量只能定义一次，即只能分配一次存储空间，但是可以多次声明。一般变量的定义要放到C文件中，不放到头文件中，因为头文件可能被多人使用，被多个文件包含，头文件经过预处理器多次展开之后也就变成了多次定义。</u>

**<u>头文件重复包含</u>**

<u>如果在一个项目中多次包含相同头文件，编译器也不会报错，因为预处理器在预处理阶段已经将头文件展开了：一个变量或函数可以有多次声明，这是编译器允许的。如果在头文件里定义了宏或一种新的数据类型，头文件再多次包含展开，编译器在编译时可能会报重定义错误。为了防止这种错误产生，可以在头文件中使用条件编译来预防头文件的多次包含。</u>

<h5 id="Q2y9W"><u>隐式声明</u></h5>
<u>（ANSI C标准支持，</u><font style="background-color:#fbf5b3;">但C99/C11/C++标准已禁止</font><u>)</u>

<u>如果一个C程序引用了在其他文件中定义的函数而没有在本文件中声明，编译器也不会报错，编译器会认为这个函数可能会在其他文件中定义，等链接的时候找不到其定义才会报错，而是会给一个警告信息并自动添加一个默认的函数声明。这个声明我们称为隐式声明。</u>

<u>函数的隐式声明可能与自定义函数冲突，如果我们引用库函数而没有包含对应的头文件，也有可能与库函数发生类型冲突。这些函数类型冲突虽然不影响程序的正常运行，但是会给程序带来很多无法预料的深层次bug，在不同的编译环境下，函数的运行结果甚至可能都不一样。为了编写高质量稳定运行的程序，我们要养成“先声明后使用”的良好编程习惯。</u>

<h5 id="JMZWU"><u>变量的声明与定义</u></h5>
<u>extern关键字对</u><u>外部文件的符号进行声明</u>

```cpp
extern int i;
extern int a[20],
extern struct student stu;
extern int function();
extern“c” int function();
```

<u>extern声明的变量或函数在别的文件里定义，在本文件使用，告诉编译器不要报错。</u>

```cpp
//i.c
int i = 10;
int a[10]={1,2,3,4,5,6,7,8,9};
struct student
int age;
int num;
```

```cpp
//main.c
#include <stdio.h>
extern int i;
extern int a[10];
struct student{
int age;
int num;
extern struct student stu;
extern int k;
int main(void)
printf("%s:i =%d\n",_func_,i);
for(int j=0;j<10;j++)
    printf("a[%d]:%d\n"，j，a[j]);
        printf("stu.age =%d,num = %d\n",stu.age, stu.num);
printf("%s:k=%d\n",_func_,k);
return 0;
```

<h5 id="Iky4L"><u>如何区分定义和声明</u></h5>
<u>定义的本质就是为对象分配存储空间，声明则将一个标识符与某个C语言对象相关联(函数、变量等)。</u>

<u>声明函数原型为了提供给编译器做函数参数格式检查，声明一个变量，是为了告诉编译器，这个变量已经在别的文件里定义，我们想在本文件里使用它。在C语言中，我们可以声明各种各样的标识符：变量名、函数名、类型、类型标志、结构体、联合、枚举常量、语句标号、预处理器宏等。</u>

<u>（1）从extern的角度区别定义和声明：</u>

<u>如果省略了extern且具有初始化语句，则为定义语句。如int i=10。</u>

<u>如果使用了extern，无初始化语句，则为声明语句。如extern int i；。</u>

<u>如果省略了extern且无初始化语句，则为试探性定义。如int i；。</u>

<u>试探性定义(int i)。该变量可能在别的文件里有定义，所以先暂时定为声明。若别的文件里没有定义，则按照语法规则初始化该变量i，并将该语句定性为定义。一般这些变量会初始化为一些默认值：NULL、0、undefined values等。</u>

<u>（2）编译链接的角度去分析int i：</u>

<u>对于未初始化的全局变量，它是一个弱符号，先定性为声明。如果其他文件里存在同名的强符号，那么这个强符号就是定义，把这个弱符号看作声明没毛病；如果其他文件里没有强符号，那么只能将这个弱符号当作定义，为它分配存储空间，初始化为默认值。</u>

<h5 id="SBGDr"><u>前向引用和前向声明</u></h5>
<u>无论声明什么类型的标识符，先声明后使用。</u>

<u>因为早期的编译器鉴于计算机内存资源限制，不可能同时编译多个文件，所以只能采取单独编译。编译器为了简化设计，采用了one-pass compiler设计，每个源文件只编译一次，这也决定了C语言“先声明后使用”的使用原则。</u>

<u>"先声明后使用"指一个标识符要在声明完成之后才能使用，在声明完成之前不能使用。</u>

**什么是声明完成呢？**

<u>一个变量的声明无非就是声明其类型，声明是给编译器看的，是为了应付编译器语法检查的。如果已经让编译器知道了这个标识符的类型，那么就认为声明完成了。</u>

<u>在C语言中，并不是所有的标识符都需要先声明后使用。</u>

<u>如果一个标识符在未声明完成之前就引用，被称为前向引用。</u>

<u>在C语言中，有3个可以前向引用的特例。</u>

<u>● 隐式声明</u>

<u>● 语句标号：跳转向后的标号时，不需要声明，可以直接使用。</u>

<u>● 不完全类型：在被定义完整之前用于某些特定用途。</u>

<font style="background-color:#fbf5b3;">语句标号</font><u>：使用C语言的goto关键字可以往前跳，也可以往后跳，不需要对语句标号进行事先声明。</u>

<u>不完全类型是 指 那些尚未提供完整信息的类型。这种类型的对象或指针可以被声明和使用，但它们不能被定义（即分配存储空间。</u>

<u>（1）数组类型未知大小：</u>

<u>当数组声明时没有指定大小，例如 </u>`int a[];`<u> 这样一个数组就是一个不完全类型。在这种情况下，编译器不知道数组的确切大小，因此无法为它分配具体的内存空间。但是你可以有一个指向该数组类型的指针，比如 </u>`int *p = a;`<u> 只要之后通过其他方式明确了数组的大小，就可以正常使用了。</u>

<u>（2）结构体或联合体类型未知内容：如果结构体或联合体只被命名而没有给出其成员的定义，那么这个结构体或联合体就是一个不完全类型。</u>

<h5 id="DROty"><u>定义与声明的一致性</u></h5>
```cpp
//add.h
int add(int a, int b);
//add.c
#include"add.h"
int add(int a, int b)
return a+b;
//main.c
#include "add.h"
int main(void){
    int sum; 
    sum = add(1,2);
    return 0;
}
```

<font style="background-color:#fbf5b3;">在模块里包含自己的头文件</font><u>，可以使用头文件中定义的宏或数据类型，还有一个好处就是可以让编译器检查定义与声明的一致性。在模块的封装中，接口函数的声明和定义是在不同的文件里分别完成的，很多人在编程时可能比较粗心，一个函</u>

<u>数在声明和定义时的类型可能不一致，但是编译器又是以文件为单位进行编译的，无法检测到这个错误，那该怎么办？很简单，我们把一个函数的声明和定义放到一个文件中，编译器在编译时就会帮我们进行自检：检查一个函数的定义和声明是否一致，避免出现低级错误。</u>

<h5 id="zGTnT"><u>头文件路径</u></h5>
<u>头文件两种包含方法</u>

```cpp
#include <stdio.h>
#include“module.h”
```

<u><>表示引用标准库的头文件</u>

<u>如果你使用的头文件是自定义的或项目中的头文件，一般使用双引号""包含。头文件路径一般分为绝对路径和相对路径：绝对路径以根目录“/”</u>

<u>编译器在编译过程中会按照这些路径信息到指定的位置查找头文件，然后通过预处理器做展开处理。在查找头文件的过程中，编译器会按照默认的搜索顺序到不同的路径下去搜索。</u>

<u>使用<>包含头文件：</u>

<u>GCC参数gcc-I指定的目录->环境变量CINCLUDEPATH指定的目录->GCC的内定目录。当不同目录下存在相同的头文件时，先搜到哪个就使用哪个，搜索到头文件后不再往下搜索。</u>

<u>在程序编译时，如果头文件没有放到官方路径下面，那么可以通过gcc-I来指定头文件路径，编译器在编译程序时，就会到用户指定的路径目录下面去搜索该头文件。如果你不想通过这种方式，也可以通过环境变量来添加头文件的搜索路径。</u>

<u>用双引号""来包含头文件路径：</u>

<u>编译器会首先在项目当前目录搜索需要的头文件，如果在当前项目目录下搜不到，则再到其他指定的路径下去搜索。</u>

<u>项目当前目录->通过GCC参数gcc-I指定的目录->环境变量CINCLUDEPATH指定的目录->GCC的内定目录.</u>

<u>常见的内定目录</u>

```cpp
/usr/include
    /usr/local/include
    /usr/include/i386-linux-gnu
    /usr/lib/gcc/i686-linux-gnu/5/include
    /usr/lib/gcc/i686-linux-gnu/5/include-fixed
    /usr/lib/gcc-cross/arm-linux-gnueabi/5/include
```

<h5 id="RWajx"><u>头文件中的内联函数</u></h5>
<u>使用inline关键字修饰的函数称为内联函数。内联函数也是函数，它和普通函数的不同之处在于，编译器在编译内联函数时，会根据需要在调用处直接展开，从而省去了函数调用开销。对于一些频繁调用而又短小精悍的函数，如果我们将其声明为内联函数，编译器编译时像宏一样展开，可以提升程序的运行效率。内联函数和宏相比，除了能像宏一样在调用处直接展开，在参数传递、参数检查、返回值等方面比宏更有优势。正是这种优势，内联函数在C语言中被广泛使用。但是函数虽然变成了内联函数，但是在编译的时候会不会展开还得由编译器决定。</u>

<u>内联函数一般定义在.C文件中，但是内联函数也可以定义在头文件中。一般来讲，变量和函数是不能在头文件中定义的，因为该头文件可能被多个C文件包含，当被预处理器展开后就变成了多次定义，很可能报重定义错误。当多个模块引用该头文件时，内联函数在编译时已经在多个调用处展开，不复存在了，不存在重定义问题。即使编译器没有对内联函数展开，也可以在内联函数前通过添加一个static关键字将该函数的作用域限制在本文件内，从而避免了重定义错误的发生。</u>

```cpp
static inline void func(int a, int b);
```

<h4 id="HHG2e"><u>模块设计原则</u></h4>
<font style="background-color:#fbf5b3;">高内聚低耦合</font><u>是模块设计的基本原则。</u>

<u>高内聚：各个模块在实现各自功能的时候，要自己的事自己做，自己的功能自己实现，尽量不麻烦其他模块。一个模块要想实现高内聚，首先模块的功能要尽可能单一，一个功能由一个模块实现，这样才能体现模块的独立性，进而实现高内聚。要尽量调用本模块实现的函数，减少对外部函数的依赖，这样可以进一步提高模块的独立性，提高模块的内聚度。</u>

<u>与模块内聚对应的是模块耦合。</u>

<u>模块耦合指的是模块间的关联和依赖，包括调用关系、控制关系、数据传递等。模块间的关联越强，耦合度就越高，模块的独立性越差，内聚度也就随之越低。</u>

<u>不同模块之间有不同的耦合方式。</u>

<u>●非直接耦合：两个模块之间没有直接联系。</u>

<u>●数据耦合：通过参数来交换数据。</u>

<u>●标记耦合：通过参数传递记录信息。</u>

<u>●控制耦合：通过标志、开关、名字等，控制另一个模块。</u>

<u>●外部耦合：所有模块访问同一个全局变量。</u>

<u>我们在设计模块时，要尽量降低模块的耦合度。</u>

<u>低耦合有很多好处，如可以让系统的结构层次更加清晰，升级维护起来更加方便。在C语言程序中，我们可以通过下面的常用方法降低模块的耦合度。</u>

<u>● 接口设计：隐藏不必要的接口和内部数据类型，模块的API封装在头文件中，其余函数使用static修饰。</u>

<u>● 全局变量：尽量少使用，可改为通过API访问以减少外部耦合。</u>

<u>● 模块设计：尽可能独立存在，功能单一明确，接口少而简单。</u>

<u>● 模块依赖：模块之间最好全是单向调用，上下依赖，禁止相互调用。</u>

<h4 id="IC1nK"><u>被误解的关键字：goto</u></h4>
<u>goto不是一无是处，其无条件跳转的特性有时候会大大简化程序的设计。如有多个出错出口的函数，我们可以使用goto将函数内的出错指定一个统一的出口，统一处理，反而会使函数的结构更加清晰。</u>

```cpp
int func(void){
    dosomething;
    if(expr1) goto err;
    do sth;
        if(expr2)
        goto err;
    return @;
    err:
    return -1
        }
```

<u>通过代码复用，将一个函数多个出口归并为一个总出口，然后在总出口处对出错统一处理，释放malloc() 申请的动态内存、释放锁、文件句柄等资源。通过函数内部这种模块化的设计，既提高了效率，又不会破坏程序原来的结构。</u>

<u>在一个多重循环程序中，如果我们想从最内层的循环直接跳出，则需要多次使用break和return，层层退出才能达到预期目的,使用goto无条件跳转，简单粗暴,</u><u>一步到位。</u>

```cpp
for(cxpr1){
    for(expr2){
        for(expr3){
            for(expr4){
                if(expr5)
                    goto endloop;
            }}}}
return @;
endloop:
return -1;
```

<u>注意事项：goto在使用的过程中，也有一些需要注意的地方，如只能往下跳，不能往上跳。使用goto只能在同一函数内跳转，函数内goto标签的位置也有一定的讲究，goto标签一般在函数体内两段不同逻辑功能代码的交界处，用来区分函数内的模块化设计和逻辑关系。</u>

<h4 id="TfEqV"><u>模块间通信</u></h4>
<u>系统内的各个模块可以通过各种耦合方式进行通信</u>

<h5 id="yHBBA"><u>全局变量</u></h5>
<u>各个模块共享全局变量是各个模块之间进行数据通信最简单直接的方式。一个全局变量具有文件作用域，但是我们可以通过extern关键字将全局变量的作用域扩展到不同的文件中，然后各个模块可以通过全局变量进行通信了。</u>

<u>但是这样耦合度比较高，改进的方法：</u><u>对全局变量的直接访问修改为通过函数接口间接访问。就像类的私有成员一样，该全局变量只能在一个模块中创建或直接修改，如果其他模块想要访问这个全局变量，则只能通过引出的函数读写接口进行访问。</u>

```cpp
//module.h
void val set(int value)；
int val_get(void)；
//module.c
int global val = 10；
void val set(int value){
    global_val = value；
        }
int val_get(void){
    return global _val；
        }
```

<u>linux内核模块1：</u>

```cpp
#include <linux/init.h>
#include <linux/module.h>
MODULE_LICENSE("GPL");
int global_val = 10;
EXPORT_SYMBOL(global_val);
int get_global_val_value(void){
    return global_val;
}
void set_global_val_value(int a){
    global_val = a;
}
static int __init module1_init(void){
    printk(KERN_INFO "hello module1!\n");
    printk(KERN_INFO "module1:global_val = %d\n", global_val);
    return 0;
}
static void __exit module1_exit(void)
{
    printk(KERN_INFO "goodbye, module1!\n");
}
module_init(module1_init);
module_exit(module1_exit);
```

<u>linux内核模块2:</u>

```cpp
#include <linux/init.h>
#include <linux/module.h>
#include <asm-generic/errno.h>
MODULE_LICENSE("GPL");
extern int global_val;
static int __init module2_init(void){
    printk(KERN_INFO "hello module2!\n");
    printk(KERN_INFO "module2:global_val = %d\n", global_val);
    return 0;
}
static void __exit module2_exit(void){
    printk(KERN_INFO "goodbye, module2!\n");
}
module_init(module2_init);
module_exit(module2_exit);
```

<u>两个模块编译后insmod到内核中，模块2可以访问到模块1的全局变量。</u>

<u>通过共享全局变量进行模块间通信，实现最简单，也最容易理解，因此在各个项目中被广泛使用，包括在生产者-消费者模型中常用的共享缓冲区，其实也是基于这个思想设计的。</u>

<h5 id="bWhpv"><u>回调函数</u></h5>
<u>一个系统的不同模块还可以通过数据耦合、标记耦合的方式进行通信，即通过函数调用过程中的参数传递、返回值来实现模块间通信。</u>

```cpp
// module.c
#include <stdio.h>
int send_data(char *buf, int len) {
    char data[100];
    int i;
    for(i = 0; i < len; i++)
        data[i] = buf[i];
    for(i = 0; i < len; i++)
        printf("received data[%d] = %d\n", i, data[i]);
    return len;
}
// main.c
#include <stdio.h>
#include "module.h"
int main(void) {
    char buffer[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
    int return_data;
    return_data = send_data(buffer, 10);
    printf("send data len:%d\n", return_data);
    return 0;
}
```

<u>通过send_data()函数将main.c模块buffer 中 的 数 据 传 递 到 module.c 模 块 并 进 行 打 印 ， 同 时 通 过send_data()函数的返回值将数据传递的长度信息从module.c模块反馈给main.c模块。</u>

<u>这种通信方式是单向调用的，无法实现双向通信。一个系统通过模块化设计，各个模块之间最理想的关系是一种上下依赖的关系，每一层的模块都是对下一层的封装，并留出API供上一层调用。每一层的模块只能主动调用下一层模块提供的API，然后自己封装成API供上一层的模块调用。但是当底层的模块想主动与上一层的模块进行通信时，该如何实现？</u>

<u>model.h</u>

```cpp
#ifndef RUNCALLBACK_H
#define RUNCALLBACK_H
// 声明回调函数类型
typedef void (*callback_func)(void);
// 声明运行回调函数的函数
void runcallback(callback_func fp);
#endif // RUNCALLBACK_H
```

<u>model.c</u>

```cpp
#include <stdio.h>
#include "module.h"
// 定义运行回调函数的函数
void runcallback(callback_func fp){
    // 调用传入的回调函数
    fp();
}
```

<u>main.c</u>

```cpp
#include <stdio.h>
#include "module.h"
// 定义两个回调函数
void func1(void)
{
    printf("func1...\n");
}
void func2(void)
{
    printf("func2...\n");
}
// 主函数
int main(void)
{
    // 运行回调函数
    runcallback(func1);
    runcallback(func2);
    return 0;
}
```

<u>通过回调函数的设计，两个模块之间可以实现双向通信。模块之间通过函数调用或变量引用产生了耦合，也就有了依赖关系。</u><u>因此为了 减少模块间的耦合性，我们可以在两个模块之间定义一个抽象接口。</u>

**device_manager.h**

```cpp
#ifndef STORAGE_DEVICE_H
#define STORAGE_DEVICE_H
typedef int (*read_fp)(void);
struct storage_device {
char name[20];
read_fp read;
};
extern int register_device(struct storage_device dev);
extern int read_device(const char* device_name);
#endif // STORAGE_DEVICE_H
```

**device_manager.c**

```cpp
#include <stdio.h>
#include <string.h>
#include "device_manager.h"
struct storage_device device_list[100] = {0};
unsigned char num = 0;
int register_device(struct storage_device dev) {
    device_list[num++] = dev;
    return 0;
}
int read_device(const char* device_name) {
    int i;
    for (i = 0; i < 100; i++) {
        if (!strcmp(device_name, device_list[i].name)) {
            return device_list[i].read();
        }
    }
    printf("Error! Can't find device: %s\n", device_name);
    return -1;
}
```

<u>main.c</u>

```cpp
#include <stdio.h>
#include "device_manager.h"
int sd_read(void) {
    printf("SD read data...\n");
    return 10;
}
int udisk_read(void) {
    printf("Udisk read data...\n");
    return 20;
}
int main(void) {
    struct storage_device sd = {"sdcard", sd_read};
    struct storage_device udisk = {"udisk", udisk_read};
    register_device(sd); // 高层模块函数注册，以便回调
    register_device(udisk);
    read_device("udisk"); // 实现回调, 控制反转
    read_device("sdcard");
    return 0;
}
```

`device_manager.h`<u> 中，我们定义了一个抽象接口 </u>`read_fp`<u>，它是一个函数指针类型，指向一个没有参数并返回 </u>`int`<u> 类型的函数。这个接口允许任何设备实现自己的 </u>`read`<u> 函数，而主模块不需要知道具体的实现细节。</u>

<u>同一个头文件中，我们定义了一个 </u>`struct storage_device`<u> 结构体，它包含一个设备名称和一个指向 </u>`read_fp`<u> 类型函数的指针。这个结构体就是模块间通信的接口。</u>

<u>在 </u>`device_manager.c`<u> 中，实现了 </u>`register_device`<u> 和 </u>`read_device`<u> 函数。</u>`register_device`<u> 函数允许设备注册自己的 </u>`read`<u> 函数，而 </u>`read_device`<u> 函数通过设备名称查找并调用相应的 </u>`read`<u> 函数</u>

<h4 id="AeIn0"><u>异步通信</u></h4>
<u>函数调用，回调函数都是同步阻塞式调用。</u>

<u>CPU在访问一个资源时，如果资源没有准备好需要等待，CPU什 么也不干，原地打转干等就是同步通信，CPU去干其他事情，等资源准 备好了通知CPU，CPU再来访问就是异步通信。</u>

<u>常用的异步通信如下。</u>

<u>● 消息机制：具体实现与平台相关。</u>

<u>● 事件驱动机制：状态机、GUI、前端编程等。</u>

<u>● 中断。</u>

<u>● 异步回调。</u>

<u>在Linux操作系统中，各个模块间也会采用不同的异步通信方式进行通信：Linux内核模块之间可以使用notify机制进行通信；内核和用户之间可以通过AIO、netlink进行通信；用户模块之间异步通信的方</u>

<u>式更多，除了操作系统支持的管道、信号、信号量、消息队列，还可以使用socket、PIPE、FIFO等方式进行异步通信(?)</u>

