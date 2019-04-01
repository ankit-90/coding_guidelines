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
* **Use Pronounceable Names** Humans are good at words. A significant part of our brains is dedicated to the concept of
words. And words are, by definition, pronounceable. It would be a shame not to take advantage of that huge portion of our brains that has evolved to deal with spoken language.
So make your names pronounceable.

If you can’t pronounce it, you can’t discuss it without sounding like an idiot. “Well,
over here on the bee cee arr three cee enn tee we have a pee ess zee kyew int, see?” This
matters because programming is a social activity.

 Compare
 ```java
class DtaRcrd102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
}
```
to
```java
class Customer {
    private Date generationTimestamp;
    private Date modificationTimestamp;;
    private final String recordId = "102";
}
```
Intelligent conversation is now possible: “Hey, Mikey, take a look at this record! The generation
timestamp is set to tomorrow’s date! How can that be?”

* **Use Searchable Names** 
Single-letter names and numeric constants have a particular problem in that they are not
easy to locate across a body of text.
One might easily grep for MAX_CLASSES_PER_STUDENT, but the number 7 could be more
troublesome.
If a variable or constant might be seen or used in multiple places in a body of code,
it is imperative to give it a search-friendly name. Once again compare
```java
for (int j=0; j<34; j++) {
    s += (t[j]*4)/5;
}
```
to
```java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
    int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```
Note that sum, above, is not a particularly useful name but at least is searchable. The
intentionally named code makes for a longer function, but consider how much easier it
will be to find **WORK_DAYS_PER_WEEK** than to find all the places where 5 was used and filter
the list down to just the instances with the intended meaning.

* **Class Names**
Classes and objects should have noun or noun phrase names like *Customer, WikiPage,
Account, and AddressParser*. Avoid words like *Manager, Processor, Data, or Info* in the name
of a class. A class name should not be a verb.

* **Method Names**
Methods should have verb or verb phrase names like *postPayment, deletePage, or save.
Accessors, mutators, and predicates* should be named for their value and prefixed with *get,
set, and is according to the javabean standard*.

```java
String name = employee.getName();
customer.setName("Ajay");
if (paycheck.isPosted()){
   ------
   ------
}
```
When constructors are overloaded, use static factory methods with names that
describe the arguments. For example,
```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```
is generally better than
```java
Complex fulcrumPoint = new Complex(23.0);
```
Consider enforcing their use by making the corresponding constructors private.

* **Don’t Be Cute**
If names are too clever, they will be
memorable only to people who share the
author’s sense of humor, and only as long
as these people remember the joke. Will
they know what the function named
*HolyHandGrenade* is supposed to do? Sure,
it’s cute, but maybe in this case
*DeleteItems* might be a better name.
Choose clarity over entertainment value.
Cuteness in code often appears in the form of colloquialisms or slang. For example,
don’t use the name *whack()* to mean *kill()*. Don’t tell little culture-dependent jokes like
*eatMyShorts()* to mean *abort()*.
Say what you mean. Mean what you say.
