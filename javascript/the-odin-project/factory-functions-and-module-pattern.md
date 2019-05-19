# Factory Functions and the Module Pattern



### Scope and Closure

**Scope** - where variables and functions can be accessed

**Closure** - "functions retain their scope even if they are called outside of that scope"



### Constructor Function

```javascript
const Person = function(name, age) {
  this.sayHello() => console.log('Hello!');
  this.name = name;
  this.age = age;
}

const jeff = new Person('Jeff', 27);
```



### Factory Functions

- "Factories are simply plain old JavaScript functions that return objects for us to use in our code."

```javascript
const personFactory = (name, age) => {
  const sayHello = () => console.log('Hello!');
  
  return { name, age, sayHello };
}

const jeff = personFactory('Jeff', 27);

console.log(jeff.name); // -> 'Jeff'
jeff.sayHello(); // -> 'Hello!'
```



### Module Pattern

- Exact same concept as Factory Functions, except the Module Pattern is wrapped in an IIFE.
- Whereas a Factory is for creating multiple objects, the Module Pattern is for creating just one. For example, we would create a calculator with the Module Pattern, since we only want one calculator.

```javascript
const calculator = (() => {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mult = (a, b) => a * b;
  const div = (a, b) => a / b;
  
  return {
    add,
    sub,
    mul,
    div
  }
})();

calculator.add(3, 5); // -> 8
calculator.sub(6, 2); // -> 4
calculator.mul(4, 5); // -> 20
```

