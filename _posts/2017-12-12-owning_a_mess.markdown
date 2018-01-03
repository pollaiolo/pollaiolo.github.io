---
layout: post
title:  "The cost of owning a mess"
subtitle: "A long post about quality"
date:   2017-12-12 23:34:01
comments: true
categories: [essentials]
published: true
---
## Recipe
<i class="fa fa-check-square" style="color:#828282"></i> **Patience to read** \\
<i class="fa fa-github" style="color:#828282"></i> **[Instant Lottery](https://github.com/pollaiolo/InstantLottery)**

## Foreword
Recently, I had a lecture at the University of Rome3 where I spoke about *Quality through Software Process*. When I started working on this talk I thought that I wouldn't have had the need to present any practical example since the topic was really abstract: *Quality*. I realized, very soon, that nothing could have explained this concept better than **code**. Because the code is the tool we use to give quality to our projects and nothing is more concise and clear than this.\\
I ended up building a fullstack application that you can see in my repository. During the talk I did a couple of live coding sessions where I explained the mistakes I intentionally did in a first version of the app. Then I refactored and committed the *correct* version during the talk. You can take a look at the bad design choices and their solutions by navigating the `GIT` history of the repository.\\
This post will not be about the web application and neither will be a transcription of the talk. I would like to show some *quality pills* and why we should strive to keep quality as high as possible.

## Quality Process
Writing code with other people, for its nature, tends to chaos. A methodological approach to software development is needed to avoid to fight with colleagues and with clients eventually. This method is the *Software Process*. There are tons of definition on the web but I'd like to define it more pragmatically: a sequence of steps through which every component has to pass. Every member of the team has to agree on the defined process and follow it.\\
In my experience I've always worked on **SCRUM** based processes where each component is *defined*, *developed*, *tested* and then *reviewed* before being considered completed. If a step fails then the component goes back to the first step. This chain of steps is the internal core of the process which guarantees the correctness of each component. 

## @author
The JavaDoc keyword `@author` says what we are: authors. Characteristic of the authors is that they have readers; someone will read the code we write and will judge our work. I would like that who will read my code will say *"That's brilliant, let's reuse this component!"* and not *"WTF dude!"*.\\
As an author, I always sign my work (every `Java` class I write) and I think it's a good way to obey me to write clean and concise code. Whenever I feel I wouldn't sign a class that means I have to refactor it because something is not good as it should be.

## Comments
Before even consider *Design Patterns*, in my opinion, we should think about code *expressiveness*. Code should be easy to read and I should be able to read the code as I read a story without losing myself investigating on which method does what. Reading a method should reveal its purpose without having to navigate infinite classes; everything should be *obvious*. Often, I realize to be little expressive when I feel the need to put a comment inside a function; I have to explain something that should be obvious.\\
Disclaimer: comments are needed to explain *non-obvious* code choices and they should be present on every `public` function.

## A time for programming
Programming is a brain work that requires focus, absolute focus. Programming for 10 hours produces bad code and headaches. Code quality depends also on when you code.

## OOP Principles
Some principles to keep in mind while programming.
### Single Responsibility
*"A class should have only one reason to change"*\\
Every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class.
### Open/Closed
*"Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"*\\
A module will be said to be open if it is still available for extension. For example, it should be possible to add fields to the data structures it contains, or new elements to the set of functions it performs.\\
A module will be said to be closed if it is available for use by other modules. This assumes that the module has been given a well-defined, stable description (the interface in the sense of information hiding).
### Liskov Substitution
if S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e. an object of type T may be substituted with any object of a subtype S) without altering any of the desirable properties of T (correctness, task performed, etc.). More formally, the Liskov substitution principle (LSP) is a particular definition of a subtyping relation, called (strong) behavioral subtyping.
### Interface segregation
*"No client should be forced to depend on methods it does not use"*\\
Split interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them.
### Dependency Inversion
*"Depends on abstractions not concretions"*\\
High-level modules should not depend on low-level modules. Both should depend on abstractions.\\
Abstractions should not depend on details. Details should depend on abstractions.
### DRY (don't repeat yourself)
*"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system"*\\
Duplication (inadvertent or purposeful duplication) can lead to maintenance nightmares, poor factoring, and logical contradictions.
### KISS (keep it simple, stupid)
Most systems work best if they are kept simple rather than made complicated; therefore simplicity should be a key goal in design and unnecessary complexity should be avoided

## The cost of owning a mess
Ok, but why? Mainly because everything we do will follow us; every poor design choice will come back to us. Working in a good way becomes a matter of professional survival. The cost we pay (how many hours we have to work) to maintain a product with poor quality is high. In products with bad code every little change that seems to be obvious it becomes complex and requires lot of time. Changing one line in one module requires to change other modules we never thought they could have been related. In the end, we just need to take care of our craft.


 
