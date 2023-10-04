Set of guidelines that deal with resource management and custom implementations of the special member functions. 
1. Destructor
2. Copy Constructor
3. Copy Assignment Operator
4. Move Constructor
5. Move Assignment Operator

The Rule of Five states that if you explicitly declare or define any of the following special member functions, then you should explicitly declare or define all of the remaining four special member functions. This is the case, because the compiler will not automatically generate the others.