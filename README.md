# Lambda language
Lambda is a language inspired by some mathematics notations and mostly influenced by the functional programming paradigm with a focus on extending typed lambda calculus.

The language supports many levels of programming as type level and value level. It is designed to be a functional lambda calculus language with a strong type system while keeping a pleasant and logical syntax.

## Summary

### Language implementation specifications
- [Parsing Lambda language]()
- [Abstract tree elements definitions]()
- [Interpretation step]()
  - [Typechecking values]()
  - [Kindchecking types]()
  - [Evaluating value expressions]()
  - [Evaluating type expressions]()
- [Optimizations]()
- [Type inference rules]()

### User applications
- [Type level programming introduction](user/type-level.md)
- [Real world usecases of type level](user/real-world.md)
- [Some theorical examples](user/theory.md)
- [Using Lambda as a theorem prover](user/theorem-prover.md)

### Examples
- [Recursive factorial for ℕ](examples/factorial.lambda)