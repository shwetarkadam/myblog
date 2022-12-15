+++
title = "Which would you go for? Spring boot cron job,scheduled tasks vs Events in Mysql."
author = ["Shweta Kadam"]
date = 2022-01-12T23:49:00+05:30
tags = ["cronjob", "debugging", "development", "events", "java", "mysql", "spring", "springboot", "sql"]
draft = false
+++

I was recently studying about using cron jobs in spring boot for a particular use case for my small side project. I ended up not using the cron job but rather went the SQL way(will explain this in detail below). However,in the process I learnt a lot about cron jobs and scheduling in spring boot so this is just a small article about my learnings.

But first I shall tell you a little about my use case and why I thought about cron jobs in the first place…..


## Use case {#use-case}

My application was inserting data (let’s call it smash data for simplicity for now)in the database.Each smash data has a certain expiry period and after that expiry period, that data should no longer remain in the database.But the expiry period will be different for each smash data.

Example:

smash 1, expiryperiod :10mins

smash 2 ,expiryperiod :60mins

smash 3 ,expiryperiod :150mins . . . etc.

Now my first line of thinking ended up being cron jobs which led to me studying about cron jobs and scheduled in spring boot.To answer it simply I didn’t end up taking this route is because cron jobs or scheduled tasks are suited when we expect the task to execute at only a particular point of time or where we expect functionality to be executed at w particular time on an hourly/daily /weekly/monthly basis. I could get the cron job to delete the data but to delete WHICH data smash 1 or smash 2? That would mean I would have to check the DB. So the process would be something like:-

Fetch all rows from DB.
Check timestamp of each row data against current timestamp and delete accordingly.
I wanted to avoid writing the searching, comparing time logic (dates, in general, can be a pain sometimes).The logic which I did ended up going through was events in SQL since I’m using MySQL db for the use case

> Mysql events are tasks that run according to a particular schedule …hence they can be called as scheduled events

When an event is created in MySQL, a named database object is created and this object consists of one or more SQL statements to be executed at some regular intervals.Using events,I didn’t have to retrieve and search the data (as I had to do in the spring boot controller ) . I could just write an event such as

```sql
Delete from table1 where
expiry period < NOW();
```

And schedule this to execute `every minute`. Which was would check for that expiryPeriod column in each row and compare with time NOW() So any rows whose expiryperiod has passed will be deleted from db.

The only thing to note I see in this approach, for now, is that this is database dependent so when I host this side project (a hopeful dream) I need to make sure events is configured for the same. So this was the use case now back to cron jobs!


## Cron jobs or schedule tasks in spring boot.Permalink {#cron-jobs-or-schedule-tasks-in-spring-boot-dot-permalink}

When a situation arises where we expect the task to execute at only a particular point of time or where we expect functionality to be executed at a particular time on an hourly/daily /weekly/monthly basis. Cron jobs are suitable for this use case. In spring this sort of scheduled task can be achieved through @Scheduled annotation.

There are a few rules while using the @Scheduled annotation:  1. The method should typically have a void return type else the returned value will be ignored.

the method should not expect any parameters. First, to enable scheduling in the spring boot project, use @EnableScheduling in the main class.

```java
public class Application {
 public static void main(String[] args) {
 SpringApplication.run(PasteBinApplication.class, args);
 }
}
```


## Scheduling using CRON expressions {#scheduling-using-cron-expressions}

```java
@Component
public class SchedulerService {
    @Scheduled(cron="*/15 * * * * ?")
    public void testScheduled()
    {
        System.out.println("Method executed at every 15 seconds. Current time is :: "+ new Date());
    }
}
```

A guide for cron jobs: cron Image source :Java Techonline
![](/img/cron.PNG)

```bash
SEC  MIN   HOURS   DAY  MONTH  WEEKDAY
 *    *      *      *     *      *
```


## Scheduling using initial delay,Fixed Delay or Fixed Rate {#scheduling-using-initial-delay-fixed-delay-or-fixed-rate}

The main difference between Fixed Delay and Fixed Rate is : Fixed Delay : controls the next execution time when the last execution finishes. Fixed Rate : makes Spring run the task on periodic intervals even if the last invocation may be still running.

Fixed Delay

```java
@Component
public class SchedulerService {
    @Scheduled(fixedDelay = 1000, initialDelay = 5000)
    public void testScheduled()
    {
        System.out.println("Method executed with fixed delay and initial delay . Current time is :: "+ new Date());
    }
}
```

Also Fixed Delay can take input in String and Integer. @Scheduled(fixedDelayString = “7000”) @Scheduled(fixedDelayString = 7000)
Fixed Rate:

```java
@Component
public class SchedulerService {
    @Scheduled(fixedRate = 1000)
    public void testScheduled()
    {
        System.out.println("Method executed with fixed rate . Current time is :: "+ new Date());
    }
}
```

That’s all folks.Learning about events and cron jobs and where could be applied was interesting to learn when applied on some small practical application.
