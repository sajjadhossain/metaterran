---
intro: true
featured: false
uniqueID:  "bddWGherkin"
title: "Behavior Driven Development with Gherkin"

shortName: "⚠️"
banner: "/images/posts/cucumber.jpg"
date: 2014-07-14
tags: ["behat", "testing", "automation", "gherkin"]
---



The idea is simple, write your tests first, and then write code until your tests pass. It helps clarify your goals before you spend time developing. You also know that as soon as your tests all pass, you should stop working! This makes it harder to over-perfect your code.


>Behavior is a more useful word than test. - Dan North

Writing tests is great, but before we do any work, we need to understand the exact behavior of the feature we're building.

1. `Define` the business value of the features
2. `Prioritize` features by their business value
3. `Describe` them with readable scenarios
4. `Implement` them.

But I've used this countless times to break a big idea into smaller pieces written in clear language. And for a developer, getting clear directions rocks!

Ok, all the theory is behind us, let's get to Gherkin, the language of BDD!

## Gherkin







```gherkin
Feature: <custom title>
  In order to <benefit or value of the feature>
  As a <user or role who will benefit from this feature>
  I need to <short feature description>
```



First, the `In order` to line defines the value. Why should we build this feature? Why is it important? Will it bring us more visitors or keep those visitors safe from dinosaur attack? The next line - starting with As a defines who will benefit from this value. Is it the admin user? Our normal web user? A defenseless park guest? If you have a hard time writing these first two lines, it's possible that this feature just isn't a good idea. After all, if we're going to spend time and money building something, shouldn't it have some value for a specific person?

`I need to` - is a short description of the types of actions the user will be able to take once this feature is complete.



```gherkin
Feature: News admin panel
  In order to maintain a list of news
  As a site administrator
  I need to be able to add/edit/delete news
```









```gherkin
Feature: News admin panel
  Scenario: List available news
```



The first is `Given`, which describes the initial state of the system for the scenario. This is the only place where you can describe things that he user can't do. In this case, the "site administrator" can't magically put 5 news entries in the database, but that's ok. To have more than one `Given` statement, start the next line with `And`.

Each line in the scenario is called a "step", and should plainly describe what the user is doing and seeing.

```gherkin
Feature: News admin panel
  Scenario: List available feeds
  ...
  Scenario: List available news
    Given there are 5 news articles
    And I am on "/admin"
    When I click "News"
    Then I should see 5 news items
```

If we didn't go any further, we would at least have a standard way of describing our features. Writing scenarios also makes you think through each feature in more detail. When you're finished, you've got a blueprint for exactly what you need to develop, written in language that your client can understand.