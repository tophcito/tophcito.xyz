---
title: "Why you should always spell out `TRUE` and `FALSE` in R"
date: 2019-10-08T03:40:19Z
categories:
  - 101 Introductions
tags:
  - Rstats
  - Programming
level:
  - intermediate
draft: false
---

In its rich history, the R language interpreter has tried to offer a number of
convenience features. Some of them are outright dangerous. In this post I'd
like to discuss the pitfalls associated with one of these features: the
ill-practice of writing `TRUE` and `FALSE` with `T` and `F`, respectively.


# Summary
If you don't have the time to dive into the background explanation given below,
here's a short summary:

* Out-of-the-box R will allow you to type `T` and `F` anyplace where the boolean
  values `TRUE` or `FALSE` are needed.
* However, `T` and `F` are mere variables, and thus can be overwritten anytime.
* Using `T` and `F` instead of `TRUE` and `FALSE` is bad practice and will break
  your code, as soon as you assign any value to `T` or `F`.
* When using the proper keywords `TRUE` and `FALSE`, you are immune against this
  specific kind of error. 


# Logical values
As in many programming languages, logical values are stored in their own data
type. Logical values are either literally defined, or are the result of
comparison tests. An example of the former would be:

```{r}
is_complete <- TRUE
```

And one example of the latter is the result of this comparison:

```{r}
a_variable <- 5
is_positive <- a > 0
```

Both of these examples define variables that are of class `logical`. This class
is used to hold boolean values. If you recall from high school, boolean values
are either true or false. In R a boolean value can also be missing (encoded as
`NA`), but that's a different story.

In case you want to read up on Boolean values and how to calculate with them,
the
[Wikipedia entry on Boolean algebra](https://en.wikipedia.org/wiki/Boolean_algebra)
is pretty complete. 


# Reserved words
One core concept to understand when writing computer code is that of reserved
words. In general, you are quite free when typing your code: you can name your
variables however you see fit as long as you stick to some basic rules. For R
for example, a variable name must start with a charcter (or a `.`). However,
there are some words that are off limits for variable names. We call them
*reserved words* and every programming language has them. Some programming
languages reserve a great number of words. R has only 19 reserved words. You
can view the list of reserved words by typing `?reserved` into an R console.

The thing with reserved words is that you cannot use them as variable names.
This might sound troubling at first when considering that common words like
`next` or `break` are among the reserved words. But it is actually quite a
salvation. By reserving these words and thus preventing a user to overwrite
their original meaning with something else, R ensures that code works as
intended.


# Putting it all together
How do these two seemingly unrelated concepts, boolean values and reserved
words, play together? Well, it's quite obvious really, once you realize that
`TRUE` and `FALSE` are reserved words, and `T` and `F` are not. Indeed, 
rather than being reserved words, the convenience abbreviations of `T` for
`TRUE` and `F` for `FALSE` are just out-of-the-box variable definitions.
This means that essentially, at the beginning of every R session, this code
is executed:

```{r}
T <- TRUE
F <- FALSE
```

This is what allows you to use `T` and `F` as shortcuts. But there is a catch;
a pretty big one I might add: as neither `T` nor `F` are reserved words, they
can be overwritten at any time in a script. Therefore, relying on these
convenience abbreviations is waiting for desaster to happen.
 
