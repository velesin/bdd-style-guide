# BDD Style Guide

## Table of Contents

* Describe intention, not implementation

### SPEC NAMING

### SPEC ORGANIZATION

### SPEC IMPLEMENTATION

### EXPECTATIONS

### MOCKING AND STUBBING

## Describe intention, not implementation

Avoid revealing parameters, return values, variables, methods and similar low-level implementation details in context and spec descriptions. Instead, focus on the purpose of the code under specification.

### BAD

```js
describe("User with isBanned flag set", function() {
	describe("logIn", function() {
		it("returns false", function() {
			//...	
		});
	});
});
```

### GOOD

```js
describe("a user banned by moderator", function() {
	it("can't log in", function() {
		//...
	});
});
```

### WHY?

Avoiding implementation details in descriptions results in clear separation of concerns. The _"why"_ (the spec description) is clearly distinguished from the _"how"_ (the spec implementation). This provides several benefits:

- Improves the readability and clarity of descriptions.
- Explicitly reveals the purpose of the code under specification, freeing reader from having to reverse-engineer it from the spec implementation.
- Allows the reader to focus on a single concern (purpose or implementation) at a time, what makes both of them easier to reason about.
- Makes specs' descriptions less brittle, by decoupling them from frequently changing implementation details.
