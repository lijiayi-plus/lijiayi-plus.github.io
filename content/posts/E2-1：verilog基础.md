---
title: "E2.1：verilog基础"
date: "2026-10-13T20:18:44+08:00"
slug: "E2-1：verilog基础"
series: "一生一芯"
weight: 3
tags: ["学习记录"]
aliases: ["/2026/10/13/E2-1：verilog基础/"]
---

## Verilog Language-Vectors章节
我们使用[Vector2 - HDLBits](https://hdlbits.01xz.net/wiki/Vector2)进行学习，我觉得这实在是学习的一个很好的途径，因为比实物好用很多，而且来说。在闲暇时间编写代码，我觉得是休息的一个很好的选择，遂记录

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20261013172050376.png)

在这里我一开始还是看错了，以为是按位的反转，没想到是按照字节进行反转，按照字节反转还是比较简单的，一方面可以直接使用多个assign进行组合：
`assign out[7:0]=in[31:24];`
这样的语句，另一方面可以使用略带一些组合的方法，例如：
`assign out ={in[7:0],in[15:8],in[23:16],in[31:24]};`

但是我发现一个有点意思的，就是按位反转，

```verilog
module top_module( 
    input [31:0] in,
    output [31:0] out );//
    genvar i;
    generate
	    for (i=0;i<32;i=i+1) begin:reverse_gate
	    assign out[i]=in[31-i];
	    end
	endgenerate

endmodule

```

这个genvar就很有意思，这个语句是声明一个i，作为循环使用的。但是verilog里面的循环是和CPU不一样的，里面是循环编译，就是这一句话会同时编译出32个线。

begin后面不加冒号，但是这里的编译需要有一个名称，所以这里是`begin:reverse_gate`。

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20261013173011262.png)
这是一个多输入的逻辑运算，分别有按位运算和整体的逻辑运算。

按位的运算，主要有 ~  &  |  ^  ~^这几个，分别是非，与，或，异或，同或。而逻辑运算则是，！，&&，|| 这几个符号。

这个也不难，最后的结果如下：
```verilog
module top_module( 
    input [2:0] a,
    input [2:0] b,
    output [2:0] out_or_bitwise,
    output out_or_logical,
    output [5:0] out_not
);
    assign out_or_bitwise=a|b;
    assign out_or_logical=a||b;
    assign out_not = {~b,~a};
endmodule
```

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20261013195113997.png)
这个也很有意思，左边等于右边的一种新写法。

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20261013195431486.png)

类似于前面循环编译的一道题，但是参考答案却非常的简洁，是不是还有点丑陋了。
`assign {out[0],out[1],out[2],out[3],out[4],out[5],out[6],out[7]} = in;`

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20261013195728969.png)
注释的魅力所在
```verilog
module top_module( 
    input [7:0] in,
    output [7:0] out
);
    always @(*) begin	
	for (int i=0; i<8; i++)
		out[i] = in[7-i];
end

endmodule

```

整体来说，复杂的组合逻辑电路相比是always里面嵌套循环更加合适，而generate的目的则只是对于代码进行复制的操作。

![image.png](https://bucket-plusone.oss-cn-wuhan-lr.aliyuncs.com/img/20261013200911802.png)
最后一题，有点意思。这道题目涉及到拼接，以及声明变量，大括号的嵌套，逻辑符号里面的小括号的填写，有点意思。