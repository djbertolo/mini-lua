# Foundational Literature Review Notes

## Reading List

### Must Reads
- [*Hindley-Milner Type System overview*](https://en.wikipedia.org/wiki/Hindley%E2%80%93Milner_type_system)
- *Write Yourself a Scheme in 48 Hours - Type Inference Section*
- *Luau Type Checking Overview* (Roblox docs)
- *Typed Lua paper*

### Medium Difficulty
- "Practical Type Inference for Dynamically Typed Languages"
- "Typing Lua: A Gradual Type System for Lua"

## Outline

### Introduction: Why Study Type Inference for a Lua-like Language?

Keypoints to cover:
- The rise of dynamic langauges in scripting (Lua, Python, JS, Ruby)
- The safety problems with dynamic typing (runtime failures, hard-to-find bugs)
- Static analysis as a way to prevent entire classes of errors
- Lua's widespread use in game engines and embedded systems
- The challenge: Lua is highly dynamic (difficult to analyze statically)
- Therefore: A small Lua-inspired language is ideal for study

Write about:
- Why dynamically typed languages are error-prone
- Why is Lua important
- How static analysis can improve developer experience
- Why full Lua is too complicated and requires a subset

### Background: Static Typing, Dynamic Typing, and Type Inference

You must show that you understand:
- Static typing vs dynamic typing
- What "type inference" is
- Two major approaches:
	- Algorithm type inference (Hindley-Milner / Damas-Milner)
	- Gradual typing / optional typing (TypeScript, Sorbet, Luau)
- Constraint generation and unification as tools for reasoning about program behavior

Explain:
- What type inference is
- Difference between syntax-directed vs constraint-based inference
- What unification is (example: unify number with T -> T = number)
- How type variables propagate
- How function types are inferred

Keep it simple but accurate

### Core Literature Section: Hindley-Milner and Constraint-Based Typing

You explain:
- Hindley-Milner (HM) as used in ML, Haskell
- Polymorphism and type variables
- Constraint-based typing:
	- Collect constraints from AST nodes
	- Solve them using unification
- Why constraint solving is suitable for your project
- Limitations of HM when applied to dynamic languages like Lua

Explain:
- The HM typing rules
- Principal types
- Let-polymorphism
- Why HM works well on functional languages
- Why HM struggles with:
	- mutation
	- dynamic tables
	- ad-hoc polymorphism

### Related Work: Typed Luau, Teal, TypeScript, Sorbet, Flow

For each system, write:
- What problem the system solves
- How it approaches typing
- What it cannot infer or handle
- Why it matters for your project

You must show:
- Typed Lua (research prototype)
- Luau (production type checker for Roblox)
- Teal (Lua with optional static typing)
- TypeScript (types layered on JS)
- Sorbet (Ruby's optional typing system)
- Flow (static checker for JS)

For each:
- Typed Lua
	- Academic project by Roberto Ierusalimschy's collaborators
	- Adds optional types to Lua
	- Not full inference; relies on annotations
	- Very dynamic table behavior and too complex for pure inference

- Luau (Roblox)
	- Production-quality type checker
	- Gradual typing
	- Heavy use of annotations + local inference
	- Not open-source in full but docs explains ideas

- Teal
	- Optional static typing for Lua
	- Treats Lua as a target language
	- Not designed for pure inference

- TypeScript
	- Extended from JS
	- Complex unification rules
	- Lots of heuristics
	- Not mathematically elegant - but extremely pragmatic

- Sorbet
	- Ruby type checker
	- Designed for huge codebases
	- Lightweight inference, heavy annotation system

### Gaps in Existing Literature / Motivation for Your Project

Here, you argue:
- Full Lua is too dynamic for complete inference so a subset is needed
- Existing systems rely heavily on annotations (Luau, TS, Teal)
- Very few systems attempt pure inference for a dynamically typed scripting language
- You build a pedagogical, transparent, fully-understood type inference pipeline

Highlight:
- No simple educational implementation of type inference for a Lua-like langauge exists
- Typed Lua and Teal require manual type annotations
- Luau performs inference but is proprietary and extremely complex internally
- Full Lua semantics are too dynamic for a clean theoretical system
- A reduced, well-defined language like Mini Lua lets you:
	- study constraint-based inference in isolation
	- create formal rules
	- design a tractable type system


### Conclusion: How This Review Informs MiniLua's Design

Summarize:
- What lessons from the literature you will adopt
- Waht complexities you will avoid
- How this review shapes your grammar, type system, and scope decisions


## Literature Notes:

### Hindley-Milner
- Initial Assessment: The Hindley-Milner type system follows the system that properly structured code can be statically analyzed to determine the type of any variables of functions present within a segment of code. The way that this type is deduced is through starting with a generalization for the typing of each, and only shortening the range of acceptable types when encountered with a use-case that indicates a constraint. Through the use of constraints, the type of a variable or function can be inferred. As more use-cases are implemented, the newly narrower inferred types are replaced across the read code segements for the given type to validate its new use-case. In the event of use-cases that result in conflicting inferences, a type error would be displayed, tying back to that the methodology works for properly structured code.