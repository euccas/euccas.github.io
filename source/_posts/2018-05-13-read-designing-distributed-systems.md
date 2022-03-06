---
layout: post
title: "Reading Notes - Designing Distributed Systems"
date: 2018-05-13 18:22:12 -0700
comments: true
categories: Reading System-Design
keywords: reading notes distributed systems design patterns
description: reading notes distributed systems design patterns
---

Recently I read a book [Designing Distributed Systems](http://shop.oreilly.com/product/0636920072768.do), which is written by [Brendan Burns](https://twitter.com/brendandburns), and published by O'Reilly earlier this year. This book introduces the patterns and components used in the development of distributed systems. 

Before I started to read this book, I had three questions in my mind, and try to find the answers from the book. Those three questions are:

1. What's the most important difference between designing distributed systems and single machine systems?
2. Why container technology, such as docker, kubernates, is so popular? How could it be helpful?
3. What are the common patterns used in distributed systems design, and when shall I use them?

This book does give me the answers, at least partial ones. I put my reading notes into a Google Slides, and  [you can find it here to read the details](https://docs.google.com/presentation/d/1srX9hRS9tbtrEx7T1abxbHiD1gASkvllf1_W2SjuadA/edit?usp=sharing). A PDF version in light background color is [available here](https://github.com/euccas/euccas.github.io/blob/source/data/read-2018-design_distributed_systems_lightver.pdf).
 
The short answers to my questions are as in the following:

<!--more--> 

## What’s the most important difference between designing distributed systems and single machine systems?

- Designing distributed systems can be significantly more complicated to design, build, and debug correctly.
- Designing distributed systems need much more efforts in designing for scalability and reliability.
- In a distributed system, tasks/data are spreaded to multiple workers. It requires techniques like containers and load balancing to utilize parallelisation

## Why container technology (docker, kubernetes) is so popular? How could they be helpful?

- Containers are not only useful for applications which have components running on multiple machines, but also for single machine applications.
- The goal of containerization is to **establish boundaries** around specific resources, team ownership, separation of concerns.
- The benefits include **resource isolation**, **scaling teams**, **reuse components and modules**, **break big problems** into smaller ones (Small, focused applications are easier to understand, be tested, updated and deployed)

## What are the common patterns used in distributed systems design, and when shall I use them?

The book describes three types of patterns.

- **Single node** patterns: sidecar, ambassadors, adapters
- **Serving** patterns: sharded services, scatter/gather, FaaS, etc.
- **Batch computational** patterns: Work queue, Event-driven batch processing, coordinated batch processsing, etc.

You can find more detailed description of each design pattern in my reading notes.


