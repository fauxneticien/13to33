---
title: "13.3 Separating your dictionary data from its display from with JavaScript"
date: 2025-03-03
layout: post
---

## Goal

Like the last tutorial where we learned to use CSS to help consistently style the dictionary, in this tutorial we'll get a small taste of how we can use JavaScript to help structure the dictionary so that a change in a single place (e.g. put part of speech after definition) is applied to all entries.

## Separating data from its display 

Let's return to our pre-CSS dictionary from the very first tutorial again, repeated below.
In the way we've created this dictionary so far, we've had to hand type every entry in HTML, marking-up how certain dictionary data (e.g. headwords, parts of speech) should be displayed.
This is still tedious to create and even more to make consistent changes, offering no advantages over doing the same thing in a word processing application like Microsoft Word.

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

It's easy to prove that the dictionary data need not be mixed in with its display, simply by displaying the same data in another way — a spreadsheet for example.
In this spreadsheet display, each headword occupies a single row and the properties of the headwords are displayed in various columns (e.g. definitions in Column C).
A cell is a column-row location that contains some data (e.g. Column C, Row 2 contains `large`).

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_spanish-dictionary-spreadsheet.png %}" width="80%">
</p>

Should we already have data in a well-structured spreadsheet, it would be nice to be able to have our dictionary displayed in HTML simply by stating:

- For each row in this table:
    - Display in bold the data from the first column (i.e. headword)
    - Display data from the second column in parentheses (i.e. part of speech)
    - Display data from the third column in italics (i.e. definition)
    - Display data from the fourth column with a `◆` prefix (i.e. example sentence)
    - Display data from the fifth column in italics (i.e. example sentence)


By the end of this tutorial, you will have learned how to do this with JavaScript.

## Creating HTML content dynamically

When we manually type HTML, we're kind of creating content that's fixed and hard to change, or 'static'.
The opposite is 'dynamic' content, which is created on-the-fly.

As a toy example of static HTML content, let's go back to our `hello world` example.
Now that you've had some experience with HTML, you can already imagine how the following snippet will be displayed: the text 'Hello world' in bold because this text appears in between the `<b>` and `</b>`.
We could say this 'Hello world' is the HTML that is inside of the `<b>` or the `innerHTML` of it (we'll come back to this keyword shortly).

```html
<b>Hello world</b>
```

We can create this same display of a bold 'Hello world' another way.
For this first taste of JavaScript, we won't break down every single part of the snippet below.
What we can notice here is that despite there being no content between the `<b>` and `</b>` tags, we can add a unique identifier (e.g. `boldarea`), and then target this element (via `document.getElementById("boldarea")`), and dynamically change its contents (i.e. `innerHTML`).

```html
<b id="boldarea"></b>

<script type="text/javascript">

document.getElementById("boldarea").innerHTML = 'Hello world'

</script>
```

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_spanish-dictionary-hello-world-dynamic.gif %}">
</p>

We can also keep adding to the content using the `+=` operator (as opposed to just `=` which replaces all the content).

```html
<b id="boldarea"></b>

<script type="text/javascript">

document.getElementById("boldarea").innerHTML  = 'Hello world. '
document.getElementById("boldarea").innerHTML += 'How are you?'

</script>
```

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_spanish-dictionary-hello-world-append.png %}">
</p>

Have a play with these snippets in our online editor at [https://fauxneticien.github.io/html_editor/](https://fauxneticien.github.io/html_editor/){:target="_blank"}.
Perhaps try:

- Using a different `id` than `boldarea`
- Swapping out `<b>...</b>` for another tag (e.g. `<i>...</i>`)
- Adding additional text content (`How are you? It's such a nice day!`)
- Adding a mix of text and HTML (`How are you? <i>It's such a nice day!</i>`)

## Representing data with JavaScript arrays

In order to display dictionary data with JavaScript (to create dynamic HTML content), we will need a way to store this data.
In this tutorial, we'll use JavaScript 'arrays', which can be though of as a list of items.
After storing the data in this list, e.g. `mylist=["a", "b", "c"]`, you can retrieve specific items from this list: `mylist[0]` (retrieve the first item from `mylist`; note JavaScript, like many programming languages, indexes data starting from 0).

Let's look at working with arrays using a concrete example.
Below we have a three-word version of our dictionary, stored as an array with the name `dictionary_words`.
We can retrieve data from this array using the notation `dictionary_words[0]`.

```html
<span id="dictionary_display"></span>

<script type="text/javascript">

dictionary_words = ["casa", "grande", "gustar"]

document.getElementById("dictionary_display").innerHTML = dictionary_words[0]

</script>
```

As we change what the value of index (e.g. `0`, `1`, `2`), we can see the data that is displayed in the `<span></span>` tags change.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_array-dynamic.gif %}">
</p>

Notably, trying to retrieve a non-existent fourth value (i.e. using index `3`) leads to JavaScript returning an `undefined` value that is displayed.

## Exercises in (Dictionary) Style

In this section, we will learn to display each of the three headwords on a new line and we will see how to accomplish the exact same thing in five different methods.
In the last method, we will introduce a fundamental structure across many programming languages called a `for` loop and gain some intuition on its usage based on the preceding  (functionally equivalent) methods.

### 1. Static HTML

First, we can simply hand-type HTML within the `<span>...</span>` tags to display 'casa', 'grande', and 'gustar' each separated by a line break `<br>`.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_for-loop-static.png %}" width="100%">
</p>

### 2. Dynamic HTML

Second, building on our dynamic HTML section above, we can start with an empty `<span>...</span>` and dynamically add HTML content using JavaScript.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_for-loop-dynamic.png %}" width="100%">
</p>

### 3. Dynamic HTML with data from array

Third, build on our data with arrays section, we can store the words first in an array `dictionary_words` and then later retrieve them using an index (e.g. `dictionary_words[0]`).

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_for-loop-dynamic-array.png %}" width="100%">
</p>

### 4. Dynamic HTML with data from array and manual index

Fourth, to build an intuition on what the for loop is doing in the next section, we will create an `index` to keep track of what the current entry we want to process is and 
then manually increase it after we are done with the entry.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_for-loop-dynamic-array-man-inc.png %}" width="100%">
</p>

### 5. Dynamic HTML with data from array and for loop

Finally, we arrive at the version with a `for` loop.
Though it has introduced new syntactic notations (e.g. `index++`, braces `{ ... }`, etc.), we have build up a sense of what it is accomplishing.

The difference between this for loop and the last method is that the for loop is 1) taking care of creating, tracking, and increasing the value of `index` and then 2) re-running the code specified between the braces `{ ... }` with the current value of `index` each time (`0` first, then `1`, then `2`).

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_for-loop-dynamic-array-for-loop.png %}" width="100%">
</p>

## Building your first dynamic dictionary

We now have all the pieces to re-build our 10-word Spanish-to-English dictionary dynamically.
First let's remind ourselves of the data structure and display instructions.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_spanish-dictionary-spreadsheet.png %}" width="80%">
</p>

Given dictionary data in a table(-ish) structure, *for* each of the 10 headwords, we would like to:

- Display in bold the data from the first column (i.e. headword)
- Display data from the second column in parentheses (i.e. part of speech)
- Display data from the third column in italics (i.e. definition)
- Display data from the fourth column with a `◆` prefix (i.e. example sentence)
- Display data from the fifth column in italics (i.e. example sentence)

### Representing data with arrays

For this tutorial, we're going to keep the data structures simple by using one array to represent a column.
So `dictionary_defs[1]` for example retrieves the 2nd item in the `dictionary_defs` array (remember JavaScript indices start from 0), which is the value 'large'.

```html
<script type="text/javascript">

dictionary_words = ["casa", "grande", "gustar", "hasta", "lunes", "madre", "muy", "perro", "pollo", "vida"]
dictionary_pos   = ["nf", "adjm, adjf", "vtr", "prep", "nm", "nf", "adv", "nm, nf", "nm", "nf"]
dictionary_defs  = ["house", "large", "to like", "until", "Monday", "mother", "very", "dog", "chicken", "life"]
dictionary_exsts = ["Este es mi casa", "Mi casa es grande", "Me gustan tacos", "Hasta mañana", "Hoy es lunes", "Este es mi madre", "El pollo es muy grande", "Este es mi perro", "El pollo es grande", "Mi vida es genial"]
dictionary_extrn = ["This is my house", "My house is large", "I like tacos", "See you tomorrow (lit. until tomorrow)", "Today is Monday", "This is my mother", "The chicken is very large", "This is my dog", "The chicken is large", "My life is great"]

</script>
```

### Displaying dictionary data dynamically 

Now that we have our data, we can use a for loop to help us iterate over each of the 10 entries and display each one according to a specific format.

#### Headwords in bold on a new line

Let's start simple by displaying just the 10 headwords with a for loop.
Have a play with the snippet in our online editor at [https://fauxneticien.github.io/html_editor/](https://fauxneticien.github.io/html_editor/){:target="_blank"}.

```html
<span id="dictionary_display"></span>

<script type="text/javascript">

dictionary_words = ["casa", "grande", "gustar", "hasta", "lunes", "madre", "muy", "perro", "pollo", "vida"]
dictionary_pos   = ["nf", "adjm, adjf", "vtr", "prep", "nm", "nf", "adv", "nm, nf", "nm", "nf"]
dictionary_defs  = ["house", "large", "to like", "until", "Monday", "mother", "very", "dog", "chicken", "life"]
dictionary_exsts = ["Este es mi casa", "Mi casa es grande", "Me gustan tacos", "Hasta mañana", "Hoy es lunes", "Este es mi madre", "El pollo es muy grande", "Este es mi perro", "El pollo es grande", "Mi vida es genial"]
dictionary_extrn = ["This is my house", "My house is large", "I like tacos", "See you tomorrow (lit. until tomorrow)", "Today is Monday", "This is my mother", "The chicken is very large", "This is my dog", "The chicken is large", "My life is great"]

for (index = 0; index <= 9; index++) {

   document.getElementById("dictionary_display").innerHTML += "<b>" + dictionary_words[index] + "</b>"
   document.getElementById("dictionary_display").innerHTML += "<br>"

}

</script>
```

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_10-word-dict-headwords.png %}" width="100%">
</p>

#### Others

Focusing just on the snippets related to retrieval and display:

- We can retrieve the relevant part of speech for the current headword using `dictionary_pos[index]`, prepending it with an open parenthesis `(` (and a space so that it's not right up against the headword), and post-pending a close parenthesis:

    ```javascript
" (" + dictionary_pos[index] + ")"
    ```

- Retrieve the definition using `dictionary_defs[index]` and wrap in `<i>...</i>` to italicize:

    ```javascript
" <i>" + dictionary_defs[index] + "</i>"
    ```

- Retrieve the example sentence using `dictionary_exsts[index]` and prefix with `◆`:

    ```javascript
" ◆ " + dictionary_exsts[index]
    ```

- Retrieve the example sentence translation using `dictionary_extrn[index]` and wrap in `<i>...</i>` to italicize:

    ```javascript
" <i>" + dictionary_extrn[index] + "</i>"
    ```

### Final dictionary

Putting the snippets altogether, we have our dictionary!

```html
<span id="dictionary_display"></span>

<script type="text/javascript">

dictionary_words = ["casa", "grande", "gustar", "hasta", "lunes", "madre", "muy", "perro", "pollo", "vida"]
dictionary_pos   = ["nf", "adjm, adjf", "vtr", "prep", "nm", "nf", "adv", "nm, nf", "nm", "nf"]
dictionary_defs  = ["house", "large", "to like", "until", "Monday", "mother", "very", "dog", "chicken", "life"]
dictionary_exsts = ["Este es mi casa", "Mi casa es grande", "Me gustan tacos", "Hasta mañana", "Hoy es lunes", "Este es mi madre", "El pollo es muy grande", "Este es mi perro", "El pollo es grande", "Mi vida es genial"]
dictionary_extrn = ["This is my house", "My house is large", "I like tacos", "See you tomorrow (lit. until tomorrow)", "Today is Monday", "This is my mother", "The chicken is very large", "This is my dog", "The chicken is large", "My life is great"]

for (index = 0; index <= 9; index++) {

   document.getElementById("dictionary_display").innerHTML += "<b>" + dictionary_words[index] + "</b>"
   document.getElementById("dictionary_display").innerHTML += " (" + dictionary_pos[index] + ")"
   document.getElementById("dictionary_display").innerHTML += " <i>" + dictionary_defs[index] + "</i>"
   document.getElementById("dictionary_display").innerHTML += " ◆ " + dictionary_exsts[index]
   document.getElementById("dictionary_display").innerHTML += " <i>" + dictionary_extrn[index] + "</i>"
   document.getElementById("dictionary_display").innerHTML += "<br>"

}

</script>
```

If we wanted to swap the order of part of speech with definition (our goal at the start of the tutorial), it is now simply a matter of swapping the two lines:

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/13.3_2025-03-03_10-word-dict-swap.gif %}" width="100%">
</p>

## Afterword

While we have covered a *lot* of ground in this tutorial, I hope we've also been able to glimpse a little how repetitive actions can be automated with programming and how data stored in a well-structured format can be displayed dynamically.
The former can help us define a template in a central place and when this template is edited, it is applied immediately across the entire dictionary (whether it's 10 words or 10,000 words).

The latter can help us make different use-appropriate versions on-the-fly. Need a word list? Just show headword and definitions.
Need a learner's dictionary? Show only commonly used words (given there's a word frequency column).
Need only place names for map-making? Show just place names (assuming they are labeled appropriately, e.g. a `noun.placename` part of speech).
