The main idea of a Pratt parser is the association of parsing functions with token types.
For each token type, the parser has two parsing functions associated to it : one for if the token is found at a prefix position and one if the token is found at a infix position. 

Whenever a given token type is encountered, the parsing functions are called to parse the appropriate expression and return an AST Node that represents it. Each token type can have two parsing functions depending on whether the token is found as a prefix or infix position of a statement.

### Precedence
Each token type is associated with a precedence. A precedence is a way to give a rank of importance to the token type and to determine whether the next token is an infix. 

```
12345
-> currToken : 1
-> peekToken : 2
// Both tokens are IntToken so they have the same precendence

1 + 1 + 2
-> currToken : 1
-> peekToken : +

// + has a higher precendence, so it's an InfixExpression
infixExp = {
	LeftExpr: 1
	Operator: +
}

call next_token

1 + 1 + 2
-> currToken : +
-> peekToken : 1

```

### Right binding power
The higher right binding power a token type has, the more token will be bind to it on it's right side.

```
function(x, y)  // function call token type has a higher right binding power 
				// then CharacterToken

					FunctionToken
					/            \
				function        x , y

1 * 2 + 3   // * has a higher right binding power then +, so + is binded to its              // right

					InfixToken
					/        \
				  1 * 2      + 3

1 + 2 - 3   // + has the same right binding power to -, so - is binded to its                // right
	
					InfixToken
					/        \
				  1 + 2      - 3
```