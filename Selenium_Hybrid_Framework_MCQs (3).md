# Selenium Hybrid Framework MCQ Set (with HTML/CSS/JS Scenarios)

## 🧩 Section 1 – Selenium + Java + Hybrid Framework (Concept + Scenario)

### Q1
**Which of the following annotations allows grouping multiple test methods in TestNG?**
- a) @type
- b) @groups
- c) @grouping
- d) @category
**✅ Answer:** b) @groups  
**Explanation:** The `groups` attribute in TestNG lets you categorize test methods and execute selected groups.

---

### Q2
**What is the primary purpose of the Actions class in Selenium?**
- a) To manage browser sessions
- b) To store configuration files
- c) To perform complex user gestures like mouse movements and clicks
- d) To verify test results  
**✅ Answer:** c)  
**Explanation:** The `Actions` class is used for advanced user interactions such as drag-and-drop, hover, or double-click.

---

### Q3 (HTML based)
```html
<input id="username123" type="text">
```
Which XPath correctly locates this element?
- a) //input[@id=starts-with('user')]
- b) //input[@id*='user']
- c) //input[starts-with(@id,'user')]
- d) //input[start(@id,'user')]
**✅ Answer:** c)

---

### Q4
**Which Java method loads a `.properties` file for reading?**
- a) load(File file)
- b) load(InputStream inputStream)
- c) parse(InputStream)
- d) read(File file)
**✅ Answer:** b)

---

### Q5 (Scenario + WebDriver)
```html
<input type="radio" id="male" name="gender">
```
Which WebDriver method selects the radio button?
- a) select()
- b) choose()
- c) click()
- d) check()
**✅ Answer:** c)

---

### Q6
**What is Page Factory in Selenium?**
- a) A debugging tool
- b) A report generator
- c) A design pattern that initializes page objects using annotations
- d) A visual test result viewer  
**✅ Answer:** c)

---

### Q7
**Which method runs automatically when a test fails?**
- a) OnFailureStart
- b) onFailure
- c) onTestFailure
- d) onTestFails  
**✅ Answer:** c)

---

### Q8
**What does assertTrue(boolean condition) verify?**
- a) That condition is a number
- b) That condition is false
- c) That condition is true
- d) That condition is a string  
**✅ Answer:** c)

---

### Q9 (Hybrid Framework + Apache POI)
```java
driver.findElement(By.id("input"));
inputField.sendKeys(sheet.getRow(1).getCell(0));
sheet.getRow(1)getCell(0)
```
Which line is incorrect?
- a) Line 1
- b) Line 2
- c) Line 3
- d) All lines  
**✅ Answer:** c)

---

### Q10
**How can TestNG reports be analyzed for failures?**
- a) Manually check console output
- b) Use the generated HTML report with stack traces and screenshots
- c) Use custom listeners to re-run failed tests
- d) Inspect browser logs  
**✅ Answer:** b)

---

## 🧩 Section 2 – Selenium + XPath + Waits (Intermediate Level)

### Q1
**XPath axis selecting siblings after current node?**
- a) preceding-sibling
- b) following-sibling
- c) ancestor
- d) descendant  
**✅ Answer:** b)

---

### Q2 (HTML Table Code)
```html
<table id="users">
<tr><td>John</td></tr>
<tr><td>Mary</td></tr>
<tr><td>David</td></tr>
</table>
```
How do you count rows using WebDriver?
- a) getRowCount()
- b) getSize()
- c) findElements(By.tagName("tr")).size()
- d) getRowSize()  
**✅ Answer:** c)

---

### Q3
**Main purpose of moveToElement() in Actions class?**
- a) Double-click on element
- b) Move mouse to a specific element
- c) Anchor at fixed coordinate
- d) Combine drag-and-drop  
**✅ Answer:** b)

---

### Q4 (HTML Scenario – Links)
```html
<a href="https://www.google.com">Google</a>
```
Which WebDriver method clicks the hyperlink?
- a) clickLink()
- b) click()
- c) navigate()
- d) openLink()  
**✅ Answer:** b)

---

### Q5
**Method to retrieve alert text?**
- a) alert.getText();
- b) alert.readText();
- c) alert.fetchText();
- d) alert.retrieveText();  
**✅ Answer:** a)

---

### Q6 (DataProvider Concept)
```java
@DataProvider(name="numbers")
public Object[][] data() {
   return new Object[][]{{1},{2},{3}};
}

@Test(dataProvider="numbers")
public void printNum(int n) {
   System.out.print(n + " ");
}
```
Output is?
- a) 1 2 3 4
- b) 1 2 3
- c) {1} {2} {3}
- d) Exception  
**✅ Answer:** b)

---

## 🧩 Section 3 – Advanced Hybrid Framework + Log4j + Waits

### Q1
**You are running tests in parallel and want a log file per thread. What should you configure in log4j?**
- a) Use ThreadContext or %t to include thread name in log file pattern
- b) Single shared log file
- c) Separate log4j file per thread
- d) Hard-code thread name  
**✅ Answer:** a)

---

### Q2 (HTML Menu Structure)
```html
<ul class="menu">
 <li>Home</li>
 <li>About</li>
 <li>Contact</li>
</ul>
```
XPath to get all `<li>` containing “Home”?
- a) //ul[@class='menu']/descendant::li[text()='Home']
- b) //ul[@class='menu']//li[text()='Home']
- c) //ul[@class='menu']//li[contains(text(),'Home')]
- d) //ul[@class='menu']//li[normalize-space(text())='Home']  
**✅ Answer:** b)

---

### Q3
**To capture a table cell’s displayed text:**
- a) getAttribute("value")
- b) getText()
- c) getContent()
- d) innerText()  
**✅ Answer:** b)

---

### Q4
**Which wait allows setting maximum time + polling interval?**
- a) Implicit Wait
- b) Explicit Wait
- c) Fluent Wait
- d) WebDriverWait  
**✅ Answer:** c)

---

## 🌐 Mini HTML / CSS / JS Code Examples

### Example 1 – Button Click and Verify Text
```html
<button id="btn">Click Me</button>
<p id="msg"></p>
<script>
document.getElementById("btn").onclick = function(){
 document.getElementById("msg").innerText = "Button Clicked!";
};
</script>
```
Which locator retrieves the text “Button Clicked!”?
- a) By.id("msg").getText()
- b) By.id("btn").getText()
- c) By.className("msg").getText()
- d) By.tagName("p").click()  
**✅ Answer:** a)

---

### Example 2 – Login Form Validation
```html
<form>
 <input id="user" type="text">
 <input id="pass" type="password">
 <input id="loginBtn" type="submit" value="Login">
</form>
```
To enter username via WebDriver:
- a) driver.findElement(By.id("user")).sendKeys("admin");
- b) driver.findElement(By.name("user")).sendKeys("admin");
- c) driver.findElement(By.className("user")).sendKeys("admin");
- d) driver.findElement(By.tagName("input")).sendKeys("admin");  
**✅ Answer:** a)

---

### Example 3 – CSS Selector Test
```html
<div class="card"><p>Hello Selenium!</p></div>
```
Which CSS selector finds the paragraph inside card?
- a) .card p
- b) #card p
- c) div#card p
- d) p.card  
**✅ Answer:** a)

---

### Example 4 – Hybrid Framework Scenario
You’re integrating **Page Objects + Data Driven + Reports**.  
Which component handles Excel input for multiple test data?
- a) Page Object Class
- b) DataProvider Class using Apache POI
- c) ExtentReport Class
- d) TestListener  
**✅ Answer:** b)
