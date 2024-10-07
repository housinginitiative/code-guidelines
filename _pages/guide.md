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

When we perform research, we want the results to be reliable and replicable. This is actually true for any important task, but is especially important in our research: we want to present conclusions and recommendations that are based on transparent and thoughtful analysis of data. We do *not* want policy decisions to be influenced by error-laden conclusions or be muddied by sloppy procedures.

Good code means code that code that does exactly this. It should lead step-by-step in a way that any careful reader can understand, from data source to the communication of the results. 

Think back to the hypothetical scenario from the top of the page, and think about what would make your life (and your colleagues' lives) easier or more difficult.

Here are some important heuristics to keep in mind throughout a project. If your code reflects these qualities, your life is likely to be much easier down the road.

- Code should be **universal**: you, and anyone else with access to the data, should be able to run your code out-of-the-box without tinkering or having to complete any procedure more complex than downloading needed packages.
- Code should be **replicable**: when you (or anyone) runs the code, the results should be the same.
- Code should be **legible**: it should be physically easy for anyone to read your code.
- Code should be **clear**: your code should not be ambiguous (either to the computer or to a human). To a human, the purpose of your code should be easily apparent.

From this point, I describe specific guideline and helpful tips to help you more easily achieve these goals.

# Basics

## Usage and style

## Naming



Dates


## Commenting




# Project and script organization

## Version control



## Ordering and organizing


# Pitfalls and how to avoid them

## Know your data!

## Dirty environments


## NA handling





# Useful tools


## Tidylog


## Janitor


## Skim