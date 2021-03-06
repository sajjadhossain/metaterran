---
intro: false
featured: false
title:  "Behat Cheat Sheet"
uniqueID: "behatCheatSheet"
description:  "A reference and style guide for Behat and Mink, based on Lepine's and Kudryashov's references and guides."
shortName: "📋 "
banner: "/images/posts/cucumber.jpg"
date: 2014-04-14
tags: ["behat", "automation", "testing", "php", "mink"]
---

## New to Behat?

1. [What is Behavior Driven Development?](/posts/Behavior-Driven-Development-w-Gherkin/)
2. [BDD with Behat and Mink](/posts/Automation-With-Behat-And-Mink/)

<br/>

### Pear

* pear channel-discover pear.symfony.com
* pear channel-discover pear.behat.org
* pear install behat/behat

<br/>

### Command Line

| Command (w/ behat) | Purpose |
| --- | --- |
| --init | Create the features directory |
| --config={file}.yml | Use config file |
| --format=html –out=report.html | Html Report |
| --expand | Display details |
| --story-syntax --lang=fr | in French |
| --tags='@{tag1},@{tag2}' | Run tags |

<br/>

### Features

```gherkin
Feature: Descriptive text of what is desired

  In order to realize a named business value
  As an explicit system actor
  I want to ...

    Scenario: Some determinable business situation

      Given some precondition
      And some other precondition
      When some action by the actor
      And some other action
      And yet another action
      Then some testable outcome is achieved
      And something else we can check happens too
      Scenario: A different situation
```

<br/>

### Using Examples

```gherkin
Scenario Outline: Some determinable business situation

  Given I have <initialAmount> euros
  When I add <money> euros
  Then I should have now <finalAmount> euros

  Examples:
  | initialAmount | money | finalAmount |
  | 15 | 5 | 20 |
  | 40 | 10 | 50 |
  | 20 | 5 | 25 |
```

<br/>

### Surf Actions

```gherkin
I am on "url"
I go to "url"
I reload the page
I move backward one page
I move forward one page
I press "button"
I follow "link"
```

<br/>

### Forms

```gherkin
I fill in "form_element" with "value"
I fill in "value" for "form_element"
I fill in the following
I select "form_option" from "form_select"
I additionally select "form_option" from "form_select"
I check "form_checkbox"
I uncheck "form_checkbox"
I attach the file "/path/file.file" to "form_file"
```

<br/>

### Assertions

```gherkin
I should see "content"
the response should contain "content"
I should not see "content"
the response should not contain "content"
the "form_element" field should contain "value"
the "form_element" field should not contain "value"
the "form_checkbox" checkbox should be checked
the "form_checkbox" checkbox should not be checked
I should be on "page"
the url should match "url"
the "num_position" element should contain "value"
I should see "value" in the "element" element
I should see an "element" element
I should not see an "element" element
I should see number "element" elements
the response status code should be code
```

<br/>

### Mink

* pear channel-discover pear.symfony.com
* pear channel-discover pear.behat.org
* pear install behat/mink-beta

<br/>

### Session

```php
$session = new \Behat\Mink\Session($driver);
$session->start(); // start
$session->reset(); // soft-reset:
$session->restart(); // hard-reset:
```

#### From the main context

```php
$session = $this->getSession();
```

#### From a sub-context

```php
$session = $this->getMainContext()->getSession();
```

| Step Definition | Purpose |
| --- | --- |
| isStarted() | Checks whether session was started |
| start() | Starts session |
| stop() | Stop session |
| restart() | Restart session|
| reset() | Reset session |
| getPage() | Returns page element |
| getSelectorHandler() | Returns Selector Handler |
| visit($url) | Visit specified URL |
| setBasicAuth($u,$p) | HTTP Basic authentification |
| setRequestHeader($n,$v) | Set request header |
| getResponseHeaders() | Get all response headers |
| setCookie($n,$v) | Sets cookie |
| getCookie($n) | Returns cookie |
| getStatusCode() | Returns response code |
| getCurrentUrl() | Returns current URL |
| reload() | Reload current page |
| back() | Moves backward |
| forward() | Move forward |
| executeScript($script) | Executes javascript |
| evaluateScript($script) | Returns javascript' response |
| wait($time, $condition) | Waits some time or until javascript condition is true |

### Elements

```php
$el->has($selector, $locator)
$el->find($selector, $locator)
$el->findAll($selector, $locator)
$el->getText()
$el->getHtml()
```

### HTML Nodes

```php
$el->isVisible()
$el->getValue()
$el->getTagName()
$el->getXpath()
$el->hasAttribute($name)
$el->getAttribute($name)
```

### Forms

```php
$el->press()
$el->check()
$el->uncheck()
$el->isChecked()
$el->selectOption($option, $multiple)
$el->attachFile($path)
$el->keypress()
$el->keyDown()
$el->keyUp()
```

### Events

```php
$el->click()
$el->doubleClick()
$el->rightClick()
$el->mouseOver()
$el->focus()
$el->blur()
$el->dragTo($element)
```

### Default behat.yml Configurations

```yaml
default:
  context:
    parameters:
      default_session: goutte
      javascript_session: sahi
      base_url: http://localhost
      browser: firefox
      goutte:
        zend_config:
          adapter: Zend\Http\Client\Adapter\Proxy
          proxy_host: host.com
          proxy_port: 8080
        sahi:
          host: localhost
          port: 9999
        zombie:
          host: 127.0.0.1
          port: 8124
          node_bin: node
          auto_server: true
        selenium:
          host: localhost
          port: 4444
        webdriver:
          host http://localhost:4444/wd/hub
```

### Available Drivers

1. [Goutte](https://github.com/fabpot/Goutte)
2. [Sahi](http://sourceforge.net/projects/sahi/)
3. [Zombie](http://zombie.labnotes.org/)
4. [Selenium (1 & 2 )](http://seleniumhq.org/)
