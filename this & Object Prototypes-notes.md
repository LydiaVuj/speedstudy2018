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



 
 
 
 
 
 
 
 
 


