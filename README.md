# Selenide quick FAQ.
- Should one restart a browser for each test? What is the best practice?
[Here](https://youtu.be/ePvrXUCeAr8?t=2306). Subtitles available.


- How does one use Jenkins with Selenide?
[Here](https://www.youtube.com/playlist?list=PLeeLZATMBcD8ayVX7VpYg-fLYG1dueL4Y). Subtitles available.

- How to clean browser cache and storage without restarting it?
```
@BeforeEach void resetBrowser() {
  Selenide.clearBrowserCookies();
  Selenide.clearBrowserLocalStorage();
}
```
- Is there a simple working example I can refer to?
[Yup.](https://github.com/selenide-examples/google)
- This is such a great project. How can I help?
  Yes. Raise awareness.

## Some of the most commonly used functions.

How to open a page:
```
@Test
public void someTest() {
    open("https://www.google.kz/");
}
```
How to change / set a browser in code?
(before open() method):
```
Configuration.browser = "firefox";
```
How to change / set a browser using system property?
``` 
-Dselenide.browser=edge
```

How to open a page in a new tab :
```
executeAsyncJavaScript("window.open(\"http://www.amazon.com\");");
```
How to switch between tabs :
```
???
```
How to make a screenshot?
```
// Set the screenshot folder in your code
Configuration.reportsFolder = "test-result/screenshots"; 
String pngFileName = screenshot("my_screenshot_file_name");
```

Click page element (in this case found by Xpath):
```
element(Selectors.byXpath("//*[contains(text(),'Some text on the button')]")).click();
```

Check if page element exists (in this case is visible):
```
element(Selectors.byXpath("//h2[contains(., 'Some visible text in an h2 text')]"))
.shouldBe(Condition.visible);
```

Launch specific or headless browser:
```
-Dselenide.headless=false
```

URL manipulations:
```
Selenide.open("https://www.google.kz/");
String url1 = WebDriverRunner.url();
String url2 = WebDriverRunner.currentFrameUrl();
```
Check url contents:
```
webdriver().shouldHave(url("https://auth.google.com"));
webdriver().shouldHave(url("https://mastercard.ee"), Duration.ofSeconds(42));
webdriver().shouldNotHave(url("http://yandex.ru");
webdriver().shouldNotHave(urlStartingWith("ftp://"));
webdriver().shouldHave(currentFrameUrl(baseUrl + "/login.html"));
webdriver().shouldHave(currentFrameUrlStartingWith(baseUrl + "/logout.html"));
```
Clipboard:
```
Clipboard clipboard = Selenide.clipboard();
String foo = clipboard().getText();
clipboard().setText("bar");
```
Check clipboard contents:
```
clipboard().shouldHave(content("Hello fast World"));
clipboard().shouldHave(content("Hello slow World"), Duration.ofMillis(1500));
```
Check local storage:
```
localStorage().shouldHave(item("cat”));
localStorage().shouldHave(itemWithValue("mouse", "Jerry”));
localStorage.getItems();
```
Check session storage:
```
sessionStorage().shouldHave(item("cat”));
sessionStorage().shouldHave(itemWithValue("mouse", "Jerry”));
Map<String, String> items = sessionStorage.getItems();
```