---
permalink: /guide/
title: "Tips and guidelines for writing code at HIP"
toc: true
toc_sticky: true
author_profile: false
---

# Motivation

Imagine the following scenario:

1. You get brought on to an existing project
2. You write some code to handle some task
3. Your supervisor asks to review your code
4. You revise your code
5. You get pulled to another project 
6. Ten months later, you're asked to revise the code you barely remember to do something slightly different

This is a scenario that occurs with some frequency not only at HIP, but also at most other organizations. Unfortunately, this kind of scenario can give rise to some major pain, for any number of reasons, for example:

- Figuring out where the code lives
- Figuring out what some particular script does in relation to the others
- Figuring out what the data sources are and if they need to be changed
- Figuring out what object and variable names mean
- Figuring out why this code was written in a particularly way 

This may be the case whether you're reading someone else's code, or (even more commonly) you're reading code you wrote 10 months ago. The good news, however, is that most of these pain points can be prevented or mitigated by following some good practices from the beginning. 

The following is a guide and a series of tips to help you create code that is clear, legible, and adaptable. It is an opinionated guide, in the sense that much of what follows establishes subjective, but carefully considered, conventions. The intent is not to mandate inflexible requirements, but to present a set of good, generally applicable practices. 

This guide is written with writing R code in mind, but should be generally relevant regardless of programming language (keeping in mind some languages have specific conventions that should take precedence), or even to general project management outside of writing code.

This guide was written by Chi-Hyun Kim and last updated October 7, 2024.

# Good code

Just now, I described the purpose of this guide as helping you "create code that is clear, legible, and adaptable". What does this mean? 

When we perform research, we want the results to be reliable. This is of course true for any important task, but is especially important in our research: we want to present conclusions and recommendations that are based on transparent and thoughtful analysis of data. We do *not* want policy decisions to be influenced by error-laden conclusions or be muddied by sloppy procedures.

Good code means code that code that does exactly this. It should lead step-by-step from the raw data source to the communication of the results, in a way that any careful reader can understand. 

Think back to the hypothetical scenario from the top of the page, and think about what would make your life (and your colleagues' lives) easier or more difficult.

Here are some important heuristics to keep in mind throughout a project. If your code reflects these qualities, your life is likely to be much easier down the road.

- Code should be **universal**: you, and anyone else with access to the data, should be able to run your code out-of-the-box without tinkering or having to complete any procedure more complex than downloading needed packages.
- Code should be **replicable**: when you (or anyone) runs the code, the results should be the same.
- Code should be **legible**: it should be physically easy for anyone to read your code.
- Code should be **clear**: your code should not be ambiguous (either to the computer or to a human). To a human, the purpose of your code should be easily apparent.

As you write your code, always imagine that someone may want to look at your code immediately and have the code make sense to them. Keeping clean code consistently can be an extra effort, but it will make for a better and more professional product, which will ultimately make the project an easier and more rewarding one for everyone.

From this point, I describe specific guideline and helpful tips to help you more easily achieve these goals. 

# Basics

This is the most boring section but quite possibly the most important one. The reason is this: before anyone (including a future version of you) can make heads or tails of any code, they must be able to read it. Code is almost inherently difficult to read because writing for computers is generally not how humans understand natural language. But there are some basic principles that can help you write more legible code.

The nature of these principles, however, means that most of what follows is conventional. That is, you could use a different set of conventions if you wanted. The most important (and uncompromisable) principle is **to be consistent**. However, the following conventions are... conventional for writing R code with tidyverse packages and should be followed unless there is some exceptionally convincing reason.

For more, the [tidyverse style guide](https://style.tidyverse.org/) has all the details.

## Usage and style

These are the most important conventions for legibility (some exceptions may exist, listed in the [tidyverse style guide](https://style.tidyverse.org/)).

Code blocks defining an object (like a pipeline) should have line breaks around them. But if there are multiple single-line statements that thematically relate, no line breaks among them are needed.

There should be one space around every operator (like pipes "%>%", +, -, /, =, %in%). 

> ✅: `sum_vector = 1 + 3`
> ✅: `ggplot(aes(x = category, y = percent))`

> 🚫: `mean(x, na.rm=TRUE)`

If a function call is longer than about 88 characters, it should be broken up into separate lines to fit the screen. One line per argument is a good idea. 

Parentheses around function calls should have no spaces surrounding them.

> ✅: `max(x)`
> 🚫: `max ( y )`

But parentheses for control statements (like `if`) and for bracketing statements (like `(1 + 1) / 10`) should have surrounding spaces.

TRUE and FALSE are special keywords and should always be written out fully in all-caps, not as 'T' or 'True'.

If you load a package with `library()` at the beginning of a script, you should not specify the package in the code (e.g., `dplyr::select`). Only use the `::` notation if you are using a one-off function without loading the package, or if you specifically need it to avoid function name conflicts.

## Naming

The tidyverse style guide recommends using `snake_case` in naming variables. This is a good recommendation, because it has good legibility and is less difficult to misspell than some other alternatives.

- `camelCase` doesn't have helpful underscores between them to separate words, and is not as apparent if you misspell (for example by missing a cap)
- `dot.case` is fine, but in some programming contexts dot-separation has a technical reserved meaning so can be potentially confusing
- `runoncase` is objectively illegible

By *no* means should you mix cases, either within a name (🚫 `Object_Name`) or within a script (🚫 `object_name_one`, `objectNameTwo`). Dealing with object names is a pain to begin with: do not make it more difficult! Inconsistent object naming conventions is the #1 cause of difficult-to-read code.

Over and above the visual conventions, much could be said about how to choose good variable names. A great name will be:

- Understandable
- Unambiguous
- Short

However, this is a more difficult task than it might sound like, especially in a larger project where a variable could have 4 or 5 different relevant attributes. The strong recommendation here is to favor understandability and unambiguousness, even at the cost of length. A long variable name is annoying, but a confusing variable name is useless—or  downright dangerous. 

> ✅: tract_geoid_2022
> 🚫: trc_GEOID_22

Using ad-hoc abbreviations in variable names is doubly problematic because it's both difficult to understand (What in the world does `trc` mean? Can you guarantee that everyone reading the code will know what that means?) and easy to mistype (Which letters are left out? If you miss a letter, will you be able to tell easily?). If in doubt, spell it out.

If you have a series of variables that are thematically related, give them the same structure so the reader has a handle on what they are.

> ✅: tract_geoid_2022, tract_geoid_2023, tract_geoid_2024
> ✅: geoid_tract_2022, geoid_county_2022, geoid_state_2022
> 🚫: tract_geoid_2022, tract_2023_geoid_, geoid_tract_2024

The same conventions apply for naming files, as well (either for script names or for outputs). You should **not** use spaces in filenames, as such names cannot be easily referenced in command line and for git. Using hyphens as a separator in filenames is an option that's not possible in R. Again, be consistent.

> Be aware that Windows *still* has a low character-length limit for filenames, so don't go too wild with deeply-nested directory structures or very long filenames.

## Miscellaneous

### Dates

When using dates in variable names or filenames, always use the [ISO 8601](https://xkcd.com/1179/) standard. This way, when you sort by name the names will also be sorted chronologically. Only use dates in non-ISO 8601 formats in code when needing to write communicative material, like in body text or plot labels (and in this case, write out the month names so that it's unambiguous internationally). 

## Commenting

Commenting your code is an indispensable requirement to make it legible and understandable. 

Section titles are a good way to orient the reader. Each script should have a heading at the top named 'Purpose' or similar, with a description for the purpose of the script written out in a short paragraph. Each following section (e.g., "Read in data", "Process data", "Output cleaned data") should have a corresponding comment line.

> Use the cmd/ctrl-shift-R shortcut in RStudio to insert a commented section heading. In RMD files, name the R chunks instead as needed.

Within each section, major steps (like starting a new pipeline) generally should have a short 1-line comment. Think of comments as descriptions of *why* you did what you did, rather than *how*. The *how* should be apparent from reading the code itself (and if it isn't, think about how you could write the code to make it clearer). Occasionally, some intermediate steps may benefit from their own comment lines. For example, you might do a particularly tricky conditional `mutate` and a comment might clear up some of your reader's questions preemptively. 

An important case: if you're changing the number of observations in your data, or changing the number of NA values in a variable, you *should* insert a comment indicating how many rows were dropped/how many values turned into NA, because this information can be critical to any further processing steps either now or in the future. The `tidylog` package (more on this later) will generate this log for you automatically which you can copy-paste in as a comment.

> Use the cmd/ctrl-shift-c shortcut in RStudio to toggle a line (or block) of code in and out of comment status.


# Project and script organization

## Version control



## Ordering and organizing


## Scripts vs RMDs


# Pitfalls and how to avoid them

## Know your data!

## Dirty environments


## NA handling

## Grouped data



# Useful tools

## RStudio

I highly recommend configuring the shortcuts for the assignment operator (`<-`) and the pipe operator to your liking. You don't want to waste your life typing out % < % individually every time.

If you use the shortcut cmd-return (or ctrl-enter), RStudio will run the statement (e.g., a pipeline) where your cursor is located.

The shortcut cmd/ctrl-shift-0 will restart R (and clear your environment) right where you are without restarting RStudio. You should do this every once in a while to avoid nasty bugs from dirty environments.


## Tidylog


## Janitor


## Skim