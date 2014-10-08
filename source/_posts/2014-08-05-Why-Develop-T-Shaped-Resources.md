---
layout: post
title: Why Develop T-Shaped Resources for Agile Development
categories:
- Articles
tags:
- Agile, Software Development, Lean, T-Shaped, Resources, Kanban
status: publish
type: post
published: true 
meta:
  _publicize_pending: '1'
author: Sathish Hariharan
---

I first came across the concept of the T-shaped resource in Donald G Reinersten's [book](http://www.leanproductflow.com/)
on Lean Product Development. It is discussed as a principle under the section on applying WIP constraints. The discussions
revolve around 3 types of individuals with different types of capabilities - experts, generalists and t-shaped resources. The significance
of this concept struck me later when I started digging into the principles of software [Kanban](http://kanbanblog.com/explained/)

The core principle of software Kanban stresses on **one-piece-flow**. Unlike techniques like scrum, there is
no sprint planning that is required to prioritize the user stories for the next sprint, instead the next set of
high-priority stories are always available in a short-listed version of the product backlog. Development team *pulls" the
next story and starts working on them as soon as there is free capacity (i.e. as long as WIP constraints are met). The difference
from other agile development processes is that when a block is experienced the entire flow is stopped to clear the blockage. This
is where the concept of different types of resources or profiles come into play. The process of addressing a block is explained in
the following diagrams that I have borrowed from the [Kanban_and_Scrum](http://www.crisp.se/henrik.kniberg/Kanban-vs-Scrum.pdf) InfoQ book

![Kanban 1](/images/Scrum_vs_Kanban1.png)

![Kanban 2](/images/Scrum_vs_Kanban2.png)

![Kanban 3](/images/Scrum_vs_Kanban3.png)

All the three types of profiles (I prefer 'profiles' to 'resources', it sounds more human) can be used to clear blockages in a
work queue. **Experts** have tremendous solving power to clear up technical bottlenecks. So deploying experts in each step can help
clear up blocks. But it is difficult to achieve significant depth of expertise and such profiles are scarce. **Generalists** are
profiles that can be deployed in any of the steps in a queue. They can be used to clear minor blocks that occur due to resource
unavailability but again finding resources with knowledge of many steps of the process is again difficult.

**T-shaped resources** provide an alternative to the constraints faced in developing and deploying experts and generalists. The idea
behind a T-shaped profile is an individual who has sufficient depth in a particular area but can also seamlessly shift to adjacent
process steps in a flow. An example would be an expert tester, who can also move easily to development and deployment. When development
faces a capacity bottleneck and cannot move a work item forward, this naturally frees up capacity of testers since there are less
items in their backlog due to upstream WIP constraints. This frees up a T-shaped test resource to easily shift focus to development to clear up
work items blocked due to lower capacity. As added benefits, such movements also result in improved communication and variety of work.