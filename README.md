# CapPyro

A small interpreter I built in Python to explore how a language works. It supports variables, functions, loops and lists, with uppercase keywords.

```sh
git clone https://github.com/eldarmuk/CapPyro.git
cd CapPyro
python shell.py
```

```text
cap > 2 + 3 * 4
14
cap > VAR x = 7
7
cap > x + 1
8
```

These arithmetic and variable examples were checked on 28 September 2026. This is a learning project, not a Python-compatible interpreter.

<details>
<summary>Language grammar</summary>

## Expression Structure
**Note**: `expr*` indicates zero or more occurrences of the `expr`, and `expr+` indicates that at least one occurrence of the `expr` is required.

**statements**: `NEWLINE* expr (NEWLINE+ expr)* NEWLINE*`

- **expr** -- Represents an expression.
  - `VAR ID EQ expr` - Assignment of a variable.
  - `comp-expr ((AND | OR) comp-expr)*` - Logical expressions combining comparison expressions.

- **comp-expr** -- Represents a comparison expression.
  - `NOT comp-expr` - A negated comparison expression.
  - `arith-expr ((ISEQ | LT | GT | LEQ | GEQ) arith-expr)*` - Comparison of arithmetic expressions using comparison operators (ISEQ, LT, GT, LEQ, GEQ).

- **arith-expr** -- Represents an arithmetic expression.
  - `term ((PLUS | MINUS) term)*` - Addition or subtraction of terms.

- **term** -- Represents a term in an expression.
  - `factor ((MULT | DIV | DOT) factor)*` - Multiplication, division, or dot operation of factors.

- **factor** -- Represents a factor in an arithmetic expression.
  - `(PLUS | MINUS)* factor` - Unary plus or minus.
  - `power` - A power operation.

- **power** -- Represents a power operation.
  - `call (POW factor)*` - Exponentiation of an atom by a factor.

- **call** -- Represents a function call allowing for passing arguments.
  - `atom (LPAR (expr (COMMA expr)*)* RPAR)*` - A call to a function passing zero or more arguments enclosed in parentheses.

- **atom** -- Represents the basic building blocks of expressions.
  - `INT | FLOAT | STRING | ID ` - Integer, floating-point number, string, or identifier.
  - `LPAR expr RPAR` - An expression enclosed in parentheses.
  - `if-expr` - An if-else statement.
  - `while-expr` - A while-loop statement.
  - `for-expr` - A for-loop statement.
  - `func-def` - A function definition statement.
  - `list-expr` - A list creation expression.

- **if-expr** -- Represents an if-else statement.
  - `IF expr THEN` - Initialization of an if-else block.
  <br>&nbsp; &nbsp; &nbsp; &nbsp;`expr`
  - `(ELIF expr THEN)*` - Optional expression for the `ELIF` branches.
  <br>&nbsp; &nbsp; &nbsp; &nbsp;`expr` 
  - `(ELSE expr)*` - Optional expression for the `ELSE` branch.
  <br>&nbsp; &nbsp; &nbsp; &nbsp;`expr`
  - `END` - Marks the end of the if-else statement.
  
- **while-expr** -- Represents a while-loop statement.
  - `WHILE expr THEN expr NEWLINE statements END` - A loop that continues while a condition is true.

- **for-expr** -- Represents a for-loop statement.
  - `FOR ID EQ expr TO expr (STEP expr)* THEN expr NEWLINE statements END` - A loop that iterates from an initial value to a final value with an optional step value (defaulting to 1 if not provided).

- **func-def** -- Represents the definition of a user-defined function.
  - `FUNC (ID)* LPAR (ID (COMMA ID)*)* RPAR COLON expr NEWLINE statements END` - Definition of a function with an identifier, a list of parameters, and a body expression.

- **list-expr** -- Represents a list creation expression.
  - `LSQUARE (expr (COMMA expr)*)* RSQUARE` - A list creation by specifying its elements, separated by commas, enclosed in square brackets.

### Special Keywords
The following keywords are reserved and may not be used as variable or function name:
```
AND     COLON   COMMA   ELSE	ELIF	END     
FOR     FUNC    IF      NOT     OR      PRINT
STEP    THEN	TO      VAR	WHILE
```



</details>
