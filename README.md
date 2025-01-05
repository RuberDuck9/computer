# 16 Bit Custom Computer

16 Bit - [0000][000000][000000] - [Instruction][Copy from address][Copy to address]

Main components:
 - Registry and registry editor
 - System syncronization clock
 - Instruction interpreter
 - Read only memory 
 - ALU

Registry editor:  
Has the ability to copy data from any registry to any other registry   
Has direct 12 bit write access to reg0  

Register Addresses:  
6 bits allocated to each address

Register 00 - [000001] - direct 12 bit write access with registry editor imm instruction  
Register 01 - [000010]  
Register 02 - [000100]  
Register 03 - [001000] 
Register 04 - [010000]  
Register 05 - [100000]  
Register 06 - [000011]  
Register alu0 - [000110] - alu has direct read access  
Register alu1 - [001100] - alu has direct read access 
Register alu2 - [011000] - alu has direct write access  

Output - [111111] - only write access  

Instructions:  
Evaluated by the instruction interpreter based off last 4 bits
16 possible due to 4 bit representative value

imm - [0000][000000000000]
immediate the value stored in the first twelve digits to reg0 using registry editor

cpy - [0001][000000][000000]
copy from the address specified in the digits 7-12 to the address specified in the digits 1-6 using registry

add - [0010]
add the values stored in reg1 and reg2 and output to reg3
reg1 + reg2 = reg3

sub - [0100]
subtract the value stored in reg2 from the value stored in reg1 and output the result to reg3
reg1 - reg2 = reg3

mlt - [1000]
multiply the values stored in reg1 and reg2 and output the result to reg3
reg1 * reg2 = reg3

div - [1001]
divide the value stored in reg1 by the value stored in reg2 and output the result to reg3
reg1 / reg2 = reg3

gto - [1010][000000000000]
go to the address in rom specified in the first twelve digits

rst - [1100]
go to address zero in rom

hlt - [1111]
halt the computer

ROM:  

[0000000000000000][0000000000000000] - [Address][Stored Value] - [Input][Output] 

16 bits available for rom address  
advance one memory address each "tick" or unit of time starting at zero   
override back to value specified in instructions "gto" and "rst"   
read value at current address and pass it through to cpu   

128 kilobytes capacity - 65536 addresses * 2 bytes per addres =  131072 bytes   

ALU:  
performs a math operation based on the value passed to it by the instruction interpreter   
can perform addition, subtraction, multiplication, division
