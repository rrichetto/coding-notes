

## The Document Object Model (DOM)

### What is the DOM?

The **Document Object Model** is a structured representation of an HTML page:

- It is essentially a tree of nodes/elements created by the browser
- You can manipulate the DOM with JavaScript
- The DOM is object-oriented - each node/element has its own set of properties and methods.



### NodeLists and HTML Collections

- NodeLists and HTML collections are array-like objects, but have a few difference:
  - HTMLCollection - you **cannot** use the forEach() method
  - NodeList - includes text nodes and you **can** use forEach() and other array methods



### Converting an HTMLCollection into an Array to enable forEach()

```javascript
let scripts = document.scripts; // gets all scripts in the file (such as JS)

let scriptsArr = Array.from(scripts);

scriptsArr.forEach(script => {
  console.log(script)
});
```



### Element Selectors

```javascript
// Single Element Selectors
document.getElementById();
document.querySelector();

// Multiple Element Selectors
document.getElementsByClassName(); // returns HTMLCollection
document.getElementsByTagName();   // returns HTMLCollection
document.querySelectorAll();       // returns NodeList

```



### DOM Traversal

```javascript
item.children; // HTMLCollection of children element nodes
item.firstElementChild;
item.lastElementChild;
item.parentElement;
item.nextElementSibling;
item.previousElementSibling;
```



### Creating Elements

```javascript
document.createElement('li');
document.createTextNode('Hello');
parent.appendChild(item);
```



### Replacing and Removing Elements

```javascript
// Replace Element
parent.replaceChild(newItem, oldItem);

// Remove Element
item.remove();
item.removeChild(element);
```



### Classes and Attributes

```javascript
item.className; // string of class name(s)
item.classList; // array-like structure containing all class names
item.classList.add('theClass');
item.classList.remove('theClass');
```

```javascript
item.getAttribute('href');
item.setAttribute('href', 'http://google.com');
item.hasAttribute('href');
item.removeAttribute('href');
```



### Event Bubbling & Delegation

- **Event bubbling** is when an event "bubbles up" from a child element to its parent element(s)
- **Event delegation** is when an event listener is placed on the parent element, and then we use logic to target the specific element we want.



### .className vs. .classList.contains()

```javascript
function deleteItem(e) {
  /* The .className property requires you to match the
  exact string. This is a bad method because if you add
  a class to your CSS, this condition no longer works. */
  if (e.target.className === 'delete-item task') {
    e.target.remove();
  }

  /* It is better to use .classList.contains('')
  to target the specific class you want */
  if (e.target.classList.contains('delete-item')) {
    e.target.remove();
  }
}
```



### Local and Session Storage

- Local storage - stays until you manually clear it
- Session storage - stays until you close the browser
- Allows you to store key/value pairs
- To view your storage: Open Dev Tools -> Application -> Storage
- Storage only stores strings, so when you set a value it must be a string.
- Use `JSON.stringify()` to save arrays and objects.
- Use `JSON.parse()` if you want to later pull out those arrays and objects

```javascript
// set storage item (you use LS and SS the same way).
localStorage.setItem('name', 'John');
sessionStorage.setItem('name', 'John');

// get storage item
localStorage.getItem('name');
sessionStorage.getItem('name');

// remove storage item
localStorage.removeItem('name');
sessionStorage.removeItem('name');

// clear storage
localStorage.clear();
sessionStorage.clear();

// Stringify to set to storage
localStorage.setItem('keyName', JSON,stringify(value));

// Parse to get from storage
JSON.parse(localStorage.getItem('keyName'));
```





## Object Oriented JavaScript

### Constructors and the 'this' keyword

- `this` refers to the current instance of the object
- a **method** is a function that exists on an object

```javascript
// Constructor function (note that normally we'd put the method on the prototype)
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayName = function() {
    return `My name is ${this.name}`;
  }
}

const ryan = new Person('Ryan', 27);
```



### Prototypes

- each object has a prototype, and a prototype is itself an object
- all objects inherit their properties and methods from their prototype
- when you are dealing with an object literal, you are inheriting from a prototype called `Object.prototype`
- when you are dealing with objects created through a constructor function (like `Person` above), you are inheriting from `Person.prototype`
- the browser gives us the pseudo-property or pointer called `__proto__`, which represents the `Person.prototype` (for example), or the `Object.prototype`.

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

Person.prototype.getFullName = function(){
  return `${this.firstName} ${this.lastName}`;
}

const john = new Person('John', 'Doe');

console.log(john.getFullName()); // 'John Doe'
```



### The `.call()` Method

- The `.call()` function lets us call another function (from somewhere else) in the current context
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



### ES6 Classes

```javascript
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  greeting() {
    return `Hello there ${this.firstName} ${this.lastName}`;
  }

  getsMarried(newLastName) {
    this.lastName = newLastName;
  }

  static addNumbers(x, y) {
    return x + y;
  }
}

const mary = new Person('Mary', 'Williams');

/* Call a static method by using the name of the
class name itself. No need for instantiation */
console.log(Person.addNumbers(1, 2));
```

- A static method is just a standalone method you can use without needing to instatiate an object. That is, you don't need to create an object from the class using `const ryan = new Person('Ryan');`. It's just a standalone method that you call with the name of the class name itself.



### Sub-Classes: Extending Classes with `Super`

```javascript
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  
  greeting() {
    return `Hello there ${this.firstName} ${this.lastName}`;
  }
}

class Customer extends Person {
  constructor(firstName, lastName, phone, membership) {
    super(firstName, lastName); // here we are calling the Person constructor

    this.phone = phone;
    this.membership = membership;
  }
  
  static getMembershipCost() {
    return 500;
  }
}

const john = new Customer('John', 'Doe', '555-555-5555', 'Standard');

console.log(john.greeting()); // 'Hello there John Doe'
console.log(Customer.getMembershipCost()); // 500
```





# Asynchronous Programming

- Most Async code you work with will be part of an API or library. You just have to handle the response in a certain way.
  - XMLHttpRequest & Fetch
  - jQuery Ajax, Axios, or other HTTP libraries



- A few ways to handle Async code
  - Callbacks
  - Promises (ES6)
  - Async/Await (ES2017) - allow us to write Async code and make them look like simple synchronous code



# Ajax & XHR Introduction

- AJAX: Asynchronous JavaScript and XML
- It's not a language or a library or a framework.
- It is a set of web technologies used to send and receive data asynchronously
- It does not interefere with the current page
- Ironically, JSON data has mostly replaced XML data, but we still refer to it as AJAX.

![Screen Shot 2019-04-26 at 2.24.52 AM](/Users/ryanrichetto/Desktop/Screen Shot 2019-04-26 at 2.24.52 AM.png)



### The XmlHttpRequest (XHR) Object

- this is the core in AJAX
- It is an API in the form of an object
- It is provided by the browsers JS environment
- It's methods transfer data between client / server
- It can be used with other protocals than HTTP
- It can work with data other than XML (JSON, plain text)



### Libraries and Methods to make HTTP Requests

- AJAX and XHR (older but still important to learn)
- Fetch API (suggested since its part of vanilla JS)
- Axios (library)
- Superagent (library)
- jQuery (library)
- Node HTTP



# Rest APIs and HTTP Requests

### What is an API?

- API: Application Programming Interface
- A contract provided by one piece of software to another
- Structured request and response

### REST APIs

- REST: Representational State Transfer
- Architectural style for designing networked applications
- Relies on a stateless, client-server protocol (almost always HTTP)
- Treats server side objects (e.g. a blog post, a user, etc) as resources that can be created or destroyed
- Can be used by virtually any programming language because it operates using HTTP requests and some standard like JSON
- An API is the messenger, and then REST lets us use HTTP requests to format that message.
- A REST API takes in multiple types of HTTP requests (GET, POST, UPDATE, DELETE)
- All APIs have their own rules and structure

### HTTP Requests

- GET: Retreive data from a specified resource
- POST: Submit data to be processed to a specified resource
- PUT: Update a specified resource
- DELETE: Delete a specified resource

### API Endpoints

- When you work with an API you will have endpoints
- Endpionts are the URLs that you access to do certain things
  - Example: http://someurl.com/api/users



