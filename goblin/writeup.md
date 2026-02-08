**Goblin Slayers**

Challenge: Goblin Attack

Category: Reverse Engineering

Tools: GDB, Linux terminal

Challenge Overview

The binary validates a 36-character input using a deterministic XOR-based check. The goal is to recover the hidden flag by analyzing and instrumenting the program at runtime.
________________________________________
*Phase 1 — Reconnaissance*

I loaded the binary into GDB:

gdb ./goblin

Disassembling main revealed a length check:

call strlen@plt

cmp $0x24, %rax

jne <error>



0x24 (hex) equals 36, meaning the program only accepts inputs of length 36. To bypass this gate, I supplied a dummy string of 36 characters:
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

After passing the length check, execution continues into the function:
_Z9check_keyPc
________________________________________
*Phase 2 — Understanding the Validation Logic*

Inside check_key, the program initializes a pseudo-random generator:
mov $0x1337, %edi
call srand@plt
Because the seed is constant (0x1337), the sequence produced by rand() is deterministic.
The validation loop works as follows:
1.	Generate a pseudo-random key with rand()
2.	XOR the user input with this key
3.	Compare the result with an encrypted byte stored in the binary
The critical comparison instruction occurs at:
cmp %eax, %edx
This is where each character is verified.
________________________________________
*Phase 3 — Runtime Exploitation*

Instead of statically reversing the algorithm, I used GDB to instrument execution and recover the flag dynamically.
1. Neutralizing the Failure Branch
The program exits immediately on mismatch. I patched the conditional jump after the comparison by overwriting it with NOP instructions:
set {unsigned char}0x... = 0x90
set {unsigned char}0x... = 0x90
This prevents early termination.
2. Automated XOR Reversal
I placed a breakpoint at the comparison instruction and attached a GDB script:
break *0x...
commands
  silent
  set $key = *(int*)($rbp - 0xa4)
  printf "%c", ($eax ^ $key)
  set $edx = $eax
  continue
end
This script:
•	extracts the XOR key from the stack
•	reverses the XOR to reveal the original character
•	forces the comparison to succeed
•	continues execution
________________________________________
*Phase 4 — Flag Recovery*

Running the program with the script active prints the flag character by character:
CodefestCTF{k3ro_kero_G0bl1n_mehehe}
![This is the image)(images/goblin_solve.png)
________________________________________
**Flag**

CodefestCTF{k3ro_kero_G0bl1n_mehehe}
________________________________________
**Lessons Learned**

•	Fixed PRNG seeds make encryption predictable

•	Runtime debugging can bypass client-side validation

•	GDB scripting is powerful for automating reverse tasks

•	XOR-based schemes are reversible when the key is known

