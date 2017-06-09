# Selenium WebDriver

## Refresh a Page
In Selenium Web Driver, if you want to refresh the current page, you can use the refresh() method as shown below.

```java
driver.nagivate().refresh();
```

Also there are 3 other ways to refresh the page as shown below.

### By sending F5 key to refresh the browser

```java
driver.findElement(By.tagName("body")).sendKeys(Keys.F5);
```

### To navigate to the same URL

```java
driver.navigate().to(driver.getCurrentUrl());
```

### Open the page again

```java
driver.get(driver.getCurrentUrl());
```

The difference between navigate().to() and get() method is that to() will not wait for the page to finish loading. But get() method will wait for the page to load.

## Javascript Executor

### Changing attributes using JavaScript

Previously, we saw how to execute JavaScript code from Web Driver. If you have not checked it before, check it now here.

JavascriptExecutor can also modify your element's property. It's just the same JavaScript code but you have them run via Selenium.

For example, the below code changes the value of a textbox. It's the equivalent of using sendKeys() method on the WebElement object.

```java
JavascriptExecutor js = (JavascriptExecutor) driver;
 
js.executeScript("document.getElementsByName('childrens')[0].setAttribute('value', 'Child1');");
```

**Arguments for JavaScript execution**:

In the above examples, we saw executing some simple JavaScript statements. In some cases, we might need to pass some dynamic values to the script. For those instances, we can pass the values as arguments to the script executor.

You can provide multiple arguments and in the script the values are taken based on the subscript.

```java
WebElement element = driver.findElement(By.id("username"));
js.executeScript("arguments[0].val='Sherlock'", element);
```

In the above example, the value “arguments[0]” represents the first argument provided, which is “element” in this case. To further explain, we have the below example.

```java
WebElement element = driver.findElement(By.id("username"));
js.executeScript("arguments[0].val='arguments[1]'", element,"Shelock");
```

### Executing JavaScript from Selenium

Just like the drivers for Firefox, Chrome, IE and etc, Selenium provides driver for JavaScript too. Don't be surprised if we tell you can write your tests even in JavaScript. But that's different story.

For now, let us see how to execute some JavaScript code using Selenium Web Driver. To start, we will execute a JavaScript snippet to throw an alert window with some message.

```java
WebDriver driver = new FirefoxDriver();
 
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("alert('Hello Selenium');");
```

For advanced users, the same above code can be rewritten in a single line.

```java
WebDriver driver = new FirefoxDriver();
 
((JavascriptExecutor) driver).executeScript("alert('Hello Selenium');");
```

From this, we understand that we can execute any JavaScript code by passing it as argument to the executeScript() method.

Of-course you can do more with the JavascriptExecutor and not just throwing some alert. You can have the script return some values back to you and do anything that you can do with JavaScript.

The below example just returns a numerical value.

```java
WebDriver driver = new FirefoxDriver();
JavascriptExecutor js = (JavascriptExecutor) driver;
Long value = js.executeScript("return 1;");
```

You would have noticed that we use Long type to get the returned value. Its because based on the returned value, Selenium will have the object created. Let's see an example for all the possible return values.

**For non-decimal numbers:**

```java
Long value = js.executeScript("return 1;");
```

**For decimal numbers:**

```java
Double value = js.executeScript("return 1.465;");
```

**For string values:**

```java
String value = js.executeScript("return 'hello';");
```

**For HTML element:**

```java
WebElement value = js.executeScript("return document.getElementById('username');");
WebElement value = js.executeScript("return $('#username');");
```

**For HTML element array:**

```java
List<WebElement> value = js.executeScript("return $('.multiple-div');");
```

So in general, its going to return a value of type Object. It's fine to capture the return value as below if you are not aware of the return type.

```java
Object value = js.executeScript("return variable;");
```

## Handling Textboxes

## Handling Selectbox

Select boxes or dropdown boxes are very common web component used in almost all web pages. It helps to group large set of data for easy presentation and selection.

Selenium provides an easy way to deal with select boxes. Now let us play with the sample application available in https://the-internet.herokuapp.com/dropdown to see it in action.

If you look at the source of the dropdown using your browser's developer console, you will see the below DOM.

```html
<select id="dropdown">
      <option value="" disabled="disabled" selected="selected">Select value</option>
      <option value="1">Option 1</option>
      <option value="2">Option 2</option>
</select>
```

In the above code you see that the dropdown selectbox has 3 options. We will analyze one of them to understand how to make the best of it.

```java
<option value="1">Option 1</option>
```

The text "Option 1" will be the visible text in the application and the value attribue "1" is the key value stored internally for business logic.

As you know now it's easy to get the WebElement of the dropdown box using the id value. Here is the code.

```java
WebElement element = driver.findElement(By.id("dropdown"));
 
Select dropdownBox = new Select(element);
```

Or simply, you can use the below single line of code too.

```java
Select dropdownBox = new Select(driver.findElement(By.id("dropdown")));
```

We can select the values from the dropdown box in 3 different ways.

**By using the visible text:**

```java
dropdownBox.selectByVisibleText("Option 1");
```

**By using the key value:**

```java
dropdownBox.selectByValue("1");
```

**By using the index:**

```java
dropdownBox.selectByIndex(1);
```

This will select the option from the index position of 1.

Note: This code will work only if the HTML dropdown box is based on <select> tags. There are some other dropdown boxes created using <ul> tags with jQuery. This will not work wtih those type of dropdown box.
