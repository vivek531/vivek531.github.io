---
layout: post
title: "Spark Design Patterns"
date: 2023-10-30
---

Spark is being used for many purposes in tech industry.

Mainly in places such as data warehousing, data science, AI/ML, A/B testing, and metrics reporting.
Best place to learn about Spark is https://www.youtube.com/@Databricks/playlists. It features many tech leaders talking about challenges faced working with practical use cases of Spark at scale.
There are many challenges when using SPark such as compute resource management, compute engine scalability, and user productivity.

Lets look at one such problem which is Spark shuffle scalability challenges.

According to this paper by LinkedIn engineering, the default spark external shuffle service has multiple challenges when used at large scale. SO, they came up with a shuffle service that improves the shuffle operation.
Few key points on how they improve shuffle are
1. Instead running shuffle service on all nodes, they run their shuffle service as a standalone service.
2. They also do merging of mapper output before the data is sent to the reducer tasks, improving the IO of the system.

https://docs.google.com/document/d/1mYzKVZllA5Flw8AtoX7JUcXBOnNIDADWRbJ7GI6Y71Q/edit
https://issues.apache.org/jira/browse/SPARK-32915

