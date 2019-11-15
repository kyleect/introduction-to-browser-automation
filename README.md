# Introduction to Browser Automation

## Agenda

Part One

- What Is Browser Automation?
- HTML
- CSS Selectors
- Setup

Part Two

- Webdriver
- Writing Your First Test
- Page Objects
- Questions

## Introduction

- Software and Quality Engineer at Source Allies
- Director of Education for DAQAA
- Hobbies
  - Writing open source test tools/libraries
  - Synthesizers
  - Cooking

### Social

- [twitter.com/testingrequired](https://twitter.com/testingrequired)
- [github.com/testingrequired](https://github.com/testingrequired)
- [testingrequired.com](https://www.testingrequired.com/)

### Links

- https://testingrequired.github.io/selector-display/
- https://exampletest.app/

## What Is Browser Automation?

Browser automation is the scripted control of a web browser. This includes navigation (go to url, refresh page, go back/forward), location elements, performing actions and waiting for application state (elements appear/disappear, title or url changes).

While browser automation is generally associated with automated testing it has many other uses such as data scraping, data entry, downloading reports or any other task performed through a web interface.

This workshop is going to focus on test automation.

## HTML

HTML is a language for structuring a web page or application. This structure is known as the document. The document is a tree comprised of many elements.

### Elements

Elements are the building blocks of an HTML document. An element has many properties: `tag`, `attributes`, `children`.

```html
<textarea name="description">Type a description</textarea>
```

- https://testingrequired.github.io/selector-display/?share=example-html-element

#### Tag

An element's tag defines what kind of element it is. In this case the tag is `textarea`. Different tags will have different attributes and behaviors.

##### Self Closing

Some tags can or must be defined as self closing. This means it has no children and has a slightly different syntax.

```html
<input type="text" />
```

- https://testingrequired.github.io/selector-display/?share=example-html-element-selfclosing

##### Common Tags

[`div`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div), [`p`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p), [`a`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a), [`ul`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul), [`input`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

#### Classes

Element classes are identifiers that can be applied to one or more elements in the document. Elements can have one or more classes defined at the same time.

```html
<a href="#" class="food vegetable" id="corn">Corn</a>
<a href="#" class="food vegetable" id="carrot">Carrot</a>
<a href="#" class="food fruit" id="apple">Apple</a>
```

- https://testingrequired.github.io/selector-display/?share=example-html-class

The class `vegetable` is defined two of the elements and the `food` class is defined on all three elements.

- https://testingrequired.github.io/selector-display/?share=example-html-class-vegetable
- https://testingrequired.github.io/selector-display/?share=example-html-class-food

#### Ids

Element ids are identifiers applied to only one element in a document.

```html
<a href="#" class="food vegetable" id="corn">Corn</a>
<a href="#" class="food vegetable" id="carrot">Carrot</a>
<a href="#" class="food fruit" id="apple">Apple</a>
```

- https://testingrequired.github.io/selector-display/?share=example-html-id

The three elements each have a unique id: `corn`, `carrot` and `apple`. All element id's should be unique within the document. This is not a hard and fast rule as most browsers will be perfectly fine with duplicate ids.

```html
<a href="#" class="food vegetable" id="corn">Corn</a>
<a href="#" class="food vegetable" id="carrot">Carrot</a>
<a href="#" class="food fruit" id="apple">Apple</a>
<a href="#" class="food fruit" id="apple">Fuji Apple</a>
```

- https://testingrequired.github.io/selector-display/?share=example-html-id-duplicate

#### Malformed

HTML is designed to be flexible. Browsers will do their best when parsing HTML and can infer things like missing end tags for elements.

```
<ul>
  <li>Cat
  <li>Dog
</ul>
```

### Tree

Elements are structured as a tree where this is a root element with many levels of nesting. Each element being the parent of elements nested inside.

```html
<form>
  <textarea name="description">Type a description</textarea>
  <button>Submit</button>
</form>
```

- https://testingrequired.github.io/selector-display/?share=example-html-tree

Here `form` is the parent and `button` is the sibling of the `textarea`.

## CSS Selectors

- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors

### Types

#### Universal

> Selects all elements. Optionally, it may be restricted to a specific namespace or to all namespaces.

https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors

Example: `*`

- https://testingrequired.github.io/selector-display/?share=example-css-selector-universal

#### Type

> Selects all elements that have the given node name.

https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors

Example: `p`

```html
<section>
  <p>Quick brown fox</p>
  <p>Jumped over the lazy dog</p>
</section>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-type

#### Class

> Selects all elements that have the given class attribute.

https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors

Example: `.description`

```html
<div id="car">
  <p class="description">Car</p>
  <img src="car.png" />
</div>

<div id="truck">
  <p class="description">Truck</p>
  <img src="truck.png" />
</div>

<div id="bike">
  <p class="description">Bike</p>
  <img src="bike.png" />
</div>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-class

#### Id

> Selects an element based on the value of its id attribute. There should be only one element with a given ID in a document.

https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors

```html
<div id="car">
  <p class="description">Car</p>
  <img src="car.png" />
</div>

<div id="truck">
  <p class="description">Truck</p>
  <img src="truck.png" />
</div>

<div id="bike">
  <p class="description">Bike</p>
  <img src="bike.png" />
</div>
```

Example: `#bike`

- https://testingrequired.github.io/selector-display/?share=example-css-selector-id

#### Attribute

> The CSS attribute selector matches elements based on the presence or value of a given attribute.

https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors

Example `input[type=submit]`

```html
<form>
  <input type="text" />
  <input type="submit" value="Save" />
</form>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-attribute

### Grouping

> The CSS selector list (,) selects all the matching nodes.

https://developer.mozilla.org/en-US/docs/Web/CSS/Selector_list

Example: `#username, #password, #loginForm button`

```html
<form action="/login" id="loginForm">
  <div>
    <label for="username">Username</label>
    <input type="text" name="username" id="username" />
  </div>
  <div>
    <label for="password">Password</label>
    <input type="text" name="password" id="password" />
  </div>
  <button>Login</button>
</form>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-grouping

### Combinators

#### Descendant

> The descendant combinator — typically represented by a single space ( ) character — combines two selectors such that elements matched by the second selector are selected if they have an ancestor (parent, parent's parent, parent's parent's parent, etc) element matching the first selector. Selectors that utilize a descendant combinator are called descendant selectors.

`A B`

https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_combinator

Example: `#parent .grandchild`

```html
<div id="parent">
  <div class="child">
    <div class="child grandchild"></div>
  </div>
</div>
```

`#parent .child` returns all children but we only want direct children. See child combinator below.

- https://testingrequired.github.io/selector-display/?share=example-css-selector-descendant

#### Child

> The child combinator (>) is placed between two CSS selectors. It matches only those elements matched by the second selector that are the direct children of elements matched by the first.

`A > B`

https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator

Example: `#parent > .child`

```html
<div id="parent">
  <div class="child">
    <div class="child grandchild"></div>
  </div>
</div>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-child

#### General Sibling

> The general sibling combinator (~) separates two selectors and matches the second element only if it follows the first element (though not necessarily immediately), and both are children of the same parent element.

`A ~ B`

https://developer.mozilla.org/en-US/docs/Web/CSS/General_sibling_combinator

Example: `#one ~ #three`

```html
<ul>
  <li id="one">One</li>
  <li id="two">Two</li>
  <li id="three">Three</li>
</ul>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-general-sibling

#### Adjacent Sibling

> The adjacent sibling combinator (+) separates two selectors and matches the second element only if it immediately follows the first element, and both are children of the same parent element.

`A + B`

https://developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_combinator

Example: `#one + #two`

```html
<ul>
  <li id="one">One</li>
  <li id="two">Two</li>
  <li id="three">Three</li>
</ul>
```

- https://testingrequired.github.io/selector-display/?share=example-css-selector-adjacent-sibling
- https://testingrequired.github.io/selector-display/?share=example-css-selector-adjacent-sibling-general

## Setup

### Terminal

The terminal is needed for some installation and running the tests. Anytime you see a command prefixed with `$` it means to run this command in your terminal.

Example:

`$ npm run test`

### Installation

#### Node

Node is an application that allows us to run javascript outside of a browser. It will be running the test scripts we're writing today.

https://nodejs.org/en/

Please install the LTS version which is currently 12.13.0

#### Git

Git is a version control application. We will just be using it to pull down test suite.

https://git-scm.com/download/win

#### Editor

You can use any editor you like but I would recommend Visual Studio Code because of it's excellent javascript support.

#### Chrome

Chrome needs to be installed for the chrome webdriver to connect and the tests to run.

##### Version

The `chromedriver` version in `package.json` must align with the version of Chrome you have.

#### Aligning With Chrome

You have two options when matching your Chrome and chromedriver version.

##### Update Chrome

Update Chrome to latest and use latest chromedriver is the easiest method. Unfortunately this isn't always possible such as enterprise environments.

##### Install correct chromedriver version

Another option is to install the correct chromedriver version for your Chrome.

1. Open Chrome
2. Click on the `...` menu
3. Click on Help > About Chrome
4. Locate Chrome major version
   - Example: `78.0.3904.97`
   - Major Version: `78`
5. Find highest `chromedriver` version that matches your Chrome major version
   - https://www.npmjs.com/package/chromedriver
   - Example: Chrome `76` chromedriver `76.0.1`
6. `$ npm install chromedriver@76.0.1` replacing with your chromedriver version

### Obtain Project

You'll need to obtain the test project to be able to run the test suite.

#### Using git

Using git is recommended as you'll be able to pull down the latest versions.

1. Open terminal
2. `$ cd ...` where `...` is the where you want the project to download to
3. `$ git clone https://github.com/testingrequired/exampletest.app-tests.git`
4. `$ cd exampletest.app-tests`

#### Download zip

Another option is to download the project as a zip file.

1. Click on the latest release of the project: https://github.com/testingrequired/exampletest.app-tests/releases
2. Click `Source code (zip)` and download the zip file
3. Unzip the project folder where ever you want it to live

### Run Tests

1. `$ cd path/to/the/project`
   Example: `C:\Users\name\exampletest.app-tests` or `~/exampletest.app-tests`
2. `$ npm install`
3. `$ npm run test`

## Webdriver

The webdriver the application that receives commands from our automation and passes those commands to the browser. Each of the major browser vendors distribute a webdriver.

### Capabilities

Webdrivers allow you to define what "capabilities" you want/need to support when running your tests. These capabilities include but not limited to: browser name, browser version & operating system. This allows for cross browser/operating system testing. There are a lot of complexities around implementing this yourself but services like [saucelabs](https://saucelabs.com/) work out of the box.

### Headless

When developing your automation scripts you'll want to watch the browser as the script runs. This gives you real time feedback on what your automation is doing.

When your automation scripts are running on a server it's not possible for the browser to launch and be visible. In fact most of the time the browser will error causing the tests to fail instantly.

Many browsers have a feature to run "headless" meaning the browser is running but nothing is shown on screen. This will allow it to run on a server and often times will run faster.

### Selenium

It's more likely you've heard of Selenium versus Webdriver. Selenium was the original implementation. Webdriver was the standard created but created with Selenium compatibility in mind.

### webdriver.io

[webdriver.io](https://webdriver.io) (wdio) is a webdriver library written in javascript. We will be using it for the workshop and

#### Sync vs ASync

wdio supports both [an async and a sync](https://webdriver.io/docs/sync-vs-async.html) mode. The biggest difference between them is with async you must do all of the waiting yourself. With sync mode wdio handles nearly all of the waiting for us. For the workshop we'll be using the sync mode as it's easier to get started with.

## Writing Your First Test

The test case we are going to write is one of the most common you'll come across: logging in.

### Test Case

All test automation should start from a test case. What are the conditions, actions and assertions need to test a piece of functionality. For logging in it might be:

```
Given an existing user of testUser
When I enter the correct username and password
Then I'm logged in as testUser
```

### Identifying/Finding Elements

Elements to identify

1. On the main page: Login Link
2. On the login page: Login form, username & password inputs and the login button

### Perform Actions

1. Click login link
2. Fill username and password
3. Click login button

### Wait And Assert State

1. Wait for login form to load
2. Wait for user page to load

## Page Objects

### What

A way to tie elements and actions together as a single UI component: e.g. login form, navigation menu.

### Why

The two main benefits to page objects are abstraction and reusability.

#### Abstraction

Page objects abstract how the UI actually works by exposing properties (elements) and methods (actions) to call. As long as the application is in the correct state then the page object will just work.

#### Reusability

The abstraction page objects provide also makes them reusable. Got a nav menu that displays on all pages? Use a single page object. Got a rating form thats on several pages? Single page object.

### Boundaries

Page objects should have some concept of the elements its responsible for. The outer boundary of the page object is often its root element. Where every other element it's responsible for is a child of that root element.

A good example of this would be an application with a login form. The root element is likely the `form` element while other elements the page object is responsible for are the username, password inputs and submit button. Any element outside the root element should not be interacted with using that page object.

### Element Getters

Element's should be defined on page objects as either methods or getters. This ensures every time you reference an element on the page you have a fresh reference to it. Anytime the page reloads or elements disappear/reappear on the page then the previous reference you had to it becomes stale. It's always better to query for elements each and every time.

### Action Methods

Actions should be defined on page objects as methods. Ideally the methods should be as atomic as possible while composing those in to larger less generic actions.

Atomic Actions:

- Fill username
- Fill password
- Click login button

Composed Actions:

- Login in as user

### Advanced Design Patterns

This [blog post](https://www.testingrequired.com/blog/modern-page-objects) goes in to more advanced page object design patterns: root element, applying page object to element query results, proxying method calls to the root element.
