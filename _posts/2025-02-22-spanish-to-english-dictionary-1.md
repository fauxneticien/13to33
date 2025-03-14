---
title: "13.1 Hola Mundo: Your first Spanish-to-English dictionary in HTML"
date: 2025-02-22
layout: post
---

## Goal

In this tutorial, you will learn to create a very simple 10-word Spanish-to-English dictionary displayed below using HTML ([Hypertext Markup Language](https://en.wikipedia.org/wiki/HTML){:target="_blank"}), which is how web browsers such as Chrome/Firefox/Safari/Edge understand how to display websites.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.0_2025-02-23_spanish-dictionary.png %}" width="80%">
</p>

## Hello world in HTML

Let's start by creating a ['hello world'](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program){:target="_blank"} example, which is a common way to demonstrate the basics of a programming language.
For this tutorial, we'll use an online HTML editor at [https://fauxneticien.github.io/html_editor/](https://fauxneticien.github.io/html_editor/){:target="_blank"}.
As you can see below, you can type in HTML on the left side (go ahead and type in `hello world`) and the content will be interpreted by the browser and displayed on the right side.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.0_2025-02-23_hello-world.gif %}">
</p>

### To boldly go...

As the name implies, HTML is a markup language in which we will mark up certain parts to indicate that it should be displayed a certain way.
We do this by using HTML tags, which are typically used in pairs such as the start tag `<b>` and the end tag `</b>` to indicate that the text in between those tags should be displayed in bold.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.0_2025-02-23_hello-world-bold.gif %}">
</p>

## Your first dictionary entry

We're just about to create our first dictionary entry for the Spanish word *casa* (house).
As common in many dictionaries, we're going to use consistent ordering and formatting to concisely display various information related to a given word.
Say we want the entries to look like:

<p style="padding-left:25px">
    <b>casa</b>. (nf). <i>house</i>. ◆ Este es mi casa. <i>This is my house.</i>
</p>

Or more specifically:

- Headword on a new line, in bold
- Period
- Part of speech (noun, adjective, preposition, etc.), in parentheses 
- Period
- English translation
- Example sentence, prefixed by a symbol ◆
- English translation of example sentence, italicised

To display the *casa* entry in the specification in the web browser, we can use the following HTML snippet: 

```html
<b>casa</b>. (nf). <i>house</i>. ◆ Este es mi casa. <i>This is my house.</i>
```

Go ahead and copy-paste this snippet into the HTML editor to verify that it does display as expected.
Notice we have introduced a new tag `<i>` and `</i>`, which displays content in between the tags in italic.

## Your second dictionary entry

Let's try to add the next entry, *grande*.
We know that it should appear on a new line.
However, when we simply add the entry on a new line in the editor, the displayed content does not contain a line break in between the two entries.

```html
<b>casa</b>. (nf). <i>house</i>. ◆ Este es mi casa. <i>This is my house.</i>
<b>grande</b>. (adjm, adjf). <i>large</i>. ◆ Mi casa es grande. <i>My house is large.</i>
```

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.0_2025-02-23_second-entry.png %}" width="80%">
</p>

To create a line break, we can use the `<br>` tag, which does not need an accompanying end tag `</br>`.

```html
<b>casa</b>. (nf). <i>house</i>. ◆ Este es mi casa. <i>This is my house.</i>
<br>
<b>grande</b>. (adjm, adjf). <i>large</i>. ◆ Mi casa es grande. <i>My house is large.</i>
```

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.0_2025-02-23_second-entry-with-break.png %}" width="80%">
</p>

## Your 10-word dictionary entry

Now we're ready to create the rest of our basic dictionary:

```html
<b>casa</b>. (nf). <i>house</i>. ◆ Este es mi casa. <i>This is my house.</i>
<br>
<b>grande</b>. (adjm, adjf). <i>large</i>. ◆ Mi casa es grande. <i>My house is large.</i>
<br>
<b>gustar</b>. (vtr). <i>to like [something].</i> ◆ Me gustan tacos. <i>I like tacos.</i>
<br>
<b>hasta</b>. (prep). <i>until</i>. ◆ Hasta mañana. <i>See you tomorrow (lit. until tomorrow).</i>
<br>
<b>lunes</b>. (nm). <i>Monday</i>. ◆ Hoy es lunes. <i>Today is Monday.</i>
<br>
<b>madre</b>. (nf). <i>mother</i>. ◆ Este es mi madre. <i>This is my mother.</i>
<br>
<b>muy</b>. (adv). <i>very</i>. ◆ El pollo es muy grande. <i>The chicken is very large.</i>
<br>
<b>perro</b>. (nm, nf). <i>dog</i>. ◆ Este es mi perro. <i>This is my dog.</i>
<br>
<b>pollo</b>. (nm). <i>chicken</i>. ◆ El pollo es grande. <i>The chicken is large.</i>
<br>
<b>vida</b>. (nf). <i>life</i>. ◆ Mi vida es genial. <i>My life is great.</i>
```

Congrats — you've created your first dictionary in HTML! 
