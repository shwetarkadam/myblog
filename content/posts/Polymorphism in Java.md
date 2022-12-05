+++
title = "Polymorphism in Java"
author = ["Shweta Kadam"]
date = 2021-07-14T23:28:00+05:30
tags = ["polymorphism", "java", "programming"]
draft = false
+++

Just revisiting and explaining myself Polymorphism concept here through a blog post. The words Polymorphism means multiple forms.

In Java ,Polymorphism means multiple forms of an object. We shall divide this article into 3 sections.

1.Syntax

2.Calling a variable polymorphically.

3.Calling a method polymorphically.

1.SyntaxPermalink
Now in polymorphism in Java, the thumb key rule to remember is

super = subPermalink
Meaning the variable reference (LHS) must always be a super class reference and the object initialization(RHS) must a sub class.

For Example: class A{

} class B extends A{ }
class C extends B{ }
class D extends A{ }

So valid and invalid syntax according to the thumb rule will be

```java
A a =new B();           //VALID
B b=new D();            //NOT VALID
C c=new A();           //VALID
A a1=new D();           //VALID
```

2.Calling a variable polymorphically.Permalink
If a variable is called from a polymorphic object,we follow the reference i.e. the super class. And if the variable is not present in the super class ,it results in a COMPILE ERROR. EG:

```java

class A{
int x=5;
}
class B extends A{
int x=10;
}
class App{
public static void main(String[]args){
A a=new B();
System.out.println(a.x);
//What do u think is the output class A x value (5)or class B x value(10)?Follow the rule.

}
}
OUTPUT:
5
```

Calling a method polymorphically.Permalink
If a method is called from a polymorphic object ,we follow a 2 step procedure: 1.We got to the super class and check whther the method is present or not.

```bash
if(present)
 Goto to step 2
else
 COMPILE ERROR
```

2.Come to the sub class and check wther the method is overrided or not.

```bash
if(overrided)
 Call the sub-class version
else
 Call the super -class version.
```

Eg:

```java
class A{
void m1(){
System.out.println("A");
}}
class B extends A{
void m1(){
System.out.println("B");
}}
class App{
public static void main(String[]args){
A a=new B();
a.m1();          //Follow the rule
B=new B();
b.m1();          //Normal sub class object method call
}}
OUTPUT:
B
B
```

So that’s all for polymorphism in java.

Happy Learning :)
