# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)
![Screenshot 2025-05-21 103851](https://github.com/user-attachments/assets/eb15c5f2-65b6-432e-93e0-3b1c232218ae)


◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

### Design Code:
module ALU ( input [3:0] A, B, input [2:0] ALU_Sel, output reg [3:0] ALU_Out, output reg
CarryOut );

```
always @(*) begin
 case (ALU_Sel)
 3'b000: {CarryOut, ALU_Out} = A + B;
 3'b001: {CarryOut, ALU_Out} = A - B;
 3'b010: ALU_Out = A & B;
 3'b011: ALU_Out = A | B;
 3'b100: ALU_Out = A ^ B;
 3'b101: ALU_Out = ~A;
 3'b110: ALU_Out = A << 1;
 3'b111: ALU_Out = A >> 1;
 default: ALU_Out = 4'b0000;
 endcase
end
endmodule
```
### TestBench:
module ALU_tb; reg [3:0] A, B; reg [2:0] ALU_Sel; wire [3:0] ALU_Out; wire CarryOut;
```
ALU uut (
 .A(A),
 .B(B),
 .ALU_Sel(ALU_Sel),
 .ALU_Out(ALU_Out),
 .CarryOut(CarryOut)
);
initial begin
 A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
 A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
 A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
 A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
 $finish;
end
endmodule
```
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,
![Screenshot 2025-05-21 123448](https://github.com/user-attachments/assets/de09000a-3965-4104-91bb-b25146323566)


• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh
◦ source /cadence/install/cshrc
![Screenshot 2025-05-21 123543](https://github.com/user-attachments/assets/fed613db-d5de-42db-8ad3-c55b15857286)


• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-21 123611](https://github.com/user-attachments/assets/1ccadc71-51a3-42b4-b910-e7302c7188f1)



• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![Screenshot 2025-05-21 114526](https://github.com/user-attachments/assets/48524f30-5254-4f2c-b7ab-3485a54e5e52)

#### Area report:
![Screenshot 2025-05-21 123720](https://github.com/user-attachments/assets/3da708e6-3ba3-4574-945d-af902c1e63d2)

#### Power Report:
![Screenshot 2025-05-21 123652](https://github.com/user-attachments/assets/956e8eb8-b5ce-42a0-9706-7b48b5858c2b)

#### Result: 
![Screenshot 2025-05-21 120943](https://github.com/user-attachments/assets/c6ef2a85-4d6f-4250-8a6c-211a2065bf48)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
