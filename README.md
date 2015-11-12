# BDD Style Guide

## Table of Contents

### SPEC NAMING

* Describe intention, not implementation
* Avoid concrete numbers or values in spec names
* Use precise and descriptive spec names
* Reveal in a spec name everything the spec verifies

### SPEC ORGANIZATION

### SPEC IMPLEMENTATION

### EXPECTATIONS

### MOCKING AND STUBBING

- - -

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

- - -

## Avoid concrete numbers or values in spec names

Hide the value under a meaningful description that reveals the purpose of the value.

### BAD

```js
describe("an upload bigger than 100 MB", function() {
	//...
});
```

### GOOD

```js
describe("an upload bigger than free daily quota", function() {
	//...
});
```

### WHY?

Concrete values are also, in a sense, implementation details. Hiding them makes specs less brittle (the meaning of a given value usually never changes, while the actual value may change often). It also reveals the business reason behind a given behavior, that otherwise might have been impossible to guess.

- - -

## Use precise and descriptive spec names

Name specs so that all the conditions, actions and results are fully clear from reading the name alone, without the need to look into the spec implementation.

### BAD

```js
describe("bot", function() {
	it("correctly checks posts", function() {
		//...
	});
});
```

### GOOD

```js
describe("anti-spam bot", function() {
	it("marks all new posts containing spam as requiring verification", function() {
		//...
	});
});
```

### WHY?

This is symmetrical to the "Use self-explanatory fixtures" rule. You usually operate at only one of the two possible levels of abstraction at any given moment: either a spec name or a spec implementation. Each of these levels of abstraction should contain all the relevant information for this level, so you can understand what's going on without the need to jump up or down the level to check additional details.

Naming all the specs this way also results in a specification that reads as a full, comprehensive documentation. Such a documentation allows to quickly understand the code base, without digging through all the implementation details and parts of it can be even discussed with business experts.

Another benefit of clear and precise spec naming are clear and precise failure messages, which make pinpointing the problem easier.

- - -

## Reveal in a spec name everything the spec verifies

Don't tell only half of the truth. If a spec body verifies any secondary behaviors or side effects, explicitly describe them in the spec name.

### BAD

```js
describe("Array.push", function() {
	it("adds elements to the end of an array", function() {
		var array = [1, 2];

		var newLength = array.push(3, 4);

		// only the first expectation is revealed in the spec name
		expect(array).toEqual([1, 2, 3, 4]);
		expect(newLength).toEqual(4);
	});
});
```

### GOOD

```js
describe("Array.push", function() {
	it("adds elements to the end of an array and returns the new length of the array", function() {
		var array = [1, 2];

		var newLength = array.push(3, 4);

		// both expectations are revealed in the spec name
		expect(array).toEqual([1, 2, 3, 4]);
		expect(newLength).toEqual(4);
	});
});
```

### WHY?

Incomplete spec names are misleading, especially if they are seemingly detailed and descriptive. They trick you to think that you understand system behavior while in reality important parts of this behavior remain hidden in the spec body.

Also, revealing everything a spec does in its name is a great design tool, as it helps uncover a common spec smell: describing too many concerns in a single spec (see also "Describe a single concern per spec" rule).
