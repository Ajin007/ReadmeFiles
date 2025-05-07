
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

# Java Locale Usage with Examples

This document explains how to use `Locale` in Java for handling culture-specific formats in real-world applications. It covers number formatting, currency, date formatting, and language localization.

---

## ✅ 1. Number Formatting with Locale

### India vs US

```java
import java.text.NumberFormat;
import java.util.Locale;

public class NumberLocaleDemo {
    public static void main(String[] args) {
        double amount = 1234567.89;

        NumberFormat indiaFormat = NumberFormat.getInstance(new Locale("en", "IN"));
        NumberFormat usFormat = NumberFormat.getInstance(Locale.US);

        System.out.println("India Format: " + indiaFormat.format(amount)); // 12,34,567.89
        System.out.println("US Format: " + usFormat.format(amount));       // 1,234,567.89
    }
}
```

---

## ✅ 2. Currency Formatting with Locale

### India vs Germany

```java
import java.text.NumberFormat;
import java.util.Locale;

public class CurrencyLocaleDemo {
    public static void main(String[] args) {
        double price = 29999.99;

        NumberFormat inr = NumberFormat.getCurrencyInstance(new Locale("en", "IN"));
        NumberFormat eur = NumberFormat.getCurrencyInstance(Locale.GERMANY);

        System.out.println("Price in INR: " + inr.format(price)); // ₹29,999.99
        System.out.println("Price in EUR: " + eur.format(price)); // 29.999,99 €
    }
}
```

---

## ✅ 3. Date Formatting with Locale

### US vs France

```java
import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;

public class DateLocaleDemo {
    public static void main(String[] args) {
        Date today = new Date();

        DateFormat usDate = DateFormat.getDateInstance(DateFormat.FULL, Locale.US);
        DateFormat frDate = DateFormat.getDateInstance(DateFormat.FULL, Locale.FRANCE);

        System.out.println("US Date: " + usDate.format(today));   // Monday, May 5, 2025
        System.out.println("France Date: " + frDate.format(today)); // lundi 5 mai 2025
    }
}
```

---

## ✅ 4. Message Translation using ResourceBundle

### Step 1: Create Properties Files

**messages_en.properties**
```
greeting=Hello!
```

**messages_fr.properties**
```
greeting=Bonjour!
```

### Step 2: Java Code

```java
import java.util.*;

public class LocaleMessageDemo {
    public static void main(String[] args) {
        Locale en = new Locale("en");
        Locale fr = new Locale("fr");

        ResourceBundle bundleEN = ResourceBundle.getBundle("messages", en);
        ResourceBundle bundleFR = ResourceBundle.getBundle("messages", fr);

        System.out.println("EN: " + bundleEN.getString("greeting")); // Hello!
        System.out.println("FR: " + bundleFR.getString("greeting")); // Bonjour!
    }
}
```

---

## ✅ 5. Using Locale with Scanner

```java
import java.util.*;

public class ScannerLocaleExample {
    public static void main(String[] args) {
        String input = "1234,56";
        Scanner sc = new Scanner(input);
        sc.useLocale(Locale.GERMANY); // uses comma as decimal separator
        double value = sc.nextDouble();
        System.out.println("Parsed: " + value);  // 1234.56
        sc.close();
    }
}
```

---

## 🧠 Summary Table

| Feature           | Locale Customization                             |
|-------------------|--------------------------------------------------|
| Number Format     | Controls grouping separators                     |
| Currency Format   | Sets currency symbol, decimal/grouping formats   |
| Date Format       | Customizes date ordering and names               |
| Language Support  | Switches text/messages via resource bundles      |
| Scanner Parsing   | Parses input correctly based on locale rules     |

---
### usage of the String.format() methods :

``` Java
    // Below given is the String
    public static String format(Locale locale, String form, Object… args);
    public static String format(String format, Object… args);

    //Exceptions possible
    NullPointerException:If the format is null.
    IllegalFormatException:If the format specified is illegal or there are insufficient arguments

    // Format Specifiers in the java
    //Escape sequence in the java:
        \t ----> inserts a tab
        \b ---> inserts a backspace
        \n ----> inserts a new line
        \r ---> cariage return .()
        \f ----> form feed
        \' ---> inserts a single quote
        \" ---> inserts a double quote
        \\ ----> inserts a backslash
        \ ---> backslah avoid the compile-time error

