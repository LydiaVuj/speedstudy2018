## Chapter 2: Lexical Scope

* Lexical scope is a scope that is definied at lexing time (place where var and blocks of scope are authored)

* Look up starts from the inermost scope bubble, if the var isn't found it goes up one level

* The look up stops as soon as it finds the first match, meaning if there is a var in the inner and the outer scope the look up will       stop as soon as the var in the inner scope is found.

* No matter where a function is invoked from, or even how it is invoked, its lexical scope is only defined by where the function was
  declared.

* The lexical scope look-up process only applies to first-class identifiers, such as the a, b, and c. If you had a reference to
  foo.bar.baz in a piece of code, the lexical scope look-up would apply to finding the foo identifier, but once it locates that
  variable, _**object property-access rules**_ take over to resolve the bar and baz properties, respectively.

*eval*

* The eval(..) function in JavaScript takes a string as an argument, and treats the contents of the string as if it had actually been authored code at that point in the program. In other words, you can programmatically generate code inside of your authored code, and run the generated code as if it had been there at author time.

*with*

* With is typically explained as a short-hand for making multiple property references against an object without repeating the object reference itself each time.

_The downside to these mechanisms is that it defeats the Engine's ability to perform compile-time optimizations regarding scope look-up, because the Engine has to assume pessimistically that such optimizations will be invalid. Code will run slower as a result of using either feature. Don't use them_


## Chapter 3: Function vs. Block Scope

* Function scope- all the variables belong to the function and can be used and reused  in its scope and nested scopes 

* Hiding var and functions- in the design of software, such as the API for a module/object, you should expose only what is minimally necessary, and "hide" everything else. By hiding var and functions not only is the code design better but it can also avoid unintended collision between two different identifiers with the same name but different intended usages.

* A particularly strong example of (likely) variable collision occurs in the global scope. Multiple libraries loaded into your program can quite easily collide with each other if they don't properly hide their internal/private functions and variables.

* Functions as scopes- If "function" is the very first thing in the statement, then it's a function declaration. Otherwise, it's a function expression.The difference is where its name is bound as an identifier.

* Function expressions can be anonymous, but function declarations cannot omit the name. Providing a name for your function expression quite effectively addresses all these draw-backs, but has no tangible downsides. The best practice is to always name your function expressions.

* IIFE- Immediately Invoked Function Expression.


```javascript
    var a = 2;

  (function IIFE(){

	var a = 3;
	console.log( a ); // 3

  })();

  console.log( a ); // 2
```

* Block Scope-declaring variables as close as possible, as local as possible, to where they will be used.it a tool to extend the "Principle of the Last Exposure". 

* let - another way to declare varaiables. The let keyword attaches the variable declaration to the scope of whatever block (commonly a { .. } pair) it's contained in. In other words, let implicitly hijacks any block's scope for its variable declaration. 
  
* Declarations made with let will not hoist to the entire scope of the block they appear in. Such declarations will not observably "exist" in the block until the declaration statement.

* const- which also creates a block-scoped variable, but whose value is fixed (constant). 

## Chapter 4 : Hoisting

* JS compilation- Part of the compilation phase was to find and associate all declarations with their appropriate scopes.

* During the compilation the declaration (var a) is processed. The the assignment (a = 2) is left for the execution phase. In other words, functions and variables are moved to the top of the code - _Hoisting_

* Hoisting is processed per-scope meaninf the declarations are hoisted at the top of the _scope_ not program. Also only function declarations are  hoisted **not** function expressions.

* Between functions and variables, functions are hoisted first.

## Chapter 5: Scope Closures

* Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

*  Closure lets the function continue to access the lexical scope it was defined in at author-time.

```javascript
function foo() {
	var a = 2;

	function bar() {
		console.log( a );
	}

	return bar;
}

var baz = foo();

baz(); // 2 
```
* closure in loops:
```js
for (var i=1; i<=5; i++) {
	setTimeout( function timer(){
		console.log( i );
	}, i*1000 );
}
```

* Block Scoping 
```js
for (var i=1; i<=5; i++) {
	let j = i; // yay, block-scope for closure!
	setTimeout( function timer(){
		console.log( j );
	}, j*1000 );
}
```

* Modules -invoking a function that returns a object that has references on it to our inner functions, but not to our inner data variables. The object return is assesed to the outer variable (function) therefore lets us access the property methods - foo.something

* There are two "requirements" for the module pattern to be exercised:

1.There must be an outer enclosing function, and it must be invoked at least once (each time creates a new module instance).

2. The enclosing function must return back at least one inner function, so that this inner function has closure over the private scope, and can access and/or modify that private state.

## Appendix A: Dynamic Scope

* Dynamic scope seems to imply, and for good reason, that there's a model whereby scope can be determined dynamically at runtime, rather than statically at author-time, Dynamic scope, by contrast, doesn't concern itself with how and where functions and scopes are declared, but rather where they are called from. In other words, the scope chain is based on the call-stack, not the nesting of scopes in code.

 * Lexical scope cares where a function was declared, but dynamic scope cares where a function was called from.
 
 ## Appendix B: Polyfilling Block Scope
 
 ```js
 try{throw 2}catch(a){
	console.log( a ); // 2
}

console.log( a ); // ReferenceError
```

## Appendix C: Lexical-this

* Arrow functions introduces a behavior called "lexical this".They discard all the normal rules for this binding, and instead take on the this value of their immediate lexical enclosing scope, whatever it is.

```js

var obj = {
	count: 0,
	cool: function coolFn() {
		if (this.count < 1) {
			setTimeout( () => { // arrow-function ftw?
				this.count++;
				console.log( "awesome?" );
			}, 100 );
		}
	}
};

obj.cool(); // awesome?
```









