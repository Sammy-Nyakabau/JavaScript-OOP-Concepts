# JavaScript-OOP-Concepts :page_with_curl:
Code Snippets which detail the Object Oriented Programming principles in JavaScript. The code was adapted from [Mosh Hamedani](https://codewithmosh.com/)

## Table of Contents :bookmark_tabs:
1. [Introduction](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#introduction)
2. [Objects](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#objects)
2. [Prototypes](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#prototypes)
3. [Prototypical Inheritance](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#prototypical-inheritance)
4. ES6 Classes 
5. Modules
---
### Introduction

The following paragraphs explaining OOP were adapted from [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS) :thought_balloon:

>To start with, let's give you a simplistic, high-level view of what Object-oriented programming (OOP) is. We say simplistic, because OOP can quickly get very complicated, and giving it a full treatment now would probably confuse more than help. The basic idea of OOP is that we use objects to model real world things that we want to represent inside our programs, and/or provide a simple way to access functionality that would otherwise be hard or impossible to make use of.

>Objects can contain related data and code, which represent information about the thing you are trying to model, and functionality or behavior that you want it to have. Object data (and often, functions too) can be stored neatly (the official word is encapsulated) inside an object package (which can be given a specific name to refer to, which is sometimes called a namespace), making it easy to structure and access; objects are also commonly used as data stores that can be easily sent across the network.

---
### Objects

#### Creating Objects
- The simplest way to create an object is using an [object literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer). Here, **circle** is the name of the object while *radius* and *draw* are properties of the object. 

##### :pushpin: Example
``` JavaScript
const circle = { 
   radius: 1, 
   draw: function() {}
}; 
```

- To create multiple objects with the same structure and behavior (methods), use a factory function or a [constructor function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/Function).

##### :pushpin: Example | *Factory Function*
``` JavaScript
function createCircle(radius) { 
   return {
      radius, 
      draw: function() {}
   } 
}

//Creating an object from a factory function
const c1 = createCircle(1);
```

##### :pushpin: Example | *Constructor Function*
``` JavaScript
//Name of function starts with an uppercase unlike all other functions
function Circle(radius) { 
    this.radius = radius; 
    this.draw = function() {}
}

//Creating an object from a constructor function
const c2 = new Circle(1)
```

#### More on Objects

- Every object has a ["constructor" ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor) property which returns the function that was used to construct or create that object.

##### :pushpin: Example | *Object Constructor*
``` JavaScript
const x = {};
x.constructor; // returns Object()
}
```

- In JavaScript, [functions are objects](https://www.dofactory.com/javascript/function-objects). They have properties and methods. 

##### :pushpin: Example | *Functions as objects*

``` JavaScript
Circle.name; 
Circle.length;
Circle.constructor; // returns Function()
Circle.call({}, 1); // to call the Circle function 
Circle.apply({}, [1]);
typeof Circle //returns object
```

- JavaScript objects are dynamic. You can add/remove properties: 

##### :pushpin: Example | *Add/Removing Properties*

``` JavaScript
circle.location = {};
circle['location'] = {};
                      
delete circle.location; 
```
- To enumerate the members in an object: 

##### :pushpin: Example | *Enumerating Properties*

``` JavaScript
for (let key in circle) console.log(key, circle[key]);

Object.keys(circle); // returns an array of a given object's own enumerable property names, iterated in the same order that a normal loop would.
```
- Abstraction means hiding the complexity/details and showing only the essentials. 
- We can hide the details by using private members. Replace "**this**" with "**let**". 

##### :pushpin: Example | *Abstraction*

``` JavaScript
function Circle(radius) { 
   // Public member 
   this.radius = radius; 

   // Private member                       
   let defaultLocation = {};                      
}  
```

- To define a getter/setter, use [Object.defineProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty):

##### :pushpin: Example | *Defining Properties*

``` JavaScript
Object.defineProperty(this, 'defaultLocation', {
    get: function() { return defaultLocation; },
    set: function(value) { defaultLocation = value; }
});
```
---

### Prototypes
>Prototypes are the mechanism by which JavaScript objects inherit features from one another. 

- Every object (except the root object) has a [prototype](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes) (parent). 
- To get the prototype of an object:

##### :pushpin: Example | *Getting Object Prototype*

``` JavaScript
Object.getPrototypeOf(obj); 
```

- In Chrome, you can inspect "`__proto__`" property. But you should not use that in the code.
- To get the attributes of a property:

##### :pushpin: Example | *Getting Attributes of a Property*

``` JavaScript
Object.getOwnPropertyDescriptor(obj, 'propertyName'); 
```

- To set the attributes for a property:

##### :pushpin: Example | *Setting Attributes of a Property*

``` JavaScript
Object.defineProperty(obj, 'propertyName', {
    configurable: false,    // cannot be deleted
    writable: false,
    enumerable: false
}); 
```

- Constructors have a ["prototype" property](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor). It returns the object that will be used as the prototype for objects created by the constructor.

##### :pushpin: Example | *Constructor Prototype*

``` JavaScript
Object.prototype === Object.getPrototypeOf({})
Array.prototype === Object.getPrototypeOf([]) 
```

- All objects created with the same constructor will have the same prototype. 
- A single instance of this prototype will be stored in the memory.

##### :pushpin: Example | *Constructor Prototype*

``` JavaScript
const x = {};
const y = {};
Object.getPrototypeOf(x) === Object.getPrototypeOf(y); // returns true 
```

- Any changes to the prototype will be immediately visible to all objects referencing this prototype. 

- When dealing with large number of objects, it's better to put their methods on their prototype. This way, a single instance of the methods will be in the memory. 

##### :pushpin: Example | *Putting Methods into Prototypes*

``` JavaScript
Circle.prototype.draw = function() {} 
```

### Prototypical Inheritance
>When it comes to inheritance, JavaScript only has one construct: objects. Each object has a private property which holds a link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. By definition, null has no prototype, and acts as the final link in this prototype chain.

>Nearly all objects in JavaScript are instances of Object which sits on the top of a prototype chain.

>While this confusion is often considered to be one of JavaScript's weaknesses, the prototypal inheritance model itself is, in fact, more powerful than the classic model. It is, for example, fairly trivial to build a classic model on top of a prototypal model.

##### :pushpin: Example | *Prototypical Inheritance*

``` JavaScript
function Shape() {}
function Circle() {}

// Prototypical inheritance 
Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.constructor = Circle;
```

- Calling the constructor of the base (super) object

##### :pushpin: Example | *Prototypical Inheritance*

``` JavaScript
function Rectangle(color) {
    // To call the super constructor 
    Shape.call(this, color); //Rectangle inherits from Shape
}
```

- To implement [method overriding](https://en.wikipedia.org/wiki/Method_overriding) in prototypical inheritance, the method in the base object is 1st called and then more logic is added depending on the object

##### :pushpin: Example | *Method Overriding*

``` JavaScript
Shape.prototype.draw = function() {}
Circle.prototype.draw = function() {
    // Call the base implementation 
    Shape.prototype.draw.call(this);

    // Do additional stuff here 
}
```

>Don't create large inheritance. One level of inheritance is fine.

#### Mixins
Use [mixins](https://javascript.info/mixins) to combine multiple objects and implement [composition](https://en.wikipedia.org/wiki/Composition_over_inheritance) in JavaScript. 

##### :pushpin: Example | *Mixins*

``` JavaScript
const canEat = { 
    eat: function() {}
};

const canWalk = {
    walk: function() {}
};

function mixin(target, ...sources) {
    // Copies all the properties from all the source objects 
    // to the target object. 
    Object.assign(target, ...sources);
}

function Person() {}

mixin(Person.prototype, canEat, canWalk);
```
---

### ES6 Classes

>JavaScript classes, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript's existing prototype-based inheritance. The class syntax does not introduce a new object-oriented inheritance model to JavaScript.

##### :pushpin: Example | *Implementing ES6 classes*

``` JavaScript
class Circle {
    constructor(radius) {
        this.radius = radius; 
    }

    // These methods will be added to the prototype. 
    draw() {
    }

    // This will be available on the Circle class (Circle.parse())
    static parse(str) {
    }
}
```