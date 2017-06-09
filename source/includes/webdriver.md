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
