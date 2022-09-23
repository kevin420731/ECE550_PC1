The introduction of the author of this project checkpoint:
This project is totally completed by myself. My name is Kevin.Shen,  my netID is ks713, My Duke Unique ID is 1195512.
The introduction of the implement logic of this project checkpoint:
The top level design entity of my project is the module alu, which accepts the given inputs and output the results in the format required for this project ,I personally use carry select adder to implement every important operations in this checkpoint.  My carry select adder takes two 32-bit input  in1, in2, and output a 32-bit sum of in1, in2 and carry out bit of in1+in2, and the carry out bit of in1[30:0]+in2[30:0]. Another important module I have used in this project is called INVERSE, which will take one 32-bit input and output the 2's complement of this input. Therefore, the top level logic of my project point is this: first, I make a new variable [31:0]c1 and let it be the output of module INVERSE in my alu.v file which take data_operandB as input, that means c1=-data_operandB,then , I make new variables c2,[31:0]c3,c4,c5, because ctrl_ALUoptcode can either be "00000" for addition or "00001" for subtraction, then, for this check point I use the last bit of ALUoptcode to determine the operation , if it is 0, I will assign c3 equals to data_operandB , otherwise I will assign c3 equals to c1 , which equals -data_operandB, then, I will call module select_adder with inputs data_operandA, c3, and desired output data_result, c2,c4 , where c2, c4 stands the carry out bits for data_operandA[31:0]+c3[31:0] and data_operandA[30:0]+c3[30:0], after that I will output the data_result, to determine the overflow that required in this checkpoint, I will first use xor gate to calculate the xor of c2 and c4 and output it as variable c5. I think the overflow is equals to c5, therefore I assign overflow=c5?1:0. That is all about my top level logic of this project checkpoint.
The introduction of the implement logic of important modules in my project checkpoint:
module FULL_ADDER(in1,in2,cin,sum,cout):
   for this module I implemented just use structural verilog by definition:
         that is sum=(in1^in2)^cin, cin=((in1^in2)&cin)|(in1&in2); (I implemented in structural verilog, this is just for clarification)
module adder_16(in1,in2,cin,sum,cout,precout);
  for this module I just implemented it step by step as a small RCA adder, here the input in1,in2 are all 16 bits and cin is 1 bit, output cout and precout are all 1 bit, The difference between my 16 bit RCA adder and normal 16 bit RCA adder is that I add a parameter called precout, while cout is the final carry out bit of the adding process of this two 16-bit integer, precout is just the carry out bit of the adding for first 15 bits for these two integers.
module not_gate(out,in);
input in;
output out;
For this module, it is just a bit wise not operation module implemented by myself, the input and output of this module are both 1 bit, my logic is that if in is 1 then out  is 0, if in is 0, then out is 1, which is implemented as assign out=in?0:1.
module INVERSE(in,out);
input [31:0]in;
output [31:0]out;
For this module, I use it to get the 2's complement of input in and output it as out, the method is that I negate every bits in original input in and let 1 plus in(which will call carry_select_adder module, the module will explained later), and then I get the correct result.
module carry_select_adder(in1,in2,sum,cout,precout);
input [31:0] in1,[31:0] in2;
output [31:0] sum;
output out ,precout;
As explained earlier, precout is the carry out bit of adding first 30 bits of two 32-bit signed inputs.
The detailed logic of this carry_select_adder is that I first add first 16 bits of these two integers, get the sum,cout, precout for first 16 bits, this sum can be assigned to first 16 bits of the output sum of this module. And then, I add another 16 bits of these two integers twice, but I use cin as 1 in the first time and cin as 0 in the second time, and get the corresponding sums,couts, precouts. And then, I use the cout bit of the adding for first 16 bits to determine the assignment of the variable sum,out,precout. The logic is that if the cout bit of the adding for first 16 bits is 1 , I will assign sum[31:16],out ,precoutwith the results by adding the second 16 bits of these two integers with cin 1. On the other hand, I will assign sum[31:16], out ,precout  with the results by adding the second 16 bits with cin 0.
module alu(data_operandA, data_operandB, ctrl_ALUopcode, ctrl_shiftamt, data_result, isNotEqual, isLessThan, overflow);
The input and output that I need to consider in this assignment are:
input [31:0] data_operandA, data_operandB;
input [5:0] ctrl_ALUopcode;
output [31:0] data_result;
output overflow;
The detailed logic of this module has been explained by myself in the very first part.
In conclusion, this README file has talked about my implementation of project checkpoint 1 in a very detailed and comprehensive way.
