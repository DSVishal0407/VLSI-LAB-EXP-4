**4. SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS**

**AIM:**

To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

**APPARATUS REQUIRED:**

Xilinx 14.7
Spartan6 FPGA

**PROCEDURE:**

1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.


**SR FLIPFLOP:**

**TRUTH TABLE:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)

**VERILOG CODE:**

```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```
**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/30cceb50-ed81-4180-ba0c-a03d9bfb637f)

**JK FLIPFLOP:**

**TRUTH TABLE:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

**VERILOG CODE:**

```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```

**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/ca9b98ec-5e8a-4657-8577-eacd8b4cba41)

**T FLIPFLOP:**

**TRUTH TABLE:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

**VERILOG CODE:**

```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```
**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/3fa1e0ce-8c6b-4bc8-8e9b-01db694fc2f5)

**D FLIPFLOP:**

**TRUTH TABLE:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

**VERILOG CODE:**

```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```

**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/1add7d64-0b35-468f-b0a6-6a273c939a6b)

**COUNTER:**

**TRUTH TABLE:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

**VERILOG CODE:**

**updown Counter:**

```
module updown(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/ac6b26c7-8f24-41ce-8c1e-50f55bd24a66)

**Mod 10 Counter:**

```
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/06b4e3c2-9630-46de-8d70-b84c563e45ce)

**Ripple Counter:**

```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```

**OUTPUT WAVEFORM:**

![image](https://github.com/DSVishal0407/VLSI-LAB-EXP-4/assets/163637297/0e48cc4f-e8c8-4953-a86c-4dbd972b67ab)

**RESULT:**

Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGNS are simulated and synthesised using Xilinx ISE.

