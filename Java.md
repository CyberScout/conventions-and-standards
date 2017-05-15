# Java Coding Conventions

This document outlines conventions for writing Java code. These conventions
should also be adhered to for Groovy code, insofar as Groovy is mostly a
superset of Java. See the [Groovy](Groovy.md) document for rules and conventions
that are specific to Groovy, or differ from Java.

## Java Configuration

###### Use JDK 8 as the basis for all Java applications

JDK version 8.x **must** be used for all new development.

_Rationale:_ Java SE 8 is the current production-grade specification of the Java
language, runtime, and development tools. Older versions should not be used for
new projects.

Java SE 9 is currently in the final stages of development. However, even after
it is released, it will take some time before we consider it stable enough for
production applications. Development tools also need time to catch up to the
current spec. After Java 9 has had some time to "gel", we will begin evaluating
it for use in our own applications.

###### Use Spring Boot as the application framework for most Java applications

For web applications and APIs, Spring Boot **must** be used.

The application **should** run as a standalone JAR (embedded Tomcat or Jetty).
Alternatively, it **may** be packaged as a WAR and run in a JBoss EAP
application server, but only if the facilities of a full application server are
truly needed.

For other types of applications, such as batch processes, Spring Boot **should**
be used.

_Rationale:_ Spring Boot is an excellent foundation for building
enterprise-grade Java applications. It greatly simplifies using Spring, Spring
Web, Spring Security, Spring Batch, and so on.

### Build

###### Use Gradle for building Java-based projects

Gradle **must** be used to build Java projects. Some older projects use Maven or
Ant, but new projects must use Gradle.

_Rationale:_ Gradle is an advanced build system, that has the declarative
convenience and dependency resolution of Maven, but also provides powerful
scripting abilities to precisely control the build process when needed. Gradle
build scripts are generally more concise and easier to read than their Maven or
Ant counterparts.

## Package and File Structure

###### Follow Java's requirements for file naming and location

Source files **must** follow Java's requirements and best practices:

- Directory structure **must** mirror package structure
- Source file names **must** be the case-sensitive name of the file's top-level
  class, plus the `.java` extension

_Rationale:_ Java source code will not properly compile unless these rules are
followed.

###### Use CyberScout's package naming conventions

CyberScout applications must use the following package naming conventions:

| Package                        | Purpose                                                                                                                                                                                               |
|:-------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `com.notaneye`                 | Common top-level package for all CyberScout code                                                                                                                                                      |
| `com.notaneye.services`        | Top-level package for back-end services, APIs, etc.                                                                                                                                                   |
| `com.notaneye.apps`            | Top-level package for user-facing applications                                                                                                                                                        |
| `com.notaneye.processes`       | Top-level package for batch processes and the like.                                                                                                                                                   |
| `com.notaneye.[type].[name]`   | Top-level package for an individual project. `[type]` would be one of the types above. `[name]` is the simple name of the project.                                                                    |
| `...[name].api`                | REST-ful controllers and other API-related code, like request & response DTOs.                                                                                                                        |
| `...[name].common`             | Classes that are shared by multiple layers or verticals within the application.                                                                                                                       |
| `...[name].config`             | Application config, including Spring config classes, property beans, etc.                                                                                                                             |
| `...[name].controller`         | MVC controllers and other Web-related code, like request & response DTOs.                                                                                                                             |
| `...[name].doc`                | Configuration and other code for self-documenting APIs.                                                                                                                                               |
| `...[name].domain`             | Domain objects, typically with JPA annotations for persistence.                                                                                                                                       |
| `...[name].exception`          | Application exceptions.                                                                                                                                                                               |
| `...[name].repository`         | DAOs or Spring Data repositories.                                                                                                                                                                     |
| `...[name].security`           | Security-related classes, beans, and configuration.                                                                                                                                                   |
| `...[name].service`            | Business services. These should be the heart of the application, encapsulating business rules and orchestration.                                                                                      |
| `...[name].validation`         | Validation classes and functions that are specific to the application's data types.                                                                                                                   |
| `...[name].[lib or framework]` | Any code written specifically to integrate with a particular library or framework, For example, Spring `BeanPostProcessor` implementations, Hibernate `UserType` implementations, or Servlet filters. |

###### Do not use the default package

Classes **must not** be defined in the
[default, or unnamed, package](http://docs.oracle.com/javase/specs/jls/se8/html/jls-7.html#jls-7.4.2).

_Rationale:_
[The default package is considered bad practice](http://stackoverflow.com/a/7849460/115541).
First, class naming collisions are more likely, since the package name cannot be
unique. Second, a class in the default package cannot be imported by other
packages. Java provides the default package "principally for convenience when
developing small or temporary applications or when just beginning development".

###### One top-level class per file

Source files **must** contain exactly one top-level class (the top-level class
may contain inner classes, but no other top-level classes).

## Code Organization

###### Organize code logically

###### Keep members of the same type together

###### Keep overloaded members together

###### Avoid "utility" classes

### Naming

## Whitespace, Line Breaks, and Empty Lines

###### Wrap and indent when chaining method calls

### Indentation

###### Use CyberScout's K&R variant indentation style

Code **must** use CyberScout's stanrdard indentation style. This style is a
variant of the classic
[K&R style](https://en.wikipedia.org/wiki/Indent_style#K.26R), and incorporates
elements of the
[1TBS](https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS_.28OTBS.29),
[Java](https://en.wikipedia.org/wiki/Indent_style#Variant:_Java), and
[Stroustrup](https://en.wikipedia.org/wiki/Indent_style#Variant:_Stroustrup)
variants.

The CyberScout style incorporates the following rules:

- Starting brace is placed on the same line as the beginning of the block
- Ending brace is placed on its own line after the block
- Single line control statements must use braces
- Keywords in multi-block statements (e.g if/else, do/while, etc.) must align

_Rationale:_ Mostly a matter of taste, but consistency is important. Using
braces in a consistent way helps them to fade into the background, reducing the
syntactic noise. Aligning keywords like if & else helps to associate the blocks
together for the reader.

_Example:_

```java
public class Example {
    
    public void myMethod(int x, int y, String z) {
        
        if (x < 0) {
            return;
        }
        else if (x == 0) {
            beAwesome(x);
        }
        else {
            doSomethingElse(x);
        }

        int i = 0;
        do {
            i++;
        }
        while (i < y);
        
        try {
            grokString(z);
        }
        catch (NumberFormatException e) {
            throw new IllegalArgumentException(e);
        }
    }
}
```

###### Use 4 spaces for general indentation

Indenting normal code levels **must** use 4 spaces.

_Rationale:_ Four spaces is a very common amount of indentation. Visually, it
makes the level changes easy to spot.

_Example: See next rule..._

###### Use 8 spaces for "continuation"

Statement continuation **must** use 8 spaces. Continuation should be used for
long lines or for method chaining (See rules below for wrapping).

_Rationale:_ This is also a very common amount of indentation for statement
continuation. The extra indentation helps to show that the code is a
continuation of the statement above, rather than its own statement

_Example:_

```java
public class Example {
    
    public void myMethod(int firstNumberParam, int secondNumberParam, String stringParam) {
        
        callThisMethodWithAReallyLongNameAndParameterList(
                firstNumberParam,
                secondNumberParam,
                new AtomicInteger(),
                stringParam,
                "Some more information for this outrageous method");
        
        if (secondNumberParam == 0) {
            for (int i = 0; i < firstNumberParam; i++) {
                soManyGoodThings(stringParam);
            }
        }
        
        new ThingyBuilder()
                .doohickey(secondNumberParam)
                .whatchamacallit(stringParam)
                .thingamajig(firstNumberParam)
                .build();
    }
}
```

### Around Code Constructs

### Line Length and Wrapping

###### Wrap and continue chained method calls

###### Keep lines under 120 characters

### Empty Lines

## Language Constructs

### Classes

### Interfaces

### Enums

### Annotations

### Methods

### Fields

### Variables

### Loops

### Conditionals

### Generics

### Lambdas

### Imports

###### Do not wrap import statements

###### Do not use wildcard imports

###### Group imports together logically

## Exception Handling

###### Do not swallow exceptions. Ever.

Exception handlers **must not** swallow exceptions silently.
