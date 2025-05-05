
# Java `Scanner` Class and Inherited Methods Explained

This guide explains how to use the `java.util.Scanner` class and also demonstrates methods inherited from the `Object` class in Java.

---

## 1. ✅ Basic Usage of `Scanner`

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter your name: ");
        String name = sc.nextLine();
        System.out.println("Hello, " + name);
        sc.close();
    }
}
```

---

## 2. 🔍 Important Methods in `Scanner`

### `useDelimiter(String pattern)`

```java
Scanner sc = new Scanner("apple,banana,grape");
sc.useDelimiter(",");
while (sc.hasNext()) {
    System.out.println(sc.next());
}
```

---

### `skip(String pattern)`

```java
Scanner sc = new Scanner("Age: 30");
sc.skip("Age: ");
int age = sc.nextInt();
System.out.println("Age is " + age);
```

---

### `close()`

```java
sc.close(); // Closes the scanner
```

---

### `useLocale(Locale locale)`

```java
Scanner sc = new Scanner("1234,56");
sc.useLocale(Locale.GERMANY);
double num = sc.nextDouble();
System.out.println(num);
```

---

### `reset()`

```java
sc.useDelimiter(",");
sc.reset();  // back to default delimiter
```

---

### `nextBigInteger()`

```java
Scanner sc = new Scanner("99999999999999999999999999");
BigInteger big = sc.nextBigInteger();
System.out.println("Big number: " + big);
```

---

### `remove()`

```java
// Not supported: throws UnsupportedOperationException
```

---

### `IOException`

Use try-catch for methods like `nextLine()` or `close()`:

```java
try {
    Scanner sc = new Scanner(System.in);
    sc.nextLine();
    sc.close();
} catch (Exception e) {
    e.printStackTrace();
}
```

---

## 3. 🧠 Inherited from `Object` Class

### `toString()`

```java
System.out.println(sc.toString());
```

---

### `equals(Object obj)`

```java
System.out.println(sc1.equals(sc2));
```

---

### `finalize()`

```java
@Override
protected void finalize() throws Throwable {
    System.out.println("Scanner is being garbage collected");
}
```

---

### `getClass()`

```java
System.out.println(sc.getClass());
```

---

### `hashCode()`

```java
System.out.println(sc.hashCode());
```

---

### `notify()`, `notifyAll()`, `wait()` - For Threading

```java
synchronized (sc) {
    sc.wait();
    sc.notify();
    sc.notifyAll();
}
```

---

## ✅ Summary Table

| Method         | Purpose                                          |
|----------------|--------------------------------------------------|
| useDelimiter   | Set a new delimiter pattern                      |
| skip           | Skip a pattern                                   |
| close          | Close the scanner                                |
| useLocale      | Change number parsing locale                     |
| reset          | Reset scanner to initial state                   |
| nextBigInteger | Read large integers                              |
| remove         | Unsupported                                       |
| toString       | Print object info                                |
| equals         | Check object equality                            |
| finalize       | Clean up before GC (deprecated)                  |
| getClass       | Get class type                                   |
| hashCode       | Get hash value                                   |
| notify/wait    | Thread coordination (not usual for Scanner)      |

---
