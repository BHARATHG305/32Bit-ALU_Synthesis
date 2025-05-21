# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)
![Screenshot 2025-05-21 103851](https://github.com/user-attachments/assets/4cad051d-8ac5-4a88-a5f5-70407c9102ca)

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
![Screenshot 2025-05-21 123448](https://github.com/user-attachments/assets/db768b0b-7b4f-4bcd-9e60-40785269ee08)

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc
![Screenshot 2025-05-21 123543](https://github.com/user-attachments/assets/956d5c77-6238-477f-9a61-af894bf47155)

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-21 123611](https://github.com/user-attachments/assets/495b1b4e-0482-429b-8d7b-cf56f0706ff1)

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![Screenshot 2025-05-21 114526](https://github.com/user-attachments/assets/d2d50ba5-2eaf-413f-8ef9-b7f3886885dd)

#### Area report:
![Screenshot 2025-05-21 123720](https://github.com/user-attachments/assets/61540328-1a1c-434b-bafa-252f5d26c801)

#### Power Report:
![Screenshot 2025-05-21 123652](https://github.com/user-attachments/assets/0922673c-dfe9-40ea-bb01-3a66dc2df39d)

#### Result: 
![Screenshot 2025-05-21 120943](https://github.com/user-attachments/assets/2a83b772-fc2c-435c-9dce-db9704a44fe7)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
