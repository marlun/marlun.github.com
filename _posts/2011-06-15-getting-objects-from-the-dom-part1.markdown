---
layout: post
title: Getting objects from the DOM - Part 1
commit: 23j023j
categories:
- html
- javascript
---

The Document Object Model (DOM) is what every web developer use to work with a web page. The DOM is an object-oriented, in-memory representation of an HTML document. To work with objects we need to be able to access them. There are several ways of doing this and I'll go through the ones I could find. Most of these methods are members of the global document object, a note will be added when so is not the case.

I was planning on writing about them all in one blog post but changed my mind when I saw how many there is. This is the first part which focus on the old and tried methods.

_**Note** that I will tell you about some browser bugs and differences but I'm all for writing for todays browsers and leaving the old behind. IE6 won't disapear until we forget about it._

## The old and the trusted

### Getting an element by its id

The most used, known and available method to access an element is `getElementById(id)`. It returns the first element that it finds which has its id attribute set to the value sent in the id parameter. The id is case-sensitive. If no element is found it will return `null`.

{% highlight html %}
<div id="errors"></div>
{% endhighlight %}
{% highlight javascript %}
var el = document.getElementById("errors");
{% endhighlight %}

_**Note** that IE versions below 8 differs from the other browsers and will also return all of the elements which has it's name attribute set to the id parameter. Another difference is that that in IE versions below 8 the id is NOT case-sensitive._

If you create an element using a DOM method like `createElement`, remember that the element needs to be in the DOM for it to be accessible through `getElementById`. Use the `insertBefore` method or any of its friends to insert the created element into the DOM.

### Getting multiple elements by class name

If you want to access several elements in the DOM one option is to add classes to the elements. A class unlike an id can be used several times in a document. To access all of the elements with a specified class you use `getElementsByClassName(classes)`. Note the plural form of elements in the method name and in the parameter. `getElementsByClassName` takes a string of classes separated by a space and returns a live NodeList. If no elements are found it will return an empty NodeList.

{% highlight html %}
<div id="sidebar">
	<div class="header">Stats</div>
	<div class="body">Text</div>
	<div class="header">Links</div>
	<div class="body">Text</div>
</div>
{% endhighlight %}

{% highlight javascript %}
// Returns a NodeList with 2 elements
var headers = document.getElementsByClassName("header");
// Returns a NodeList with 4 elements
var elements = document.getElementsByClassName("header body");
{% endhighlight %}

`getElementsByClassName` is not just a method of the document object but is also available on all HTML elements. This means that you can call it on another element and it will only search for elements which are descendants of that element (how about another element in this sentence). This can be a lot faster depending on the size of the document.

{% highlight javascript %}
var sidebar = document.getElementById("sidebar");
var headers = sidebar.getElementsByClassName("headers");
{% endhighlight %}

_**Note** that `getElementsByClassName` is not supported until IE9 and Firefox 3. You'll have to add a [polyfill/shim](http://code.google.com/p/getelementsbyclassname/source/browse/trunk/getElementsByClassName.js) for the old browsers)_

The returned NodeList objects are live. Live means that if the DOM (web page) changes, the list will be updated. This can cause errors if you depend on the order of the items in the list. You can read more about it [here](http://www.w3.org/DOM/faq.html#nodelist "W3C FAQ about NodeList").

### Getting multiple elements of the same type

To reduce the use of classes when not needed you can use `getElementsByTagName(tag)` instead. It works like `getElementsByClassName` but searches for specific elements like `p` or `div` and you can only send in one tag name. You can use `*` to get all elements.

Just as `getElementsByClassName` you can run `getElementsByTagName` on all HTML elements to only get descendants of that element.

_**Note** that IE7 has a bug where using `*` on a `<object>` element will always return an empty NodeList._

{% highlight javascript %}
var allElements = document.getElementsByTagName("*");
var divs = document.getElementsByTagName("div");

// This line will get all the `h3` elements inside the `content` element.
// No need to add classes to those headers.
var divs = document.getElementById("content").getElementsByTagName("h3");

// Will return an empty array
var elements = document.getElementsByTagName("h1 h2");
{% endhighlight %}

### Get elements by their name

`getElementsByName(name)` gets all the elements which has the name attribute set to the name parameter. The method is case-sensitive so if you send in 'browser' and it says 'BROWSER' in the DOM it won't find it.

_**Note** that in IE the method is not case-sensitive. IE and Opera also returns elements with the id set to the given name parameter._

{% highlight html %}
<input type="text" name="name" value="My Name" />
<input type="text" name="age" value="26" />
<input type="radio" name="sex" value="male" />
<input type="radio" name="sex" value="female" />
<a name="local">Text</a>
{% endhighlight %}

{% highlight javascript %}
// Returns a NodeList with 1 element
var els = document.getElementsByName("name");
// Returns a NodeList with 2 elements
var els = document.getElementsByName("sex");
// Returns an empty NodeList
var els = document.getElementsByName("mao");
// Returns a NodeList with 1 HTMLAnchorElement
var els = document.getElementsByName("local");
{% endhighlight %}

## Bugs and differences between browsers

If you know about more bugs and differences, especially on newer browsers, please don't hesitate to tell me about it.

## Part 2 - The new and the shiny

The next part will focus on some newer methods, to some probably a little more interesting. The methods I will go through are querySelector, querySelectorAll, elementFromPoint, activeElement and evaluate.
