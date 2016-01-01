---
layout: post
title: "Print HTML <div> using Javascript"
description:
headline:
modified: 2016-01-02
category: Web Development
tags: [html,javascript,window,print]
imagefeature: img.jpg
mathjax:
chart:
comments: true
featured: true
share: true
---

One day while working on one of the many projects, I had to print a HTML div using __Javascript__. A naive way would be to use the `window.print()` function with the **onclick** handler of the button. But, this has issues with the whole body of the page being printed in the output. I wanted only specific HTML *div* uniquely identified by an ID to be printed and not the whole body of the page. Hence, I found this below function to be very useful and have been using it in similar scenarios whenever I need a certain *div* to be printed.

{%highlight javascript%}
<script>
function printContent(el){
var restorePage = document.body.innerHTML;
var printContent = document.getElementById(el).innerHTML;
document.body.innerHTML = printContent;
window.print();
document.body.innerHTML = restorePage;
}
</script>
{%endhighlight%}
__Note__:*window.print()* prints the body of HTML page.

`restorePage` variable is used to store the body of the page. Now the content that needs to be printed is assigned to `printContent` and the body of page is replaced with `printContent`. Using `window.print()` method the required content is printed. Now, the body is to be restored with `restorePage` after the `window.print()` method is executed.

To use the above function just use an onclick handler on a button as shown below:
{%highlight html%}
<button id="btn" onclick="printContent('quotation');">
<div id="quotation">
  ...
</div>
{%endhighlight%}

Hope, this article helps someone who is having a similar requirement as mine and this script comes in handy many times specifically when working on printing a certain HTML DIV.

Cheers!!
