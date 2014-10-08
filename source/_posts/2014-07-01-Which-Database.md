---
layout: post
title: Which database?
categories:
- Articles
tags:
- Database, SQL, NoSQL, Graph, Redis, Neo4J, CouchDB, MongoDB, PostGreSQL
status: publish
type: post
published: true  
meta:
  _publicize_pending: '1'
author: 
---

We have come a long way from the days where database development meant designing relational models  for a database like Oracle or
SQL Server. The last few years have seen a proliferation of databases that are meant to perform very specific tasks.Application
server middle-ware have also become more flexible and now support multiple data sources instead of having to use just a single DB.

Since there are so many options out there it is important to understand the strength and weakness of each and use databases
appropriately, based on functional or non-functional requirements. Here's a handy map of some of the most popular databases and
where they would fit into your application architecture.

![Which database?](/images/Which_Database.png "Which Database")

In addition to picking a database based on functional requirements, one may require to access them based on the compromises
each one makes in terms of supporting *consistency*, *availability* and *partitioning tolerance*. A popular thumb-rule for such
an assessment is known as the **CAP Theorem**. CAP theorem states that most databases would be able to satisfy two of the
three conditions above, but not all - so every database makes a compromise in one of these parameters to satisfy the other
two. If one of these parameters are important for an architecture, it may be pertinent to know if a database is making a compromise
before making a choice.

Want to know more? Check out [Seven Databases in Seven Weeks](http://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921/ref=sr_1_1?ie=UTF8&qid=1404529485&sr=8-1&keywords=seven+databases+in+seven+weeks "Seven Databases in Seven Weeks")

