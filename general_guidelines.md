# 1. Introduction
After years of experience of Software Development, I came to know that irrespective of the framework or language that we are working in, there must be some guidelines we should follow. While I am writing this article my co-worker **Arpan** told me there is huge differencce between a readable code and working code. You may be wondering how we can write a better readable code. I have tried to list down some of rule with everyone can write readable code. 

## 1.1 Topics we are going to cover:
 * Naming Convention
 * Functions
 * Comments
 * Formatting
 * Error/Exception Handling
 * Coding Myths
 
 # 2. Naming Convention
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

* **Output Arguments**
Arguments are most naturally interpreted as inputs to a function. If you have been programming
for more than a few years, I’m sure you’ve done a double-take on an argument
that was actually an output rather than an input. For example:
```java
appendFooter(s);
```
Does this function append s as the footer to something? Or does it append some footer
to s? Is s an input or an output? It doesn’t take long to look at the function signature
and see:
```java
public void appendFooter(StringBuffer report)
```
This clarifies the issue, but only at the expense of checking the declaration of the function.
Anything that forces you to check the function signature is equivalent to a double-take. It’s
a cognitive break and should be avoided.
In the days before object oriented programming it was sometimes necessary to have
output arguments. However, much of the need for output arguments disappears in OO languages
because this is intended to act as an output argument. In other words, it would be
better for appendFooter to be invoked as
```java
report.appendFooter();
```
In general output arguments should be avoided. If your function must change the state
of something, have it change the state of its owning object.

# 4. Comments
*Don't comment bad code, review it*.<br/>
*Code never lies, comments sometimes do.*<br/>
*Code is like joke, it is bad if you have to explain it.*<br/>


Nothing can be quite so helpful as a well-placed comment. Nothing can clutter up a module
more than frivolous dogmatic comments. Nothing can be quite so damaging as an old
crufty comment that propagates lies and misinformation.
The proper use of comments is to compensate for our failure to express ourself in
code. Note that I used the word **failure**. I meant it. Comments are always failures. We must
have them because we cannot always figure out how to express ourselves without them,
but their use is not a cause for celebration. 

So when you find yourself in a position where you need to write a comment, think it
through and see whether there isn’t some way to turn the tables and express yourself in
code. Every time you express yourself in code, you should pat yourself on the back. Every
time you write a comment, you should grimace and feel the failure of your ability of
expression.
Why am I so down on comments? Because they lie. Not always, and not intentionally,
but too often. The older a comment is, and the farther away it is from the code it describes,
the more likely it is to be just plain wrong. The reason is simple. Programmers can’t realistically
maintain them.
Code changes and evolves. Chunks of it move from here to there. Those chunks bifurcate
and reproduce and come together again to form chimeras. Unfortunately the comments
don’t always follow them—can’t always follow them. And all too often the
comments get separated from the code they describe and become orphaned blurbs of everdecreasing
accuracy. For example, look what has happened to this comment and the line it
was intended to describe:

```java
  MockRequest request;
    private final String HTTP_DATE_REGEXP =
    "[SMTWF][a-z]{2}\\,\\s[0-9]{2}\\s[JFMASOND][a-z]{2}\\s"+
    "[0-9]{4}\\s[0-9]{2}\\:[0-9]{2}\\:[0-9]{2}\\sGMT";
    private Response response;
    private FitNesseContext context;
    private FileResponder responder;
    private Locale saveLocale;
    // Example: "Tue, 02 Apr 2003 22:18:49 GMT"
```   
Other instance variables that were probably added later were interposed between the
**HTTP_DATE_REGEXP** constant and it’s explanatory comment.
It is possible to make the point that programmers should be disciplined enough to
keep the comments in a high state of repair, relevance, and accuracy. I agree, they should.
But I would rather that energy go toward making the code so clear and expressive that it
does not need the comments in the first place.
Inaccurate comments are far worse than no comments at all. They delude and mislead.
They set expectations that will never be fulfilled. They lay down old rules that need not, or
should not, be followed any longer.
Truth can only be found in one place: the code. Only the code can truly tell you what
it does. It is the only source of truly accurate information. Therefore, though comments are
sometimes necessary, we will expend significant energy to minimize them.

* **Comments Do Not Make Up for Bad Code**
One of the more common motivations for writing comments is bad code. We write a module
and we know it is confusing and disorganized. We know it’s a mess. So we say to ourselves,
“Ooh, I’d better comment that!” No! You’d better clean it!
Clear and expressive code with few comments is far superior to cluttered and complex
code with lots of comments. Rather than spend your time writing the comments that
explain the mess you’ve made, spend it cleaning that mess.

* **Explain Yourself in Code**
There are certainly times when code makes a poor vehicle for explanation. Unfortunately,
many programmers have taken this to mean that code is seldom, if ever, a good means for
explanation. This is patently false. Which would you rather see? This:
```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65)) 
```
Or this?

```java
if (employee.isEligibleForFullBenefits())
```
It takes only a few seconds of thought to explain most of your intent in code. In many
cases it’s simply a matter of creating a function that says the same thing as the comment
you want to write.

* **Good Comments**
Some comments are necessary or beneficial. We’ll look at a few that I consider worthy of
the bits they consume. Keep in mind, however, that the only truly good comment is the
comment you found a way not to write.

* **Legal Comments**
Sometimes our corporate coding standards force us to write certain comments for legal
reasons. For example, copyright and authorship statements are necessary and reasonable
things to put into a comment at the start of each source file.
Here, for example, is the standard comment header that we put at the beginning of
every source file in FitNesse. I am happy to say that our IDE hides this comment from acting
as clutter by automatically collapsing it.

```java
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```
Comments like this should not be contracts or legal tomes. Where possible, refer to a standard
license or other external document rather than putting all the terms and conditions
into the comment.

* **Informative Comments**
It is sometimes useful to provide basic information with a comment. For example, consider
this comment that explains the return value of an abstract method:
```java
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
```
A comment like this can sometimes be useful, but it is better to use the name of the function
to convey the information where possible. For example, in this case the comment
could be made redundant by renaming the function: *responderBeingTested*.
Here’s a case that’s a bit better:

```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile(
 "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
In this case the comment lets us know that the regular expression is intended to match a
time and date that were formatted with the SimpleDateFormat.format function using the
specified format string. Still, it might have been better, and clearer, if this code had been
moved to a special class that converted the formats of dates and times. Then the comment
would likely have been superfluous.

* **Explanation of Intent**
Sometimes a comment goes beyond just useful information about the implementation and
provides the intent behind a decision. In the following case we see an interesting decision
documented by a comment. When comparing two objects, the author decided that he
wanted to sort objects of his class higher than objects of any other.

```java
public int compareTo(Object o) {
        if (o instanceof WikiPagePath) {
            WikiPagePath p =(WikiPagePath) o;
            String compressedName = StringUtil . join (names, "");
            String compressedArgumentName = StringUtil . join (p.names, "");
            return compressedName.compareTo(compressedArgumentName);
        }
        return 1; // we are greater because we are the right type.
    }
```
Here’s an even better example. You might not agree with the programmer’s solution to
the problem, but at least you know what he was trying to do.

```java
 public void testConcurrentAddWidgets() throws Exception {
        WidgetBuilder widgetBuilder =
                new WidgetBuilder(new Class[]{BoldWidget.class});
        String text = "'''bold text'''";
        ParentWidget parent =
                new BoldWidget(new MockWidgetRoot(), "'''bold text'''");
        AtomicBoolean failFlag = new AtomicBoolean();
        failFlag.set(false);
        //This is our best attempt to get a race condition
        //by creating large number of threads.
        for (int i = 0; i < 25000; i++) {
            WidgetBuilderThread widgetBuilderThread =
                    new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
            Thread thread = new Thread(widgetBuilderThread);
            thread.start();
        }
        assertEquals(false, failFlag.get());
    }
```

* **Clarification**
Sometimes it is just helpful to translate the meaning of some obscure argument or return
value into something that’s readable. In general it is better to find a way to make that argument
or return value clear in its own right; but when its part of the standard library, or in
code that you cannot alter, then a helpful clarifying comment can be useful.

```java
public void testCompareTo() throws Exception {
        WikiPagePath a = PathParser.parse("PageA");
        WikiPagePath ab = PathParser.parse("PageA.PageB");
        WikiPagePath b = PathParser.parse("PageB");
        WikiPagePath aa = PathParser.parse("PageA.PageA");
        WikiPagePath bb = PathParser.parse("PageB.PageB");
        WikiPagePath ba = PathParser.parse("PageB.PageA");
        assertTrue(a.compareTo(a) == 0); // a == a
        assertTrue(a.compareTo(b) != 0); // a != b
        assertTrue(ab.compareTo(ab) == 0); // ab == ab
        assertTrue(a.compareTo(b) == -1); // a < b
        assertTrue(aa.compareTo(ab) == -1); // aa < ab
        assertTrue(ba.compareTo(bb) == -1); // ba < bb
        assertTrue(b.compareTo(a) == 1); // b > a
        assertTrue(ab.compareTo(aa) == 1); // ab > aa
        assertTrue(bb.compareTo(ba) == 1); // bb > ba
    }
```
There is a substantial risk, of course, that a clarifying comment is incorrect. Go
through the previous example and see how difficult it is to verify that they are correct. This
explains both why the clarification is necessary and why it’s risky. So before writing comments
like this, take care that there is no better way, and then take even more care that they
are accurate.

* **Warning of Consequences**
Sometimes it is useful to warn other programmers
about certain consequences. For
example, here is a comment that explains
why a particular test case is turned off:

```java
// Don't run unless you
    // have some time to kill.
    public void _testWithReallyBigFile() {
        writeLinesToFile(10000000);
        response.setBody(testFile);
        response.readyToSend(this);
        String responseString = output.toString();
        assertSubString("Content-Length: 1000000000", responseString);
        assertTrue(bytesSent > 1000000000);
    }

```
* **TODO Comments**
It is sometimes reasonable to leave “To do” notes in the form of **//TODO comments**. In the
following case, the TODO comment explains why the function has a degenerate implementation
and what that function’s future should be. 

```java
 //TODO-MdM these are not needed
    // We expect this to go away when we do the checkout model
    protected VersionInfo makeVersion() throws Exception {
        return null;
    }
```
TODOs are jobs that the programmer thinks should be done, but for some reason
can’t do at the moment. It might be a reminder to delete a deprecated feature or a
plea for someone else to look at a problem. It might be a request for someone else to
think of a better name or a reminder to make a change that is dependent on a
planned event. Whatever else a TODO might be, it is not an excuse to leave bad code in
the system.
Nowadays, most good IDEs provide special gestures and features to locate all the
TODO comments, so it’s not likely that they will get lost. Still, you don’t want your code
to be littered with TODOs. So scan through them regularly and eliminate the ones you
can.

* **Amplification**
A comment may be used to amplify the importance of something that may otherwise seem
inconsequential.

```java
String listItemContent = match.group(3).trim();
// the trim is real important. It removes the starting
// spaces that could cause the item to be recognized
// as another list.
new

    ListItemWidget(this,listItemContent, this.level +1);
return

    buildList(text.substring(match.end()));
```

* **Bad Comments**
Most comments fall into this category. Usually they are crutches or excuses for poor code
or justifications for insufficient decisions, amounting to little more than the programmer
talking to himself.

* **Mumbling**
Plopping in a comment just because you feel you should or because the process requires it,
is a hack. If you decide to write a comment, then spend the time necessary to make sure it
is the best comment you can write. 

```java
public void loadProperties() {
        try {
            String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
            FileInputStream propertiesStream = new FileInputStream(propertiesPath);
            loadedProperties.load(propertiesStream);
        } catch (IOException e) {
// No properties files means all defaults are loaded
        }
    }
```
* **Redundant Comments**
 A simple function with a header comment that is completely redundant.
The comment probably takes longer to read than the code itself.

```java

    // Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
    public synchronized void waitForClose(final long timeoutMillis)
            throws Exception {
        if (!closed) {
            wait(timeoutMillis);
            if (!closed)
                throw new Exception("MockResponseSender could not be closed");
        }
    }
```
What purpose does this comment serve? It’s certainly not more informative than the
code. It does not justify the code, or provide intent or rationale. It is not easier to read than
the code. Indeed, it is less precise than the code and entices the reader to accept that lack of
precision in lieu of true understanding. It is rather like a gladhanding used-car salesman
assuring you that you don’t need to look under the hood. 

Some more examples:

```java
public abstract class ContainerBase implements Container, Lifecycle, Pipeline,
        MBeanRegistration, Serializable {
    /**
     * The processor delay for this component.
     */
    protected int backgroundProcessorDelay = -1;
    /**
     * The lifecycle event support for this component.
     */
    protected LifecycleSupport lifecycle =
            new LifecycleSupport(this);
    /**
     * The container event listeners for this Container.
     */
    protected ArrayList listeners = new ArrayList();
    /**
     * The Loader implementation with which this Container is
     * associated.
     */
    protected Loader loader = null;
    /**
     * The Logger implementation with which this Container is
     * associated.
     */
    protected Log logger = null;
    /**
     * Associated logger name.
     */
    protected String logName = null;

    /**
     * The Manager implementation with which this Container is
     * associated.
     */
    protected Manager manager = null;
    /**
     * The cluster with which this Container is associated.
     */
    protected Cluster cluster = null;
    /**
     * The human-readable name of this Container.
     */
    protected String name = null;
    /**
     * The parent Container to which this Container is a child.
     */
    protected Container parent = null;
    /**
     * The parent class loader to be configured when we install a
     * Loader.
     */
    protected ClassLoader parentClassLoader = null;
    /**
     * The Pipeline object with which this Container is
     * associated.
     */
    protected Pipeline pipeline = new StandardPipeline(this);
    /**
     * The Realm with which this Container is associated.
     */
    protected Realm realm = null;
    /**
     * The resources DirContext object with which this Container
     * is associated.
     */
    protected DirContext resources = null;
}


```

* **Misleading Comments**
Sometimes, with all the best intentions, a programmer makes a statement in his comments
that isn’t precise enough to be accurate. 
This subtle bit of misinformation, couched in a comment that is harder to read than
the body of the code, could cause another programmer to blithely call this function in the
expectation that it will return as soon as this.closed becomes true. That poor programmer
would then find himself in a debugging session trying to figure out why his code executed
so slowly

* **Mandated Comments**
It is just plain silly to have a rule that says that every function must have a javadoc, or
every variable must have a comment. Comments like this just clutter up the code, propagate
lies, and lend to general confusion and disorganization. 

This clutter adds nothing and serves only to obfuscate the code and create the
potential for lies and misdirection.

```java
/*
     * @param title The title of the CD
     * @param author The author of the CD
     * @param tracks The number of tracks on the CD
     * @param durationInMinutes The duration of the CD in minutes
     */
    public void addCD(String title, String author,
                      int tracks, int durationInMinutes) {
        CD cd = new CD();
        cd.title = title;
        cd.author = author;
        cd.tracks = tracks;
        cd.duration = duration;
        cdList.add(cd);
    }
```

* **Journal Comments**
Sometimes people add a comment to the start of a module every time they edit it. These
comments accumulate as a kind of journal, or log, of every change that has ever been
made. I have seen some modules with dozens of pages of these run-on journal entries. 

```java
/* Changes (from 11-Oct-2001)
 * --------------------------
 * 11-Oct-2001 : Re-organised the class and moved it to new package
 * com.jrefinery.date (DG);
 * 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate
 * class (DG);
 * 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate
 * class is gone (DG); Changed getPreviousDayOfWeek(),
 * getFollowingDayOfWeek() and getNearestDayOfWeek() to correct
 * bugs (DG);
 * 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
 * 29-May-2002 : Moved the month constants into a separate interface
 * (MonthConstants) (DG);
 * 27-Aug-2002 : Fixed bug in addMonths() method, thanks to N???levka Petr (DG);
 * 03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
 * 13-Mar-2003 : Implemented Serializable (DG);
 * 29-May-2003 : Fixed bug in addMonths method (DG);
 * 04-Sep-2003 : Implemented Comparable. Updated the isInRange javadocs (DG);
 * 05-Jan-2005 : Fixed bug in addYears() method (1096282) (DG);
```

Long ago there was a good reason to create and maintain these log entries at the start
of every module. We didn’t have source code control systems that did it for us. Nowadays,
however, these long journals are just more clutter to obfuscate the module. They should be
completely removed.

* **Noise Comments**
Sometimes you see comments that are nothing but noise. They restate the obvious and
provide no new information.

```java
/**
 * Default constructor.
 */
protected AnnualDateRule() {
}
```
No, really? Or how about this:

```java
/** The day of the month. */
 private int dayOfMonth;
```
And then there’s this paragon of redundancy:

```java
 /* Returns the day of the month.
 *
 * @return the day of the month.
 */
public int getDayOfMonth() {
 return dayOfMonth;
}
```
These comments are so noisy that we learn to ignore them. As we read through code, our
eyes simply skip over them. Eventually the comments begin to lie as the code around them
changes.

Example below explains why the catch block
is being ignored. But the second comment is pure noise. Apparently the programmer was
just so frustrated with writing try/catch blocks in this function that he needed to vent.

```java
  private void startSending() {
        try {
            doSending();
        } catch (SocketException e) {
// normal. someone stopped the request.
        } catch (Exception e) {
            try {
                response.add(ErrorResponder.makeExceptionString(e));
                response.closeAll();
            } catch (Exception e1) {
//Give me a break!
            }
        }
    }
```

* **Scary Noise**
 They are just redundant noisy comments
written out of some misplaced desire to provide documentation.

```java
/** The name. */
private String name;
/** The version. */
private String version;
/** The licenceName. */
private String licenceName;
/** The version. */
private String info;
```
Read these comments again more carefully. Do you see the cut-paste error? If authors
aren’t paying attention when comments are written (or pasted), why should readers be
expected to profit from them?

* **Don’t Use a Comment When You Can Use a Function or a Variable**
Consider the following stretch of code:

```java
// does the module from the global list <mod> depend on the
    // subsystem we are part of?
    if(smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```

This could be rephrased without the comment as

```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```
The author of the original code may have written the comment first (unlikely) and then
written the code to fulfill the comment. However, the author should then have refactored
the code, as I did, so that the comment could be removed.

* **Position Markers**
Sometimes programmers like to mark a particular position in a source file. For example, I
recently found this in a program I was looking through:

```java
// Actions //////////////////////////////////

*****************************************
*                                       *
*****************************************
```
There are rare times when it makes sense to gather certain functions together beneath a
banner like this. But in general they are clutter that should be eliminated—especially the
noisy train of slashes at the end.
Think of it this way. A banner is startling and obvious if you don’t see banners very
often. So use them very sparingly, and only when the benefit is significant. If you overuse
banners, they’ll fall into the background noise and be ignored.

* **Closing Brace Comments**

Sometimes programmers will put special comments on closing braces, as in example below.
Although this might make sense for long functions with deeply nested structures, it serves
only to clutter the kind of small and encapsulated functions that we prefer. So if you find
yourself wanting to mark your closing braces, try to shorten your functions instead.

```java
public class wc {
    public static void main(String[] args) {

        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line;
        int lineCount = 0;
        int charCount = 0;
        int wordCount = 0;
        try {
            while ((line = in.readLine()) != null) {
                lineCount++;
                charCount += line.length();
                String words[] = line.split("\\W");
                wordCount += words.length;
            } //while
            System.out.println("wordCount = " + wordCount);
            System.out.println("lineCount = " + lineCount);
            System.out.println("charCount = " + charCount);
        } // try
        catch (IOException e) {
            System.err.println("Error:" + e.getMessage());
        } //catch
    } //main
}
```

* **Attributions and Bylines**
```java
/* Added by Rick */
```
Source code control systems are very good at remembering who added what, when.
There is no need to pollute the code with little bylines. You might think that such comments
would be useful in order to help others know who to talk to about the code. But the
reality is that they tend to stay around for years and years, getting less and less accurate
and relevant.
Again, the source code control system is a better place for this kind of information.

* **Commented-Out Code**
Few practices are as odious as commenting-out code. Don’t do this!

```java
InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));
```
Others who see that commented-out code won’t have the courage to delete it. They’ll think
it is there for a reason and is too important to delete. So commented-out code gathers like
dregs at the bottom of a bad bottle of wine.

* **HTML Comments**
HTML in source code comments is an abomination, as you can tell by reading the code
below. It makes the comments hard to read in the one place where they should be easy to
read—the editor/IDE. If comments are going to be extracted by some tool (like Javadoc) to
appear in a Web page, then it should be the responsibility of that tool, and not the programmer,
to adorn the comments with appropriate HTML.

```java
/**
 * Task to run fit tests.
 * This task runs fitnesse tests and publishes the results.
 * <p/>
 * <pre>
 * Usage:
 * &lt;taskdef name=&quot;execute-fitnesse-tests&quot;
 * classname=&quot;fitnesse.ant.ExecuteFitnesseTestsTask&quot;
 * classpathref=&quot;classpath&quot; /&gt;
 * OR
 * &lt;taskdef classpathref=&quot;classpath&quot;
 * resource=&quot;tasks.properties&quot; /&gt;
 * <p/>
 * &lt;execute-fitnesse-tests
 * suitepage=&quot;FitNesse.SuiteAcceptanceTests&quot;
 * fitnesseport=&quot;8082&quot;
 * resultsdir=&quot;${results.dir}&quot;
 * resultshtmlpage=&quot;fit-results.html&quot;
 * classpathref=&quot;classpath&quot; /&gt;
 * </pre>
 */
```

* **Non Local Information**
If you must write a comment, then make sure it describes the code it appears near. Don’t
offer systemwide information in the context of a local comment. Consider, for example,
the javadoc comment below. Aside from the fact that it is horribly redundant, it also offers
information about the default port. And yet the function has absolutely no control over
what that default is. The comment is not describing the function, but some other, far distant
part of the system. Of course there is no guarantee that this comment will be changed
when the code containing the default is changed.

```java
/**
 * Port on which fitnesse would run. Defaults to <b>8082</b>.
 *
 * @param fitnessePort
 */
public void setFitnessePort(int fitnessePort){
    this.fitnessePort = fitnessePort;
}
```

* **Too Much Information**
Don’t put interesting historical discussions or irrelevant descriptions of details into your
comments. The comment below was extracted from a module designed to test that a function
could encode and decode base64. Other than the RFC number, someone reading this
code has no need for the arcane information contained in the comment. 

```java
/*
 RFC 2045 - Multipurpose Internet Mail Extensions (MIME)
 Part One: Format of Internet Message Bodies
 section 6.8. Base64 Content-Transfer-Encoding
 The encoding process represents 24-bit groups of input bits as output
 strings of 4 encoded characters. Proceeding from left to right, a
 24-bit input group is formed by concatenating 3 8-bit input groups.
 These 24 bits are then treated as 4 concatenated 6-bit groups, each
 of which is translated into a single digit in the base64 alphabet.
 When encoding a bit stream via the base64 encoding, the bit stream
 must be presumed to be ordered with the most-significant-bit first.
 That is, the first bit in the stream will be the high-order bit in
 the first 8-bit byte, and the eighth bit will be the low-order bit in
 the first 8-bit byte, and so on.
 */
```

* **Inobvious Connection**
The connection between a comment and the code it describes should be obvious. If you are
going to the trouble to write a comment, then at least you’d like the reader to be able to
look at the comment and the code and understand what the comment is talking about.
Consider, for example, this comment drawn from apache commons:

```java
/*
 * start with an array that is big enough to hold all the pixels
 * (plus filter bytes), and an extra 200 bytes for header info
 */
 this.pngBytes = new byte[((this.width + 1) * this.height * 3) + 200];
```
What is a filter byte? Does it relate to the +1? Or to the *3? Both? Is a pixel a byte? Why
200? The purpose of a comment is to explain code that does not explain itself. It is a pity
when a comment needs its own explanation. 


 * **Function Headers**
 Short functions don’t need much description. A well-chosen name for a small function that
does one thing is usually better than a comment header. 


