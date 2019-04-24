# Examining the DOM

- You CAN use forEach() on a NodeList

- You CANNOT use forEach() on an HTMLCollection (but you can use a regular `for` loop).

- To convert an HTMLCollection into an array so that you can use forEach()...

```javascript
let lis = document.getElementsByTagName('li'); // HTMLCollection
lis = Array.from(lis); // Converted to Array

lis.forEach(...)
```



# Multiple Element Selectors

- A NodeList includes things like text nodes

```javascript
document.getElementsByClassName(); // returns HTMLCollection
document.getElementsByTagName(); // returns HTMLCollection
document.querySelectorAll(); // returns NodeList
```



# .className vs .classList.contains()

```javascript
function deleteItem(e) {
  /* The .className property requires you to match the
  exact string. This is a bad method because if you add
  a class to your CSS, this condition no longer works. */
  if (e.target.className === 'delete-item task') {
    e.target.remove()
  }

  /* It is better to use .classList.contains('')
  to target the specific class you want */
  if (e.target.classList.contains('delete-item')) {
    e.target.remove()
  }
}
```



# Local & Session Storage

- Local storage - stays until you manually clear it
- Session storage - stays until you close the browser
- To view your storage: Open Dev Tools -> Application -> Storage
- Storage only stores strings, so when you set a value it must be a string.
- Use JSON.stringify to save arrays and objects.
- Use JSON.parse if you want to later pull out those arrays and objects



# The .call() Method

- `.call()` is a function that allows us to call another function from somewhere else in the current context
```javascript



// Customer constructor
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

function Customer(firstName, lastName, phone, membership) {

  Person.call(this, firstName, lastName);
  // the line above is like adding:

  // this.firstname = firstName;
  // this.lastName = lastName;
  this.phone = phone;
  this.membership = membership;
}
```



# Static Methods

- A static method is one you can use without needing to instatiate an object. That is, you don't need to create an object from the class using `const ryan = new Person('Ryan');`. It's just a standalone method that you call with the name of the constructor function itself.
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello there, ${this.name}`;
  }

  static addNumbers(x, y) {
    return x + y;
  }
}

/* Call a static method by using the name of the
constructor itself. No need for instantiation */
console.log(Person.addNumbers(1, 2));
```



# Sub-Classes: Extending Classes with 'Super'

```javascript
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

class Customer extends Person {
  constructor(firstName, lastName, phone, membership) {
    super(firstName, lastName);

    this.phone = phone;
    this.membership = membership;
  }
}
```



