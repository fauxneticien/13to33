---
title: "13.2 Styling your Spanish-to-English dictionary with CSS"
date: 2025-03-01
layout: post
---

## Goal

In this tutorial, you will learn to style your newly created Spanish-to-English dictionary using 
Cascading Style Sheets [(CSS)](https://en.wikipedia.org/wiki/CSS){:target="_blank"}, which help minimize repetition and make it much easier to apply changes throughout your dictionary.

## Our dictionary so far

At the end of the last tutorial, we had created our 10-word Spanish-to-English dictionary with the following code.
Let's go ahead and enter this code into the online HTML editor at [https://fauxneticien.github.io/html_editor/](https://fauxneticien.github.io/html_editor/){:target="_blank"}.

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

## Changing styling for definitions

Suppose we want to change the style from italicizing the definitions of headwords to using underlines.
Using only HTML, this would involve removing the `<i>...</i>` tags around each definition and replacing them with the tags for underling `<u>...</u>`: for example, `<i>house</i>` to `<u>house</u>` for the entry *casa*.

```html
<b>casa</b>. (nf). <u>house</u>. ◆ Este es mi casa. <i>This is my house.</i>
<br>
<b>grande</b>. (adjm, adjf). <u>large</u>. ◆ Mi casa es grande. <i>My house is large.</i>
<br>
<b>gustar</b>. (vtr). <u>to like [something].</u> ◆ Me gustan tacos. <i>I like tacos.</i>
<br>
<b>hasta</b>. (prep). <u>until</u>. ◆ Hasta mañana. <i>See you tomorrow (lit. until tomorrow).</i>
<br>
<b>lunes</b>. (nm). <u>Monday</u>. ◆ Hoy es lunes. <i>Today is Monday.</i>
<br>
<b>madre</b>. (nf). <u>mother</u>. ◆ Este es mi madre. <i>This is my mother.</i>
<br>
<b>muy</b>. (adv). <u>very</u>. ◆ El pollo es muy grande. <i>The chicken is very large.</i>
<br>
<b>perro</b>. (nm, nf). <u>dog</u>. ◆ Este es mi perro. <i>This is my dog.</i>
<br>
<b>pollo</b>. (nm). <u>chicken</u>. ◆ El pollo es grande. <i>The chicken is large.</i>
<br>
<b>vida</b>. (nf). <u>life</u>. ◆ Mi vida es genial. <i>My life is great.</i>
```

After applying this to every entry, our re-styled dictionary would now look like:

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.1_2025-03-01_spanish-dictionary-underlined.png %}" width="80%">
</p>

If we wanted to try out another style or change our mind and go back to italicized definitions, we'd have to manually update every single definition again.
This is already starting to get cumbersome for a 10-word dictionary, let alone one that might have 1000 or 10,000 words.

## Styling with spans

Instead of directly specifying the style using purpose-specific tags such as `<i>` or `<u>`, we can use a `<span>` tag, which has no inherent style associated with it.

```html
<b>casa</b>. (nf). <span>house</span>. ◆ Este es mi casa. <i>This is my house.</i>
<br>
<b>grande</b>. (adjm, adjf). <span>large</span>. ◆ Mi casa es grande. <i>My house is large.</i>
<br>
<b>gustar</b>. (vtr). <span>to like [something].</span> ◆ Me gustan tacos. <i>I like tacos.</i>
<br>
<b>hasta</b>. (prep). <span>until</span>. ◆ Hasta mañana. <i>See you tomorrow (lit. until tomorrow).</i>
<br>
<b>lunes</b>. (nm). <span>Monday</span>. ◆ Hoy es lunes. <i>Today is Monday.</i>
<br>
<b>madre</b>. (nf). <span>mother</span>. ◆ Este es mi madre. <i>This is my mother.</i>
<br>
<b>muy</b>. (adv). <span>very</span>. ◆ El pollo es muy grande. <i>The chicken is very large.</i>
<br>
<b>perro</b>. (nm, nf). <span>dog</span>. ◆ Este es mi perro. <i>This is my dog.</i>
<br>
<b>pollo</b>. (nm). <span>chicken</span>. ◆ El pollo es grande. <i>The chicken is large.</i>
<br>
<b>vida</b>. (nf). <span>life</span>. ◆ Mi vida es genial. <i>My life is great.</i>
```

Notice that the definition `house` appears as un-styled, despite the `<span>` tags around it.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.1_2025-03-01_spanish-dictionary-span.png %}">
</p>

To italicize all content within these `<span>` tags, we can target them with CSS as follows:

```html
<style type="text/css">
span {
    font-style: italic;
}
</style>
```

We won't break down what each line means/does for this first impression of CSS.
What we can notice/appreciate for now is that the specification for italicizing all spans is only written once at the top.
When we change this CSS span style, for example by specifying a different font color (e.g. by adding `color: red`), we can see that it applies to all definitions:

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.1_2025-03-01_spanish-dictionary-color.gif %}">
</p>

## Target styling with classes

To make experimenting with different styles easier, let's convert all parts within the entries to use `<span>` tags then.

```html
<style type="text/css">
span {
    font-style: italic;
}
</style>

<span>casa</span>. (nf). <span>house</span>. ◆ Este es mi casa. <span>This is my house.</span>
<br>
<span>grande</span>. (adjm, adjf). <span>large</span>. ◆ Mi casa es grande. <span>My house is large.</span>
<br>
<span>gustar</span>. (vtr). <span>to like [something].</span> ◆ Me gustan tacos. <span>I like tacos.</span>
<br>
<span>hasta</span>. (prep). <span>until</span>. ◆ Hasta mañana. <span>See you tomorrow (lit. until tomorrow).</span>
<br>
<span>lunes</span>. (nm). <span>Monday</span>. ◆ Hoy es lunes. <span>Today is Monday.</span>
<br>
<span>madre</span>. (nf). <span>mother</span>. ◆ Este es mi madre. <span>This is my mother.</span>
<br>
<span>muy</span>. (adv). <span>very</span>. ◆ El pollo es muy grande. <span>The chicken is very large.</span>
<br>
<span>perro</span>. (nm, nf). <span>dog</span>. ◆ Este es mi perro. <span>This is my dog.</span>
<br>
<span>pollo</span>. (nm). <span>chicken</span>. ◆ El pollo es grande. <span>The chicken is large.</span>
<br>
<span>vida</span>. (nf). <span>life</span>. ◆ Mi vida es genial. <span>My life is great.</span>
```

Naively applied, we can see that the browser is doing exactly as instructed, italicizing *everything* in between `<span>` tags:

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.1_2025-03-01_spanish-dictionary-all-italics.png %}" width="80%">
</p>

What we would like to do is differentiate between different kinds of spans: those that wrap around headwords, those that wrap around definitions, and those that wrap around translations of example sentences.

To accomplish this, we use the `class` attribute to give each of these span types a unique name (respectively `headword`, `def`, and `te`; each shorter than the other to show that the names are arbitrary and can be whatever you want to call them).
Now we can target specific span types for styling (via the CSS dot notation, e.g. `span.headword`).

```html
<style type="text/css">
span.headword {
    font-weight: bold;
}

span.def {
    font-style: italic;
}

span.te {
    font-style: italic;
}
</style>

<span class="headword">casa</span>. (nf). <span class="def">house</span>. ◆ Este es mi casa. <span class="te">This is my house.</span>
<br>
<span class="headword">grande</span>. (adjm, adjf). <span class="def">large</span>. ◆ Mi casa es grande. <span class="te">My house is large.</span>
<br>
<span class="headword">gustar</span>. (vtr). <span class="def">to like [something].</span> ◆ Me gustan tacos. <span class="te">I like tacos.</span>
<br>
<span class="headword">hasta</span>. (prep). <span class="def">until</span>. ◆ Hasta mañana. <span class="te">See you tomorrow (lit. until tomorrow).</span>
<br>
<span class="headword">lunes</span>. (nm). <span class="def">Monday</span>. ◆ Hoy es lunes. <span class="te">Today is Monday.</span>
<br>
<span class="headword">madre</span>. (nf). <span class="def">mother</span>. ◆ Este es mi madre. <span class="te">This is my mother.</span>
<br>
<span class="headword">muy</span>. (adv). <span class="def">very</span>. ◆ El pollo es muy grande. <span class="te">The chicken is very large.</span>
<br>
<span class="headword">perro</span>. (nm, nf). <span class="def">dog</span>. ◆ Este es mi perro. <span class="te">This is my dog.</span>
<br>
<span class="headword">pollo</span>. (nm). <span class="def">chicken</span>. ◆ El pollo es grande. <span class="te">The chicken is large.</span>
<br>
<span class="headword">vida</span>. (nf). <span class="def">life</span>. ◆ Mi vida es genial. <span class="te">My life is great.</span>
```

Awesome!
Using HTML and CSS together means that we can control from a central location the styling for specific parts of every entry in the entire dictionary (be it just 10 words or 10,000 words):

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.1_2025-03-01_spanish-dictionary-span-classes.gif %}">
</p>
