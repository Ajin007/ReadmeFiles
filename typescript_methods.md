
# TypeScript Number Type Methods and Properties

## Methods
1. **toFixed(digits: number): string**  
   Formats the number with fixed-point notation.  
   Example:  
   ```ts
   let num = 3.14159;
   console.log(num.toFixed(2));  // "3.14"
   ```

2. **toExponential(digits: number): string**  
   Returns the number in exponential notation.  
   Example:  
   ```ts
   let num = 12345;
   console.log(num.toExponential(2));  // "1.23e+4"
   ```

3. **toPrecision(digits: number): string**  
   Returns the number to a specified precision.  
   Example:  
   ```ts
   let num = 3.14159;
   console.log(num.toPrecision(3));  // "3.14"
   ```

4. **toString(radix?: number): string**  
   Converts the number to a string, optionally using a specified base.  
   Example:  
   ```ts
   let num = 255;
   console.log(num.toString(16));  // "ff"
   ```

5. **valueOf(): number**  
   Returns the primitive value of the number.  
   Example:  
   ```ts
   let num = new Number(5);
   console.log(num.valueOf());  // 5
   ```

## Constants (Static Properties)
- **Number.MAX_VALUE**  
  The largest number that can be represented in JavaScript.  
  Example:  
  ```ts
  console.log(Number.MAX_VALUE);  // 1.7976931348623157e+308
  ```

- **Number.MIN_VALUE**  
  The smallest positive number in JavaScript.  
  Example:  
  ```ts
  console.log(Number.MIN_VALUE);  // 5e-324
  ```

- **Number.NaN**  
  Represents "Not-A-Number".  
  Example:  
  ```ts
  console.log(Number.NaN);  // NaN
  ```

- **Number.POSITIVE_INFINITY**  
  Represents positive infinity.  
  Example:  
  ```ts
  console.log(Number.POSITIVE_INFINITY);  // Infinity
  ```

- **Number.NEGATIVE_INFINITY**  
  Represents negative infinity.  
  Example:  
  ```ts
  console.log(Number.NEGATIVE_INFINITY);  // -Infinity
  ```

- **Number.EPSILON**  
  The smallest difference between two representable numbers.  
  Example:  
  ```ts
  console.log(Number.EPSILON);  // 2.220446049250313e-16
  ```

## Static Methods
1. **Number.isFinite(value: any): boolean**  
   Checks if the value is a finite number.  
   Example:  
   ```ts
   console.log(Number.isFinite(42));  // true
   ```

2. **Number.isNaN(value: any): boolean**  
   Checks if the value is NaN.  
   Example:  
   ```ts
   console.log(Number.isNaN(NaN));  // true
   ```

3. **Number.isInteger(value: any): boolean**  
   Checks if the value is an integer.  
   Example:  
   ```ts
   console.log(Number.isInteger(42));  // true
   ```

4. **Number.isSafeInteger(value: any): boolean**  
   Checks if the value is a safe integer.  
   Example:  
   ```ts
   console.log(Number.isSafeInteger(9007199254740991));  // true
   ```

5. **Number.parseFloat(value: string): number**  
   Converts a string to a floating-point number.  
   Example:  
   ```ts
   console.log(Number.parseFloat("3.14"));  // 3.14
   ```

6. **Number.parseInt(value: string, radix?: number): number**  
   Converts a string to an integer.  
   Example:  
   ```ts
   console.log(Number.parseInt("10", 10));  // 10
   ```

## Conclusion
The **`number`** type in TypeScript can be enhanced with several built-in methods and constants to manipulate and work with numeric values efficiently.



# TypeScript Types and Methods Summary

## 1. String Methods

### 1.1 `toUpperCase()`
Converts the string to uppercase.
```ts
let str = "hello";
console.log(str.toUpperCase());  // "HELLO"
```

### 1.2 `toLowerCase()`
Converts the string to lowercase.
```ts
let str = "HELLO";
console.log(str.toLowerCase());  // "hello"
```

### 1.3 `slice(start: number, end?: number): string`
Extracts a section of the string.
```ts
let str = "Hello, World!";
console.log(str.slice(0, 5));  // "Hello"
```

### 1.4 `substring(start: number, end?: number): string`
Extracts a substring, similar to `slice()` but with different behavior when the start index is greater than the end.
```ts
let str = "Hello, World!";
console.log(str.substring(7, 12));  // "World"
```

### 1.5 `split(separator: string): string[]`
Splits the string into an array of substrings.
```ts
let str = "apple,banana,orange";
console.log(str.split(","));  // ["apple", "banana", "orange"]
```

### 1.6 `includes(searchString: string): boolean`
Checks if a substring exists within the string.
```ts
let str = "Hello, World!";
console.log(str.includes("World"));  // true
```

### 1.7 `indexOf(searchValue: string): number`
Finds the first occurrence of a substring and returns its index.
```ts
let str = "Hello, World!";
console.log(str.indexOf("o"));  // 4
```

### 1.8 `replace(searchValue: string, newValue: string): string`
Replaces the first occurrence of a substring.
```ts
let str = "Hello, World!";
console.log(str.replace("World", "Everyone"));  // "Hello, Everyone!"
```

### 1.9 `charAt(index: number): string`
Returns the character at the specified index.
```ts
let str = "Hello";
console.log(str.charAt(1));  // "e"
```

## 2. Object Methods

### 2.1 `Object.keys(obj: object): string[]`
Returns an array of the object's property names.
```ts
let person = { name: "John", age: 30 };
console.log(Object.keys(person));  // ["name", "age"]
```

### 2.2 `Object.values(obj: object): any[]`
Returns an array of the object's property values.
```ts
let person = { name: "John", age: 30 };
console.log(Object.values(person));  // ["John", 30]
```

### 2.3 `Object.entries(obj: object): [string, any][]`
Returns an array of the object's key-value pairs.
```ts
let person = { name: "John", age: 30 };
console.log(Object.entries(person));  // [["name", "John"], ["age", 30]]
```

### 2.4 `Object.assign(target: object, ...sources: object[]): object`
Copies the values of all properties from one or more source objects to a target object.
```ts
let person = { name: "John" };
let details = { age: 30 };
Object.assign(person, details);
console.log(person);  // { name: "John", age: 30 }
```

### 2.5 `Object.freeze(obj: object): object`
Freezes an object to prevent changes.
```ts
let person = { name: "John", age: 30 };
Object.freeze(person);
person.age = 31;  // This will have no effect
console.log(person.age);  // 30
```

### 2.6 `Object.seal(obj: object): object`
Seals an object, preventing new properties from being added, but allowing modification of existing properties.
```ts
let person = { name: "John", age: 30 };
Object.seal(person);
person.address = "New York";  // Will be ignored
person.age = 31;  // Will work
console.log(person);  // { name: "John", age: 31 }
```

## 3. JSON Methods

### 3.1 `JSON.stringify(value: any): string`
Converts a JavaScript object to a JSON string.
```ts
let person = { name: "John", age: 30 };
let jsonStr = JSON.stringify(person);
console.log(jsonStr);  // '{"name":"John","age":30}'
```

### 3.2 `JSON.parse(text: string): any`
Parses a JSON string and returns the corresponding JavaScript object.
```ts
let jsonStr = '{"name":"John","age":30}';
let person = JSON.parse(jsonStr);
console.log(person);  // { name: "John", age: 30 }
```

## 4. Array Methods

### 4.1 `forEach(callback: (value: T, index: number, array: T[]) => void): void`
Executes a function on each element in the array.
```ts
let numbers = [1, 2, 3];
numbers.forEach((num) => console.log(num));  // 1 2 3
```

### 4.2 `map(callback: (value: T, index: number, array: T[]) => U): U[]`
Creates a new array by applying a function to each element.
```ts
let numbers = [1, 2, 3];
let doubled = numbers.map(num => num * 2);
console.log(doubled);  // [2, 4, 6]
```

### 4.3 `filter(callback: (value: T, index: number, array: T[]) => boolean): T[]`
Creates a new array with elements that pass the test in the callback.
```ts
let numbers = [1, 2, 3, 4];
let even = numbers.filter(num => num % 2 === 0);
console.log(even);  // [2, 4]
```

### 4.4 `reduce(callback: (accumulator: U, value: T, index: number, array: T[]) => U, initialValue: U): U`
Executes a function on each element to accumulate a result.
```ts
let numbers = [1, 2, 3];
let sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum);  // 6
```

## 5. Other Important TypeScript Features

### 5.1 `any` Type
Used when you don't know the type of a variable.
```ts
let data: any = "Hello";
data = 42;
data = true;
```

### 5.2 `unknown` Type
Like `any`, but you must do some type-checking before performing operations on it.
```ts
let data: unknown = "Hello";
if (typeof data === "string") {
  console.log(data.toUpperCase());  // "HELLO"
}
```

### 5.3 `never` Type
Represents a value that never occurs, such as in a function that always throws an error.
```ts
function throwError(message: string): never {
  throw new Error(message);
}
```

### 5.4 `void` Type
Represents the absence of a value, commonly used as the return type of functions that don’t return anything.
```ts
function logMessage(message: string): void {
  console.log(message);
}
```

### 5.5 Type Aliases and Interfaces
Used to define custom types.
```ts
type Point = { x: number, y: number };
interface Shape { 
  area(): number; 
}
```

## Conclusion
Mastering these TypeScript features will help you build strong, efficient, and maintainable applications. These types and methods are commonly used in real-time projects to handle data manipulation, object handling, JSON parsing, and more.


