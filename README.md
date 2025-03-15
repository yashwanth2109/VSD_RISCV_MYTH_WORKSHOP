RISC-V BASED MYTH WORKSHOP:

A RISC-V ISA is defined as a base integer ISA, which must be present in any implementation, plus optional extensions to the base ISA. Each base integer instruction set is characterized by
Width of the integer registers (XLEN)
Corresponding size of the address space
Number of integer registers (32 in RISC-V)

GNU COMPILER TOOLCHAIN:

The GNU Toolchain is a set of programming tools in Linux systems that programmers can use to make and compile their code to produce a program or library. So, how the machine code which is understandable by processer is explained below.
Preprocessor - Process source code before compilation. Macro definition, file inclusion or any other directive if present then are preprocessed.
Compiler - Takes the input provided by preprocessor and converts to assembly code.
Assembler - Takes the input provided by compiler and converts to relocatable machine code.
Linker - Takes the input provided by Assembler and converts to Absolute machine code.
Under the risc-v toolchain,

Below is the sample code on how to write an C code and view the output in spike simulator:

![image](https://github.com/user-attachments/assets/f7fd80e8-3b31-44e3-8bd2-4707773d7d65)

To use the risc-v gcc compiler use the below command:

riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <object filename> <C filename>


![image](https://github.com/user-attachments/assets/81a02460-fefc-4a6b-9ea7-e8a3a4d276b1)


More generic command with different options:

riscv64-unknown-elf-gcc <compiler option -O1 ; Ofast> <ABI specifier -lp64; -lp32; -ilp32> <architecture specifier -RV64 ; RV32> -o <object filename> <C filename>

![image](https://github.com/user-attachments/assets/7391c32d-2bd1-41e1-8d10-dcd37fc44370)


To view assembly code use the below command,

riscv64-unknown-elf-objdump -d <object filename>

To use SPIKE simualtor to run risc-v obj file use the below command,

spike pk <object filename>

To use SPIKE as debugger

spike -d pk <object Filename>


![image](https://github.com/user-attachments/assets/f5194197-e84b-4ffc-9dbe-91b32aaa4232)




APPLICATION BINARY INTERFACE:

An Application Binary Interface is a set of rules enforced by the Operating System on a specific architecture. So, Linker converts relocatable machine code to absolute machine code via ABI interface specific to the architecture of machine.
So, it is system call interface used by the application program to access the registers specific to architecture. Overhere the architecture is RISC-V, so to access 32 registers of RISC-V below is the table which shows the calling convention (ABI name) given to registers for the application programmer to use.


![image](https://github.com/user-attachments/assets/b3b79937-3b33-4b75-bafb-26eb1b39019c)

The below image shows the main function:

![image](https://github.com/user-attachments/assets/ff97ac3d-48ee-41cb-8c3c-59a454dbce5b)

Create a new file custom.c and Load.s and view in using  cat <program name>

![image](https://github.com/user-attachments/assets/fbd1bd84-2cc9-4120-b496-a6266fa5a790)


Clone the following Github repository and observe its files:

git clone https://github.com/kunalg123/riscv_workshop_collaterals

![image](https://github.com/user-attachments/assets/cb19eaf8-8802-4dbc-9eb6-0056e8b53f48)

![image](https://github.com/user-attachments/assets/9e7dc08e-6a53-43da-b072-66d402a85afd)



![image](https://github.com/user-attachments/assets/311e29ec-7019-4838-82e4-d5ef48e09509)



![image](https://github.com/user-attachments/assets/14a7ff78-5074-419e-bc81-bbc331d1f2cb)


DIGITAL LOGIC WITH TRANSACTION LEVEL -VERILOG and MAKERCHIP:

Makerchip is a free online environment for developing high-quality integrated circuits. You can code, compile, simulate, and debug Verilog designs, all from your browser. Your code, block diagrams, and waveforms are tightly integrated.
All the examples shown below are done on Makerchip IDE using TL-verilog. Also there are other tutorials present on IDE which can be found here under Tutorials section.


![image](https://github.com/user-attachments/assets/175d11a3-f31e-48f5-a102-47e2ee981437)


SOME OF THE BASIC EXAMPLES DONE IN MAKERCHIP:

COUNTER:


![image](https://github.com/user-attachments/assets/912d40fa-eb3f-4958-8fb0-f64af135c286)


INVERTER:


![image](https://github.com/user-attachments/assets/d042fbcd-3f60-4fe8-aec0-5e8d44f5f7b9)


2x1 MULTIPLEXER:

![image](https://github.com/user-attachments/assets/559a6add-6960-4fe6-bc80-73e1044ef8fc)


SQUARE ROOT:


![image](https://github.com/user-attachments/assets/be6dd04c-1515-40ce-a526-cb1e0c6d085d)


COMBINATIONAL LOGIC:

Starting with basic example in combinational logic is an inverter. To write the logic of inverter using TL-verilog is $out = ! $in;. There is no need to declare $out and $in unlike Verilog. There is also no need to assign $in. Random stimulus is provided, and a warning is produced.
Below is snapshot of Combinational Calculator:


![image](https://github.com/user-attachments/assets/8a0f59c6-d8bc-4872-8aa7-64398be3e4b9)


SEQUENTIAL LOGIC:

Starting with basic example in sequential logic is Fibonacci Series with reset. To write the logic of Series using TL-Verilog is $num[31:0] = $reset ? 1 : (>>1$num + >>2$num). This operator >>? is ahead of operator which will provide the value of that signal 1 cycle before and 2 cycle before respectively.
Below is snapshot of Sequential Calculator which remembers the last result, and uses it for the next calculation.

![image](https://github.com/user-attachments/assets/b28519d8-e346-4eca-a8db-0c7169491dea)


PIPELINED LOGIC:

Timing abstract powerful feature of TL-Verilog which converts a code into pipeline stages easily. Whole code under |pipe scope with stages defined as @?
Below is snapshot of 2-cycle calculator which clears the output alternatively and output of given inputs are observed at the next cycle.


![image](https://github.com/user-attachments/assets/dc3b59ba-8e72-4369-8ea7-9f2f398badf7)


ERROR COMPUTATION WITHIN PIPELINE:

The ERROR_SIGNALS are OR together to check the various error conditions that can occur within a computational pipeline. The idea of this exercise is to develop a visual understanding of how the TL-Verilog code is translated into the diagram / architecture in the visualization pane.

TWO CYCLE CALCULATOR(PIPELINE):

The calculation happens in the first cycle, and in the second cycle, the outputs are assigned based on the VALID SIGNAL, which is determined by $reset | !cnt

![image](https://github.com/user-attachments/assets/dc5c7aa7-3fa1-4f63-8c38-d13e39ead134)

VALIDITY:

Validity is TL-verilog means signal indicates validity of transaction and described as "when" scope else it will work as don't care. Denoted as ?$valid. Validity provides easier debug, cleaner design, better error checking, automated clock gating.
Below is snapshot of 2-cycle calculator with validity.



TWO CYCLE CALCULATOR WITH VALIDITY:


![image](https://github.com/user-attachments/assets/2728209b-de31-4250-97d4-3b567e34feba)


CALCULATOR WITH SINGLE VALUE MEMORY:

![image](https://github.com/user-attachments/assets/f3cb1201-bc0b-4ec6-a55c-f5b648a43fa7)


Program for above Section:

Combinational Calculator:

\TLV

    $out[7:0] = $sel ? $in1[7:0] : $in2[7:0]

Sequential Calculator:

\TLV

   // Fibonacci Series Example

    $num[31:0] = $reset ? 1 : (>>1$num + >>2$num);

\TLV
   
   // 8-Bit Free Running Counter
   
    |calc
      @0
         $reset = *reset;
 
         $cnt[7:0] = $reset ? 0 : (>>1$cnt + 1);
         
   // Limiting Simulation
   
   *passed = *cyc_cnt > 20;
   *failed = 1'b0;

Pipelined Logic:

\TLV

    |calc
      @1 // Stage
         $aa_sq[31:0] = $aa * $aa; 
         $bb_sq[31:0] = $bb * $bb;
      @2
         $cc_sq[31:0] = $aa_sq + $bb_sq;
      @3
         $cc[31:0] = sqrt($cc_sq);

\TLV

   // Design Under Test

    |calc
      @2 // Stage
         $aa_sq[31:0] = $aa * $aa; 
         $bb_sq[31:0] = $bb * $bb;
      @4
         $cc_sq[31:0] = $aa_sq + $bb_sq;
      @6
         $cc[31:0] = sqrt($cc_sq);
\TLV

   // Error in Pipeline
   
    |error
      @1
         $err1 = $bad_input || $illegal_op;
      @3
         $err2 = $over_flow || $err1;
      @6
         $err3 = $div_by_zero || $err2;

   // Limiting Testing Cycles
   
    *passed = *cyc_cnt > 10;
    *failed = 1'b0;


Validity:

\TLV

    |calc
     @1
         $reset = *reset;
      
      ?$valid
         @1 // Stage
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0]; 
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0]    = sqrt($cc_sq);
            
      @4
         $tot_dist[63:0] = $reset ? '0 :
                           $valid ? >>1$tot_dist + $cc : // Accumulate
                                    >>1$tot_dist;        // Retain







BASIC RISC-V CPU MICRO-ARCHITECTURE:

Designing the basic processor of 3 stages fetch, decode and execute based on RISC-V ISA.
FETCH
Program Counter (PC): Holds the address of next Instruction
Instruction Memory (IM): Holds the set of instructions to be executed
During Fetch Stage, processor fetches the instruction from the IM pointed by address given by PC.
Below is snapshot from Makerchip IDE after performing the Fetch Stage.


![image](https://github.com/user-attachments/assets/4a4f9bdd-8d39-4fc9-a6c3-32425f38c792)

DECODE:

6 types of Instructions:
R-type - Register
I-type - Immediate
S-type - Store
B-type - Branch (Conditional Jump)
U-type - Upper Immediate
J-type - Jump (Unconditional Jump)
Instruction Format includes Opcode, immediate value, source address, destination address. During the Decode Stage, the processor decodes the instruction based on the instruction format and type of instruction.


![image](https://github.com/user-attachments/assets/17cd2b87-c0f9-4f51-a9c7-444677713cdf)


SINGLE CYCLE FETCH AND DECODE IMPLEMENTATION:

![image](https://github.com/user-attachments/assets/08483542-84f2-4780-808c-6affe68dffc4)


REGISTER FILE READ AND WRITE:

Here the Register file is 2 read, 1 write means 2 read and 1 write operation can happen simultanously.
Inputs:
Read_Enable - Enable signal to perform read operation
Read_Address1 - Address1 from where data has to be read
Read_Address2 - Address2 from where data has to be read
Write_Enable - Enable signal to perform write operation
Write_Address - Address where data has to be written
Write_Data - Data to be written at Write_Address
Outputs:
Read_Data1 - Data from Read_Address1
Read_Data2 - Data from Read_Address2
Below is snapshot from Makerchip IDE after performing the Register File Read followed by Register File Write.

![image](https://github.com/user-attachments/assets/5609698e-00b5-4d63-87a2-f48eca1806de)


Single-Cycle RISC-V32I Implementation

![image](https://github.com/user-attachments/assets/2425625b-39f5-4a67-b7c3-f917c35cbd29)






EXECUTE:

During the Execute Stage, both the operands perform the operation based on Opcode.
Below is snapshot from Makerchip IDE after performing the Execute Stage.


![image](https://github.com/user-attachments/assets/7f857038-fb0f-42e7-a3ad-7552bb8ba485)


CONTROL LOGIC:

During Decode Stage, branch target address is calculated and fed into PC mux. Before Execute Stage, once the operands are ready branch condition is checked.
Below is snapshot from Makerchip IDE after including the control logic for branch instructions.


Program for the above section:


\TLV

    |cpu
      @0
         $reset = *reset;
         $pc[31:0] = (>>1$reset) ? '0 : >>1$pc + 32'h4;

// Below the Program Counter Statement

         $imem_rd_en         = !>>1$reset ? 1 : 0;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];

      @1
         $instr[31:0] = $imem_rd_data[31:0];

// Below Instruction Fetch Assignment

         $is_i_instr = $instr[6:2] ==? 5'b0000x || $instr[6:2] ==? 5'b001x0 || $instr[6:2] ==? 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 || $instr[6:2] ==? 5'b011x0 || $instr[6:2] ==? 5'b10100;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_j_instr = $instr[6:2] == 5'b11011;

// Below Instruction Type Decode

         $imm[31:0] = $is_i_instr   ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr   ? {{21{$instr[31]}}, $instr[30:25], $instr[11:8], $instr[7]} :
                      $is_b_instr   ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr   ? {$instr[31], $instr[30:20], $instr[19:12], 12'b0} :
                      $is_j_instr   ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                      32'b0;    
    
// Below Immediate Instruction Decode, Note Immediate Instructions are Taken Care

         $rs1_valid    = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid    = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid     = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;

         $opcode[6:0]    = $instr[6:0];

         ?$rs1_valid
            $rs1[4:0]    = $instr[19:15];

         ?$rs2_valid
            $rs2[4:0]    = $instr[24:20];

         ?$rd_valid
            $rd[4:0]     = $instr[11:7];

         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];

         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];

// Below Extract Instruction Fields Code

         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};

         $is_beq  = $dec_bits ==? 11'bx_000_1100011;
         $is_bne  = $dec_bits ==? 11'bx_001_1100011;
         $is_blt  = $dec_bits ==? 11'bx_100_1100011;
         $is_bge  = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add  = $dec_bits ==? 11'b0_000_0110011;

// Below Basic Instruction Set Decode, Read

         ?$rs1_valid
            $rf_rd_en1         = $rs1_valid;
            $rf_rd_index1[4:0] = $rs1[4:0];
            
         ?$rs2_valid
            $rf_rd_en2         = $rs2_valid;
            $rf_rd_index2[4:0] = $rs2[4:0];
            
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;

         // Below Arithemtic and Logic Unit, Register Write

         $rf_wr_en = ($rd == 5'h0) ? 1'b0 : $rd_valid;
         
         ?$rf_wr_en
            $rf_wr_index[4:0] = $rd[4:0];
            
         $rf_wr_data[31:0]  = $result[31:0];     
  
         // Arithmetic and Logic Unit, Below Register File

         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add  ? $src2_value + $src1_value : 32'bx;
         
         // Updated Program Counter

         $pc[31:0] = (>>1$reset) ? '0 : >>1$taken_br ? >>1$br_tgt_pc : >>1$pc + 32'h4;

         // Branch Instructions Check
         
         $taken_br = $is_beq  ? ($src1_value == $src2_value) :
                     $is_bne  ? ($src1_value != $src2_value) :
                     $is_blt  ? ($src1_value <  $src2_value) ^ ($src1_value[31] != $src2_value[31]) :
                     $is_bge  ? ($src1_value >  $src2_value) ^ ($src1_value[31] != $src2_value[31]) :
                     $is_bltu ? ($src1_value <= $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) :
                     1'b0;
                     
         // Branch Instruction Address Update
         
         $br_tgt_pc[31:0] = $pc + $imm;




PIPELINING THE RISC-V CPU MICRO-ARCHITECTURE:

Converting non-piepleined CPU to pipelined CPU using timing abstract feature of TL-Verilog.

PIPELINING THE CPU:

![image](https://github.com/user-attachments/assets/75a6868b-7d6c-4161-9db2-79e718cfc168)


Pipelining the CPU with branches still having 3 cycle delay rest all instructions are pipelined. Pipelining the CPU in TL-Verilog can be done in following manner:

|<pipe-name>

    @<pipe_stage>
       Instruccions present in this stage
       
    @<pipe_stage>
       Instruccions present in this stage


![image](https://github.com/user-attachments/assets/76072efe-7aa8-4a1b-8ce1-a752d2244827)



Below is snapshot of pipelined CPU with a test case of assembly program which does summation from 1 to 9 then stores to r10 of register file. In snapshot r10 = 45. Test case:
*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);



LOAD AND STORE INSTRUCTIONS AND MEMORY

Similar to branch, load will also have 3 cycle delay. So, added a Data Memory 1 write/read memory.
Inputs:
Read_Enable - Enable signal to perform read operation
Write_Enable - Enable signal to perform write operation
Address - Address specified whether to read/write from
Write_Data - Data to be written on Address (Store Instruction)
Output:
Read_Data - Data to be read from Address (Load Instruction)
Added test case to check fucntionality of load/store. Stored the summation of 1 to 9 on address 4 of Data Memory and loaded that value from Data Memory to r17.
*passed = |cpu/xreg[17]>>5$value == (1+2+3+4+5+6+7+8+9);

Below is snapshot from Makerchip IDE after including load/store instructions.


![image](https://github.com/user-attachments/assets/c933bb23-3e2d-462e-a633-a445b0ecc3c9)


COMPLETING THE RISC-V CPU

Added Jumps and completed Instruction Decode and ALU for all instruction present in RV32I base integer instruction set.
Below is final Snapshot of Complete Pipelined RISC-V CPU.

![image](https://github.com/user-attachments/assets/9b4d6762-088b-4fb0-89fd-973d11aa687a)

Acknowledgements:

Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.

Steve Hoover, Founder, Redwood EDA

Shivam Potdar, GSoC 2020 @fossi-foundation

Vineet Jain, GSoC 2020 @fossi-foundation

































