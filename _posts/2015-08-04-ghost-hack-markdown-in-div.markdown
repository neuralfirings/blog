---
layout: post
title: Ghost Hack
date: '2015-08-04 04:06:27'
---

One of the good things about markdown is it lets you interject HTML in the middle. So far example, 

```
<div class="red">I'm red</div>
**I'm bold**
```

Gives you something like: 
<div class="red">I'm red</div>
**I'm bold**

---

## The Problem
Here's the problem though, when you are writing in html, you can't switch back to Markdown. So for content in a div, you can't take care of all the ==cool== *markdown* styles. 

So, for example, 

```
**I'm bold**
<div class="red">**I'm not bold, still red though**</div>
```

will give you: 

<div class="red">**I'm not bold, still red though**</div>
**I'm bold**

---

## Installation: Markdown-in-Div Preprocessor

So I made a small Markdown preprocessor. It basically uses img tags to store div info. I use img tags because it doesn't require closing tags. 

Copy/paste this in after jQuery in the header but before anything that moves around elements or add elements to the HTML. 

```
<script>
    // Markdown In Div
    $(document).ready(function() {
        html = $(".post-content").html().replace(/<img src="start:/g, '<div class="')
            .replace(/<img src="end" alt="" title="">/g, '</div>')
        	.replace(/<img src="end" alt="">/g, "</div>");
        $(".post-content").html(html);
        $(".post-content").find("div").each(function() {
            class_cleaned = $(this).attr("class").replace("&", " ");
            $(this).attr("class", class_cleaned)
        })
    })
</script>
```

---

## Example Usage

Now, when you want to open close tag, you can use 

```
 ![](start:red)
 this should be red ==with== *formatting*!
 ![](http://)
```

This will become:

 ![](start:red)
 this should be red ==with== *formatting*!
 ![](end)

ooooo... Markdown in a Div ~~using~~ hacking the img tag.

Spiffy!

<style>
.red { color: #f00; }
</style>