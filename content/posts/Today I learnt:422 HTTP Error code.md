+++
title = "Today I learnt:422 HTTP Error code"
author = ["Shweta Kadam"]
date = 2022-11-20T19:38:00+05:30
tags = ["http", 422, "422unprocessableentity", "httperrorcode"]
draft = false
+++

Today while testing a soap API at work, I came across this HTTP error code called ****HTTP/1.1 422 Unprocessable Entity**** . According to MDN Web docs, it means the following :

>
>
> The HyperText Transfer Protocol (HTTP) 422 Unprocessable Entity response status code indicates that the server understands the content type of the request entity, and the syntax of the request entity is correct, but it was unable to process the contained instructions.

It means that the syntax of the request is correct and well-formed but it has semantic, logical errors. Meaning the soap body xml format will be correct but the issue arises because of the content inside the XML tags\*. In this case, it could be the following:

-   Wrong character within the code.
-   The server doesn’t understand the content within a particular XML tag.
-   Or it refuses to process any other content inside the tag other than a fixed decided value).

Difference between 422,404 and 415 Error codes .Permalink
According to [RFC](https://www.rfc-editor.org/rfc/rfc4918#section-11.2),

>
>
> The 422 (Unprocessable Entity) status code means the server understands the content type of the request entity (hence a 415(Unsupported Media Type) status code is inappropriate), and the syntax of the request entity is correct (thus a 400 (Bad Request) status code is inappropriate) but was unable to process the contained instructions. For example, this error condition may occur if an XML request body contains well-formed (i.e., syntactically correct), but semantically erroneous, XML instructions.

In testing a soap API, the content type of the request body was correct. I checked for Content-Type header while testing) – Hence 415(Unsupported Media Type) was not valid. For soap,it was Content-Type: text/xml; charset=UTF-8. And the syntax of the request body was also correct– Hence 404(Bad request) was not valid.

The error occurred due to an incorrect value in the XML tag in my case. Value should have been `<ns8:exampleTag>123</ns8:exampleTag>` instead of `<ns8:exampleTag>456</ns8:exampleTag>`
