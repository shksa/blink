# What is this?
This is an implementation of a compiler for a programming language called <b>Blink</b> described in the medium blog series : https://hackernoon.com/lets-build-a-programming-language-2612349105c6

## Features of Blink:
* Object-oriented.
* Statically-typed.

## Overview of Blink:
* <b>Datatypes</b>: int, float, bool, string. All types inherit from supertype <b>Object</b>.
* <b>Let expressions to declare variables</b>: 
```
let message: String = "Hello, Blink!" in {
    Console.println(message)
}
```
* <b>Omitting the curly braces</b>: Whenever the body contains a single expression the curly braces around the body can be omitted.
* <b>Functions</b>: 
```
func sum(a: Int, b: Int): Int = {
    a + b
}
```
```
func sum(a: Int, b: Int) = a + b
```
* <b>Classes</b>: all non-function properties are private and all function properties are public, getters and setters to access non-function properties
```
class Person {
    //non-function properties
    var firstname: String = "Klaus"
    var lastname: String
    var age: Int

    //getter
    func firstname(): String = {
        firstname
    }

    //setter
    func setFirstname(name: String) = {
        firstname = name
    }
}

let p = new Person() in { }
```
* <b>Constructors, inheritence, overriding</b>:
> 1. constructors:
```
class Person(firstname: String, lastname: String) {
    func firstname(): String = firstname
    func setFirstname(name: String) = firstname = name
    func lastname(): String = lastname
    func setLastname(name: String) = lastname = name
}
```
> 2. inheritence:
```
class Employee(firstname: String, lastname: String) extends Person(firstname, lastname) {
}
```
> 3. overriding:
```
class Person(firstname: String, lastname: String) {
    override func toString(): String = {
        firstname + " " + lastname
    }
}
```
* <b>Everything is an object</b>: Everything is an object. primitives like int's and double's are also objects. 1 + 2 is evaluated as 1.+(2). This is awesome feature which enables us to define operators to custom types.
* <b>There is no statement, only expressions and definitions</b>
The difference b/w an expression and a statement is that an expression always evaluates to a value but a statement just performs an action without evaluating to a value.
In javaScript:
```
if (<some condition>) {
    // some code that is evaluated
}
```
This is an if-statement, it does not evaluate to a value.
In Blink:
```
let isAnAdult = if(age >= 18) { true } else { false }
```
This is an if-expression, it evaluates to a boolean type value, so this if-expression can be used anywhere an expression can be used, like in an variable declaration.


## Stages the source code goes through in a compiler.
<img src="./images/compiler_stages.png" />

## Lexical Analysis:
Source code is analyzed for lexemes, which are meaningfull elements in the source language like <b>func, if, while, identifiers, strings, numbers, operators, single characters like { [ ; : , . etc.</b>.
> <b>A <i>lexeme</i> is uniquely identifiable string of characters in a source language</b>

From lexemes a sequence of tokens is generated.

> <b>A <i>token</i> is an object describing a <i>lexeme</i>.Along with the value of the lexeme (the actual string of characters) it contains information such as its type - <i>is it a keyword? is it a identifier? an operator?</i> and the position in source code where it appears (row number/ column number)</b>

If the compiler comes a string of characters it cannot identify as a meaningfull element of the source language it will throw an error and stop its execution.

<img src="./images/lexical_analysis.png"/>