<h1>Chapter 2: Lexical Scope</h1>

*Lexical scope is a scope that is definied at lexing time (place where var and blocks of scope are authored)

*Look up starts from the inermost scope bubble, if the var isn't found it goes up one level

*The look up stops as soon as it finds the first match, meaning if there is a var in the inner and the outer scope the look up will stop as soon as the var in the inner scope is found.

*No matter where a function is invoked from, or even how it is invoked, its lexical scope is only defined by where the function was declared.

*The lexical scope look-up process only applies to first-class identifiers, such as the a, b, and c. If you had a reference to foo.bar.baz in a piece of code, the lexical scope look-up would apply to finding the foo identifier, but once it locates that variable, _**object property-access rules**_ take over to resolve the bar and baz properties, respectively.

_eval_

*The eval(..) function in JavaScript takes a string as an argument, and treats the contents of the string as if it had actually been authored code at that point in the program. In other words, you can programmatically generate code inside of your authored code, and run the generated code as if it had been there at author time.

_with_
*with is typically explained as a short-hand for making multiple property references against an object without repeating the object reference itself each time.

_The downside to these mechanisms is that it defeats the Engine's ability to perform compile-time optimizations regarding scope look-up, because the Engine has to assume pessimistically that such optimizations will be invalid. Code will run slower as a result of using either feature. Don't use them_
