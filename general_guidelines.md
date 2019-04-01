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

* **Final Words**
The hardest thing about choosing good names is that it requires good descriptive skills and
a shared cultural background. This is a teaching issue rather than a technical, business, or
management issue. As a result many people in this field don’t learn to do it very well.
People are also afraid of renaming things for fear that some other developers will
object. We do not share that fear and find that we are actually grateful when names change
(for the better). Most of the time we don’t really memorize the names of classes and methods.
We use the modern tools to deal with details like that so we can focus on whether the
code reads like paragraphs and sentences, or at least like tables and data structure (a sentence
isn’t always the best way to display data). You will probably end up surprising someone
when you rename, just like you might with any other code improvement. Don’t let it
stop you in your tracks.
Follow some of these rules and see whether you don’t improve the readability of your
code. If you are maintaining someone else’s code, use refactoring tools to help resolve these
problems. It will pay off in the short term and continue to pay in the long run.

# 3. Functions
Functions are the first line of organization in any program.Consider the following example:

```java
 public static String testableHtml(PageData pageData,boolean includeSuiteSetup) throws Exception {
    WikiPage wikiPage = pageData.getWikiPage();
    StringBuffer buffer = new StringBuffer();
    if (pageData.hasAttribute("Test")) {
        if (includeSuiteSetup) {
            WikiPage suiteSetup = PageCrawlerImpl.getInheritedPage(SuiteResponder.SUITE_SETUP_NAME, wikiPage);
            if (suiteSetup != null) {
                WikiPagePath pagePath = suiteSetup.getPageCrawler().getFullPath(suiteSetup);
                String pagePathName = PathParser.render(pagePath);
                buffer.append("!include -setup .")
                    .append(pagePathName)
                     .append("\n");
            }
        }
        WikiPage setup = PageCrawlerImpl.getInheritedPage("SetUp", wikiPage);
        if (setup != null) {
            WikiPagePath setupPath = wikiPage.getPageCrawler().getFullPath(setup);
            String setupPathName = PathParser.render(setupPath);
            buffer.append("!include -setup .")
                .append(setupPathName)
                .append("\n");
        }
    }
    buffer.append(pageData.getContent());
    if (pageData.hasAttribute("Test")) {
        WikiPage teardown = PageCrawlerImpl.getInheritedPage("TearDown", wikiPage);
        if (teardown != null) {
            WikiPagePath tearDownPath = wikiPage.getPageCrawler().getFullPath(teardown);
            String tearDownPathName = PathParser.render(tearDownPath);
            buffer.append("\n")
                .append("!include -teardown .")
                .append(tearDownPathName)
                .append("\n");
        }
}
```
 Not only is it long, but it’s got duplicated
code, lots of odd strings, and many strange and inobvious data types and APIs. See how
much sense you can make of it in the next three minutes. Do you understand the function after three minutes of study? Probably not. There’s
too much going on in there at too many different levels of abstraction. There are strange
strings and odd function calls mixed in with doubly nested if statements controlled by
flags.

* **Small**
The first rule of functions is that they should be small. The second rule of functions is that
they should be smaller than that. This is not an assertion that I can justify. I can’t provide
any references to research that shows that very small functions are better. What I can tell
you is that for nearly 5 years I have written functions of all different sizes. I’ve written
several nasty 3,000-line abominations. I’ve written scads of functions in the 100 to 300
line range. And I’ve written functions that were **20 to 30** lines long. What this experience
has taught me, through long trial and error, is that functions should be very small.

```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData)){
        includeSetupAndTeardownPages(pageData, isSuite);
    }
    return pageData.getHtml();
 }
```
* **Blocks and Indenting**
This implies that the blocks within if statements, else statements, while statements, and
so on should be one line long. Probably that line should be a function call. Not only does
this keep the enclosing function small, but it also adds documentary value because the
function called within the block can have a nicely descriptive name.
This also implies that functions should not be large enough to hold nested structures.
Therefore, the indent level of a function should not be greater than one or two. This, of
course, makes the functions easier to read and understand. Consider the following example:

```java
if(data.code == Constants.API_SUCCESS && data.message.equals("success")){
    --------
    --------
    --------
}
```
to

```java
if(isSuccess(data)){
    -------
    -------
    -------
}
```
* **Do One Thing**
*FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.
THEY SHOULD DO IT ONLY*. The problem with this statement is that it is hard to know what “one thing” is. 

* **Use Descriptive Names**
I changed the name of our example function from **testableHtml** to
**SetupTeardownIncluder**. This is a far better name because it better describes what
the function does. I also gave each of the private methods an equally descriptive name
such as isTestable or includeSetupAndTeardownPages. It is hard to overestimate the value
of good names. Remember Ward’s principle: “You know you are working on clean code
when each routine turns out to be pretty much what you expected.” Half the battle to
achieving that principle is choosing good names for small functions that do one thing.
The smaller and more focused a function is, the easier it is to choose a descriptive
name.
Don’t be afraid to make a name long. A long descriptive name is better than a short
enigmatic name. A long descriptive name is better than a long descriptive comment. Use
a naming convention that allows multiple words to be easily read in the function names,
and then make use of those multiple words to give the function a name that says what
it does.

Choosing descriptive names will clarify the design of the module in your mind and
help you to improve it. It is not at all uncommon that hunting for a good name results in a
favorable restructuring of the code.
Be consistent in your names. Use the same phrases, nouns, and verbs in the function
names you choose for your modules. Consider, for example, the names *includeSetupAndTeardownPages,
includeSetupPages, includeSuiteSetupPage, and includeSetupPage*.

* **Function Arguments**
The ideal number of arguments for a function is
*zero (niladic)*. Next comes *one (monadic)*, followed
closely by *two (dyadic). Three arguments (triadic)*
should be avoided where possible. More than three
(polyadic) requires very special justification—and
then shouldn’t be used anyway.
Arguments are hard. They take a lot of conceptual
power. That’s why I got rid of almost all of
them from the example. Consider, for instance, the
StringBuffer in the example. We could have
passed it around as an argument rather than making
it an instance variable, but then our readers
would have had to interpret it each time they saw
it. When you are reading the story told by the
module, *includeSetupPage()* is easier to understand than *includeSetupPageInto(newPageContent)*.
The argument is at a different level of abstraction than the function name and
forces you to know a detail (in other words, StringBuffer) that isn’t particularly important
at that point.

* **Flag Arguments**
Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It
immediately complicates the signature of the method, loudly proclaiming that this function
does more than one thing. It does one thing if the flag is true and another if the flag is false! For example:

```java
public void enableUiControls(boolean isEnabled){
    if(isEnabled == true){
        ---------
        --------
    }else{
        -------
        --------
        --------
    }
}
```
In this example you can see if value of *isEnabled* is true then we are enabling UI controls and also in near future there can be added functionality we have to do based on the flag. In that case it will get messy over the period of time. A better approach would be to write seperate functions for enable and disable state. For example:

```java
if(isEnabled == true){
    enableUiControls();
}else{
    disableUiControls();
}
```

* **Dyadic Functions** *(Fucntions with two parameters)*<br/>
//TODO

* **Triads** *(Functions with three paramters)*<br/>
//TODO

* **Argument Objects**
When a function seems to need more than two or three arguments, it is likely that some of
those arguments ought to be wrapped into a class of their own. Consider, for example, the
difference between the two following declarations:
```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```
Reducing the number of arguments by creating objects out of them may seem like
cheating, but it’s not. When groups of variables are passed together, the way x and
y are in the example above, they are likely part of a concept that deserves a name of its
own.

* **Verbs and Keywords**
Choosing good names for a function can go a long way toward explaining the intent of
the function and the order and intent of the arguments. In the case of a monad, the
function and argument should form a very nice verb/noun pair. For example,
write(name) is very evocative. Whatever this “name” thing is, it is being “written.” An
even better name might be writeField(name), which tells us that the “name” thing is a
“field.”
This last is an example of the keyword form of a function name. Using this form we
encode the names of the arguments into the function name. For example, *assertEquals*
might be better written as *assertExpectedEqualsActual(expected, actual)*. This strongly
mitigates the problem of having to remember the ordering of the arguments.

* **Have No Side Effects**
Side effects are lies. Your function promises to do one thing, but it also does other hidden
things. Sometimes it will make unexpected changes to the variables of its own class.
Sometimes it will make them to the parameters passed into the function or to system globals.
In either case they are devious and damaging mistruths that often result in strange
temporal couplings and order dependencies.
Consider, for example, the seemingly innocuous function in Listing 3-6. This function
uses a standard algorithm to match a userName to a password. It returns true if they match
and false if anything goes wrong. But it also has a side effect. Can you spot it?

```java
public class UserValidator {

        private Cryptographer cryptographer;

        public boolean checkPassword(String userName, String password) {
            User user = UserGateway.findByName(userName);
            if (user != User.NULL) {
                String codedPhrase = user.getPhraseEncodedByPassword();
                String phrase = cryptographer.decrypt(codedPhrase, password);
                if ("Valid Password".equals(phrase)) {
                    Session.initialize();
                    return true;
                }
            }
            return false;
        }
    }
```

The side effect is the call to Session.initialize(), of course. The checkPassword function,
by its name, says that it checks the password. The name does not imply that it initializes
the session. So a caller who believes what the name of the function says runs the risk
of erasing the existing session data when he or she decides to check the validity of the
user.
This side effect creates a temporal coupling. That is, checkPassword can only be
called at certain times (in other words, when it is safe to initialize the session). If it is
called out of order, session data may be inadvertently lost. Temporal couplings are confusing,
especially when hidden as a side effect. If you must have a temporal coupling,
you should make it clear in the name of the function. In this case we might rename the
function checkPasswordAndInitializeSession, though that certainly violates “Do one
thing.”
