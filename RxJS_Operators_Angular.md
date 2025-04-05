# Understanding RxJS Operators in Angular

RxJS (Reactive Extensions for JavaScript) is a library for handling asynchronous operations using **observables**. Operators in RxJS help **transform, filter, and manage data streams** effectively.

## 1️⃣ Categories of RxJS Operators

| Category | Description | Example Operators |
|----------|------------|------------------|
| **Creation** | Create new observables | `of()`, `from()` |
| **Transformation** | Modify data emitted by observables | `map()`, `mergeMap()`, `switchMap()` |
| **Filtering** | Emit only specific values | `filter()`, `debounceTime()`, `distinctUntilChanged()` |
| **Combination** | Merge multiple observables | `combineLatest()`, `forkJoin()`, `concat()` |
| **Error Handling** | Handle errors gracefully | `catchError()`, `retry()`, `throwError()` |
| **Utility** | Perform actions on emitted values | `tap()`, `delay()`, `timeout()` |

---

## 2️⃣ Commonly Used RxJS Operators

### 🔹 `of()` Operator
- **Creates an observable** from a sequence of values.
- Emits values one by one and then completes.

✅ **Example:**
```typescript
import { of } from 'rxjs';

const observable$ = of(10, 20, 30);
observable$.subscribe(value => console.log(value));
```
🔹 **Output:**
```
10
20
30
```
- The `of()` operator emits each value separately **in sequence**.

---

### 🔹 `from()` Operator
- Converts **arrays, promises, or iterables** into observables.
- Works well with async data sources.

✅ **Example (Using Array):**
```typescript
import { from } from 'rxjs';

const numbers = [1, 2, 3, 4, 5];
const observable$ = from(numbers);

observable$.subscribe(value => console.log(value));
```
🔹 **Output:**
```
1
2
3
4
5
```
- Each item in the array is emitted **individually**.

✅ **Example (Using Promise):**
```typescript
const promise = new Promise(resolve => resolve("Hello from Promise!"));
const observable$ = from(promise);

observable$.subscribe(value => console.log(value));
```
🔹 **Output:**
```
Hello from Promise!
```
- Emits a **single** value when the promise resolves.

---

### 🔹 `map()` Operator
- Transforms emitted values.

✅ **Example (Transform Data):**
```typescript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

of(5, 10, 15).pipe(
  map(value => value * 2)
).subscribe(result => console.log(result));
```
🔹 **Output:**
```
10
20
30
```
- Each value is **multiplied by 2** before being emitted.

---

### 🔹 `catchError()` Operator
- Handles **errors** and returns an alternative observable.

✅ **Example:**
```typescript
import { throwError, of } from 'rxjs';
import { catchError } from 'rxjs/operators';

const failingObservable$ = throwError(() => new Error('Something went wrong!'));

failingObservable$.pipe(
  catchError(error => {
    console.log('Error caught:', error.message);
    return of('Default Value');
  })
).subscribe(result => console.log(result));
```
🔹 **Output:**
```
Error caught: Something went wrong!
Default Value
```
- Instead of breaking, it **recovers with a default value**.

---

## 3️⃣ Summary

- `of()` → Creates an observable from values.
- `from()` → Converts arrays, promises, or iterables into observables.
- `map()` → Transforms emitted values.
- `catchError()` → Handles errors gracefully.

