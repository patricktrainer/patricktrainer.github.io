---
date: '2023-02-16'
draft: false
title: Front-Controller-Microsoft-Docs
---

# Front-Controller-Microsoft-Docs

You have reviewed the *[Page Controller](https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff649595%28v%3dpandp.10%29)* pattern, but your page controller classes have complicated logic, are part of a deep inheritance hierarchy, or your application determines the navigation between pages dynamically based on configurable rules.
The following forces might persuade you to use *Front Controller* as opposed to *Page Controller*:
A common implementation of *Page Controller* involves creating a base class for behavior shared among individual pages.
Because *Page Controller* is implemented with a single object per logical page, it is difficult to consistently apply a particular action across all the pages in a Web application.
When implemented with *Page Controller*, the optional pages would have to be implemented with conditional logic in the base class to select the next page.
## Solution
*Front Controller* solves the decentralization problem present in *Page Controller* by channeling all requests through a single controller.
As described in the *Page Controller* pattern, testing the controller may be hindered by the fact that the controller contains code that makes it dependent on the HTTP run-time environment.
*Page Controller* has a single controller object per page as opposed to the single object for all requests.
