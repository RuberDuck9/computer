# 16 Bit Custom Computer

ALL INFORMAION IN HERE IS MOST LIKELY CORRECT, BUT PLEASE LET ME KNOW IF THERE ARE INCONSISTENCIES THAT I MISSED   

16 Bit - [0000][000000][000000] - [Instruction][Copy from address][Copy to address]

Main components:
 - Registry and registry editor
 - System clock   
 - Instruction interpreter
 - Read only memory 
 - Memory Controller
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
Output - [111111] - symbolic in name only, functions as the first 7 registers do 

Instructions:  
Evaluated by the instruction interpreter based off last 4 bits
16 possible due to 4 bit representative value

imm - [0000][000000000000]
immediate the value stored in the first twelve digits to reg0 using registry editor

cpy - [0001][000000][000000]
copy from the address specified in the digits 7-12 to the address specified in the digits 1-6 using registry

clc - [0010][000000000000]
do the math operation specified in the first 12 digits (0 add, 1 sub, 2 mult, 3 div, 4 and)

gto - [1010][000000000000]
go to the address in rom specified in the first twelve digits

rst - [1100]
go to address zero in rom

hlt - [1111]
halt the computer

ROM:  

[000000000000][0000000000000000] - [Address][Stored Value] - [Input][Output] 

12 bits used for rom address (could be higher but would be unnecessary)
data stored as hex values for space
read value at current address and pass it through to cpu   

Memory Controller:

advance one memory address each "tick" or unit of time starting at zero   
override back to value specified in instructions "gto" and "rst"   

ALU:  
performs a math operation based on the value passed to it by the instruction interpreter   
can perform addition, subtraction, multiplication, division
save output in alu2
