# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
module SRFF(s,r,clk,rst,Q);
input s,r,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
  Q=1'b0;
else if(s==0 && r==0)
   Q=Q;
else if(s==0 && r==1)
  Q=1'b0;
else if(s==1 && r==0)
  Q=1'b1;
else
   Q=1'bx;
 end
 endmodule 

```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_SRFF;
 reg s,r,clk,rst;
 wire Q;
 SRFF uut(s,r,clk,rst,Q);
 always #5 clk=~clk;
 initial begin
 clk=0;s=0;r=0;rst=1;
 #10 rst=0;
 #10 s=1;r=0;
 #10 s=0;r=0;
 #10 s=0;r=1;
 #10 s=1;r=1;
 #10 s=0;r=0;
 #20 $finish;
 end 
 endmodule



```
#### SIMULATION OUTPUT
<img width="940" height="563" alt="image" src="https://github.com/user-attachments/assets/9019c515-10e2-4c58-91eb-14642bb26fd2" />


### JK Flip-Flop (Blocking)
```verilog
module JKFF(J,K,clk,rst,Q);
input J,K,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
  Q=1'b0;
else if(J==0 && K==0)
   Q=Q;
else if(J==0 && K==1)
  Q=1'b0;
else if(J==1 && K==0)
  Q=1'b1;
else
   Q=~Q;
 end
 endmodule 

```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
 module tb_JKFF;
 reg J,K,clk,rst;
 wire Q;
 JKFF uut(s,r,clk,rst,Q);
 always #5 clk=~clk;
 initial begin
 clk=0;J=0;K=0;rst=1;
 #10 rst=0;
 #10 J=1;K=0;
 #10 J=0;K=0;
 #10 J=0;K=1;
 #10 J=1;K=1;
 #10 J=0;K=0;
 #20 $finish;
 end 
 endmodule



```
#### SIMULATION OUTPUT

<img width="940" height="561" alt="image" src="https://github.com/user-attachments/assets/be84a8ee-cb02-43eb-9161-7e8ca1cd86bb" />


### D Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module DFF(clk,rst,d,q);
input clk,rst,d;
output reg q;
always @(posedge clk)
begin
if(rst==1)
q=0;
else
q=q;
end 
endmodule

```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_DFF;
reg clk,rst,d;
wire q;
DFF uut(clk,rst,d,q);
always #5 clk=~clk;
initial
begin
clk=0;
d=0;
rst=1;
#10
rst=0;
d=0;
#10
d=1;
#10
$finish;
end 
endmodule


```

#### SIMULATION OUTPUT

<img width="940" height="566" alt="image" src="https://github.com/user-attachments/assets/38f60b18-4f09-4bf8-9c0e-dd691b2370b5" />


### T Flip-Flop (Blocking)
```verilog
module TFF(clk,rst,T,Q);
input clk,rst,T;
output reg Q;
always @(posedge clk)
begin
if(rst==1)
Q=0;
else if(T==0)
Q=Q;
else
Q=~Q;
end
endmodule

```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_TFF;
reg clk,rst,T;
wire Q;
TFF uut(clk,rst,T,Q);
always #5 clk=~clk;
initial
begin
clk=0;
T=0;
rst=1;
#10
rst=0;
T=0;
#10
T=1;
$finish;
end 
endmodule


```

#### SIMULATION OUTPUT

<img width="940" height="566" alt="image" src="https://github.com/user-attachments/assets/be85b8e3-82ef-4ddc-8c43-079ea5b04375" />


### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
