Computer Design Principles

Remarkably, most of the operations performed by digital computers can be reduced to elementary additions of binary numbers.


When we press the keyboard key '1', '9' and ENTER while running, say, a spreadsheet program, what ends up in some register in the computer's memory is the binary code 10011. bin(10011) -> 19

If the computer happens to be 32 bit than what gets stored in the register is the bit pattern 00000000.00000000.00000000.00010011

Adding negative/signed numbers
2's complement

positive -> negative, flip, + 1
negative -> postive, -1, flip

notice the symmetry
- flip +1 -1 flip, pos->neg->pos
- -1 flip flip +1, neg->pos->neg
- + F 1 -1 F
- - -1 F F 1

How do you syncrhonize the overall computer architecture?

Suppose

- ALU does x + y
- x comes from a nearby register
- y comes from remote RAM register
- because of various physical constraints x and y will likely arrive at the ALU at different times
- the ALU is a combinational chip, it has no concept of time and therefore no concept of ordering so will continuously add data that happens to be lodged in its input
- it will take some time before the ALU output stabilizes to x+y
- before that the ALU will generate garbage
- since the output of an ALU is always routed to a sequential chip(can keep track of time, therefore can hold state)

What is the most important part?
When we build the computer's clock, the length of the clock cycle has to be slightly longer than the length of time it takes a bit to travel the longest distance from one chip in the architecture to another

clock cycle time > max travel time of a bit in the system