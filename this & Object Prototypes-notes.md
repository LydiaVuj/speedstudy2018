## Chapter 1: this Or That?

* the this mechanism provides a more elegant way of implicitly "passing along" an object reference, leading to cleaner API design and easier re-use.

* Ways _this_doesnt work:
1. Itself- assume this refers to the function itself.
2. That it refers to the functions scope - this does not, in any way, refer to a function's *lexical scope*

 * Right way to use this:
```js
function foo(num) {
	console.log( "foo: " + num );

	// keep track of how many times `foo` is called
	// Note: `this` IS actually `foo` now, based on
	// how `foo` is called (see below)
	this.count++;
}

foo.count = 0;

var i;

for (i=0; i<10; i++) {
	if (i > 5) {
		// using `call(..)`, we ensure the `this`
		// points at the function object (`foo`) itself
		foo.call( foo, i );
	}
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

// how many times was `foo` called?
console.log( foo.count ); // 4
```

* What's _this_?
  - this binding has nothing to do with where a function is declared, but has instead everything to do with the manner in which the function is called.
  - When a function is invoked, an activation record, otherwise known as an execution context, is created. This record contains information about where the function was called from (the call-stack), how the function was invoked, what parameters were passed, etc. One of the properties of this record is the this reference which will be used for the duration of that function's execution.
  
 ## Chapter 2: this All Makes Sense Now!
 
 * this is a binding made for each function invocation, based entirely on its call-site (how the function is called).
 
 * call-site: the location in code where a function is called (not where it's declared) in order to understand to what does _this_ reference.
 
 * it is important to think about the call-stack (the stack of functions that have been called to get us to the current moment in execution). *The call-site we care about is in the invocation before the currently executing function.*
 
 ```js
 function baz() {
    // call-stack is: `baz`
    // so, our call-site is in the global scope

    console.log( "baz" );
    bar(); // <-- call-site for `bar`
}

function bar() {
    // call-stack is: `baz` -> `bar`
    // so, our call-site is in `baz`

    console.log( "bar" );
    foo(); // <-- call-site for `foo`
}

function foo() {
    // call-stack is: `baz` -> `bar` -> `foo`
    // so, our call-site is in `bar`

    console.log( "foo" );
}

baz(); // <-- call-site for `baz`
```

_Note_ If you're trying to diagnose this binding, use the developer tools to get the call-stack, then find the second item from the top, and that will show you the real call-site.
 
 ### How the call-site determines where this will point during the execution of a function
 
 **4 rules**
 
 #### Default Binding -standalone function invocation
 *default catch-all rule when none of the other rules apply*
 ```js
 function foo() {
	console.log( this.a );
}

var a = 2;

foo(); // 2
```
* In order to know that the default binding is rule applies here we need to examine the call-site of the function `foo()`.
* If strict mode is in effect, the global object is not eligible for the default binding, so the this is instead set to undefined.


 #### Implicit Binding
 * Another rule to consider is: does the call-site have a context object, also referred to as an owning or containing object, though these alternate terms could be slightly misleading
 
 ```js
 function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

obj.foo(); // 2
```
* At the point that foo() is called, it's preceded by an object reference to obj. When there is a context object for a function reference, the implicit binding rule says that it's that object which should be used for the function call's this binding.

* Because obj is the this for the foo() call, this.a is synonymous with obj.a.

### Implicit Lost

* One of the most common frustrations that this binding creates is when an implicitly bound function loses that binding, which usually means it falls back to the default binding, of either the global object or undefined, depending on strict mode

* It's quite common that our function callbacks lose their this binding, as we've just seen. But another way that this can surprise us is when the function we've passed our callback to intentionally changes the this for the call. Event handlers in popular JavaScript libraries are quite fond of forcing your callback to have a this which points to, for instance, the DOM element that triggered the event. While that may sometimes be useful, other times it can be downright infuriating. Unfortunately, these tools rarely let you choose.

### Explicit Binding
* How do these utilities work? They both take, as their first parameter, an object to use for the this, and then invoke the function with that this specified. Since you are directly stating what you want the this to be, we call it explicit binding.

Consider:

```function foo() {
	console.log( this.a );
}

var obj = {
	a: 2
};

foo.call( obj ); // 2
```
* Invoking foo with explicit binding by foo.call(..) allows us to force its this to be obj.

#### Hard Biding
```
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2
};

var bar = function() {
	foo.call( obj );
};

bar(); // 2
setTimeout( bar, 100 ); // 2

// `bar` hard binds `foo`'s `this` to `obj`
// so that it cannot be overriden
bar.call( window ); // 2
```
* Let's examine how this variation works. We create a function bar() which, internally, manually calls foo.call(obj), thereby forcibly invoking foo with obj binding for this. No matter how you later invoke the function bar, it will always manually invoke foo with obj. This binding is both explicit and strong, so we call it **hard binding.**

* Since hard binding is such a common pattern, it's provided with a built-in utility as of ES5: ```Function.prototype.bind```, and it's used like this:
```
function foo(something) {
	console.log( this.a, something );
	return this.a + something;
}

var obj = {
	a: 2
};

var bar = foo.bind( obj );

var b = bar( 3 ); // 2 3
console.log( b ); // 5
```
 
 #### API Call "Contexts"
 
 ### ```new``` Binding
 
 * When a function is invoked with new in front of it, otherwise known as a constructor call, the following things are done automatically:

1.a brand new object is created (aka, constructed) out of thin air
2.the newly constructed object is [[Prototype]]-linked
3.the newly constructed object is set as the this binding for that function call
4.unless the function returns its own alternate object, the new-invoked function call will automatically return the newly constructed object.

### Determining this

* Now, we can summarize the rules for determining this from a function call's call-site, in their order of precedence. Ask these questions in this order, and stop when the first rule applies.

1.Is the function called with new (new binding)? If so, this is the newly constructed object.

var bar = new foo()

2.Is the function called with call or apply (explicit binding), even hidden inside a bind hard binding? If so, this is the explicitly specified object.

var bar = foo.call( obj2 )

3.Is the function called with a context (implicit binding), otherwise known as an owning or containing object? If so, this is that context object.

var bar = obj1.foo()

4.Otherwise, default the this (default binding). If in strict mode, pick undefined, otherwise pick the global object.

### Binding Exceptions

* ***Ignored this***
  If you pass ```null``` or ```undefined``` as a ```this``` binding parameter to ```call, apply, or bind```, those values are effectively ignored, and instead the default binding rule applies to the invocation

* Perhaps a somewhat "safer" practice is to pass a specifically set up object for this which is guaranteed not to be an object that can create problematic side effects in your program. the easiest way to set it up as totally empty is Object.create(null).

* ***Indirection*** 

* Another thing to be aware of is you can (intentionally or not!) create "indirect references" to functions, and in those cases, when that function reference is invoked, the default binding rule also applies.

### Softening Binding

* providing a different default for default binding (not global or undefined), while still leaving the function able to be manually ```this``` bound via implicit binding or explicit binding techniques.
```
if (!Function.prototype.softBind) {
	Function.prototype.softBind = function(obj) {
		var fn = this,
			curried = [].slice.call( arguments, 1 ),
			bound = function bound() {
				return fn.apply(
					(!this ||
						(typeof window !== "undefined" &&
							this === window) ||
						(typeof global !== "undefined" &&
							this === global)
					) ? obj : this,
					curried.concat.apply( curried, arguments )
				);
			};
		bound.prototype = Object.create( fn.prototype );
		return bound;
	};
}
```
### Lexical this

* Arrow-functions are signified not by the function keyword, but by the => so called "fat arrow" operator. Instead of using the four standard this rules, arrow-functions adopt the this binding from the enclosing (function or global) scope.

```
function foo() {
	// return an arrow function
	return (a) => {
		// `this` here is lexically adopted from `foo()`
		console.log( this.a );
	};
}

var obj1 = {
	a: 2
};

var obj2 = {
	a: 3
};

var bar = foo.call( obj1 );
bar.call( obj2 ); // 2, not 3!
```
* The arrow-function created in foo() lexically captures whatever foo()s this is at its call-time. Since foo() was this-bound to obj1, bar (a reference to the returned arrow-function) will also be this-bound to obj1. The lexical binding of an arrow-function cannot be overridden (even with new!).

## Chapter 3: Objects

### Syntax

The literal syntax for an object looks like this:
```
var myObj = {
	key: value
	// ...
};
```
The constructed form looks like this:
```
var myObj = new Object();
myObj.key = value;
```
## Type

* Function is a sub-type of object (technically, a "callable object"). Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

* Arrays are also a form of objects, with extra behavior. The organization of contents in arrays is slightly more structured than for general objects.

## Built-in Objects

* `string`
* `number`
* `boolean`
* `null`
* `undefined`
* `object`

* These are actually just built-in functions. Each of these built-in functions can be used as a constructor (that is, a function call with the new operator -- see Chapter 2), with the result being a newly constructed object of the sub-type in question. 
```
var strPrimitive = "I am a string";

console.log( strPrimitive.length );			// 13

console.log( strPrimitive.charAt( 3 ) );	// "m"
```
* In both cases, we call a property or method on a string primitive, and the engine automatically coerces it to a String object, so that the property/method access works.

The same sort of coercion happens between the number literal primitive 42 and the new Number(42) object wrapper, when using methods like 42.359.toFixed(2). Likewise for Boolean objects from "boolean" primitives.

* ```null``` and `undefined` have no object wrapper form, only their primitive values. By contrast, Date values can only be created with their constructed object form, as they have no literal form counter-part.

* `Objects, Arrays, Functions, and RegExps` (regular expressions) are all objects regardless of whether the literal or constructed form is used. The constructed form does offer, in some cases, more options in creation than the literal form counterpart. Since objects are created either way, the simpler literal form is almost universally preferred. Only use the constructed form if you need the extra options.

* `Error` objects are rarely created explicitly in code, but usually created automatically when exceptions are thrown. They can be created with the constructed form new Error(..), but it's often unnecessary.

### Contents

* As mentioned earlier, the contents of an object consist of values (any type) stored at specifically named locations, which we call properties.

* In objects, property names are always strings. If you use any other value besides a string (primitive) as the property, it will first be converted to a string. This even includes numbers, which are commonly used as array indexes, so be careful not to confuse the use of numbers between objects and arrays.

### Computed Property Names
* ES6 adds computed property names, where you can specify an expression, surrounded by a [ ] pair, in the key-name position of an object-literal declaration:

```
var prefix = "foo";

var myObject = {
	[prefix + "bar"]: "hello",
	[prefix + "baz"]: "world"
};

myObject["foobar"]; // hello
myObject["foobaz"]; // world
```

### Property vs. Method

* Every time you access a property on an object, that is a property access, regardless of the type of value you get back. If you happen to get a function from that property access, it's not magically a "method" at that point. There's nothing special (outside of possible implicit `this` binding as explained earlier) about a function that comes from a property access.

* Because it's tempting to think of the function as belonging to the object, and in other languages, functions which belong to objects (aka, "classes") are referred to as "methods", it's not uncommon to hear, "method access" as opposed to "property access".

### Arrays

* Arrays are objects, so even though each index is a positive integer, you can also add properties onto the array

* adding named properties (regardless of . or [ ] operator syntax) does not change the reported length of the array.

### Duplicating Objects

* objects which are JSON-safe (that is, can be serialized to a JSON string and then re-parsed to an object with the same structure and values) can easily be duplicated with:

'var newObj = JSON.parse( JSON.stringify( someObj ) );'

* ES6 has now defined 'Object.assign(..)' for this task. 'Object.assign(..)' takes a target object as its first parameter, and one or more source objects as its subsequent parameters. It iterates over all the enumerable , owned keys (immediately present) on the source object(s) and copies them (via = assignment only) to target. It also, helpfully, returns target.

`
var newObj = Object.assign( {}, myObject );

newObj.a;						// 2
newObj.b === anotherObject;		// true
newObj.c === anotherArray;		// true
newObj.d === anotherFunction;	// true
`

### Property Descriptors

* property descriptor can hold other characteristics except `value`, such as `writable`, `enumerable` and `configurable`.
* we can use `Object.defineProperty(..)` to dreate a new (or modify an existing) property.
* `writable` - alows you to change the value of the property
* `configurable` allows us to modify the descriptor definition. Changing `configurable`  to false is **one way action**.
* `configurable:false` prevents is the ability to use the delete operator to remove an existing property.
* `enumerable` controls if a property will show up in a certain 	object property enumerations such as `for..in` loop. 

### Immutability

* making properties and objects that can not be changed. The following approached create only _shallow_ immutability, meaning that they only affect directly the object/property and not the connected objects/properties.

***Object Constant***
* By combining `writable:false` and `configurable:false`, you can essentially create a constant (cannot be changed, redefined or deleted) as an object property.

***Prevent Extensions***
* If you want to prevent an object from having new properties added to it, but otherwise leave the rest of the object's properties alone, call `Object.preventExtensions(..)`

***Seal***
* `Object.seal(..)` creates a "sealed" object, which means it takes an existing object and essentially calls `Object.preventExtensions(..)` on it, but also marks all its existing properties as configurable:false.

***Freeze*** - highest level of immutability
* `Object.freeze(..)` creates a frozen object, which means it takes an existing object and essentially calls `Object.seal(..)` on it, but it also marks all "data accessor" properties as `writable:false`, so that their values cannot be changed.

### [[Get]]

* According to the spec, the code above actually performs a `[[Get]]` operation (kinda like a function call: [[Get]]()) on the `myObject`.But one important result of this [[Get]] operation is that if it cannot through any means come up with a value for the requested property, it instead returns the value `undefined`.

### [[Put]]

* When invoking [[Put]], how it behaves differs based on a number of factors, including (most impactfully) whether the property is already present on the object or not.

 If the property is present, the `[[Put]]` algorithm will roughly check:

1. Is the property an accessor descriptor (see "Getters & Setters" section below)? If so, call the setter, if any.
2. Is the property a data descriptor with `writable` of `false`? If so, silently fail in `non-strict mode`, or throw `TypeError` in strict mode.
3. Otherwise, set the value to the existing property as normal.

### Getters & Setters

* [[Put]] and [[Get]] operations for objects completely control how values are set to existing or new properties, or retrieved from existing properties.

* in ES5 there is a new way to override this operations at a per-property level, through the use of ***getters and setters***.

* ***Getters*** are properties which actually call a hidden function to _retrieve_ a value. 
* ***Setters*** are properties which actually call a hidden function to _set_ a value.

* ***accessor descriptor*** - defining a property to have either a getter or a setter or both. The `value` and `writable` characteristics of the descriptor are moot and ignored, and instead JS considers the `set and get` characteristics of the property (as well as configurable and enumerable).

`
var myObject = {
	// define a getter for `a`
	get a() {
		return 2;
	}
};

Object.defineProperty(
	myObject,	// target
	"b",		// property name
	{			// descriptor
		// define a getter for `b`
		get: function(){ return this.a * 2 },

		// make sure `b` shows up as an object property
		enumerable: true
	}
);

myObject.a; // 2

myObject.b; // 4
`
* properties should also be defined with setters, which override the default [[Put]] operation (aka, assignment), per-property.

`var myObject = {
	// define a getter for `a`
	get a() {
		return this._a_;
	},

	// define a setter for `a`
	set a(val) {
		this._a_ = val * 2;
	}
};

myObject.a = 2;

myObject.a; // 4
`
### Existence

`
var myObject = {
	a: 2
};

("a" in myObject);				// true
("b" in myObject);				// false

myObject.hasOwnProperty( "a" );	// true
myObject.hasOwnProperty( "b" );	// false
`
* The `in` operator will check to see if the property is in the object, or if it exists at any higher level of the [[Prototype]] chain object traversal 

 * `hasOwnProperty(..)` checks to see if _only_ myObject has the property or not, and will not consult the [[Prototype]] chain




























 
 
 
 
 
 
 


