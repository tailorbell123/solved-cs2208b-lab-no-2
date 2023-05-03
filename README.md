Download Link: https://assignmentchef.com/product/solved-cs2208b-lab-no-2
<br>
<strong>ARM pseudo-instructions </strong>

The ARM assembler supports a number of pseudo-instructions that are translated into the appropriate combination of ARM instructions at assembly time. ARM pseudo-instructions include:




<h2>LDR ARM pseudo-instruction</h2>

The LDR pseudo-instruction loads a register with either:

<ul>

 <li>a 32-bit constant value</li>

 <li>an address</li>

</ul>

<h3>Syntax</h3>

The syntax of LDR is:

LDR{<strong>condition</strong>} <strong>register</strong>,=[<strong>expression</strong> |<strong> label-expression</strong>] where: <strong>condition</strong> is an optional condition code, <strong>register</strong> is the register to be loaded, <strong>expression</strong>evaluates to a numeric constant:

<ul>

 <li>If the value of <strong>expression</strong> is within range of a MOV or MVN instruction, the assembler generates the appropriate instruction.</li>

 <li>If the value of <strong>expression</strong> is <strong>not</strong> within range of a MOV or MVN instruction, the assembler places the constant in a <strong><em>literal pool</em></strong> and generates a program-relative LDR instruction that reads the constant from the literal pool.</li>

</ul>

The offset from the PC to the constant must be less than 4KB. You are responsible for ensuring that there is a literal pool within range.

<strong>label-expression</strong> is a program-relative expression.

The assembler places the value of <strong>label-expression</strong> in a literal pool and generates a program-relative LDR instruction that loads the value from the literal pool.

The offset from the PC to the value in the literal pool must be less than 4KB. You are responsible for ensuring that there is a literal pool within range.

<h3>Usage</h3>

The LDR pseudo-instruction is used for two main purposes:

<ul>

 <li>to generate literal constants when an <strong>immediate</strong> value cannot be moved into a register because it is out of range of the MOV and MVN</li>

 <li>to load a program-relative address into a register.</li>

</ul>

<h3>Example</h3>

LDR r1,=0xfff        ; loads 0xfff into r1

LDR r2,=place        ; loads the address of place into r2




<h2>ADR ARM pseudo-instruction</h2>

The ADR pseudo-instruction loads a program-relative or register-relative address into a register.

<h3>Syntax</h3>

The syntax of ADR is:

ADR{<strong>condition</strong>} <strong>register</strong>,<strong>expression</strong> where: <strong>condition</strong> is an optional condition code, <strong>register</strong> is the register to load, <strong>expression</strong>is a program-relative or register-relative expression that evaluates to an address. The address can be either before or after the address of the instruction or the base register.

<h3>Usage</h3>

ADR always assembles to one instruction. The assembler attempts to produce a single ADD or SUB instruction to load the address.

<strong><em>Example </em></strong>start MOV r0,#10

ADR r4,start         ; =&gt; SUB r4,pc,#0xc




<strong>PROBLEM SET </strong>

<ol>

 <li>The ARM uses a pipeline to increase the speed of the flow of instructions to the processor. This allows several operations to take place simultaneously. Instructions are executed in three pipeline stages: fetch, decode, and execute. During normal operation, while one instruction is being executed, its successor is being decoded, and a third instruction is being fetched from memory. Hence, when an ARM processor starts executing an instruction, the PC will not be pointing to that instruction any more.</li>

</ol>

Consider the following instruction:

MOV r0, pc

Use the Keil simulator to write, assemble, and run the above program fragment.

Note that you will need to use appropriate assembly directives to make this program fragment a program. What did you find the value of r0 after executing the instruction?  Justify your finding..




<ol start="2">

 <li>Consider the following instructions:</li>

</ol>

LDR r1, [r0]

LDR r2, = 0x12345678      LDR r3, = 0x12

Use the Keil simulator to write, assemble, and run the above program fragment.

Note that you will need to use appropriate assembly directives to make this program fragment a program.




Study and relate the generated disassembled code to the code written above. Specifically, you need to understand the role of the PC register and the location of the literal pool, as well as the pipeline effect, in this situation.




Why does each LDR instruction encode differently?




<ol start="3">

 <li>Consider the following instructions:</li>

</ol>

LDR r3, X

LDR r4, =X      ADR r5, X loop B   loop X    DCD 0x70707070




Use the Keil simulator to write, assemble, and run the above program fragment.

Note that you will need to use appropriate assembly directives to make this program fragment a program.




Study and relate the generated disassembled code to the code written above. Specifically, you need to understand the role of the PC register and the location of the literal pool, as well as the pipeline effect, in this situation.




<ol start="4">

 <li>Consider the following assembly programs:</li>

</ol>

AREA prog1, CODE, READONLY

ENTRY

LDR r0, = 0x12345678  loop b loop

AREA prog1, READONLY

X    DCD 0x70707070

END




AREA prog2, CODE, READONLY

ENTRY

LDR r0, = 0x12345678  loop b loop X    DCD 0x70707070      END




Use the Keil simulator to run the above two programs.

Study and compare the generated disassembled code for the LDR instruction in each program.

Justify the difference between the two generated codes. Think of the location of the literal pool.