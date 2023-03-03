+++
title = "Today I learnt TIL: jq"
author = ["Shweta Kadam"]
date = 2022-12-22T21:45:00+05:30
tags = ["til", "jq", "json"]
draft = false
+++

Today at work once again I had to inspect a json body which was not beautified. Normally I turn to Postman and use the beautify option.
      But my mac cried and was freezing in instances begging for me to not open more application :(
      This is where I came across a nifty tool called  ****jq****

jq is a lightweight and flexible command-line JSON processor. It is like sed for JSON data. It can used to transform json data into more readableformat.
For example :

```json
         ❯ echo  '{"fullName": {"firstName": "Bruce","middleName": "Clark", "lastName": "Wayne" }}' | jq .
       {
         "fullName": {
           "firstName": "Bruce",
           "middleName": "Clark",
           "lastName": "Wayne"
         }
       }
```


## Where and why would you use it? {#where-and-why-would-you-use-it}

There are a few reasons I could think of why I would use jq regularly:

<!--list-separator-->

-  Similarly like my situation above, if you want to avoid opening gui apps or online code beautifiers ,this is a great option.

<!--list-separator-->

-  Once can prettify a curl output with jq.

    This is a great option when you pretty json output on the go for example `healthcheck` urls of your application apis.

    ```json
            curl http://example-api-url-you-are-calling.com | jq .
            curl http://example-api-healthcheck.com/healthcheck | jq .
    ```

<!--list-separator-->

-  jq is ubiquitous means it is pre-installed in most machines (even cloud vms such as aws and microsoft vms).

    So next time you want pretty output of a json which is present in an ec2 instance.
    You dont need to do the manual work of copy and paste and json and figuring it out later.

<!--list-separator-->

-  Also I think its pretty secure than the online third party websites developers tend to use to prettify json ,xml while working. Especially when dealing with secret private data which is sometimes pasted on to a random code beautifier website.

<!--list-separator-->

-  And pretty handy when you lose internet connection ;)

<!--list-separator-->

-  When used in shell scripts , it can save a lot of time and manual effort.

    This is useful cheat sheet with good example to refer <https://lzone.de/cheat-sheet/jq>
