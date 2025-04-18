# JavaScript Concepts - Explanation and Practical Usage

## 1. Constructor Function
### **Explanation:**
A constructor function is used to create and initialize objects in JavaScript. It allows object instantiation using the `new` keyword.

### **Code Example:**
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.greet = function() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
    };
}
const person1 = new Person("John", 25);
person1.greet();
```

### **Advantages:**
- Allows object instantiation
- Reusable
- Encapsulates data

### **Disadvantages:**
- No private variables
- Higher memory consumption for multiple instances

### **Practical Usage:**
- Creating User, Product, or Employee objects in applications.

---

## 2. Default Parameter to Avoid NaN
### **Explanation:**
Default parameters ensure functions don’t return `NaN` by providing a default value.

### **Code Example:**
```javascript
function calculateTotal(price, tax = 0.05) {
    return price + price * tax;
}
console.log(calculateTotal(100)); // 105
console.log(calculateTotal(100, 0.1)); // 110
```

### **Advantages:**
- Prevents `NaN` errors
- Provides default behavior

### **Practical Usage:**
- Used in billing systems, tax calculations, and financial computations.

---

## 3. Rest Parameter
### **Explanation:**
Rest parameters allow functions to accept multiple arguments as an array.

### **Code Example:**
```javascript
function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

### **Advantages:**
- Handles multiple arguments efficiently
- Avoids unnecessary looping

### **Practical Usage:**
- Creating dynamic functions like mathematical operations or form data handling.

---

## 4. Generator Function
### **Explanation:**
A generator function allows pausing and resuming function execution.

### **Code Example:**
```javascript
function* generateNumbers() {
    yield 1;
    yield 2;
    yield 3;
}
const gen = generateNumbers();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
```

### **Advantages:**
- Improves performance with lazy evaluation
- Reduces memory usage

### **Practical Usage:**
- Infinite scrolling, pagination, or handling asynchronous processes.

---

## 5. Reduce Concept
### **Explanation:**
The `reduce` method accumulates values into a single result.

### **Code Example:**
```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```

### **Practical Usage:**
- Summing up cart totals, filtering datasets, and aggregating data.

---

## 6. Prototype Usage
### **Explanation:**
Prototypes enable object inheritance.

### **Code Example:**
```javascript
function Animal(name) {
    this.name = name;
}
Animal.prototype.speak = function() {
    console.log(`${this.name} makes a noise.`);
};
const dog = new Animal("Dog");
dog.speak();
```

### **Advantages:**
- Efficient memory usage
- Allows method sharing among instances

### **Practical Usage:**
- Extending JavaScript objects dynamically.

---

## 7. Callback Function
### **Explanation:**
A function passed as an argument to another function.

### **Code Example:**
```javascript
function greet(name, callback) {
    console.log("Hello " + name);
    callback();
}
greet("John", function() {
    console.log("Welcome!");
});
```

### **Practical Usage:**
- Asynchronous operations like API calls and event handling.

---

## 8. Function Expression
### **Explanation:**
A function stored in a variable.

### **Code Example:**
```javascript
const add = function(a, b) {
    return a + b;
};
console.log(add(5, 10));
```

### **Practical Usage:**
- Used in callbacks and event handlers.

---

## 9. Arrow Function
### **Explanation:**
A concise way to write functions.

### **Code Example:**
```javascript
const multiply = (a, b) => a * b;
console.log(multiply(3, 4)); // 12
```

### **Practical Usage:**
- Writing clean and concise code.

---

## 10. Function Declaration
### **Explanation:**
A function defined with the `function` keyword.

### **Code Example:**
```javascript
function sayHello() {
    console.log("Hello!");
}
sayHello();
```

### **Practical Usage:**
- Used for defining reusable functions globally.

---

## 11. Immediately Invoked Function Expression (IIFE)
### **Explanation:**
A function that executes immediately after its definition.

### **Code Example:**
```javascript
(function() {
    console.log("I am invoked immediately!");
})();
```

### **Practical Usage:**
- Avoiding variable conflicts in scripts.

---

## 12. Higher-Order Function
### **Explanation:**
A function that takes another function as a parameter or returns a function.

### **Code Example:**
```javascript
function operate(a, b, func) {
    return func(a, b);
}
console.log(operate(3, 4, (x, y) => x + y));
```

### **Practical Usage:**
- Used in map, filter, and reduce operations.

---

## Summary Table

| Concept | Key Feature | Practical Use Case |
|---------|------------|--------------------|
| Constructor Function | Object creation | User, Product models |
| Default Parameter | Prevents `NaN` | Financial calculations |
| Rest Parameter | Handles multiple arguments | Dynamic function inputs |
| Generator Function | Lazy evaluation | Infinite scrolling |
| Reduce | Accumulates values | Aggregating data |
| Prototype | Enables inheritance | Object extensions |
| Callback | Asynchronous execution | API calls |
| Function Expression | Stores functions in variables | Event handlers |
| Arrow Function | Shorter syntax | Cleaner code |
| Function Declaration | Reusable functions | Global utility functions |
| IIFE | Immediate execution | Avoiding global scope conflicts |
| Higher-Order Function | Functions as parameters | Functional programming |

---
# 🧠 Object Class Methods in JavaScript & Java

This document compares and explains the commonly used methods in the `Object` class in **JavaScript** and **Java**.

---

## 🌐 JavaScript: `Object` Methods

### 🔧 Static Methods (`Object.method()`)

| Method | Description |
|--------|-------------|
| `Object.keys(obj)` | Returns an array of keys from the object |
| `Object.values(obj)` | Returns an array of values from the object |
| `Object.entries(obj)` | Returns an array of `[key, value]` pairs |
| `Object.assign(target, source)` | Copies properties from source to target |
| `Object.create(proto)` | Creates a new object with the given prototype |
| `Object.freeze(obj)` | Makes an object immutable |
| `Object.seal(obj)` | Prevents adding/removing properties |
| `Object.getOwnPropertyNames(obj)` | Lists all own property names |
| `Object.hasOwn(obj, prop)` | Checks if a property exists (safe version) |
| `Object.getPrototypeOf(obj)` | Returns the prototype of the object |
| `Object.setPrototypeOf(obj, proto)` | Sets the prototype of the object |

### 🧬 Instance Methods (`Object.prototype`)

| Method | Description |
|--------|-------------|
| `toString()` | Returns a string representation of the object |
| `hasOwnProperty(prop)` | Checks if the object has the given property directly |
| `isPrototypeOf(obj2)` | Checks if object is in prototype chain of another |
| `valueOf()` | Returns the primitive value of the object |
| `toLocaleString()` | Returns a localized string representation |
| `propertyIsEnumerable()` | Checks if property is enumerable |

---

## ☕ Java: `java.lang.Object` Methods

Every class in Java implicitly inherits from `Object`.

| Method | Description |
|--------|-------------|
| `toString()` | Returns a string representation of the object |
| `equals(Object obj)` | Compares two objects for equality |
| `hashCode()` | Returns a hash code for use in hashing |
| `getClass()` | Returns the runtime class of the object |
| `clone()` | Creates and returns a copy of the object (if cloneable) |
| `finalize()` | Cleanup before object is garbage collected (deprecated) |
| `wait()` | Causes the current thread to wait |
| `notify()` | Wakes up a single thread waiting on this object |
| `notifyAll()` | Wakes up all threads waiting on this object |

---

## ✅ Quick Comparison Table

| Feature | JavaScript (`Object`) | Java (`Object`) |
|--------|------------------------|------------------|
| Root Class | `Object` | `java.lang.Object` |
| Primary Use | Utilities, serialization | Inheritance base, threading |
| toString() | Basic, often not informative | Often overridden for readability |
| equals() | Not available (`===` used) | Overridden for deep comparison |
| Threads | ❌ Not applicable | ✅ wait/notify supported |

---


## Download as Markdown File
Now, download the Markdown file to save the content locally.
