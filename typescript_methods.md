
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


## Spread and Rest usage:
![image](https://github.com/user-attachments/assets/b7f32f46-c1cf-49fa-be7a-bfb3ef760a50)


# TypeScript: Type, Union, and Intersection Types - Practical Usage

In TypeScript, types help ensure that variables and functions receive the correct kind of values. These types can be further refined using **union** and **intersection** types, which allow you to define flexible yet safe data structures. Let's explore their practical applications in real-world scenarios, starting from basic to advanced concepts.

---

## 1. **Type Aliases**
A **type alias** in TypeScript allows you to define a new name for a type. It's useful for simplifying complex types, making your code more readable and maintainable.

### Example:
```ts
type Person = {
  name: string;
  age: number;
};

const person1: Person = {
  name: 'John Doe',
  age: 30
};
```
- **Practical Use Case**: This is useful when dealing with objects that have the same structure across different parts of your application. For example, a `Person` type could be reused in multiple places, ensuring consistency.

---

## 2. **Union Types**
A **union type** allows a variable to hold multiple types of values. You can use the `|` operator to define a union of types. This is helpful when a variable might hold one of several types of values.

### Example:
```ts
type StringOrNumber = string | number;

let value: StringOrNumber;
value = 123; // valid
value = 'Hello'; // valid
value = true; // Error: 'boolean' is not assignable to 'string | number'
```
- **Practical Use Case**: In a function where a parameter could accept multiple types (e.g., a function that accepts either a `string` or a `number` for input), union types provide flexibility.
  
### Advanced Example:
```ts
type FetchResponse = { data: string } | { error: string };

function handleResponse(response: FetchResponse) {
  if ('data' in response) {
    console.log('Data:', response.data);
  } else {
    console.log('Error:', response.error);
  }
}
```
- **Practical Use Case**: You could use union types to represent responses from an API that could either be successful (containing `data`) or unsuccessful (containing an `error`).

---

## 3. **Intersection Types**
An **intersection type** combines multiple types into one, meaning the resulting type will have all properties of the combined types. You use the `&` operator to define an intersection type.

### Example:
```ts
type Car = {
  make: string;
  model: string;
};

type Electric = {
  battery: string;
  range: number;
};

type ElectricCar = Car & Electric;

const tesla: ElectricCar = {
  make: 'Tesla',
  model: 'Model 3',
  battery: 'Lithium-ion',
  range: 350
};
```
- **Practical Use Case**: Intersection types are often used to combine properties from different types. For instance, you can combine a `Car` type with an `Electric` type to create a new `ElectricCar` type.

### Advanced Example:
```ts
type User = {
  name: string;
  email: string;
};

type Admin = {
  role: string;
};

type AdminUser = User & Admin;

const admin1: AdminUser = {
  name: 'Alice',
  email: 'alice@example.com',
  role: 'Admin'
};
```
- **Practical Use Case**: When you have types that represent different roles (e.g., a `User` and `Admin`), you can use intersection types to combine them into a new type `AdminUser`.

---

## Practical Scenario: Union and Intersection in a Real-World Application

### Scenario: Building an E-Commerce System
Imagine you're building an e-commerce system that has products of different types: physical products and digital products. You might also need to manage orders, which could contain different types of items.

1. **Union Type in Orders**:
   - An order could contain a mix of physical products (like a book) and digital products (like an eBook). So, we can use a union type to represent the order items.

```ts
type Product = { id: number; name: string };
type PhysicalProduct = Product & { weight: number; shippingFee: number };
type DigitalProduct = Product & { downloadUrl: string; fileSize: number };

type OrderItem = PhysicalProduct | DigitalProduct;

const order: OrderItem[] = [
  { id: 1, name: 'Book', weight: 1.2, shippingFee: 5.0 },
  { id: 2, name: 'eBook', downloadUrl: 'link_to_download', fileSize: 1.5 }
];
```

2. **Intersection Type in Customers**:
   - A customer can have personal details and an account status. We can use an intersection type to combine both types.

```ts
type PersonalInfo = { name: string; email: string };
type AccountStatus = { isActive: boolean; membershipLevel: string };

type Customer = PersonalInfo & AccountStatus;

const customer: Customer = {
  name: 'John Doe',
  email: 'john.doe@example.com',
  isActive: true,
  membershipLevel: 'Gold'
};
```

---

## Conclusion: When to Use Union and Intersection Types

- **Use Union Types**:
  - When a variable or parameter can hold one of several types. This gives you flexibility but requires checks at runtime to differentiate between the types.
  
- **Use Intersection Types**:
  - When you need to combine multiple types into one, typically when you're combining multiple sets of properties. This helps you create complex, reusable structures.

---

# Type Narrowing in TypeScript

Type narrowing in TypeScript refers to refining the type of a variable as more information becomes available in the code. TypeScript performs type narrowing automatically using different mechanisms like control flow analysis, type guards, and type assertions.

### Mechanisms of Type Narrowing:
1. **Control Flow Analysis**:
   - TypeScript can automatically narrow types based on conditional checks (like `if` statements).

2. **Type Guards**:
   - Custom checks using `typeof`, `instanceof`, and user-defined functions.

3. **Type Assertions**:
   - Forcing TypeScript to treat a variable as a more specific type.

---

### Example: Using Type Narrowing

#### Code Snippet:

```typescript
function printId(id: string | number) {
    // Narrowing type using `typeof`
    if (typeof id === "string") {
        console.log(`The ID is a string: ${id.toUpperCase()}`);  // string specific operation
    } else {
        console.log(`The ID is a number: ${id.toFixed(2)}`);  // number specific operation
    }
}

printId("abc123"); // Output: The ID is a string: ABC123
printId(123);      // Output: The ID is a number: 123.00
```

#### Explanation:
1. **Initial Type**: The function `printId` accepts an argument `id` which can be either a `string` or a `number`.
2. **Type Narrowing**: Inside the `if` block, `typeof id === "string"` narrows the type to `string`. In the `else` block, TypeScript understands that `id` must be a `number`.
3. **Type-Specific Operations**: We can safely call `toUpperCase()` on `string` and `toFixed()` on `number`, as TypeScript knows the type after narrowing.

---

### Type Guards Example

Custom Type Guard helps you define more precise narrowing when you have complex types.

```typescript
type Admin = { role: "admin"; name: string };
type User = { role: "user"; name: string };

function isAdmin(account: Admin | User): account is Admin {
    return account.role === "admin";  // Type guard logic
}

function printRole(account: Admin | User) {
    if (isAdmin(account)) {
        console.log(`Admin Name: ${account.name}`);  // Now we know it's Admin
    } else {
        console.log(`User Name: ${account.name}`);   // Now we know it's User
    }
}

const userAccount: User = { role: "user", name: "John" };
const adminAccount: Admin = { role: "admin", name: "Alice" };

printRole(userAccount); // Output: User Name: John
printRole(adminAccount); // Output: Admin Name: Alice
```

#### Explanation:
- **Type Guard Function**: `isAdmin` checks whether the given account is of type `Admin`.
- **Return Type**: The return type of `isAdmin(account: Admin | User): account is Admin` helps TypeScript understand that within the `if` block, the `account` variable is now specifically an `Admin`.

---

### 1. **`typeof` Type Narrowing**

The `typeof` operator is used to narrow types when you know that the value can only be a primitive type (`string`, `number`, `boolean`, etc.).

#### Example:
```typescript
function print(value: string | number) {
    if (typeof value === "string") {
        console.log(value.toUpperCase());  // string-specific operation
    } else {
        console.log(value.toFixed(2));     // number-specific operation
    }
}

print("hello");  // Output: HELLO
print(123.456);  // Output: 123.46
```

- **`typeof` checks**: Narrow types between `string`, `number`, `boolean`, etc.

---

### 2. **`instanceof` Type Narrowing**

The `instanceof` operator is used for narrowing types involving objects that are instances of classes.

#### Example:
```typescript
class Animal {
    makeSound() {
        console.log("Some generic sound");
    }
}

class Dog extends Animal {
    bark() {
        console.log("Woof");
    }
}

function handleAnimal(animal: Animal) {
    if (animal instanceof Dog) {
        animal.bark();  // dog-specific operation
    } else {
        animal.makeSound();  // generic Animal operation
    }
}

const dog = new Dog();
const animal = new Animal();

handleAnimal(dog);   // Output: Woof
handleAnimal(animal); // Output: Some generic sound
```

- **`instanceof` checks**: Narrow the type to a specific class type (like `Dog` in this case) from a parent class (`Animal`).

---

### 3. **User-defined Type Guards**

You can create your own custom type guards, which are functions that use TypeScript's type narrowing to define more specific types.

#### Example:
```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "rectangle"; width: number; height: number };

function isCircle(shape: Shape): shape is { kind: "circle"; radius: number } {
    return shape.kind === "circle";
}

function getArea(shape: Shape): number {
    if (isCircle(shape)) {
        return Math.PI * shape.radius * shape.radius;  // Circle-specific logic
    } else {
        return shape.width * shape.height;  // Rectangle-specific logic
    }
}

const circle: Shape = { kind: "circle", radius: 5 };
const rectangle: Shape = { kind: "rectangle", width: 10, height: 5 };

console.log(getArea(circle));    // Output: 78.53981633974483 (Circle area)
console.log(getArea(rectangle)); // Output: 50 (Rectangle area)
```

- **User-defined type guards**: The `shape is { kind: "circle"; radius: number }` predicate narrows the `Shape` type to only `circle` in the `if` block.

---

### 4. **`in` Operator for Property Checks**

You can use the `in` operator to narrow types based on whether a certain property exists on the object. This is helpful in working with union types.

#### Example:
```typescript
type Car = { type: "car"; wheels: number; doors: number };
type Bike = { type: "bike"; wheels: number; handlebar: string };

function isCar(vehicle: Car | Bike): vehicle is Car {
    return "doors" in vehicle;  // Narrow type to Car based on property 'doors'
}

function printVehicle(vehicle: Car | Bike) {
    if (isCar(vehicle)) {
        console.log(`Car with ${vehicle.wheels} wheels and ${vehicle.doors} doors`);
    } else {
        console.log(`Bike with ${vehicle.wheels} wheels and a ${vehicle.handlebar} handlebar`);
    }
}

const myCar: Car = { type: "car", wheels: 4, doors: 4 };
const myBike: Bike = { type: "bike", wheels: 2, handlebar: "racing" };

printVehicle(myCar);   // Output: Car with 4 wheels and 4 doors
printVehicle(myBike);  // Output: Bike with 2 wheels and a racing handlebar
```

- **`in` operator**: It checks whether a property (`doors` in this case) exists in the object and narrows the type based on that.

---

### 5. **Type Assertions (using `as`)**

While not strictly type narrowing, Type Assertions let you override TypeScript's inferred types when you know more about the type than it can infer. This can sometimes be used to "narrow" types when necessary.

#### Example:
```typescript
interface Animal {
    name: string;
}

interface Dog extends Animal {
    breed: string;
}

const animal: Animal = { name: "Rex" };

const dog = animal as Dog;  // Assertion narrows animal to Dog

console.log(dog.breed); // TypeScript allows this, but will throw a runtime error
```

- **Type assertions**: Using `as` narrows the type to a specific type, but use it with caution since it doesn't perform any runtime checks.

---

### 6. **`never` Type and Exhaustive Checks**

The `never` type is useful in narrowing types in exhaustive checks, especially when working with union types. It can help ensure all cases are handled.

#### Example:
```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "rectangle"; width: number; height: number };

function getShapeDetails(shape: Shape) {
    switch (shape.kind) {
        case "circle":
            return `Circle with radius: ${shape.radius}`;
        case "rectangle":
            return `Rectangle with width: ${shape.width} and height: ${shape.height}`;
        default:
            // Exhaustive check
            throw new Error(`Unknown shape: ${shape}`);
    }
}

const myShape: Shape = { kind: "circle", radius: 10 };
console.log(getShapeDetails(myShape));  // Output: Circle with radius: 10
```

- **Exhaustive checks**: The `default` case helps catch any unhandled cases and prevents TypeScript from missing out on narrowing logic.

---

### Summary of Available Narrowing Techniques:
- **`typeof`**: Use for primitive types like `string`, `number`, `boolean`.
- **`instanceof`**: Use for narrowing types with classes or constructors.
- **User-defined type guards**: Use for more complex type narrowing logic based on custom conditions.
- **`in` operator**: Use to check for the existence of a property on an object.
- **Type assertions (`as`)**: Forcefully narrow the type when you're sure of the variable's type.
- **`never` type**: Use for exhaustive checks in union types.

These tools will help you write more robust and type-safe code by ensuring that TypeScript correctly narrows types as needed.



```Examples to try 

const arrayInput:any[]=["1",2,{}];

arrayInput.push("ajin");

arrayInput.pop();

console.log(arrayInput)

arrayInput.forEach((value)=>console.log(value))
for(const value of arrayInput){
  console.log(value);
}

console.log(arrayInput.some((value)=>value==2));
arrayInput.filter((value)=>console.log(value, typeof value))

// common arrow function using the map,filter and the reduce

const datafromRepo:String[]=["Ajin","poda","epdae iruja","solu"];
const dataNUmberFormat:Number[]=[1,2,3,4,5,6];

// type narrowing
// i have used all the concepts over here 
const answer=dataNUmberFormat.filter((value)=> typeof value === 'number' && value / 1 == value ).map((value)=>parseFloat(value.toFixed(2))).reduce((acc,initialValue)=>acc+initialValue,0);
console.log(answer);

for(const value of datafromRepo){
  console.log(value);
}

const dataFiltered=datafromRepo.filter((value)=>console.log(value.split(" ")));
console.log(dataFiltered);



// const dataNumberFilter=dataNUmberFormat.filter((value)=>console.log(value.toFixed(2)));
// console.log(dataNumberFilter);

// const mapFilter=dataNUmberFormat.map((value)=>console.log(value.toFixed(2)));
// console.log(mapFilter);
// const reduceFilter=dataNUmberFormat.reduce((value)=>console.log(value.toFixed(2)));


// String to array conversion
// usage of the unknown 
let str= "apple,grape,mango";
console.log(str.split(","));

let arrayType:unknown[]=["Ajin",1,{name:"poda",age:36}];

console.log(arrayType);

for(const value of arrayType){

if(typeof value === "string"){
  console.log(value.toUpperCase());
}
  
}

//Type alias

type person={
  name:string;
  age:number;
}

const person1:person ={
  
  name:"Ajin",
  age:16
  
}

// union usage 
type SumorNumber=number | string;
 let value:SumorNumber;
 value=1;
 value="hi";
 
// Interection types:
type Car = {
  make: string;
  model: string;
};

type Electric = {
  battery: string;
  range: number;
};

type ElectricCar = Car & Electric;

const tesla: ElectricCar = {
  make: 'Tesla',
  model: 'Model 3',
  battery: 'Lithium-ion',
  range: 350
};


//Another example
type User = {
  name: string;
  email: string;
};

type Admin = {
  role: string;
};

type AdminUser = User & Admin;

const admin1: AdminUser = {
  name: 'Alice',
  email: 'alice@example.com',
  role: 'Admin'
};


// Interface understanding:
// interface Person{
//   ageee:number;
//   namenew:string;
//   greet:()=>void;
//   readonly father:string;
//   address ?: string;
//   greetings:(message:string)=>void;
  
//   // index signature -----> have the global effect of the properties over here
//   [key:string]: number | string |(()=>void) |string[];
//   hobbies:string[];
// }


// interface UniquePerson<T> extends Person{
//   value:T;
// }


// class Employee implements Person {
  
// ageee: number;
//   namenew: string;
//   readonly father: string;
//   address?: string;
//   hobbies: string[];

//   // Implementing the greet method
//   greet(): void {
//     console.log(`Hello, my name is ${this.namenew}`);
//   }

//   // Implementing the greetings method
//   greetings(message: string): void {
//     console.log(message);
//   }

//   // Implementing the index signature
//   [key: string]: number;

//   constructor(ageee: number, namenew: string, father: string, hobbies: string[]) {
//     this.ageee = ageee;
//     this.namenew = namenew;
//     this.father = father;
//     this.hobbies = hobbies;
//   }
  
// }








