<!--
	Reviewed Literature should follow this template.

	## Title of the Paper

	### Topics Covered
	- Topic 1
	- Topic 2

	### Summary
	A brief summary of the paper.

	### Key Findings
	- Finding 1
	- Finding 2

	### Analysis and Critique
	Your analysis and critique of the paper.

	### BibTeX Entry
	```bibtex
	@article{author2024title,
		title={Title of the Paper},
		author={Author, A. and Author, B.},
		journal={Journal Name},
		volume={10},
		number={2},
		pages={100-110},
		year={2024},
		publisher={Publisher}
	}
	```
-->

# **Reviewed Literature**

---

## **1. Principal Type-Schemes for Functional Programs (Damas & Milner, 1982)**

### **Topics Covered**

* Polymorphic type discipline
* Type inference
* Algorithm W
* Principal type-schemes
* Semantics of ML-style polymorphism

### **Summary**

This seminal 1982 paper by Luís Damas and Robin Milner establishes the formal theoretical foundation for the Hindley–Milner (HM) type system. It provides the first complete proof that every typable expression in ML has a **principal type-scheme**, and that an algorithm (Algorithm W) can compute it. This work generalizes earlier results by Hindley for combinatory logic and provides the theoretical guarantees that make full static type inference both sound and practical.

### **Key Findings**

* Every typable expression in the HM system has a **principal type-scheme**, from which all other types are generic instances.
* Types and type-schemes are formally distinguished (monotypes vs. polytypes with ∀-quantification).
* Algorithm W is proved **sound and complete**, and always computes the most general type for any expression.
* The work provides the formal foundation for type inference in ML and all HM descendants.

### **Analysis and Critique**

This paper forms the theoretical foundation for a “pure HM” MiniLua type checker. It is not an implementation guide but the formal specification of the polymorphic type discipline that MiniLua must follow. A key implication for the project is the strict form of **let-polymorphism**, which forbids polymorphism in function parameters and prevents many Lua idioms from type-checking. The Damas–Milner proof of principality justifies the project’s commitment to purity and establishes the soundness guarantees that MiniLua inherits.

### **BibTeX Entry**

```bibtex
@inproceedings{Damas:1982:PTS:582153.582176,
  author = {Damas, Luís and Milner, Robin},
  title = {Principal Type-Schemes for Functional Programs},
  booktitle = {POPL '82: Proceedings of the 9th ACM SIGPLAN-SIGACT Symposium on Principles of Programming Languages},
  year = {1982},
  pages = {207--212},
  doi = {10.1145/582153.582176},
  publisher = {ACM},
  address = {New York, NY, USA},
}
```

---

## **2. Algorithm W Step by Step (Gräber, 2011)**

### **Topics Covered**

* Hindley–Milner implementation
* Algorithm W
* Unification
* Haskell implementation
* Abstract Syntax Trees
* Type inference monad

### **Summary**

This literate programming report by Martin Gräber provides a complete, clear, and executable implementation of Algorithm W in Haskell. It defines the AST for expressions and types, the structure of type schemes and environments, and the complete inference function. The implementation demonstrates the mechanics of HM inference, including instantiation, generalization, and unification.

### **Key Findings**

* Defines concrete Haskell data types for expressions, types, and type schemes.
* Provides a runnable implementation of Algorithm W (`ti`).
* Clearly demonstrates the distinction between **EAbs** (monomorphic parameters) and **ELet** (polymorphic generalization).
* Shows practical use of the occurs check and error handling mechanisms.

### **Analysis and Critique**

This document is an ideal implementation reference for the MiniLua type checker. It offers executable pseudocode, a clean architecture for the type inference monad, and an implementation that directly reflects the theoretical rules defined by Damas–Milner. Its explicit treatment of let-polymorphism is especially valuable, as it illustrates the central constraint that will cause most Lua idioms to fail under a pure HM typing discipline.

### **BibTeX Entry**

```bibtex
@techreport{Graber:AWStepByStep,
  author = {Gräber, Martin},
  title = {Algorithm W Step by Step},
  institution = {Institut für Informatik, Ludwig-Maximilians-Universität München},
  year = {2011},
  note = {Available at \url{https://raw.githubusercontent.com/mgrabmueller/AlgorithmW/master/pdf/AlgorithmW.pdf}}
}
```

---

## **3. Operational Semantics for Featherweight Lua (Lin, 2015)**

### **Topics Covered**

* Formal Lua semantics
* Core Featherweight Lua calculus
* Tables
* Metatables and metamethods
* First-class functions

### **Summary**

This master’s thesis defines “Featherweight Lua” (FWLua), a formal core calculus for Lua that strips away syntactic sugar to provide a minimal, precise language suitable for formal reasoning. It identifies Lua’s essential features—first-class functions, tables, and metatables—and provides operational semantics for each, particularly focusing on the dynamic behavior introduced by metatables.

### **Key Findings**

* Provides a formal syntax and semantics for a minimal Lua calculus.
* Identifies Lua’s “exotic and important” features, including tables and metatables.
* Describes how operators are desugared into metamethod calls (e.g., `__add`).
* Establishes a formal foundation for reasoning about Lua behavior.

### **Analysis and Critique**

This work is crucial for defining the MiniLua subset. It offers a formal language from which MiniLua can be derived by removing features incompatible with pure HM: metatables, nil-propagation semantics, and dynamic table mutation. Its formalization of metatables is particularly useful, as it gives a rigorous definition of the features that MiniLua must omit to maintain soundness and decidability.

### **BibTeX Entry**

```bibtex
@mastersthesis{Lin2015OperationalSF,
  title={Operational Semantics for Featherweight Lua},
  author={Hanshu Lin},
  year={2015},
  school={San Jose State University}
}
```

---

## **4. Static Type Inference in a Dynamically Typed Language (Aiken & Murphy, 1991)**

### **Topics Covered**

* Type inference
* Dynamic languages
* Abstract interpretation
* Regular tree types
* Program optimization

### **Summary**

This paper presents a type inference system for FL, a dynamically typed functional language. Unlike HM systems, which aim for soundness and principality, this system uses an abstract interpretation of operational semantics to gather precise type information for compiler optimization rather than error detection.

### **Key Findings**

* Introduces a type language based on regular trees to represent dynamic flow of types.
* Uses operational semantics to “run” a program abstractly and track type behavior.
* Can infer useful type information for programs HM would reject as un-typeable.
* Prioritizes optimization precision over static soundness.

### **Analysis and Critique**

This work represents the opposite philosophical direction from MiniLua. Instead of restricting the language to fit a pure type system, Aiken and Murphy extend the type language to accommodate dynamic behavior. For MiniLua’s positioning, this paper is important because it highlights the design decision the project makes: choosing *rejection for safety* (HM) over *precision for optimization* (abstract interpretation). It provides a critical contrast demonstrating the constraints of pure HM.

### **BibTeX Entry**

```bibtex
@inproceedings{Aiken:1991:STI:99583.99611,
  author = {Aiken, Alexander and Murphy, Brian R.},
  title = {Static Type Inference in a Dynamically Typed Language},
  booktitle = {POPL '91: Proceedings of the 18th ACM SIGPLAN-SIGACT Symposium on Principles of Programming Languages},
  year = {1991},
  pages = {279--290},
  doi = {10.1145/99583.99611},
  publisher = {ACM},
  address = {New York, NY, USA},
}
```

---

## **5. Typed Lua: An Optional Type System for Lua (Maidl, Mascarenhas & Ierusalimschy, 2014)**

### **Topics Covered**

* Optional typing
* Flow typing
* Union types
* Record typing
* Lua type annotations

### **Summary**

Typed Lua is an optionally typed extension to Lua designed to provide early error detection without disrupting Lua’s idioms. It introduces type annotations, union types (especially for nil), and flow typing. Non-annotated code remains dynamically typed, distinguishing it from classical gradual typing.

### **Key Findings**

* Introduces explicit type annotations with optional type checking.
* Adds **union types** (e.g., `number?`) to model nil—the most central Lua idiom.
* Includes **flow typing** to refine types based on conditionals.
* Provides a powerful record type system to model Lua’s flexible tables.

### **Analysis and Critique**

Typed Lua represents the pragmatic approach to typing Lua. Its willingness to extend the type system, especially with union types and flow typing, stands in sharp contrast to MiniLua’s pure HM approach. It demonstrates that preserving Lua idioms requires abandoning principality, soundness, or both. The project’s strict interpretation of HM provides a useful baseline against which Typed Lua’s pragmatic compromises can be measured.

### **BibTeX Entry**

```bibtex
@inproceedings{Maidl:2014:TLO:2617548.2617553,
  author = {Maidl, André Murbach and Mascarenhas, Fabio and Ierusalimschy, Roberto},
  title = {Typed Lua: An Optional Type System for Lua},
  booktitle = {Proceedings of the 1st Workshop on Dynamic Languages and Datalog},
  series = {Dyla '14},
  year = {2014},
  pages = {27--36},
  doi = {10.1145/2617548.2617553},
  publisher = {ACM},
  address = {New York, NY, USA},
}
```

---

## **6. Goals of the Luau Type System (Brown, Friesen & Jeffrey, 2021)**

### **Topics Covered**

* Gradual typing
* Human-centered PL design
* Strict vs. non-strict type checking
* Type-driven tooling
* Roblox programming environment

### **Summary**

This position paper outlines the design goals for Luau, Roblox’s gradually-typed Lua-derived language. Luau supports both strict mode (sound, HM-like) and non-strict mode (“no false positives”). It emphasizes developer experience, accessibility for beginners, and tooling such as autocomplete and refactoring support.

### **Key Findings**

* Prioritizes developer experience over academic purity.
* Defines “strict mode” (sound, no false negatives) and “non-strict mode” (helpful, no false positives).
* Supports rich tooling even for ill-typed programs.
* Designed for a diverse developer community with a wide range of experience.

### **Analysis and Critique**

Luau exemplifies an industrial rejection of academic purity in favor of usability. Its non-strict mode directly contradicts the behavior of a pure HM system, which produces many false positives by design. For MiniLua, Luau provides a practical counterpoint: where Luau minimizes friction for learners, MiniLua enforces maximal rigor. This enables MiniLua to serve as the formal baseline for understanding what Luau and Typed Lua must compromise to support real-world development.

### **BibTeX Entry**

```bibtex
@inproceedings{Brown:2021:GOL:3486606.3486770,
  author = {Brown, Lily and Friesen, Andy and Jeffrey, Alan},
  title = {Position Paper: Goals of the Luau Type System},
  booktitle = {HATRA '21: Human Aspects of Types and Reasoning Assistants},
  year = {2021},
  pages = {1--7},
  publisher = {ACM},
  address = {New York, NY, USA},
  note = {arXiv:2109.11397v1 [cs.PL]}
}
```

---

## **7. Typing Haskell in Haskell (Jones, 1999)**

### **Topics Covered**

* Hindley–Milner
* Type inference implementation
* Type classes
* Haskell language design
* Polymorphism

### **Summary**

Mark Jones’ classic paper provides a literate implementation of a type checker for a substantial subset of Haskell, written in Haskell itself. It goes beyond pure HM by including type classes—a principled form of ad-hoc polymorphism—but also serves as the most widely used pedagogical reference for implementing HM-style inference.

### **Key Findings**

* Provides a full, clear implementation of HM type inference.
* Demonstrates extension of HM with **type classes**.
* Serves as a standard reference for constructing type inference engines.
* Includes test suites illustrating polymorphism, let-binding, and occurs check failures.

### **Analysis and Critique**

While MiniLua will not implement type classes, this paper remains the “gold standard” for designing a real-world HM type checker. Its clarity makes it valuable for implementation methodology, test case construction, and architectural patterns. It also provides a conceptual bridge: Lua’s metatables are a dynamic form of overloading, while Haskell’s type classes are a static one. MiniLua includes neither, but this comparison helps situate future work.

### **BibTeX Entry**

```bibtex
@inproceedings{Jones:1999:THH,
  author = {Jones, Mark P.},
  title = {Typing Haskell in Haskell},
  booktitle = {Proceedings of the 1999 Haskell Workshop},
  year = {1999},
  month = {September},
  note = {Published as a University of Utrecht technical report UU-CS-1999-28.}
}
```

Here is the literature review entry for Benjamin C. Pierce’s *Types and Programming Languages*, formatted to match your existing document.

-----

## **8. Types and Programming Languages (Pierce, 2002)**

### **Topics Covered**

  * Operational semantics
  * Lambda calculus
  * Type systems and safety proofs
  * Type reconstruction (inference)
  * Unification algorithms
  * Let-polymorphism

### **Summary**

Widely regarded as the comprehensive standard text for type theory, this book provides a rigorous introduction to type systems and programming language theory. It systematically builds from un-typed lambda calculus to complex features like subtyping, recursive types, and polymorphism. Of particular relevance to this project are the chapters on type reconstruction and unification, which mathematically formalize the process of inferring types in the absence of explicit annotations.

### **Key Findings**

  * Establishes the standard approach for proving type safety via **Progress** (a well-typed term is not stuck) and **Preservation** (evaluation preserves types).
  * Formalizes **Type Reconstruction** as a constraint satisfaction problem, providing the theoretical basis for separating constraint generation from solving.
  * Details the **Robinson Unification Algorithm**, the core mechanism used to solve type constraints in Hindley–Milner systems.
  * Provides the canonical notation and definitions for constraint-based typing used in modern academic literature.

### **Analysis and Critique**

For MiniLua, this text serves as the primary authority for the "Background" and "Methodology" sections. While papers like Damas–Milner (1982) provide the foundational proofs, Pierce provides the modern, pedagogical, and algorithmic blueprints necessary for implementation. Replacing informal tutorials with Pierce validates the project's definitions of "Constraint Generation" and "Unification," ensuring the type checker is built upon formally verified algorithms rather than ad-hoc heuristics.

### **BibTeX Entry**

```bibtex
@book{Pierce:2002:TPL,
  author = {Pierce, Benjamin C.},
  title = {Types and Programming Languages},
  year = {2002},
  isbn = {0-262-16209-1},
  publisher = {MIT Press},
  address = {Cambridge, MA, USA}
}
```

-----

## **9. A Simple Algorithm and Proof for Type Inference (Wand, 1987)**

### **Topics Covered**

  - Constraint-based type inference
  - Constraint generation vs. Unification
  - Algorithm W alternatives
  - Correctness proofs
  - Type error localization

### **Summary**

Mitchell Wand’s paper presents a reformulation of the Hindley-Milner inference algorithm. Unlike the original Algorithm W, which interleaves constraint generation and unification (substitution), Wand’s algorithm separates these into two distinct phases: (1) generating a set of equations (constraints) from the AST, and (2) solving them via unification. This separation simplifies the proof of correctness and the implementation of the inference engine.

### **Key Findings**

  - Proves that type inference can be distinctively separated into **Action generation** (constraints) and **Equation solving** (unification).
  - Demonstrates that the unification algorithm is the sole source of type errors.
  - Provides a simpler recursive structure for the inference algorithm compared to Damas-Milner.
  - Establishes the methodology used by most modern "constraint-based" type checkers.

### **Analysis and Critique**

This paper is the direct architectural blueprint for the "Constraint Generation" and "Constraint Solving" phases described in section 2.4 of the MiniLua draft. While Damas-Milner (1982) provides the theory, Wand (1987) provides the engineering strategy. For MiniLua, adopting Wand’s approach over the standard Algorithm W allows for better error reporting and a cleaner codebase, aligning with the project's goal of a practical implementation.

### **BibTeX Entry**

```bibtex
@inproceedings{Wand:1987:SAP:41625.41630,
  author = {Wand, Mitchell},
  title = {A Simple Algorithm and Proof for Type Inference},
  booktitle = {POPL '87: Proceedings of the 14th ACM SIGPLAN-SIGACT Symposium on Principles of Programming Languages},
  year = {1987},
  pages = {215--222},
  doi = {10.1145/41625.41630},
  publisher = {ACM},
  address = {New York, NY, USA}
}
```

-----

## **10. Gradual Typing for Functional Languages (Siek & Taha, 2006)**

### **Topics Covered**

  - Gradual typing
  - The `?` (dynamic) type
  - Consistency relation (\~ via subtyping)
  - Runtime casts
  - Integrating static and dynamic typing

### **Summary**

Siek and Taha formally introduce "Gradual Typing," the system that allows parts of a program to be statically typed, and other parts dynamically typed, mediated by a consistency relation. They introduce the notion of the dynamic type (`?`), which functions similarly to the `any` type mentioned in the MiniLua draft. They provide the formal semantics for how static assumptions can safely interact with dynamic values.

### **Key Findings**

  - Defines the **consistency relation**, which replaces standard unification in gradual systems.
  - Demonstrates how to insert runtime casts to ensure type safety at the boundaries of typed and un-typed code.
  - Proves that a gradually typed program behaves identical to a statically typed one if no dynamic types are used.

### **Analysis and Critique**

This paper defines exactly what MiniLua is *rejecting*. Section 2.3 and 6.3 of the MiniLua draft explicitly choose pure HM over gradual typing. To justify this decision, it is necessary to cite the foundational definition of Gradual Typing. This entry allows the MiniLua project to contrast its "Unification" approach against Siek and Taha’s "Consistency" approach, highlighting that MiniLua prioritizes total static guarantees over the flexibility offered by Siek and Taha.

### **BibTeX Entry**

```bibtex
@inproceedings{Siek:2006:GTF:1159876.1159881,
  author = {Siek, Jeremy G. and Taha, Walid},
  title = {Gradual Typing for Functional Languages},
  booktitle = {Scheme '06: Proceedings of the 2006 Workshop on Scheme and Functional Programming},
  year = {2006},
  pages = {81--92},
  publisher = {University of Chicago},
  address = {Chicago, IL, USA}
}
```

-----

## **11. Understanding TypeScript (Bierman et al., 2014)**

### **Topics Covered**

  - Structural typing
  - JavaScript semantics
  - Gradual typing in practice
  - Ambient definitions
  - Type erasure

### **Summary**

This paper provides a formalization of TypeScript, one of the languages cited in the MiniLua draft as a primary influence on modern dynamic typing. It explores how TypeScript layers a static type system over JavaScript’s dynamic semantics. Unlike HM systems which use nominal typing, this paper details TypeScript’s use of **structural subtyping** and its specific handling of object literals, which closely mirrors how Lua tables function.

### **Key Findings**

  - Formalizes a safe subset of TypeScript and its type checking rules.
  - Describes the **Erasure** semantics: types are removed at runtime, with no runtime enforcement (unlike Siek & Taha).
  - Details how structural types interact with class-based hierarchies.
  - Highlights the challenges of inferring types for overloaded dynamic functions.

### **Analysis and Critique**

The MiniLua draft frequently references TypeScript (Source 74, 89) as a benchmark for industry-standard type inference. This paper provides the academic verification of TypeScript's mechanics. It is particularly relevant for its discussion on **structural typing** for objects. MiniLua must decide whether to treat tables as nominal records (like C structs) or structural shapes (like TypeScript interfaces); this paper provides the arguments for the structural approach, which Teal and Luau partially adopt.

### **BibTeX Entry**

```bibtex
@inproceedings{Bierman:2014:UT:2660193.2660237,
  author = {Bierman, Gavin and Abadi, Mart\'{i}n and Torgersen, Mads},
  title = {Understanding TypeScript},
  booktitle = {ECOOP 2014: Object-Oriented Programming},
  year = {2014},
  pages = {257--281},
  doi = {10.1007/978-3-662-44202-9_11},
  publisher = {Springer},
  address = {Berlin, Heidelberg}
}
```

-----

## **12. Lua: An Extensible Extension Language (Ierusalimschy, de Figueiredo & Celes, 1996)**

### **Topics Covered**

  - Language design
  - Associative arrays (Tables)
  - Fallback mechanisms (Metatables precursor)
  - Embeddable languages
  - Dynamic typing philosophy

### **Summary**

This is the seminal paper introducing Lua to the academic world. It explains the rationale behind Lua's design choices: simplicity, portability, and the use of a single data structure (the table) for arrays, records, and objects. It articulates the "mechanisms, not policies" philosophy that leads to the highly dynamic nature (Source 28) that makes static analysis so difficult.

### **Key Findings**

  - Establishes the **Table** as the sole data structuring mechanism.
  - Explains the imperative, dynamic nature of the language environment.
  - Details the design of "fallbacks" (which evolved into metatables), the mechanism that MiniLua must restrict.
  - Justifies the lack of explicit types in favor of rapid prototyping.

### **Analysis and Critique**

To define a "Lua-like" language (Source 36), one must reference the definition of Lua. This paper explains *why* Lua is imperative and dynamic. It supports the MiniLua draft's assertion that Lua is primarily imperative (Source 197) and highlights the specific features (Tables) that MiniLua must "break" (Source 291) to achieve sound inference. It provides the "Before" picture for the MiniLua transformation.

### **BibTeX Entry**

```bibtex
@article{Ierusalimschy:1996:LEE:226264.226283,
  author = {Ierusalimschy, Roberto and de Figueiredo, Luiz Henrique and Celes, Waldemar},
  title = {Lua: An Extensible Extension Language},
  journal = {Software: Practice and Experience},
  volume = {26},
  number = {6},
  year = {1996},
  pages = {635--652},
  doi = {10.1002/(SICI)1097-024X(199606)26:6<635::AID-SPE26>3.0.CO;2-P},
  publisher = {Wiley}
}
```

-----

## **13. The Principal Type-Scheme of an Object in Combinatory Logic (Hindley, 1969)**

### **Topics Covered**

  - Combinatory Logic
  - Principal Type-Schemes
  - Type Inference Algorithm
  - Intuitionist Logic
  - Curry-Howard correspondence

### **Summary**

J. Roger Hindley's 1969 paper is the historical origin of the type inference algorithm that eventually became the "H" in "HM". Working within Combinatory Logic rather than Lambda Calculus, Hindley proved that if a term has a type, it has a "principal" type scheme—a most general type from which all other valid types can be derived.

### **Key Findings**

  - First discovery of the **principal type property** for simple type systems.
  - Describes the algorithm that computes the principal type (a precursor to Algorithm W).
  - Links type inference to theorem proving in intuitionist propositional logic.
  - Establishes the theoretical possibility of inferring types without annotations.

### **Analysis and Critique**

Including Hindley completes the theoretical genealogy of the MiniLua project. While Damas-Milner (1982) applied these concepts to programming languages (ML), Hindley established the mathematical logic. Citing this acknowledges that the "pure type inference" (Source 205) goal of MiniLua relies on logic discovered over 50 years ago. It reinforces the "Soundness and Completeness" goals (Source 278) by pointing to the mathematical root of those proofs.

### **BibTeX Entry**

```bibtex
@article{Hindley:1969:PTS,
  author = {Hindley, J. Roger},
  title = {The Principal Type-Scheme of an Object in Combinatory Logic},
  journal = {Transactions of the American Mathematical Society},
  volume = {146},
  year = {1969},
  pages = {29--60},
  doi = {10.1090/S0002-9947-1969-0253905-6},
  publisher = {American Mathematical Society}
}
```