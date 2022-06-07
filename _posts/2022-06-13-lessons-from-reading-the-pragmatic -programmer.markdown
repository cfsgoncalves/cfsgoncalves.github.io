---
layout: post
title:  "Important lessons from reading the Pragmatic Programmer"
date:   2022-06-13
published: true
categories:
---

# Important lessons from reading the Pragmatic Programmer
<br /> The Pragmatic Programmer is a book by Andy Hunt e Dave Thomas, focused on modern software engineers' techniques. Recently, the authors did a remake of the book for the 20th year of publication, and as a person that did not have read the prior version, I took the chance to buy it and finally read it. <br />
The book has a lot of knowledge to offer on every page due to the author's extension career. Personally, I enjoy it so much that I can certainly say that every young programmer must read it at least once. That's the main reason I opt to write this article, to advise young programmers to read it and to pass judgement on the concepts that impressed me and stayed in my mind after completing it.

## Orthogonality

<br /> Orthogonality was the first concept that resonated with me once I started digging through the book's pages. The idea behind it is pretty much straightforward. It simply states that software systems must be capable of being built, tested and deployed easily, at any time during their development. Seam's easy to put in words, but it's pretty hard to be done. So, to help us out, while writing code, you must remember that:

> *Systems should be composed of a set of cooperating modules, each implements functionality independent of the others*

And while this seems like the first big lesson you learn while developing software in school or college, as software grows and modules become more extensive, this rule begins to fade over time. Remember:

> *Modules should do one thing and one thing well*

Live by independent modules and die by the [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle), the S in [SOLID](https://en.wikipedia.org/wiki/SOLID). This is the way to avoid coupling and make your software easier to test. <br />

## It's all about coupling 

<br /> Coupling is the enemy of change and is the following principle I will write about. It's what links components together, which is why making changes to software systems a real challenge.
In the book, the authors talk a great deal about coupling. I could argue that the concept echoes from page one to the book's last page. In each chapter, you could feel that coupling is directly related to the core theme. So, the authors also offer numerous solutions on how to avoid coupling. <br />
Although there are numerous to make your code decoupled, for the sake of simplicity, I would state that while you are writing code, you should remember that you must always:

> *Have the code deal with things that it only directly knows about*

Again, like in the last topic, easier said than done. So, the authors facilitate our life again, giving us the most usual ways to how coupled is enabled. Watch out; it's gonna become a little bit more technical than high-level: <br />
First, the methods of a class should only access things passed by arguments or variables/methods that that class is only responsible for. 
You should not try to access the internal states of an object and chain method calls. Otherwise, you are enabling coupling regarding dependencies and destroying the benefits of encapsulation. <br />

---
{% highlight java %}
// Imagine that you have a class customer with the object Orders

//You should not calculate discounts this way
customer.orders.find(order_id).getTotals().applyDiscount(discount);

// You should create a findOrder method to maintain the encapsulation
customer.findOrder(order_id).applyDiscount(discount);

{% endhighlight %}
---
<br>
Next, we have inheritance, a built-in feature in most objected-oriented programming (OOP) languages. The most common use of this built-in feature is applying it to reuse code or represent new types in classes. You should instead use interfaces and delegations of responsibilities through composition. 
But why? If inheritance is a programming language feature, why is it so bad? Remember that every time you change a parent class, the effects will ripple through multiple subclasses and code may break in multiple parts of the application. <br>
Finally, the last attention point. Be careful of shared states and globalization of variables. If you need to make something global, at least wrap it in a function. This way, you can change the internal logic without breaking things up.

## Developing with tracer bullets

<br /> Modern software development can become messy due to constant changes in the requirements while the project is in the early stage. Another recurring problem is the interaction between what the client wants and what the product team understands.
<br /> The authors offer a solution, tracer bullets, to guarantee that what we develop as an artefact is what the user asked in terms of functional and non-functional requirements. Tracer bullets is a technique that defines that you should implement software gradually, within multiple layers, to always have a solution that can be built and shown to the client to be approved by it. <br /> 
In a practical example, a defined flow A should be built and tested through the user interface up to the database, going through the business logic layers. Only after that, you can start developing the next flow of the application. So, in layman's terms, you should develop the base case and build from there up to completion. <br />
It seems simple and intuitive, but with the current division of tasks between frontend and backend, teams usually handle different parts of the software, and normally, inconsistencies appear. Sometimes you end up with software that can't be built and can't be shown to the user.  <br />
On the other hand, one hidden advantage of this approach is that you always validate with the user what you build. You are always receiving feedback, and you always have something to show. Early project decisions could be changed if they are a little bit off of what a user wants because, yes, you guessed it:

> *The decisions you make are always approved by the user*

## Blank Screen Syndrome

<br /> Well, I wrote a little bit on how you should write code and the best ways to avoid coupling in your project, so now, let's focus on the beginning part of the project, on its starts. Concentrate on your daily tasks as a programmer, you receive the requirements on your desk, and your mind is empty. So you write a line of code and fastly delete it. And you do this process three or four more times. You may think something is wrong with you, but I can assure you there isn't. You just have a case of the Blank Screen Syndrome (BSS).
The BSS is a condition that most developers suffer in the first phase of a new project. Basically, you could define it as: 

> *Staring at a blank empty screen, unable to start the project and write code*

The authors offer multiple techniques to surpass this dreaded syndrome. From the presented solutions, I found one that always works for me. It mainly focuses on changing the topic of the matter at hand. So, how do I do it? I start by going on a walk and letting the subconscious work. While I am enjoying myself, the brain is working in the background on the problem I have at hand. Sonner, I will realize that the solution is in front of my eyes and that my marvellous brain did all the hard work for me. Now I just have to do the remaining job of transcribing my thoughts into code. <br /> 
On the other hand, this solution may not be suitable for everyone, or you are on a limited time schedule, and you need to start coding write now. So, as the book suggests, you start prototyping. Prototyping, in this scenario, focuses on beginning with the part of the problem that you found most interesting. Then, after you are done with the exciting part of the requirements, you are deep on the project, and you will be tackling the problem from a holistic approach in no time. 

## Client interaction

Finally, some advice on the human side of the software engineering process, the client. Most programmers, like me, usually have a lot of difficulties dealing with clients directly. Since my time in college, I have listened to professors, and industry professionals say that:

> *The client doesn't know what it wants*

The book has a process on how to harvest requirements the right way, but if you squeeze it, you get the following sentence as dogma on how to get the requirements from clients:

> *Requirements should be learned through a feedback loop*

So, the pre-coding part of the project is not a process that ends before coding. You should execute multiple iterations until you are satisfied with the objective requirements and have no doubts about what the client wants. And even after you start coding, you should initiate a feedback loop on what you are doing, as was explained in the tracer bullet topic.  <br />
On the other hand, if you are unfamiliar with the domain you are working on, you must do prototypes and mockups to understand what the client wants. Before shipping a specific feature to a client, you must understand the client's desires and intentions.