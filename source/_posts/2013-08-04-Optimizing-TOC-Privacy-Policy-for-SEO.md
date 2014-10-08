---
layout: post
title: Optimizing TOC and Privacy Policy for Single Page Apps
categories:
- Articles
tags:
- SEO, Single Page Apps
status: publish
type: post
published: true 
meta:
  _publicize_pending: '1'
author: Sathish Hariharan
---

**One Line Advice = ‘Don’t Include in your Single Page’**

Single Page Applications written in Javascript are very popular these days. All content loads in a single page and when the user clicks on links they see ‘blazing’ performance since pages don’t load from the server.

Almost all Apps today need to include pages around the Terms and Conditions (TOC) of use and Privacy Policy pages. Often times these pages have content that runs into many paragraphs and could be a significant portion of your site/apps content.

What we don’t realize when we add these monstrous pages of legal ramblings is how they impact our websites SEO in a negative fashion. When we have 100 words or relevant content in our app and 2000 words of legalese all included in a single page, the relevant content becomes 5% of overall site from a search engine perspective. Important keywords will have a much lower density and this has a significant effect on your page rankings.

The solution. Get rid of TOC and Privacy from your single page and add them as separate page URLs. Use your robot.txt to disallow the terms and privacy pages from getting indexed. Soon you will start seeing much more relevant content keywords within your webmaster console and better impressions overall.

See below a sample robots.txt on how you should configure your website. Reach out to your webmaster now.

![Sample Robots Txt](/images/robots_txt.png)