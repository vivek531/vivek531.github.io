---
layout: post
title: "Divide and Conquer"
date: 2017-10-28
---


Divide and conquer algorithm design technique is one of the first designs that we learn in college. But, how many of us remember the principle and use in our day to day activities.
I want to give a refresher on the topic and also explain some concrete problems solved by it.

There are three steps of designing a divide and conquer strategy.

1 - Divide the problems in smaller problems.
2 - Recursively solve the smaller problems.
3 - Combine the results obtained by recursive calls.

Just looking at this 3 step procedure without understanding it would be a disservice to this useful technique. Lets understand it using a concrete example.

Sorting is a canonical example of applying divide and conquer strategy. Our input is an unsorted array of integers and we want to sort this
array.

We divide the array into two subarrarys of equal length and solve the subarrays recursively. After getting the results of recursive calls,
we need to combine the results of these two subarrays.

