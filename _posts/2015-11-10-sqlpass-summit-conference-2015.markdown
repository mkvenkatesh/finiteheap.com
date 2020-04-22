---
layout: post
title:  "PASS Summit Conference 2015"
date:   2015-11-10 20:15
categories: microsoft
comments: true
disqus_id: "pass_summit_conference_2015"
---

## PASS Summit ##

This month is full of conferences. I was at the
[Tableau Conference]({% post_url 2015-11-03-tableau-conference-2015 %})
recently and the following week I had the privilege to attend PASS
Summit 2015, which is about Microsoft SQL Server and BI, courtesy of a
free conference pass from Microsoft. The conference took place in
Seattle this year at the Washington State Convention Center between
Oct 27-30. There were about 4,000 registered attendees this year.

<img class="center-image" src="/assets/images/pass15_reception.jpg"
alt="PASS Summit 2015 Welcome Reception">

## SQL Server 2016 ##

The talk was mostly about SQL Server 2016, no surprise there. The
starting keynote pretty much went through the features of SQL Server
2016. Here's the cliff notes version of keynote that I scribbled on my
notepad.

* **Stretch DB**: You can store part of a table in Azure and the rest
  on-site. When you issue a query against the table using a client such
  as SSMS, the SQL engine does a remote query to Azure and combines
  the on-site data and produces the result.

* **Always Encrypted**: You can select the columns you want to encrypt
  in a table using a simple wizard. You can select deterministic
  (searchable data) or randomized encryption for the columns. The
  encryption/decryption happens on the client side. SQL Server itself
  doesn't do anything. The first time you try to turn on the
  encryption, the data is downloaded to the client, encrypted with a
  key on the client and pushed the SQL server. The data in the SQL
  server is now encrypted for these columns. You need the key on the
  client side to decrypt the data.

* **Real Time Analytics**: SQL 2016 combines in-memory OLTP with
  in-memory columnar storage so that you can perform real time
  anaytics on the transaction system with minimal impact. You don't
  need to do ETL from OLTP to DW to perform reporting and analytics.

* **Advanced Analytics**: R is integrated right into SQL 2016. You can
  just copy/past any R code directly into T-SQL and run the script
  with the results.

* **Mobile BI**: Datazen and Power BI Mobile integration comes with
  SQL Server 2016.

## Tools Clarity ##

There was some clarity on what tools to use for BI and when to use
them. Microsoft has a mess of products when it comes to BI and with
the recent acquisition of Datazen it wasn't clear where the different
products stand. Here's what Microsoft now recommends on BI tools
usage.

|             | Model    | Analyze & Authorize                              | Deliver  |
| ----------- | -------- | ------------------------------------------------ | -------- |
| **Cloud**   | Power BI | Power BI                                         | Power BI |
| **On-Prem** | SSAS     | Excel, Power BI Desktop, Report Builder, Datazen | SSRS     |

<br>

## Features & Improvements ##

Here are some of the new features and improvements to the different BI
tools that I gathered from the conference.

### SSRS in SQL 2016  ###

* SSRS is being pushed as the primary reporting tool for
  on-prem. PowerBI is for the cloud.

* SSRS in SQL 2016 is HTML5 based. Visuals are updated to look more
  modern like PowerBI.

* Better SSRS parameter controls. You can add spaces, multiple lines
  and all that but the parameters are still grouped on to the top or
  the side of the report. You can’t add a parameter in the middle of
  the report say.

* SSRS is going to have its own web portal (responsive and really
  nice). The portal shows all the SSRS reports built with report
  builder/SSDT and also the mobile reports built with PowerBI
  mobile/DataZen.

* Report builder has a new look and feel. Looks more modern.

* You can pin any SSRS report directly to a PowerBI dashboard.

### SSAS Tabular in SQL 2016 ###

* SSAS 2016 provides many-many relationships and bi-directional
  cross-filtering out of the box.

* We can now organize dimensions and measures into folders (like BIDS
  helper functionality) now available in both Visual Studio and
  PowerPivot.

* Visual Studio 2015 has better DAX editing support and so does the
  new report builder. You can enter DAX into multiple lines, add
  comments, declare variables, syntax highlighting and better error
  status.

* There’s no more workspace server that’s required for building SSAS
  tabular models in Visual Studio.

* Direct Query mode (SSAS queries data sources directly instead of
  pulling into in-memory first while processing) is 20x faster than in
  SQL 2014.

### DataZen/PowerBI Mobile ###

* Datazen and PowerBI mobile is going to be combined into one product
  to build on-prem mobile reports. PowerBI/SSRS reports are not mobile
  friendly so if want mobile stuff we really need to use two different
  products.

* Datazen will be part of SQL Server 2016.

### Power BI ###

* PowerBI can now connect to on-prem SSAS server directly.

* PowerBI is going to come with something called “enterprise gateway”
  where you can take any on-prem database and provide it as a source
  to PowerBI without pushing any of the data to the cloud. You can set
  security, policies, admins etc at this level.

* You can embed Excel reports in PowerBI now.

* Visualizations are based on D3.JS and is open sourced so we can built
  custom visualizations and publish it to PowerBI.

* PowerBI Desktop is a windows application that you can download and
  run to build PowerBI content and publish it to PowerBI.com
