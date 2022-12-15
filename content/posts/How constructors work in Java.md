+++
title = "How constructors work in Java"
author = ["Shweta Kadam"]
date = 2021-06-14T21:41:00+05:30
tags = ["constructors", "java", "programming", "", "concepts"]
draft = false
+++

Constructors are used every time to initialize instance variables. There are some additional rules associated with constructors that are often asked in interviews.Hence revising those here through a blog post.


## A constructor is used to initialize instance variables {#a-constructor-is-used-to-initialize-instance-variables}


## When an object of an class is created,JVM goes to the class and searches for that matching constructor.If Constructor is NOT PRESENT it gives a compile error. {#when-an-object-of-an-class-is-created-jvm-goes-to-the-class-and-searches-for-that-matching-constructor-dot-if-constructor-is-not-present-it-gives-a-compile-error-dot}


## By default every class has a constructor called default no argument constructor. {#by-default-every-class-has-a-constructor-called-default-no-argument-constructor-dot}

```java
class A{
A(){ //default no arg constructor
}}
```


## A programmer can have multiple constructors in a class provided their signatures are different this is called constructor overloading. {#a-programmer-can-have-multiple-constructors-in-a-class-provided-their-signatures-are-different-this-is-called-constructor-overloading-dot}

```java
class A{
A(){
//some code
}

A(int x){
//some code
}

A(float x){
//some code
}

A(float x,int y){
//some code
}
A(int x,float y){
}
A(int z){}//THIS WILL GIVE COMPILE ERROR SInce its already defined on top.

}

A a=new A();
new A();//goes to first matching constructor
```


## JVM always calls the matching constructor from the class.HOWEVER,a programmer can call other constructors of this class by using the the this() method. {#jvm-always-calls-the-matching-constructor-from-the-class-dot-however-a-programmer-can-call-other-constructors-of-this-class-by-using-the-the-this-method-dot}

```java
class A{
A(){
System.out.println("A");    //I
A(int x){
this();                     //this will go to constructor A();
System.out.println("AA");   //II
}
}
class App{
public static void main(String[]args){
new A(5);
}}

OUTPUT:
A
AA
```


## If a programmer desires it can call the constructor of the super class as well from its own constructor using the super() method. {#if-a-programmer-desires-it-can-call-the-constructor-of-the-super-class-as-well-from-its-own-constructor-using-the-super-method-dot}

```java
class A{
A(){
System.out.println("A");    //I
}
}
class B extends A{
B(){
super();             //this is called implicitly refer next point also
System.out.println("B");
}}


class HelloWorld {
    public static void main(String[] args) {
        new B();
    }
}
OUTPUT:
A
B
```


## Whenever a programmer creates a constructor ,JVM writes super() in every constructor implicitly as its first line. {#whenever-a-programmer-creates-a-constructor-jvm-writes-super-in-every-constructor-implicitly-as-its-first-line-dot}

Note:If a class does not extend any class it by default extends the Object class. Do Try this code in your ide to see it for yourself

```java
class A{
A(){
//super will be called implicitly at the first line of this constructor and here since it does not extend any class it will extend the Object class
System.out.println("A");    //I
}

A(int x){
//super will be called implicitly at the first line of this constructor
System.out.println("AA");
}}


class HelloWorld {
    public static void main(String[] args) {
        new A(5);
    }
}
OUTPUT:
A
AA
```

That’s all for constructors in Java.

Happy Learning :)
