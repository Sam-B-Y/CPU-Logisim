# CPU in Logisim
Fully functional CPU with 8 registers and 16-bit instructions, made using Logisim. 

![CPU](https://github.com/Sam-B-Y/CPU/blob/main/images/cpu.png?raw=true)

## Running the CPU
The CPU's memory follows the Harvard architecture, meaning that the instruction memory and data memory are separate.

To simulate the test program, convert MIPS assembly code to an instruction memory file (.imem.lgsim) and a data memory file (.dmem.lgsim). Then, open the CPU.circ file in Logisim and load the .imem.lgsim and .dmem.lgsim files into the instruction memory and data memory, respectively.

## Instruction Set
| Instruction | Opcode | Format | Usage              | Description                                      |
|-------------|--------|--------|--------------------|--------------------------------------------------|
| add         | 0000   | R      | add $rd, $rs, $rt  | $rd = $rs + $rt                                  |
| sub         | 0001   | R      | sub $rd, $rs, $rt  | $rd = $rs - $rt                                  |
| addi        | 0010   | I      | addi $rt, $rs, Imm | $rt = $rs + Imm                                  |
| not         | 0011   | R      | not $rd, $rs       | $rd = NOT ($rs)                                  |
| xor         | 0100   | R      | xor $rd, $rs, $rt  | $rd = $rs XOR $rt                                |
| sll         | 0101   | R      | sll $rd, $rs, <shamt> | $rd = $rs << shamt (shamt is unsigned)       |
| srl         | 0110   | R      | srl $rd, $rs, <shamt> | $rd = $rs >> shamt (logical shift: no special treatment of sign bit; shamt is unsigned) |
| lw          | 0111   | I      | lw $rt, D($rs)     | $rt = Mem[$rs+D]                                 |
| sw          | 1000   | I      | sw $rt, D($rs)     | Mem[$rs+D] = $rt                                 |
| beqz        | 1001   | I      | beqz $rs, B        | if ($rs==0) then PC=PC+1+B; else PC=PC+1         |
| blt         | 1010   | I      | blt $rs, $rt, B    | if ($rs<$rt) then PC=PC+1+B; else PC=PC+1        |
| j           | 1011   | J      | j L                | PC = L                                           |
| jr          | 1100   | R      | jr $rs             | PC = $rs                                         |
| jal         | 1101   | J      | jal L              | $r7=PC+1; PC = L                                 |
| input       | 1110   | R      | input $rd          | $rd = keyboard input                             |
| output      | 1111   | R      | output $rs         | print $rs on a TTY display                       |

## Convention
- Registers: $r0, $r1, $r2, $r3, $r4, $r5, $r6, $r7
- $r0 is hardwired to 0
- $r7 is the link register for jal
- $r6 should be used as the stack pointer

## Limitations
- The CPU doesn't have a OS kernel. It can only run a single program, and users will have direct access to I/O devices.
- Syscalls are not implemented. The input and output instructions are used to interact with the keyboard and TTY display, respectively.
- Protection mechanisms are not implemented. Users can access any memory location and any register.
- Exception handling is not implemented. The CPU will not handle any exceptions, such as divide by zero or invalid memory access.
- Finally, and most importantly, the CPU is slow and inefficient. It isn't pipelined, and it doesn't have a cache. (To be implemented in the future.)