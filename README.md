# Monkey Interpreter

A tree-walking interpreter for the **Monkey** programming language, written from scratch in **Go** — no parser generators, no external dependencies. Built by following Thorsten Ball's *Writing an Interpreter in Go*, implementing every stage of the language pipeline by hand.

## Why this project

The goal wasn't to use an interpreter — it was to understand how one works end to end. Each stage (lexing, parsing, evaluation) is a self-contained problem, and the interesting part is *why* each design choice holds together. The whole pipeline is covered by unit tests at every layer.

## Language pipeline

```
source code → Lexer → Pratt Parser → AST → Tree-walking Evaluator → result
```

- **Lexer** — turns raw source into a stream of tokens.
- **Pratt parser** — top-down operator-precedence parsing; handles prefix/infix operators and their precedence cleanly without a grammar generator.
- **AST** — typed node tree built on Go interfaces (structural typing).
- **Evaluator** — walks the tree and evaluates it against an environment, with lexical scoping and closures.

## Language features

- Integers, booleans, strings
- Arrays and hash maps
- Prefix and infix operators with correct precedence
- `let` bindings and lexical scope
- First-class functions and **closures**
- Conditionals and return values

## Example

```monkey
let fibonacci = fn(x) {
  if (x < 2) {
    return x;
  }
  return fibonacci(x - 1) + fibonacci(x - 2);
};

fibonacci(10); // => 55
```

## Running it

```bash
go run .        # start the REPL
go test ./...   # run the full test suite
```

## Tests

Unit tests cover the lexer, parser, and evaluator independently — each stage is verified on its own so a failure points to exactly one layer of the pipeline.
