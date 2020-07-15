# JavaScript-OOP-Concepts :page_with_curl:
Code Snippets which detail the Object Oriented Programming principles in JavaScript. The code was adapted from [Mosh Hamedani](https://codewithmosh.com/)

## Table of Contents :bookmark_tabs:
1. [Introduction](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#introduction)
2. [Objects](https://github.com/Sammy-Nyakabau/JavaScript-OOP-Concepts#objects)
2. Prototypes
3. Prototypical Inheritance
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