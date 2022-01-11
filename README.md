# Lambda language
Lambda is a language inspired by some mathematics notations and mostly influenced by the functional programming paradigm with a focus on extending typed lambda calculus.

The language supports many levels of programming as type level and value level. It is designed to be a functional lambda calculus language with a strong type system while keeping a pleasant and logical syntax.

## Summary

### Language implementation specifications
- [Parsing Lambda language](language/parsing.md)
- [Abstract tree elements definitions](language/grammar.md)
- [Interpretation step](language/runtime)
  - [Typechecking values](language/runtime/typechecking.md#values)
  - [Kind-checking types](language/runtime/typechecking.md#types)
  - [Evaluating value expressions](language/runtime/evaluation.md#values)
  - [Evaluating type expressions](language/runtime/evaluation.md#types)
- [Optimizations](language/optimization.md)
- [Type inference rules](language/inference-rules.md)

### User applications
- [Type level programming introduction](user/type-level.md)
- [Real world use-cases of type level](user/real-world.md)
- [Some theoretical examples](user/theory.md)
- [Using Lambda as a theorem prover](user/theorem-prover.md)

### Examples
- [Recursive factorial for ℕ](examples/factorial.lambda)