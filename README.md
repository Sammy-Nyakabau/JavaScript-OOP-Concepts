![JavaScript](https://i.ibb.co/NTVx1jW/download.jpg)

# :computer:JavaScript-OOP-Concepts :page_with_curl:

Code Snippets which detail the Object Oriented Programming principles in JavaScript.

## Table of Contents :book:

1. [Introduction](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#introduction)
2. [Objects](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#objects)
3. [Prototypes](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#prototypes)
4. [Prototypical Inheritance](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#prototypical-inheritance)
5. [ES6 Classes](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#es6-classes)

---

### Introduction

The following paragraphs explaining OOP were adapted from [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS) :thought_balloon:

> To start with, let's give you a simplistic, high-level view of what Object-oriented programming (OOP) is. We say simplistic, because OOP can quickly get very complicated, and giving it a full treatment now would probably confuse more than help. The basic idea of OOP is that we use objects to model real world things that we want to represent inside our programs, and/or provide a simple way to access functionality that would otherwise be hard or impossible to make use of.

> Objects can contain related data and code, which represent information about the thing you are trying to model, and functionality or behavior that you want it to have. Object data (and often, functions too) can be stored neatly (the official word is encapsulated) inside an object package (which can be given a specific name to refer to, which is sometimes called a namespace), making it easy to structure and access; objects are also commonly used as data stores that can be easily sent across the network.

---

### Objects

#### Creating Objects

- The simplest way to create an object is using an [object literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer). Here, **circle** is the name of the object while _radius_ and _draw_ are properties of the object.

##### :pushpin: Example | _Object Literal_

```JavaScript
const circle = {
   radius: 1,
   draw: function() {}
};
```

- Objects can also be created using the [Object Constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/Object)

##### :pushpin: Example | _Object Constructor_

```JavaScript
const circle = new Object()

circle.radius = 1
circle.draw = () => {

}
```
- One can also create a object using properties of another object using the 
[object.create()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create) method.

##### :pushpin: Example | _object.create()_

```JavaScript
const circle = {
   radius: 1, //default values
   draw: function() {}
};

const circle1 = object.create(circle)
circle1.radius = 2
circle1.draw = () => {

}
```

- To create multiple objects with the same structure and behavior (methods), use a factory function or a [constructor function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/Function).

##### :pushpin: Example | _Factory Function_

```JavaScript
function createCircle(radius) {
   return {
      radius,
      draw: function() {}
   }
}

//Creating an object from a factory function
const c1 = createCircle(1);
```

##### :pushpin: Example | _Constructor Function_

```JavaScript
//Name of function starts with an uppercase unlike all other functions
function Circle(radius) {
    this.radius = radius;
    this.draw = function() {}
}

//Creating an object from a constructor function
const c2 = new Circle(1)
```

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**

#### More on Objects

- Every object has a ["constructor" ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor) property which returns the function that was used to construct or create that object.

##### :pushpin: Example | _Object Constructor_

```JavaScript
const x = {};
x.constructor; // returns Object()
}
```

- In JavaScript, [functions are objects](https://www.dofactory.com/javascript/function-objects). They have properties and methods.

##### :pushpin: Example | _Functions as objects_

```JavaScript
Circle.name;
Circle.length;
Circle.constructor; // returns Function()
Circle.call({}, 1); // to call the Circle function
Circle.apply({}, [1]);
typeof Circle //returns object
```

- JavaScript objects are dynamic. You can add/remove properties:

##### :pushpin: Example | _Add/Removing Properties_

```JavaScript
circle.location = {};
circle['location'] = {};

delete circle.location;
```

- To enumerate the members in an object:

##### :pushpin: Example | _Enumerating Properties_

```JavaScript
for (let key in circle) console.log(key, circle[key]);

Object.keys(circle); // returns an array of a given object's own enumerable property names, iterated in the same order that a normal loop would.
```

- Abstraction means hiding the complexity/details and showing only the essentials.
- We can hide the details by using private members. Replace "**this**" with "**let**".

##### :pushpin: Example | _Abstraction_

```JavaScript
function Circle(radius) {
   // Public member
   this.radius = radius;

   // Private member
   let defaultLocation = {};
}
```

- To define a getter/setter, use [Object.defineProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty):

##### :pushpin: Example | _Defining Properties_

```JavaScript
Object.defineProperty(this, 'defaultLocation', {
    get: function() { return defaultLocation; },
    set: function(value) { defaultLocation = value; }
});
```

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**

---

### Prototypes

> Prototypes are the mechanism by which JavaScript objects inherit features from one another.

- Every object (except the root object) has a [prototype](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes) (parent).
- To get the prototype of an object:

##### :pushpin: Example | _Getting Object Prototype_

```JavaScript
Object.getPrototypeOf(obj);
```

- In Chrome, you can inspect "`__proto__`" property. But you should not use that in the code.
- To get the attributes of a property:

##### :pushpin: Example | _Getting Attributes of a Property_

```JavaScript
Object.getOwnPropertyDescriptor(obj, 'propertyName');
```

- To set the attributes for a property:

##### :pushpin: Example | _Setting Attributes of a Property_

```JavaScript
Object.defineProperty(obj, 'propertyName', {
    configurable: false,    // cannot be deleted
    writable: false,
    enumerable: false
});
```

- Constructors have a ["prototype" property](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor). It returns the object that will be used as the prototype for objects created by the constructor.

##### :pushpin: Example | _Constructor Prototype_

```JavaScript
Object.prototype === Object.getPrototypeOf({})
Array.prototype === Object.getPrototypeOf([])
```

- All objects created with the same constructor will have the same prototype.
- A single instance of this prototype will be stored in the memory.

##### :pushpin: Example | _Constructor Prototype_

```JavaScript
const x = {};
const y = {};
Object.getPrototypeOf(x) === Object.getPrototypeOf(y); // returns true
```

- Any changes to the prototype will be immediately visible to all objects referencing this prototype.

- When dealing with large number of objects, it's better to put their methods on their prototype. This way, a single instance of the methods will be in the memory.

##### :pushpin: Example | _Putting Methods into Prototypes_

```JavaScript
Circle.prototype.draw = function() {}
```

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**

### Prototypical Inheritance

> When it comes to inheritance, JavaScript only has one construct: objects. Each object has a private property which holds a link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. By definition, null has no prototype, and acts as the final link in this prototype chain.

> Nearly all objects in JavaScript are instances of Object which sits on the top of a prototype chain.

> While this confusion is often considered to be one of JavaScript's weaknesses, the prototypal inheritance model itself is, in fact, more powerful than the classic model. It is, for example, fairly trivial to build a classic model on top of a prototypal model.

##### :pushpin: Example | _Prototypical Inheritance_

```JavaScript
function Shape() {}
function Circle() {}

// Prototypical inheritance
Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.constructor = Circle;
```

- Calling the constructor of the base (super) object

##### :pushpin: Example | _Prototypical Inheritance_

```JavaScript
function Rectangle(color) {
    // To call the super constructor
    Shape.call(this, color); //Rectangle inherits from Shape
}
```

- To implement [method overriding](https://en.wikipedia.org/wiki/Method_overriding) in prototypical inheritance, the method in the base object is 1st called and then more logic is added depending on the object

##### :pushpin: Example | _Method Overriding_

```JavaScript
Shape.prototype.draw = function() {}
Circle.prototype.draw = function() {
    // Call the base implementation
    Shape.prototype.draw.call(this);

    // Do additional stuff here
}
```

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**

> Don't create large inheritance. One level of inheritance is fine.

#### Mixins

Use [mixins](https://javascript.info/mixins) to combine multiple objects and implement [composition](https://en.wikipedia.org/wiki/Composition_over_inheritance) in JavaScript.

##### :pushpin: Example | _Mixins_

```JavaScript
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

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**

---

### ES6 Classes

> JavaScript classes, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript's existing prototype-based inheritance. The class syntax does not introduce a new object-oriented inheritance model to JavaScript.

##### :pushpin: Example | _Implementing ES6 classes_

```JavaScript
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

#### Encapsulation

> Encapsulation is the packing of data and functions into one component (for example, a class) and then controlling access to that component to make a "blackbox" out of the object. Because of this, a user of that class only needs to know its interface (that is, the data and functions exposed outside the class), not the hidden implementation.

##### :pushpin: Example | _Implementing Encapsulation Method 1_

```JavaScript
// Using symbols to implement private properties and methods
const _size = Symbol();
const _draw = Symbol();

class Square {
    constructor(size) {
        // "Kind of" private property
        this[_size] = size;
    }

    // "Kind of" private method
    [_draw]() {
    }

}
```

- By "kind of" I mean: these properties and methods are essentally part of the object and are accessible from the outside. But accessing them is hard and awkward.

##### :pushpin: Example | _Implementing Encapsulation Method 2_

```JavaScript
// using WeakMaps to implement private properties and methods
const _width = new WeakMap();

class Rectangle {
    constructor(width) {
        _width.set(this, width);
    }

    draw() {
        console.log('Rectangle with width' + _width.get(this));
    }
}
```

- [WeakMaps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap) give us better protection than symbols. There is no way to access private members implemented using WeakMaps from the outside of an object.

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**

#### Inheritance

##### :pushpin: Example | _Implementing Inheritance_

```JavaScript
class Triangle extends Shape {
    constructor(color) {
        // To call the base constructor
        super(color);
    }

    draw() {
        // Call the base method
        super.draw();

        // Do some other stuff here
    }
}
```

##### **[Back To Top :arrow_up:](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#table-of-contents-book)**
