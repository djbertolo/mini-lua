# MiniLua: A Static Type Inference Engine for a Lua-Like Language

Author: Dominic Bertolo

Institution: California State University, San Bernardino

Topics: Compilers, Static Analysis, Programming Languages

---

## Overview

MiniLua is a research project exploring static type inference for a dynamically-typed scripting language.
The project aims to involve:
- Designing a simplified subset of the Lua language
- Implementing a full lexer, recursive descent parser, and abstract syntax tree (AST)
- Constructing a constraint-based type inference engine
- Implementing a Hindley-Milner style of unification system
- Detecting type-errors, misuse of tables, and inconsistent returns

---

## Goals of the Project

- Built a complete compiler front-end from scratch
- Explore constraint-based type systems
- Model functions, tables, and control flow within a statically-analyzable type environment
- Understand limitations of type inference in dynamic languages
- Produce a research report documenting methodology and results

---

## Key Features

MiniLua Language

A simplified subset of Lua that supports:
- Variables & Assignment
- Arithmetic & boolean expressions
- Conditionals
- While loops
- Function definitions & calls
- Table literals (simplified)
- Return statements

Static Type Inference

The type engine infers:
- Primitive types
- Function signatures
- Table key/value types
- Branch-dependent types
- Type variable propagation

Error Detection

The system detects:
- Type mismatches
- Invalid operations
- Incorrect function calls
- Inconsistent return paths
- Table misuse

---

## Development Timeline (12 Weeks)

Here is a summary of development focuses for each week throughout the duration of this project. More detail about each week can be found in the [Weekly Progress Log](/docs/progress_log.md).
- Weeks 1–2: Lexer & grammar
- Weeks 3–4: Recursive descent parser
- Week 5: Tables
- Week 6: Parser testing
- Week 7: Symbol tables
- Weeks 8–9: Constraint generation
- Weeks 10–11: Unification engine
- Week 12: Final type inference + report

---

## Research Documentation

Related documentation including the finalized research report will be located in `docs/`.

Documents will contain topics including:
- Background & motivation
- Grammar & language design
- Constraint system
- Unification algorithm
- Evaluation results
- Limitations
- Future directions