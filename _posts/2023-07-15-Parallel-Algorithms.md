---
layout: post
title: "Parallel Algorithms"
date: 2023-07-15
---

Now, we have multiple cores in our machines and we want to use those cores to work for us. How do we implement algorithms such that we use all the cores and how do we reason about the efficiency gains we get from new algorithms?

One model that helps in reasoning about the time complexity of parallel algorithms is called work depth model. It very simply tells us the run time of our parallel algorithm in terms of two parameters, work and depth.

What is `work` and what is `depth`?

To work out the `work` done by the algorithm, we ask ourselves the question - if we have one core to run our algorithm, how much time will it take to finish the work.
To work out the `depth` , we ask ourselves the question - if we have infinite number of cores, how much time do we take to accomplish the task.

The expression for time complexity for p number of cores then would be - `w/p + d`
