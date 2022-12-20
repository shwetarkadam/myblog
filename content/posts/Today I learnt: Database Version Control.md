+++
title = "Today I learnt: Database Version Control"
author = ["Shweta Kadam"]
date = 2022-11-07T15:49:00+05:30
tags = ["flyway", "liquibase", "databaseversioncontrol", "databaseschemachanges", "til"]
draft = false
+++

Upon stumbling upon this motivating HN post by [Simon Willison](https://simonwillison.net/2022/Nov/6/what-to-blog-about/) I have been inspired to start a Today I learnt(TIL) series of my own. This seems like a doable promising idea where I do not have the self-imposed pressure of researching for a blog idea and making a seperate time to write that specific post. Wrting this TIL flows naturally in day-to-day work flow where I could just say “Hey I just learnt about this XYZ ,I should write about it”.

Starting with Today’s TIL : ****Database Version Control****

What it is : A practice or form of maintining and tracking every change made to database schema, just like git version control(But this is specifically for Database). It acts like a single source of truth (like a git code repository)

This concept solves a lot of problems we face as developers such as :

As a developer,One must have faced a situation where to solve a particular problem statement or feature , you need to do database changes,however for those changes to reflect application needs to be restarted or you might have database and application code changes, an organization already has some processes defined for deployment. In development phase, one usually runs the db changes or sql queries in local generally via a sql client application.For example,Update some existing db property.

But for that same change to be reflected in production db, CICD processes are define fdd for deployment or a seperate team might be responsible for deployment altogether.Hence we cant expect a seperate db team to always be in sync with deployment team or that particular CICD process. Hence, DB schema changes should be deployed as a part of application code changes.

This is where database version control comes in handy where :

You need traceability and a commit history of db schema changes done before.
Protect prodcution database tables from unwanted or uncontrolled changes
Help in communication between teams regarding data(where a member can look at the query and provide feedback as a part of Pull request)
Applications such as liquidbase,flyway scripts come in handy Speaking of liquibase which works on changelog concept where you have

> A Changelog file which inside has -&gt; ChangeSet (which are used to define Db changes)- &gt; Which can include SQL Queries and Rollback queries if the changes dont work in that specific environment.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog
	xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
	xmlns:pro="http://www.liquibase.org/xml/ns/pro"
	xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
		http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-latest.xsd
		http://www.liquibase.org/xml/ns/dbchangelog-ext http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd
		http://www.liquibase.org/xml/ns/pro http://www.liquibase.org/xml/ns/pro/liquibase-pro-latest.xsd">


     <changeSet  id="1"  author="XYZ">
        <comment>

        </comment>
        <sql>
        INSERT INTO Exampledb.exampletable('id','name,'serial')
        VALUES("1","test","serial");
        </sql>

        <rollback>
        DELETE FROM  Exampledb.exampletable where id="1";
        </rollback>
 </databaseChangeLog>
```

This changelog file needs to be included in a master changelog file which consists a list of all change log files (Similar to how a git commit history consists of all commit ids)
