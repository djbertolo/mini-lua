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

This paper forms the theoretical foundation for a “pure HM” MiniLua type checker. It is not an implementation guide but the formal specification of the polymorphic type discipline that MiniLua must follow. A key implication for the project is the strict form of **let-polymorphism**, which forbids polymorphism in function parameters and prevents many Lua idioms from typechecking. The Damas–Milner proof of principality justifies the project’s commitment to purity and establishes the soundness guarantees that MiniLua inherits.

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

* Defines concrete Haskell datatypes for expressions, types, and type schemes.
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
* Can infer useful type information for programs HM would reject as untypeable.
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

Typed Lua is an optionally typed extension to Lua designed to provide early error detection without disrupting Lua’s idioms. It introduces type annotations, union types (especially for nil), and flow typing. Unannotated code remains dynamically typed, distinguishing it from classical gradual typing.

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

Widely regarded as the comprehensive standard text for type theory, this book provides a rigorous introduction to type systems and programming language theory. It systematically builds from untyped lambda calculus to complex features like subtyping, recursive types, and polymorphism. Of particular relevance to this project are the chapters on type reconstruction and unification, which mathematically formalize the process of inferring types in the absence of explicit annotations.

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