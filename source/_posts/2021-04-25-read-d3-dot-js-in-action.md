---
layout: post
title: "Read D3.js in Action"
date: 2021-04-25 17:56:43 -0700
comments: true
categories: frontend reading javascript
keywords: javascript d3.js frontend
description: book D3.js in Action reading notes
---

Recently at work, I have been working on developing a few features on top of [Apache Airflow](https://airflow.apache.org/). Some of the features are UI heavy, and require some amount of the data visualization using [D3.js](https://d3js.org/). While working on those features, I thought it could be a good chance to spend some time on learning D3.js in-depth, so I chose to read this book [**D3.js in Action**](https://www.manning.com/books/d3js-in-action-second-edition) on manning.com. Here comes a summary of this book, and some notes I took while reading.

{% img center /images/post_images/2021/20210425-d3js-book.png 360px %}

Overall I find this book is easy to read as long as you have some knowledge in JavaScript.  In this book, a few key concepts in D3.js are clearly laid out,  and the examples cover a good set of common usages and tactics you need to know for building data visualization features using D3.js.

This book has 11 chapters. Chapter 1, 2 and 3 are introduction to D3.js, the high level flow and common operations of using D3.js for information visualization, and how to structure a data visualization project with D3.js. 

In the first three chapters, alongside with the basic concepts, a few tactics I find worth learning from the very beginning are:

- **Integrate scales in data binding**: D3.js provides handy scale functions to normalize data values for better display. Example built-in scale functions include: ```d3.scaleLinear()```, ```d3.scaleSequential()```, ```d3.scaleQuantize()``` and so on. A D3 scale has two primary functions: .```.domain()``` and ```.range()```, both of which expect arrays and must have arrays of the same length to get the right results. The array in ```.domain()``` indicates the series of values being mapped to ```.range()```.

- **Enter, update, merge, and exit to update DOM elements**: Understanding how to create, change, and move elements using ```enter()```, ```exit()```, and selections is the basis for all the complex D3 functionality. One note here is D3 doesn’t follow the convention that when the data changes, the corresponding display is updated; you need to build that functionality yourself.

- **Getting access to the actual DOM element** in the selection can be accomplished in one of two ways:
  - Using ```this``` in the inline functions (cannot be used with arrow functions)
  - Using the ```.node()``` function

Using ```this```

```
d3.select("circle").each(function(d,i) {
    console.log(d);console.log(i);console.log(this);
})
```

Using ```.node()``` function

```
d3.select("circle").node();
```


Chapter 4, 5, 6, 7 and 8 introduce the methods and details of building specific types of visualization for specific types of data: chart components, layouts, complex hierarchical data visualization,  network visualization, and visualizing geospatial information. 

- One note about **Layouts**: D3 contains a variety of functions, referred to as layouts, that help you format your data so that it can be presented using a popular charting method. D3 layouts don’t result in charts; they result in the settings necessary for charts. Example D3 built-in layouts: ```d3.layout.histogram()```, ```d3.layout.pie()```, ```d3.layout.tree()``` etc.


Chapter 9 covers how to using D3 with React. The challenge of integrating D3 with React is that React and D3 both want to control the DOM. The entire select/enter/exit/update pattern with D3 is in direct conflict with React and its virtual DOM. The way most people use D3 with React is to use React to build the structure of the application, and to render traditional HTML elements, and then when it comes to the data visualization section, they pass a DOM container (typically an ```<svg>```) over to D3 and use D3 to create and destroy and update elements.


Chapter 10 and 11 are advanced usages about customizing layouts and components, and mixed mode rendering in HTML canvas.