+++
title = "Integrating Swagger OpenAPI for easy API documentation in spring boot"
author = ["Shweta Kadam"]
date = 2022-01-16T22:53:00+05:30
tags = ["api", "apidocumentation", "restapi", "springboot", "swaggeropenapi"]
draft = false
+++

These days I am more into creating backend projects which include microservices.But if anyone wants to test these services one needs postman or do the old classic way of curl command.

Both do the job brilliantly but what if I wanted some user who doesn’t want to install postman or use curl and still wants to test my live APIs thru the browser? I came across this ****swagger open API specification****  and this is a really handy tool!

In layman’s terms, Swagger OpenAPI specification provides API documentation for REST APIs. An OpenAPI file allows you to describe all the APIs within the project and even lets you try out the APIs!

Available endpoints can be /projectApi and all operations on each endpoint which can GET /getProjectApi , POST /insertProjectApi , DELETE /deleteProjectApi .

[[]]
Also, integration of swagger open API is pretty painless in spring boot and it lets users try out the APIs within the browser without any installation of any software from the user (sounds pretty convenient and sweet to me)

In this post, I will describe how I integrated swagger open API in Spring boot project.First you need a spring boot project having basic dependcies using Spring Initializr <https://start.spring.io/> or you could use this project used in the example here

First add the springdoc-openapi-ui dependency to pom.xml:

```xml
<dependency>
   <groupId>org.springdoc</groupId>
   <artifactId>springdoc-openapi-ui</artifactId>
   <version>1.6.4</version>
</dependency>
<dependency>
```

Then run the application and check the below url to check open api specification

```bash
http://localhost:8080/v3/api-docs/
```

You should be able to see something like this

You can also add a custom path by adding entry in ****application.properties**** file

```bash
springdoc.api-docs.path=/api
springdoc.swagger-ui.path=/swagger
springdoc.swagger-ui.operationsSorter=method
```

Check <http://localhost:8080/swagger> for web UI.To show you in this example we have a following apis in the controller

```java
package com.TestDocker.BooksDocker.Controllers;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.server.ResponseStatusException;

import com.TestDocker.BooksDocker.Models.Book;
import com.TestDocker.BooksDocker.Repository.BookRepository;

@RestController
public class MainController {
	@Autowired
	public BookRepository bookRepository;

	@GetMapping("/test")
	public String test() {
		return new String("Working from DOcker Bopoks proj ");
	}
	@GetMapping("/")
	public List<Book> fetchAllBooks() {
		List<Book> books;
		try {
			books = bookRepository.findAll();

		} catch (Exception ex) {
			throw new ResponseStatusException(HttpStatus.INTERNAL_SERVER_ERROR, "Error occured in fetchAllBooks", ex);

		}
		return books;
	}

	@GetMapping("/{bookID}")
	public Book fetchBookfromID(@PathVariable("bookID") Long bookID) {
		Book book;
		try {
			book = bookRepository.getById(bookID);

		} catch (Exception ex) {
			throw new ResponseStatusException(HttpStatus.INTERNAL_SERVER_ERROR, "Error Occured in fetchBookfromID", ex);

		}
		return book;
	}

	@GetMapping("/search/{title}")
	public List<Book> searchBookByTitle(@PathVariable("title") String title) {
		List<Book> books;
		try {
			//System.out.println(title);
			books = bookRepository.fuzzySearchByTitle(title);
			System.out.println(books);

		} catch (Exception ex) {
			throw new ResponseStatusException(HttpStatus.INTERNAL_SERVER_ERROR, "Error Occured in searchBookByTitle", ex);
		}
		return books;
	}

	@PostMapping("/insertBooks")
	public String insertBooks(@RequestBody List<Book> books) {

		for (Book b : books) {
			System.out.println(b.toString());
			Book b1 = bookRepository.save(b);
			if (b1 == null)
				return "Book object is null";
		}
		return null;
	}
}
```

 So the swagger ui look something like this.
 Also json docs will be available at <http://localhost:8080/api> springdoc.swagger-ui.operationsSorter=method sorts the API paths in order of their HTTP methods.
You can try and test the apis from web ui too.It also shows schema information!
Overall this is a much convenient way of setting up documentation for your apis which can be handy in some situations.

That’s all folks!
