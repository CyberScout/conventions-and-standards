# Java Coding Conventions

This document outlines conventions for writing Java code. These conventions
should also be adhered to for Groovy code, insofar as Groovy is mostly a
superset of Java. See the [Groovy](Groovy.md) document for rules and conventions
that are specific to Groovy, or differ from Java.

## Java Configuration

JDK version 8.x must be used for all new development.

For web applications and APIs, Spring Boot must be used. The application should
run as a standalone JAR (embedded Tomcat or Jetty). Alternatively, it may be
packaged as a WAR and run in a JBoss EAP application server, but only if the
facilities of a full application server are needed.

### Build

Gradle must be used to build Java projects.

## Package and File Structure

Source files will follow Java's requirements:

- Directory structure must mirror package structure
- Source file names must be the case-sensitive name of the file's top-level
  class, plus the `.java` extension.

Source files must contain exactly one top-level class (the top-level class may
contain inner classes).

## Code Organization

## Whitespace, Line Breaks, and Empty Lines

### Indentation

### Around Code Constructs

### Line Length and Wrapping

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

## Exception Handling
