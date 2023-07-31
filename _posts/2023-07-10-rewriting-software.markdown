---
layout: post
title:  "Lessons learned from rewriting legacy software"
date:   2023-07-30
published: true
categories:
---

# Lessons learned from rewriting legacy software

<br /> My last big project @Truphone is the rewriting of one of their core products with the help of one of their tech leads. The project is very challenging there is a couple of lessons to be learned from it. From the error that I and my colleague made while starting it. Here, in the next couple of sections, I will give you a view of how we proceeded, how the project unroll and how we made the roadmap, and most importantly, the errors in our ways.

## The Prologue

<br /> Our prologue starts on a magic land where everything is possible and we try to do everything by the book. So, naturally, we start by trying to understand what was the original software about and the pains regarding this software. Understanding the business part behind is critical, we thought. Long story short, the legacy software had a couple of problems, mainly two big ones. The first one was the use of a rules engine that was a mess in the long run. There was a lack of transparency and redundancy regarding the effect of the rules that were mapped in the software. The second one, the most critical, part of this system used proprietary Red Hat technology that could not scale very well. To scale it, the company needed to buy more machines from Red Hat and maintain them. This imposed a problem. Thus, a rewrite was in need. We search for a few options to substitute the fuse part of the software and thus, avoid the rewrite. We concluded that it would not work… a wrong conclusion.

## The Beginning

<br /> After a little bit of discussion, we decide to do a little reverse engineering and try to map the system in terms of functionalities. Later, we found this to be a mistake. The code was hard to understand and we lost too many man-hours trying to do it. The system did not have tests, the database was a mess in terms of normalization and the code was too outdated to run normally locally. It was a lot of versions behind the current Java Spring version. Ah, also it used a lot of queues for doing simple tasks and it was a lot over-engineered. So, naturally, in the middle of the mapping functionalities in Golang code, we came up with a different solution

## The Project Structure

<br /> After a couple of weeks of digging, and not finding every flow of the project, we finally decided to start writing code. We decided to use microservices as architecture because of the need to scale faster and more efficiently. Dividing it this way makes scaling individual parts easy. Also, consequently, the system would turn out highly efficient and resource-oriented. In terms of low-level details, we start by creating 2 microservices:
- The management part, where an API would control all the information that would need to be on the system for it to perform all the requirements set.
- The rules engine part, where we would need to still have a rules engine, to trigger multiple components and to force flows in code. It is easier for business people to add rules, instead of adding code. Also, at this point, we theorize that we would need two more microservices, which would not be done at this part and would be kicked out to the end of the project.
- Live reporting, a system that tracks and adds transparency to the system gives us a view of the internal status of the objects that are being manipulated by the system. We have metrics and logs, but that doesn’t give us an accurate status of every object that the system produces and its internal status. And yes, this is important for business people.
- The UI for the rules engine. So, as stated above, we need to find a way to know which rules are in the system and not create redundancy of the rules. Also, having a way to simulate a dry run of specific is a must-have. A UI would be ideal for that.
- Also, we decided to use something to communicate between microservices, because there is a need for that to be shared. So an extra component like an Apache Kafka or a RabbitMQueue would be needed to be used.

## Interaction with other teams

<br />Being this enterprise, a big company it is divided into multiple departments with multiple responsibilities. We, being in the software engineering part, do not concern ourselves with data migration. So, we created a Jira ticket for the infra team to migrate the database, which was on an on-prem machine to AWS. This was the first milestone of the project. The infra team could only do this at the end of the project, so as you can imagine our roadmap became a mess. So, here I give you the first big lesson:

> *If you need work done by other departments, pressure them and mark your work as important. Otherwise, it will always be kicked down for the end of the road. Remember, be selfish regarding this, and your project will succeed*

To give you the full story, the thing is that each department has a lot of responsibilities and a lot of work in its backlog. You need to push your project and pressure them a little bit for it to be done. Otherwise, other stuff will always be more important. It was my first time working and a big company and this lesson will always be in my mind during the journey in the corporate world.

## The first realization

<br />  In the middle of the rewrite, we had an epiphany. We decided to check with other teams what endpoints and flows they were using regarding the old system. We found out that it was a lot less than we expect. By our luck, we have already covered most of them, but we still, had a lot of man-hours wasted on trying to reverse-engineer a legacy project. So, here is your second piece of advice:

> *When rewriting software, seek learning processes not reverse engineer the product*

This lesson is pretty much self-explanatory, but given a little more context, legacy projects tend to be a lot more over-engineered with a lot of hacks, that new technology may support by default. So, you should not waste time reverse-engineering it. You should seek the processes that the project uses and implement them in the new software that you are writing. In conclusion, treat the rewrite as a whole new software, not an upgrade version of an old system.

## The second realization

<br /> Businesses are organic and move on their own. A learned this the hard way. You can plan a rewrite for a year, but you should acknowledge that priorities may change. Business needs are always changing, and what is important today, may not be important tomorrow. So, you should always default to the old moto:

> *Move fast, break stuff*

You should always move fast and try to integrate with the old software. If you are working on a distributed system, redirect some requests from production to see the output and if you rewrite works correctly. Because you may not have the time you plan on the beginning to rewrite the old legacy system. In our case, life happens, the company was bought and the main objectives for the year changed. We are currently working on the project, but with the change of the company to more client-oriented, some shortcuts will give us a pain in the ass to fix in the future. 

## The conclusion
<br />  What I first thought would be a clean rewrite, turned out to be more of a grey one. So, at this point, I don’t know what to expect. I still see a light at the end of the tunnel, a medium one. I think this rewrite will take a little more time than I was expecting. If you ask me what I would do differently, I would certainly not do this rewrite. It turns out to be a waste of man-hours in the end. Yes, it most certainly will work and the company will benefict greatly from it. But, if I had a chance to do it again, I would start by substituting the fuse flows with Golang code and later concern myself with the rest of the system. Little by little, I could do it easier and be always adapted to the business context.




