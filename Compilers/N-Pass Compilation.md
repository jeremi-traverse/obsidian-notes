A compiler has two jobs : 
1. It parses the user's code to understand what it means. 
2. Takes that knowledge and outputs low-level instructions that produce the same semantics.

#### Two-Pass Compilation
Many languages split those two roles into two separate passes in the implementation. A parser produces an AST and then a code generator traverses the AST and outputs target code.

#### Single-Pass Compilation
Only one pass to peep into the user's code and generating the matching code in another language