A Binary operator is an operator that operates on two operands to produce a new value (result).

`Operand_1 Operator Operand_2` i.e. `1 + 2`

They are a type of Infix operators since they are in a middle of an operation. While parsing an Infix operation, we don't know that we are in the middle of a binary operator until after we've parsed its left operand and then stumble onto the operator token in the middle.

A prefix expression is an expression where the operator comes before it's first operand

`Operator Operand_1...` i.e. `(a`