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


Mini Test App Snippets (to plug into any sandbox)
2.1 Shadow DOM host (simplified)
<app-drawer>
  #shadow-root
    <header><span class="title">Orders Drawer</span></header>
    <section>...</section>
</app-drawer>

2.2 Angular-style table
<table role="grid" class="mat-table">
  <thead><tr><th>Order ID</th><th>Status</th><th>Total</th></tr></thead>
  <tbody>
    <tr><td>O-1001</td><td>Shipped</td><td>₹ 5,600</td></tr>
    <tr><td>O-1002</td><td>Processing</td><td>₹ 2,300</td></tr>
  </tbody>
</table>

2.3 iframe wrapper
<iframe id="content-frame" src="/embedded.html"></iframe>

2.4 React virtualized list (conceptual)
<div class="react-virtualized">
  <div role="row">Item 1</div>
  <div role="row">Item 2</div>
</div>

3) Hard, Code-Based MCQs (tough level) — with options & answers
MCQ-1 (Shadow DOM)

You must click a button inside Shadow DOM:

<order-panel>
  #shadow-root
    <div class="toolbar">
      <button id="approve">Approve</button>
    </div>
</order-panel>


Which Java code correctly clicks Approve?

a) driver.findElement(By.cssSelector("order-panel #approve")).click();
b)

WebElement host = driver.findElement(By.cssSelector("order-panel"));
host.getShadowRoot().findElement(By.cssSelector("#approve")).click();


c)

WebElement host = driver.findElement(By.cssSelector("order-panel"));
host.findElement(By.cssSelector("#approve")).click();


d)

((JavascriptExecutor)driver).executeScript("document.querySelector('#approve').click()");


Answer: b)
Why: Selenium 4 requires getShadowRoot() on the host to pierce shadow boundary.

MCQ-2 (Backward traversal)

HTML:

<div class="field">
  <label>PIN Code</label>
  <div><input id="pin"><button class="act">Validate</button></div>
</div>


Pick an XPath that finds the Validate button by starting from the label text:

a) //label[.='PIN Code']/../button
b) //label[.='PIN Code']/ancestor::div[contains(@class,'field')][1]//button[@class='act']
c) //button[preceding-sibling::label='PIN Code']
d) //label[text()='PIN Code']/following::button[1]

Answer: b)
Why: Go up to nearest .field, then down to the button reliably.

MCQ-3 (Angular infinite scroll + React)

You must ensure “Invoice #500” is visible in a virtualized list (React) that only renders visible rows. Which is most robust?

a)

driver.findElement(By.xpath("//*[text()='Invoice #500']")).isDisplayed();


b)

for(int i=0;i<30;i++){
  if(!driver.findElements(By.xpath("//*[text()='Invoice #500']")).isEmpty()) break;
  ((JavascriptExecutor)driver).executeScript("window.scrollBy(0,700)");
  Thread.sleep(250);
}


c)

new Actions(driver).scrollByAmount(0, 10000).perform();


d)

((JavascriptExecutor)driver).executeScript("document.body.scrollTop=document.body.scrollHeight");


Answer: b)
Why: Progressive scroll with presence check suits virtualized lists.

MCQ-4 (iframe + locator strategy)

You must type into #email that is inside an iframe #auth-iframe. What is correct?

a)

driver.switchTo().frame("auth-iframe");
driver.findElement(By.id("email")).sendKeys("e@x.com");
driver.switchTo().defaultContent();


b)

driver.findElement(By.id("auth-iframe")).sendKeys("e@x.com");


c)

driver.switchTo().frame(driver.findElement(By.id("auth-iframe")));
driver.findElement(By.cssSelector("#email")).sendKeys("e@x.com");
driver.switchTo().parentFrame();


d) Both a and c

Answer: d)

MCQ-5 (Tables: dynamic column by header)

HTML headers change order. Which code reads the cell in row 3 under header “Amount”?

a)

int idx = driver.findElements(By.cssSelector("thead th"))
  .indexOf("Amount") + 1;


b)

List<WebElement> ths = driver.findElements(By.cssSelector("thead th"));
int idx=-1; for(int i=0;i<ths.size();i++) if(ths.get(i).getText().trim().equals("Amount")) { idx=i+1; break; }
String val = driver.findElement(By.xpath("(//tbody/tr)[3]/td["+idx+"]")).getText();


c)

String val = driver.findElement(By.xpath("//td[.='Amount'][3]")).getText();


d)

String val = driver.findElement(By.cssSelector("tbody tr:nth-child(3) td[data-col='Amount']")).getText();


Answer: b)

MCQ-6 (POI modeling — numeric vs string)

You must read a cell that may be numeric or string. Which is safest?

a)

cell.getStringCellValue();


b)

String v = new DataFormatter().formatCellValue(cell);


c)

String v = String.valueOf(cell.getNumericCellValue());


d)

String v = cell.toString();


Answer: b)

MCQ-7 (Log4j2 per-thread logs)

Best way to emit per-thread file logs without separate configs?

a) Use %d in pattern
b) Use ThreadContext.put("threadName", ...) and reference ${ctx:threadName} in appender fileName
c) Use a single RollingFile for all threads
d) Use System.setProperty("thread")

Answer: b)

MCQ-8 (Shadow DOM + nested)

Host inside host:

<shell-root>
 #shadow-root
  <panel-drawer>
   #shadow-root
    <button class="ok">OK</button>
  </panel-drawer>
</shell-root>


Which code clicks OK?

a)

driver.findElement(By.cssSelector("shell-root panel-drawer .ok")).click();


b)

SearchContext s1 = driver.findElement(By.cssSelector("shell-root")).getShadowRoot();
SearchContext s2 = s1.findElement(By.cssSelector("panel-drawer")).getShadowRoot();
s2.findElement(By.cssSelector("button.ok")).click();


c)

((JavascriptExecutor)driver).executeScript("document.querySelector('button.ok').click()");


d)

driver.switchTo().frame("panel-drawer").findElement(By.cssSelector(".ok")).click();


Answer: b)

MCQ-9 (DOM backward axis / sibling precise)

Choose the most stable XPath to hit the edit icon next to the User ID value:

<div class="row">
  <span class="label">User ID</span>
  <span class="value">U-0099</span>
  <button class="edit">✎</button>
</div>


a) //button[@class='edit']
b) //span[text()='User ID']/following-sibling::button[@class='edit']
c) //span[text()='User ID']/parent::div//button[@class='edit']
d) //*[@class='row']//button

Answer: c)
Why: Ties the button to its labeled row; resilient if additional spans appear.

MCQ-10 (React portal + scrolling)

Tooltip content rendered into body via React portal after hover:

<div class="cell" data-id="A1">Amount</div>
<!-- later -->
<div class="portal tooltip">Net Amount: ₹ 7500</div>


To assert tooltip text:

a)

new Actions(driver).moveToElement(driver.findElement(By.cssSelector(".cell[data-id='A1']"))).perform();
new WebDriverWait(driver, Duration.ofSeconds(5))
  .until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(".portal.tooltip")));
String tip = driver.findElement(By.cssSelector(".portal.tooltip")).getText();


b) driver.findElement(By.cssSelector(".portal.tooltip")).getText();
c) driver.findElement(By.cssSelector(".cell[data-id='A1']")).getText();
d) Use alert.getText()

Answer: a)

MCQ-11 (All locator strategies — trick)

You must click only this button:

<button class="cta primary" data-id="save">Save</button>


Pick the most specific locator:

a) By.cssSelector("button.cta.primary[data-id='save']")
b) By.className("cta primary")
c) By.xpath("//button[text()='Save']")
d) By.tagName("button")

Answer: a)

MCQ-12 (Scrolling large Angular grid)

Which approach is best to reliably fetch the last row text in a large, virtualized Angular grid?

a)

((JavascriptExecutor)driver).executeScript("window.scrollTo(0, document.body.scrollHeight)");
driver.findElement(By.cssSelector("table tr:last-child")).getText();


b)

for(int i=0;i<40;i++){
 ((JavascriptExecutor)driver).executeScript("window.scrollBy(0,800)");
 if(!driver.findElements(By.cssSelector("table[role='grid'] .end-flag")).isEmpty()) break;
}
String last = driver.findElement(By.cssSelector("table[role='grid'] tbody tr:last-child")).getText();


c) new Actions(driver).scrollByAmount(0, 999999).perform();
d) driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(60));

Answer: b)
Why: Incremental scroll with a sentinel (e.g., hidden “end-flag”) is reliable for virtualized content.

Answer Key (MCQs 1–12)

b 2) b 3) b 4) d 5) b 6) b 7) b 8) b 9) c 10) a 11) a 12) b
