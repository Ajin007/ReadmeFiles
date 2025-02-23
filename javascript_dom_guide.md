# JavaScript Concepts and DOM Manipulation

## 📌 JavaScript Basics

### 1️⃣ Keywords
- Reserved words in JavaScript that have special meanings.
- Examples:
  ```js
  var, let, const, if, else, function, return, while, for
  ```

---

### 2️⃣ Identifiers
- Names for variables, functions, objects, or classes.
- **Rules**:
  - Can contain letters, digits, underscores `_`, or dollar signs `$`
  - Cannot start with a number.
  - **Case-sensitive** (`MyVar` is different from `myvar`).

  ```js
  let myVariable = "Hello"; // Correct
  let _name = "John";       // Correct
  let 1name = "Error";      // ❌ Incorrect (Cannot start with a number)
  ```

---

### 3️⃣ Comments
- **Single-line comment:**
  ```js
  // This is a single-line comment
  ```
- **Multi-line comment:**
  ```js
  /*
    This is a multi-line comment
  */
  ```

---

### 4️⃣ Statements & Expressions
- **Statement:** A complete line of code that performs an action.
  ```js
  let x = 10; // Declaration statement
  console.log(x); // Function call statement
  ```
- **Expression:** A piece of code that evaluates to a value.
  ```js
  let sum = 10 + 5; // "10 + 5" is an expression
  ```

---

## 📌 DOM (Document Object Model)

### What is DOM?
- The **DOM is an interface** that represents the **HTML document** as a tree structure.
- **JavaScript can manipulate HTML elements dynamically** using the DOM.

### Common Methods to Access DOM Elements

| Method | Usage |
|--------|-------|
| `document.getElementById("id")` | Selects an element by its `id` |
| `document.querySelector("selector")` | Selects the **first** matching element |
| `document.querySelectorAll("selector")` | Selects **all** matching elements as a `NodeList` |
| `document.getElementsByClassName("class")` | Selects elements by class name |
| `document.getElementsByTagName("tag")` | Selects elements by tag name |

#### Example: Accessing DOM Elements
```js
let element = document.getElementById("myElement");
let firstButton = document.querySelector(".btn");
let allButtons = document.querySelectorAll(".btn");
```

---

## 📌 Why is DOM an Interface?
- The DOM **provides a structured representation** of the document (HTML).
- It acts as a **bridge** between HTML and JavaScript.
- Using the DOM API, **JavaScript can modify the structure, content, and styles of a webpage**.

---

## 📌 DOM Events
- **Events are actions that happen in a webpage** (e.g., clicks, inputs, loads).
- JavaScript can **listen** and **respond** to events.

### Common Events

| Event | Description |
|--------|-------------|
| `click` | Fired when an element is clicked |
| `change` | Triggered when input changes |
| `mouseover` | Triggered when the mouse is over an element |
| `keydown` | Triggered when a key is pressed |

#### Example: Handling a Button Click
```js
document.getElementById("myButton").addEventListener("click", function() {
    alert("Button Clicked!");
});
```

---

## 📌 JavaScript Libraries
- **Libraries provide pre-written JavaScript code** to simplify development.
- Examples:
  - **jQuery** → Simplifies DOM manipulation.
  - **React.js** → Used for building UI components.
  - **Lodash.js** → Utility functions.

#### Example: Using jQuery
```js
$(document).ready(function(){
    $("#myButton").click(function(){
        alert("Button Clicked!");
    });
});
```

---

# 🔹 Simple Webpage: Button & Form Using `appendChild()` & `createElement()`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Manipulation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
          /*
              margin: auto will make the container come centre top...
              margin: 50% auto will make the container centre of the page
            */

        .container {
            width: 50%;
            margin: auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
        }

        ul {
            text-align: left;
            padding: 0;
        }

        ul li {
            list-style-type: none;
            background-color: #f4f4f4;
            margin: 5px 0;
            padding: 10px;
            border-radius: 5px;
        }

        button {
            padding: 10px;
            background-color: rgb(0, 123, 255);
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            margin-top: 10px;
        }

        button:hover {
            background-color: rgb(0, 102, 204);
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Dynamic List Generator</h2>
        
        <label for="itemInput">Enter Item:</label>
        <input type="text" id="itemInput" placeholder="Type something...">
        <button id="addItemBtn">Add Item</button>

        <ul id="itemList"></ul>
    </div>

    <script>
        let button = document.getElementById("addItemBtn");
        let inputField = document.getElementById("itemInput");
        let itemList = document.getElementById("itemList");

        button.addEventListener("click", function() {
            let inputValue = inputField.value.trim();

            if (inputValue !== "") {
                let newItem = document.createElement("li");
                newItem.textContent = inputValue;

                itemList.appendChild(newItem);
                inputField.value = "";
            } else {
                alert("Please enter a valid item.");
            }
        });

        inputField.addEventListener("keypress", function(event) {
            if (event.key === "Enter") {
                button.click();
            }
        });
    </script>

</body>
</html>
```

---

**📌 Key Features**
✅ **Creates a new list item dynamically** on button click  
✅ **Uses `createElement()` and `appendChild()`** to add items  
✅ **Event listeners** handle both button click and "Enter" keypress  
✅ **Styled with CSS** for better UI  

---

**Would you like additional enhancements? 🚀**
