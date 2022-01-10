# Parsing step
Lambda language syntax can be represented by an universal grammar file. Almost all the syntax is an expression which returns some value. Even the rarely statements in the language can be described in term of an expression.

### Lexing elements
Some basic lexing elements like `identifier` or `number` are described with regex rules.
| Rule name  | Regex expression |
| ---------- | ---- |
| identifier | `~(keyword \| number \| string) (~space any)+` |
| number 	 | `digit+` |
| string 	 | `"\"" (~"\"" any)* "\""` |
| keyword 	 | `"λ" \| "∈" \| "⟨" \| "⟩" \| "?" \| ":" \| "→" \| "∃" \| "←" \| "⇒" \| "⇐" \| "∀" \| "," \| "(" \| ")" \| "/" \| ";" \| "{" \| "}" \| "\|" \| "+" \| "*" \| "-"`
| comment	 | `"//" (~eol any)*` |
| multiline  | `"/*" (~"*/" any)* "*/"` |
| eol 	     | `"\n" \| "\r"` |

### Expressions
An expression represents in Lambda all syntax that must return a value.
```js
Expression
  = Lambda | Condition | LetExpression
  | FunctionCall | Addition | Variable
  | Set | Value
```
#### Typed expression
Typed expression is an expressio that let you describe how your value must satisfy a type. Everything that is an expression can be used in a typed expression. The runtime typechecking also let you calling functions which can be recursive or impures.
```js
Typed
  = Forall | Exists | Set
  | Declaration | Expression
```

#### Forall and existance
The `forall` and `exists` keywords are used to describe the existance state of a variable. Forall means that regardless the type, it must satisfy the way in which the type is described. Exists means that it exists at least one type that satisfy the type description.
```js
// Domain shouldn't always be specified when it can be infered
Forall = "∀" identifier ("∈" identifier)?
Exists = "∃" identifier ("∈" identifier)?
```

#### Value
```js
Value 
  = "(" Expression ")"
  | identifier
  | number
  | string
```

#### Set
A set in Lambda is the same as a set in mathematics. It can be represented by a higher and stronger version of the common lists in other programming languages. Set can describe values but also types, implying that it can exists set of types.
```js
Set 
  = "{" 
      // Set elements
      ListOf<(Typed | Expression), ",">
      // Set comprehension
      ("|" ListOf<(Typed | Expression), ",">)?
    "}"
```

#### Variable
A variable can be simply an identifier which is going to be infered at runtime but it can also be a typed variable using typed expression rules.
```js
Variable
  = "⟨" ListOf<Typed, ","> "⟩"
  | identifier
```

#### Lambda
Here is the main feature of Lambda causing its name. Lambda is a function in the mathematical sense that's based on the lambda calculus properties. 
```js
Lambda = "λ" Variable "→" Expression
```

#### Condition
Condition is also described as a form of expression as it must return a value from its result. Its syntax is inspired by the conditional operator in other programming languages.
```js
Condition = Operator "?" Expression ":" Expression
```

#### Let expression
Let expression is a way to define a variable and directly use it in the expression. So the variable do not persist in the scope and the let-expression only returns its expression result.
```js
LetExpression
  = Declaration "⇒" Expression
  | Expression "⇐" Declaration
```

### Calls
A call in Lambda can be of several kinds as an operator call in infix style or merely a standard function call

```js
FunctionCall
  = Operator | Call
```

#### Operator
An operator is a basically a function call but in infix form for symbols function names.
```js
Operator = Expression symbols Expression
```

#### Function
A function call is not delimited by parenthesis like in other languages. So, it truly depends on the way you do parenthesising.
```js
Call = (~symbols Expression) (~Declaration Value)
```

### Arithmetic
Basic arithmetic is natively supported from the parser as it requires a predescence rule and logic.

#### Addition
```js
Addition
  = Addition "+" Product
  | Addition "-" Product
  | Product
```

#### Product
```js
Product
  = Product "*" Value
  | Product "/" Value
  | Value
```

