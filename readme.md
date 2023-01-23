# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)  SOFTWARE ENGINEERING IMMERSIVE

# JavaScript Objects

### Objectives
*After this lesson, students will be able to:*

- Compare objects and key-value stores to arrays as data structures
- Explain the difference between object properties and methods
- Create empty objects and objects with multiple properties and methods using object literal syntax
- Compare adding and retrieving properties to an existing object using the dot and bracket notations
- Access properties of an object using keys and helper methods.
- Iterate over the keys of an object to return and manipulate values

### Preparation
*Before this lesson, students should already be able to:*

- Create and manipulate variables with javascript
- Use the chrome dev tools console

Objects in JavaScript
=====

### What is an object?

* Objects are a type of data structure that is nearly universal across programming languages, although they may have different names in different languages
* Like arrays, objects can hold multiple pieces of data of varying types; but unlike arrays, objects use named keys rather than indices to order and access those pieces of data
* Objects in general are made up of two things – properties and methods. Properties are data attached to an object that describe it or are related to it in some way. Methods are just functions, but because they're attached to an object, you can think of them as actions that the object can invoke on itself
* In JavaScript, an object is a type of key-value store, or a way to group many pairs of keys and values together, so sometimes it's used like a hash (in Ruby) or a dictionary (in other languages)

Example: A car has properties, a type of engine, a color, a certain number of seats etc. Following the same logic, a JavaScript object may have **properties** and **values** for these properties.
### Collection of key-value pairs

The following is an example of an object's key-value pair syntax:

```javascript
const car = {
  make: 'Honda',
  model: 'Civic',
  year: 1989,
  engine: '1.5 liter',
  seats: 5,
  color: 'grey'
}
```
> "make" is the key, while "Honda" is the value

> Objects must have both a key and a value - neither can be empty.

Unlike arrays, objects use *named keys* rather than ordered indexes. Each piece of data is bound to its key, rather than assigned an index. The data is not sequential.

We could store this same information in an array like this:

```js
const car = ['Honda', 'Civic', 1989]
```

But with the array above, we don't know what the values mean. Does 'Civic' refer to the name of the owner, or the model of the vehicle?

#### Independent Practice: Model SEI Student

Your goal is to code an object:

- In pairs, spend 2 minutes thinking about what attributes an SEI student should have (think of at least 5!).
- Take 3 minutes to construct your object with the appropriate key-value pairs by drawing it on the table.
- **Bonus** - One key value pair contains an array
- **Double Bonus** - one key value pair contains another object


Aside from the values `null` and `undefined`, **everything in JavaScript is an object**.

### Collections of name-value pairs

Javascript objects work as lists of keys (**A property name**) and corresponding values (**A property value**).

This way of storing/reading data is widely used across programs and languages because it’s highly customizable and quick to implement.

A key can be either a name, a number or a string, the corresponding value to a
key can be any valid JavaScript, including arrays, `null` or `undefined`and even another object. Objects structures can therefore be nested (objects inside objects) and of any complexity.

## Creating Objects

There are a few ways to create an object.


#### Object literal syntax

This is also called an [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer).


```javascript
const myObject = {};
```

#### Factory Function

It is also possible to use a `function` to create an object.

```javascript
function createClassroom(name, numberOfStudents) {
  return {
    name,
    numberOfStudents,
  }
}

const sei = createClassroom('SEI NYC', 31);
```

Alternatively you may use an arrow function for a shorter syntax:

```js
const createClassroom = (name, numberOfStudents) => ({
  name,
  numberOfStudents,
})

const sei = createClassroom('SEI NYC', 31);
```

It's important to note that the object must be wrapped in `()` otherwise the `{}` will define the function body rather than the return.

## Object Properties

Objects in JavaScript **always** have properties associated with them.

You can think of a property on a JavaScript object as a type of variable that contains a value. The properties of an object can be accessed using 'dot notation':

```javascript
const person = {
  name: 'Gerry'
}

person.name
=> "Gerry"
```

You can define or re-assign a property by assigning it a value using `=` as you would a normal variable.

```javascript
const person = {
  name: 'Gerry'
}

person.name
=> "Gerry"

person.name = 'Alex'
person.name
=> "Alex"
```

## Creating an object with properties

We are going to create an object `classroom` that contains properties `name` and `campus`:

```javascript
const classroom = {};
=> undefined

classroom.name = 'SEI';
=> "SEI"

classroom.campus = 'NYC';
=> "NYC"

classroom
=> Object {name: 'SEI', campus: 'NYC'}
```

#### Bracket notation

There is another way to set properties on a JavaScript object.

```javascript
classroom['name']   = 'SEI';
classroom['campus'] = 'NYC';
```

This syntax can also be used to read properties of an object:

```javascript
console.log(classroom['name']);
=> "SEI";

const property = 'campus';

console.log(classroom[property]);
=> "NYC";
```

For more details see [MDN's Documentation on Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors).


#### Deleting properties

If you want to delete a property of an object (and by extension, the value attached to the property), you need to use the [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete) operator:

The following code shows how to remove a property:

```javascript
const classroom = {name: 'SEI', campus: 'NYC', start: '1/1/2000'};
delete classroom.start;
classroom
=> {name: "SEI", campus: "NYC"}
```

## Object methods

As we've said before, the value of a property can be anything in JavaScript, means we can also attach functions to objects properties. When a function is attached to a property, this function becomes a `method`. Methods are defined the exact same way as a function, except that they have to be defined as the property of an object.

```javascript
const classroom = {
  name: "SEI",
  campus: "NYC",
  sayHello() {
    console.log("Hello");
  }
};
```

To call the method, we add a pair of parentheses to execute it:

```javascript
classroom.sayHello();
=> Hello
```

If that syntax feels familiar, it's because you have been constantly using
methods since you started learning JavaScript, most notably the `log()` method
of the `console` object! There's plenty of other stuff that the
[console](https://developer.mozilla.org/en-US/docs/Web/API/console) object can
do!

#### Assigning a previously-defined function

We can attach regular functions to objects as methods, even after they are created.

```javascript
const sayHello = function() { console.log("Hello"); }
classroom.sayHello = sayHello;  
classroom.sayHello()
=> Hello
```

## `this` for object references

In JavaScript, `this` is a keyword that refers to the current object. When used in a method on an object, it will always refer to the current object.


```javascript
const classroom = {
  name: 'SEI',
  campus: 'NYC',
  classInfo(){
    console.log(`This is ${this.name} and on ${this.campus} campus`);
  },
  missOutdoors() {
    console.log(`Missing ${this.campus} outdoors.`)
  }
};

classroom.classInfo()
// => This is SEI and on NYC campus

classroom.missOutdoors()
// => Missing NYC outdoors.

```

#### Enumerating properties of an object

There are three native ways to list the properties of an object:

* **[for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) loops** This method traverses all enumerable properties of an object and its prototype chain
* **[Object.keys(someName)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)**  This method returns an array with all the own (not in the prototype chain) enumerable properties' names ('keys') of an object someName.
* **[Object.getOwnPropertyNames(someName)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames)** This method returns an array containing all own properties' names (enumerable or not) of an object someName.

**Loop over an object's properties**


You can use the bracket notation with for...in to iterate over all the enumerable properties of an object.

```javascript
const car = { 
  make: 'Ford', 
  model: 'Mustang', 
  year: 1969 
}

const showProps = function(obj, objName) {
  for (let key in obj) {
      console.log(`${objName}.${key} = ${obj[key]}`)
  }
}

showProps(car, 'Car')
=> Car.make = Ford
=> Car.model = Mustang
=> Car.year = 1969
```

This section from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Creating_new_objects#Objects_and_properties)


## Conclusion

We will use objects in JavaScript every day, and you will have plenty of time to practice creating and using objects in Javascript. There are a lot of resources available on the web for you to dive deeper, but the most detailed and understandable one is probably MDN.

## References

- [JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [Intro to Object-Orientated Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
- [Objects in Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
