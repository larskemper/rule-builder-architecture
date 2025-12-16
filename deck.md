---
marp: true
theme: custom
paginate: true
---

<!-- _class: lead -->
# Rule Builder

fundamentals@after-sales

---

## What is the Rule Builder?

The Rule Builder allows merchants to create _dynamic business rules_ without code to control:

- Shipping method availability
- Payment method availability
- Promotions & Discounts
- Product pricing
- Flow Builder conditions

---

<!-- _class: lead -->
## Definition

"Compare an _input_ value from the _scope_ with a configured _value_ using an _operator_."

---

<!-- _class: lead -->
## Rule

Every rule implements a simple interface:

<img src="./diagrams/rule-interface.png" height="250px">

Core question: Does this condition match the current context?

---

<!-- _class: lead -->
## Example

"If the _customer's group_ is _'VIP'_ **AND** the _cart amount_ is greater than or equal to _€150_ **AND** the _shipping country_ is _Germany_, then offer the _'Express Shipping'_ method."

---

<!-- _class: lead -->
## Example tree

<img src="./diagrams/rule-example-tree.png" height="400px">

---

<!-- _class: lead -->
## Composite Pattern (Container Rules)

Rules are composed as a _tree structure_ using logical containers:

<img src="./diagrams/rule-container-tree.png" height="400px">

---

## Container Types

| Container             | Logic          |
| --------------------- | -------------- |
| AndRule               | ALL            |
| OrRule                | ANY            |
| NotRule               | NEGATE         |
| XorRule               | EXACTLY ONE    |
| MatchAllLineItemsRule | ALL LINE ITEMS |

---

<!-- _class: lead -->
## Evaluation Context (Rule scope)

Scopes provide the _context data_ for rule evaluation:

<img src="./diagrams/rule-scopes.png" height="400px">

---

<!-- _class: lead -->
## Rule Evaluation

<img src="./diagrams/rule-cart-evaluation.png" height="400px">

---

<!-- _class: lead -->
## Payload Storage

Rules are stored as _serialized PHP objects_ for fast runtime evaluation.

<img src="./diagrams/rule-storage.png" height="100px">

---

<!-- _class: lead -->
## Architecture Summary

<img src="./diagrams/rule-overview.png" height="400px">

---

<!-- _class: lead -->
## Bottleneck

Rule evaluation needs the cart.
Cart calculation needs the rules.

That creates a costly dependency cycle (lots of loading on each request).

=> Rule System v2 [RFC](https://github.com/shopware/shopware/discussions/3406)

---

## Questions?
