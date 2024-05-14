# EXP.NO:01
# DATE  :13/02/2024
# SIMULATION AND IMPLEMENTATION OF LOGIC GATES,ADDERS AND SUBTRACTOR

**AIM:**

To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

**APPARATUS REQUIRED:**

VIVADO 2023.1

**PROCEDURE:**

Open Vivado: Launch Xilinx Vivado software on your computer.

Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

Logic Diagram :

Logic Gates:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)


CODE
```
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);  
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```

OUTPUT

<img width="838" alt="320503583-671893c0-3f17-4f78-a7de-7dcd11c016bb" src="https://github.com/naveenkumar0404/VLSI-LAB-EXP-01/assets/127510390/faa6c9f7-d3b0-4929-9e59-8842e17190bf">

Half Adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)

CODE
```
module HalfAdder(a,b,sum,carry);

input a,b;

output sum,carry;

xor (sum,a,b);

and (carry,a,b);

endmodule
```

OTUPUT

<img width="809" alt="320504329-3bf4e32e-680a-46f0-92ac-2ccdd182bf07" src="https://github.com/naveenkumar0404/VLSI-LAB-EXP-01/assets/127510390/a593fd8b-fa77-44c3-869a-dc3fad51899c">


Full adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)

CODE
```
 module FA(a,b,cin,sum,cout);

input a,b,cin;

output sum,cout;

wire w1,w2,w3;

xor g1(w1,a,b);

and g2(w2,w1,cin);

and g3(w3,a,b);

xor g4(sum,w1,cin);

or g5(cout,w2,w3);

endmodule
```
OUTPUT

<img width="1203" alt="320504863-03d00b9d-c7dc-4341-92dd-46ac1f066b25" src="https://github.com/naveenkumar0404/VLSI-LAB-EXP-01/assets/127510390/a89de9d0-0cd0-4858-8af3-6e67f639db3c">

Half Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)

CODE 
```
 module halfsubtractor(a,b,diff,borrow);

input a,b;

output diff,borrow;

xor g1(diff,a,b);

and g2(borrow,~a,b);

endmodule
```

OUTPUT

<img width="785" alt="320505250-4fba2152-ff5d-4f96-8679-5f3f03224ce5" src="https://github.com/naveenkumar0404/VLSI-LAB-EXP-01/assets/127510390/b81bc3c5-9354-44e8-8284-b95f8eeac696">

Full Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)

CODE
```
module full_sub(a,b,bin,diff,borrow);

input a,b,bin;

output diff,borrow;

wire w1,w2,w3;

xor g1(w1,a,bin);

and g2(w2,~a,b);

xor g3(diff,w1,bin);

or g4(borrow,w2,w3);

and g5(w3,~w1,bin);

endmodule
```

OUTPUT
<img width="1280" alt="320505639-cf6fdf6a-2a09-4954-ad40-4f387712a9f9" src="https://github.com/naveenkumar0404/VLSI-LAB-EXP-01/assets/127510390/64c20015-f1f1-42b9-8468-1684380c7049">

8 Bit Ripple Carry Adder

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)

CODE
```
 module fa(a,b,c,sum,carry);

input a,b,c;

output sum,carry;

assign sum = a^b^c;

assign carry=(a&b)|(b&c)|(c&a);

endmodule

module rca(a,b,cin,sum,cout);

input [7:0]a,b;

input cin;

output [7:0]sum;

output cout;

wire c1,c2,c3,c4,c5,c6,c7;

fa fa1(a[0],b[0],cin,sum[0],c1);

fa fa2(a[1],b[1],c1,sum[1],c2);

fa fa3(a[2],b[2],c2,sum[2],c3);

fa fa4(a[3],b[3],c3,sum[3],c4);

fa fa5(a[4],b[4],c4,sum[4],c5);

fa fa6(a[5],b[5],c5,sum[5],c6);

fa fa7(a[6],b[6],c6,sum[6],c7);

fa fa8(a[7],b[7],c7,sum[7],cout);

endmodule
```
OUTPUT

<img width="752" alt="320506086-3807a057-7d3b-4a1e-83cf-bc61eab17a03" src="https://github.com/naveenkumar0404/VLSI-LAB-EXP-01/assets/127510390/bda2c7bc-b6e5-42c5-8108-f63de1ecd34d">

**RESULT:**
 Thus the simulation and implementation of combinational logic circuit is done and outputs are verified successfully.

