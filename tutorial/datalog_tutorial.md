# Datalog Tutorial for LLM Logic Project (Task 6)

## What is Datalog?

Datalog is a declarative logic programming language used for querying and reasoning over relational data. It’s syntactically similar to Prolog but more restricted, which ensures termination and makes it suitable for database-style use cases. It’s commonly used in program analysis, static analysis, and knowledge representation.

---

## Basic Concepts

- **Facts**: Atomic statements about data.

  ```prolog
  parent(john, mary).
  parent(mary, alice).
  ```

- **Rules**: Logical implications that define relationships.

  ```prolog
  grandparent(X, Y) :- parent(X, Z), parent(Z, Y).
  ```

- **Queries**: Ask questions of the system.

  ```prolog
  ?- grandparent(john, Y).
  ```

---

## Semantics

Datalog uses *bottom-up evaluation* (also called fixpoint semantics). It computes all logical consequences from the given facts and rules until no more conclusions can be drawn.

---

## How to Run Datalog

### Option 1: Soufflé

- High-performance Datalog engine
- Install and run via CLI
- Website: [https://souffle-lang.github.io](https://souffle-lang.github.io)

### Option 2: PyDatalog (Python)

- Install using pip:
  ```bash
  pip install pyDatalog
  ```
- Example:
  ```python
  from pyDatalog import pyDatalog

  pyDatalog.create_terms('parent, grandparent, X, Y, Z')
  +parent('john', 'mary')
  +parent('mary', 'alice')
  grandparent(X,Y) <= parent(X,Z) & parent(Z,Y)

  print(grandparent(X, 'alice'))
  ```

---

## Why It Matters for LLMs

- Datalog provides a symbolic, interpretable format that LLMs can learn to generate.
- LLMs can translate natural language into Datalog facts and rules, allowing structured reasoning.
- This hybrid approach bridges natural language understanding and formal logic execution.

---

## LLM + Datalog Example

**Input Prompt:**  
"If Mary is Alice's mother and John is Mary's father, who is Alice's grandfather?"

**LLM-Generated Output:**
```prolog
parent(john, mary).
parent(mary, alice).
grandparent(X, Y) :- parent(X, Z), parent(Z, Y).
?- grandparent(X, alice).
```


