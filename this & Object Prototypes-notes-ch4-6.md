# Chapter 4: Mixing (Up) "Class" Objects

##Class Theory

 * OO or class oriented programming stresses that data intrinsically has associated behavior (of course, different depending on the type and nature of the data!) that operates on it, so proper design is to package up (aka, encapsulate) the data and the behavior together. This is sometimes called "data structures" in formal computer science

 * For example, a series of characters that represents a word or phrase is usually called a "string". The characters are the data. But you almost never just care about the data, you usually want to do things with the data, so the behaviors that can apply to that data (calculating its length, appending data, searching, etc.) are all designed as methods of a String class.

 * A car can be described as a specific implementation of a more general "class" of thing, called a vehicle.

 * We model this relationship in software with classes by defining a Vehicle class and a Car class.

 * It might not make sense in our software to re-define the basic essence of "ability to carry people" over and over again for each different type of vehicle. Instead, we define that capability once in Vehicle, and then when we define Car, we simply indicate that it "inherits" (or "extends") the base definition from Vehicle. The definition of Car is said to specialize the general Vehicle definition.

 * "polymorphism", which describes the idea that a general behavior from a parent class can be overridden in a child class to give it more specifics. In fact, relative polymorphism lets us reference the base behavior from the overridden behavior.

###  JavaScript "Classes"

 * But does that mean JavaScript actually has classes? Plain and simple: No. * 

 * While we may have a syntax that looks like classes, it's as if JavaScript mechanics are fighting against you using the class design pattern, because behind the curtain, the mechanisms that you build on are operating quite differently. Syntactic sugar and (extremely widely used) JS "Class" libraries go a long way toward hiding this reality from you, but sooner or later you will face the fact that the classes you have in other languages are not like the "classes" you're faking in JS.

## Class Mechanics

#Building

 * The architectural blue-prints she produces are only plans for a building. They don't actually constitute a building we can walk into and sit down. We need a builder for that task. A builder will take those plans and follow them, exactly, as he builds the building. In a very real sense, he is copying the intended characteristics from the plans to the physical building.

 * The relationship between building and blue-print is indirect. You can examine a blue-print to understand how the building was structured, for any parts where direct inspection of the building itself was insufficient. But if you want to open a door, you have to go to the building itself -- the blue-print merely has lines drawn on a page that represent where the door should be.

 * A class is a blue-print. To actually get an object we can interact with, we must build (aka, "instantiate") something from the class. The end result of such "construction" is an object, typically called an "instance", which we can directly call methods on and access any public data properties from, as necessary.

 * This object is a copy of all the characteristics described by the class.

 * A class is instantiated into object form by a copy operation.

#Constructor

 * Instances of classes are constructed by a special method of the class, usually of the same name as the class, called a constructor. This method's explicit job is to initialize any information (state) the instance will need.

 * constructors pretty much always need to be called with `new` to let the language engine know you want to construct a new class instance.


# Class Inheritance

 * In class-oriented languages, not only can you define a class which can be instantiated itself, but you can define another class that inherits from the first class

 * once a child class is defined, it's separate and distinct from the parent class. The child class contains an initial copy of the behavior from the parent, but can then override any inherited behavior and even define new behavior.

# Polymorphism

 * `Car` defines its own `drive()` method, which overrides the method of the same name it inherited from `Vehicle`. But then, Cars `drive()` method calls `inherited:drive()`, which indicates that `Car` can reference the original pre-overridden drive() it inherited. SpeedBoats `pilot()` method also makes a reference to its inherited copy of `drive()`.

 * the idea that any method can reference another method (of the same or different name) at a higher level of the inheritance hierarchy. We say "relative" because we don't absolutely define which inheritance level (aka, class) we want to access, but rather relatively reference it by essentially saying "look one level up".

 * Another aspect of polymorphism is that a method name can have multiple definitions at different levels of the inheritance chain, and these definitions are automatically selected as appropriate when resolving which methods are being called.

 * When classes are inherited, there is a way for the classes themselves (not the object instances created from them!) to relatively reference the class inherited from, and this relative reference is usually called `super`.

 * the child class is merely given a copy of the inherited behavior from its parent class. If the child "overrides" a method it inherits, both the original and overridden versions of the method are actually maintained, so that they are both accessible.

 * Don't let polymorphism confuse you into thinking a child class is linked to its parent class. A child class instead gets a copy of what it needs from the parent class. Class inheritance implies copies.

# Multiple Inheritance

 * JavaScript is simpler: it does not provide a native mechanism for "multiple inheritance". Many see this is a good thing, because the complexity savings more than make up for the "reduced" functionality. But this doesn't stop developers from trying to fake it in various ways, as we'll see next.

## Mixins

 * Since observed class behaviors in other languages imply copies, let's examine how JS developers fake the missing copy behavior of classes in JavaScript: mixins. We'll look at two types of "mixin": explicit and implicit.

## Explicit Mixins
"Polymorphism" Revisited

  * because both `Car` and `Vehicle` had a function of the same name: `drive()`, to distinguish a call to one or the other, we must make an absolute (not relative) reference. We explicitly specify the Vehicle object by name, and call the `drive()` function on it.
 
 * But if we said `Vehicle.drive()`, the this binding for that function call would be the `Vehicle `object instead of the `Car` object (see Chapter 2), which is not what we want. So, instead we use `.call( this )` (Chapter 2) to ensure that drive() is executed in the context of the `Car `object.












