
# TypeScript Conceptual MCQs

## Question 1
**What will be the output of the following code?**
```ts
function double<T extends number>(value: T): T {
  return (value * 2) as T;
}

const result = double(5);
console.log(typeof result);
```
1. "number"  
2. "string"  
3. "object"  
4. "undefined"  
**Answer:** 1

---

## Question 2
**What does the following function return?**
```ts
function mapArray<T, U>(arr: T[], func: (val: T) => U): U[] {
  return arr.map(func);
}

const lengths = mapArray(['hi', 'hello'], (s) => s.length);
console.log(lengths);
```
1. [2, 5]  
2. [1, 2, 3]  
3. ['hi', 'hello']  
4. undefined  
**Answer:** 1

---

## Question 3
**What is printed when the following code is run?**
```ts
function logParam<T>(param: T): void {
  console.log(typeof param);
}

logParam({ x: 10 });
```
1. object  
2. number  
3. undefined  
4. function  
**Answer:** 1

---

## Question 4
**Which of the following best describes what this code does?**
```ts
type Immutable<T> = {
  readonly [P in keyof T]: T[P];
};

interface Config {
  port: number;
  protocol: string;
}

const cfg: Immutable<Config> = { port: 8080, protocol: 'https' };
cfg.port = 3000;
```
1. Throws an error at runtime  
2. Compiles but logs undefined  
3. Compilation error due to assignment  
4. Works fine and changes the port  
**Answer:** 3

---

## Question 5
**What is the output of the following code?**
```ts
class Vehicle {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Car extends Vehicle {
  constructor(name: string) {
    super(name);
  }
}

const v = new Car('Sedan');
console.log(v.name);
```
1. undefined  
2. Car  
3. Sedan  
4. Compilation error  
**Answer:** 3

---

## Question 6
**What will be the result of executing the following?**
```ts
function identity<T>(arg: T): T {
  return arg;
}

const output = identity<string>('Hello');
console.log(output.toUpperCase());
```
1. HELLO  
2. hello  
3. undefined  
4. Compilation error  
**Answer:** 1

---

## Question 7
**Given the following `Rectangle` class and function, what does the output represent?**
```ts
class Rectangle {
  constructor(public length: number, public width: number) {}
}

function area(shape: Rectangle): number {
  return shape.length * shape.width;
}

console.log(area(new Rectangle(4, 5)));
```
1. 20  
2. 9  
3. 45  
4. Compilation Error  
**Answer:** 1

---

## Question 8
**Which decorator pattern allows modifying property access?**
```ts
function propertyLogger(target: any, key: string) {
  let val = target[key];

  Object.defineProperty(target, key, {
    get() {
      console.log(`Accessing ${key}`);
      return val;
    },
    set(newVal) {
      console.log(`Updating ${key} to ${newVal}`);
      val = newVal;
    }
  });
}

class Sample {
  @propertyLogger
  value = 100;
}

const s = new Sample();
s.value = 200;
console.log(s.value);
```
1. Logs access and update  
2. Logs only the update  
3. Compilation error  
4. Logs nothing  
**Answer:** 1

---

## Question 9
**Which utility type ensures deeply nested properties are readonly?**
```ts
type DeepFreeze<T> = {
  readonly [K in keyof T]: T[K] extends object ? DeepFreeze<T[K]> : T[K];
};

interface Profile {
  id: number;
  details: {
    name: string;
    age: number;
  };
}

const p: DeepFreeze<Profile> = {
  id: 1,
  details: { name: 'Raj', age: 23 }
};

p.details.age = 24;
```
1. Runtime Error  
2. Compilation Error  
3. Returns 24  
4. Logs undefined  
**Answer:** 2

---

## Question 10
**What is the return type of this function?**
```ts
function compute<T>(value: T): T[] {
  return [value];
}

const output = compute(99);
console.log(Array.isArray(output));
```
1. true  
2. false  
3. undefined  
4. Compilation error  
**Answer:** 1
