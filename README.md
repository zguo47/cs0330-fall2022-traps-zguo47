# Traps
## Level 4 explanation:
I set a breakpoint at level_four, and then use ni and layout regs to observe the
value changes in registers. I noticed that 0 are stored in 0x2b(%rsp) and 
0x2f(%rsp), and our input string, is first stored in %rdi and then copied to 
%rbx and %rsi. From level_three, we know that the four numbers of our input
string will be stored inside %rsp, 0x8(%rsp), 0x10(%rsp) and 0x18(%rsp) 
respectively. Then, %rdx is given a value, using x/s, we know that it contains
string "bdta", at the address 0x55555555990c. %rdi is then set to 3, and %rax to
0 . Jump to 1a84, and we move the first input number to %rcx, then compare it 
with 3. In my case, it is bigger than 3 so we jump to 1a76, and we add 1 to 
%rax, and subtract 4 from %rdx, so now it stores "arutbdta". Compare %rax with
4, it is smaller than 4, so we proceed to move the next number. All four of my
input numbers are bigger than 3, so following the program, I get the full string
stored in %rdx, which should be "psaigaotarutbdta", at 0x555555559900. Now
%rax is equal to 4, so jump to 1a9e, and we then get a new value stored inside
%rsi, which is a string "bugs". The lines after will call strings_not_equal, so
it is not hard to imply that we want to get our %rdi to contain "bugs" as well.
By looking at the string stored in %rdx, we find that "b", "u", "g", "s" are all
contained in the string. Thus, the program wants us to extract the four 
letters from the string. We also know that we compare our input number with 3
everytime, and we get 4 new letters in the string with every loop, so our
input numbers are related to the index of string referring to the char we want
to extract. The final index is 3 minus our input number, so our input should be
3 minus the index we want, which should be 3 1 3 2, the final password. 