# 1. Introduction
After years of experience of Software Development, I came to know that irrespective of the framework or language that we are working in, there must be some guidelines we should follow. While I am writing this article my co-worker **Arpan** told me there is huge differencce between a readable code and working code. You may be wondering how we can write a better readable code. I have tried to list down some of rule with everyone can write readable code. 

## 1.1 Topics we are going to cover:
 * Naming Convention
 * Functions
 * Comments
 
 # 2. Naming Conventions
Names are everywhere in software. We name our variables, our functions, our arguments,
classes, and packages. We name our source files and the directories that contain them. We
name our jar files and war files and ear files. We name and name and name. Because we do so much of it, we’d better do it well. What follows are some simple rules for creating
good names.

* **Use Intention-Revealing Names**
 The name of a variable, function, or class, should answer all the big questions. It
should tell you why it exists, what it does, and how it is used. If a name requires a comment,
then the name does not reveal its intent. 
```java
int d; // elapsed time in days
```
The name d reveals nothing. It does not evoke a sense of elapsed time, nor of days. We
should choose a name that specifies what is being measured and the unit of that measurement:
```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```
