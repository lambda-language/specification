# Parsing step
Lambda language syntax can be represented by an universal grammar file. Almost all the syntax is an expression which returns some value. Even the rarely statements in the language can be described in term of an expression.

### Lexing elements
Some basic lexing elements like `identifier` or `number` are described with regex rules.
| Rule name  | Regex expression |
| ---------- | ---- |
| identifier | `~(symbol | number | string) (~space any)+` |
| number 	 | `digit+` |
| string 	 | `"\"" (~"\"" any)* "\""` |
| symbol 	 | `"←" \| "λ" \| "⟨" \| "⟩" \| "∀" \| "∈" \| "ℕ" \| "⇒"` |
| comment	 | `"//" (~eol any)*` |
| multiline  | `"/*" (~"*/" any)* "*/"` |
| eol 	     | `"\n" \| "\r" \| "\u2028" \| "\u2029"` |

### Expressions
#### Typed expression
```js
TypedExpression
  = "⟨" ListOf<Expression, ","> "⟩"
  | identifier
```

#### Forall and uniqueness 
```js
Forall = "∀" identifier ("∈" identifier)?
Exists = "∃" identifier ("∈" identifier)?
```
