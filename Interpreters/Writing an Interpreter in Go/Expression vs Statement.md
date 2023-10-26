### Expression

An expression is a bit a code that produces a value : 

```
1 -> produces 1
2 + 2 -> produces 4
[1, 2, 3].pop(2) -> produces 3
```

### Statement

In most languages, a program is sequence of statements. I like to think that a statement is an instruction for the computer to do something. Often times, a statement has one or many slots for expression :

```
let x = \* slot for expression \* -> a variable declaration is a statement
throw new Error( \* slot for expression *\ )
```

Expressions can be statements : 

```
1 + 2 + 3
```