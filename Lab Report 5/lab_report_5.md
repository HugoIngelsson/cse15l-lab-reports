# Lab Report 5
In this lab report, I'll be creating an imaginary scenario where a student has a bug in their code and gets help from EdStem. Then I'll describe something I've learned in CSE 15L.

## Debugging Scenario
<span style="color:red">Peliz Hjelpmi</span>  
3 hours ago in <span style="color:blue">General</span>

Hi,  
I have a bug for this week's PA that I am unsure how to solve. I've been looking online for hours at this point and really cannot see what I did wrong. This is what the terminal tells me at this point:

```
Peliz@Peliz-Laptop src % bash test.sh
MainTester.java:2: error: package org.junit does not exist
import static org.junit.Assert.*;
                       ^
MainTester.java:1: error: package org.junit does not exist
import org.junit.*;
^
MainTester.java:5: error: cannot find symbol
    @Test
     ^
  symbol:   class Test
  location: class MainTester
MainTester.java:16: error: cannot find symbol
    @Test
     ^
  symbol:   class Test
  location: class MainTester
MainTester.java:27: error: cannot find symbol
    @Test
     ^
  symbol:   class Test
  location: class MainTester
MainTester.java:12: error: cannot find symbol
        assertEquals("aaaa\nbb\n\nd\n",
        ^
  symbol:   method assertEquals(String,String)
  location: class MainTester
MainTester.java:23: error: cannot find symbol
        assertEquals("\n",
        ^
  symbol:   method assertEquals(String,String)
  location: class MainTester
MainTester.java:34: error: cannot find symbol
        assertEquals("\n\n\n\n\t\nyay\n!!!\n",
        ^
  symbol:   method assertEquals(String,String)
  location: class MainTester
8 errors
Error: Could not find or load main class org.junit.runner.JUnitCore
Caused by: java.lang.ClassNotFoundException: org.junit.runner.JUnitCore
```
I think the bash program that I run can't find the JUnit files needed to run the tests for some reason. But this doesn't make any sense to me! I have downloaded the "lib" folder like we always do in class, and I use "-cp" when I run both "javac" and "java". Furthermore, I use the class path we always use and copied it over from a previous PA, so I know I didn't make any typo mistakes.

This is what my bash script looks like:
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

javac -cp $CPATH *.java
java -cp $CPATH org.junit.runner.JUnitCore MainTester
```
I'm really stressed about this and would love some help. Does anyone have any solutions to my problem?

---
<span style="color:red">Ghood Tudor</span> STAFF  
2 hours ago

Hello Peliz!

It would be nice to know a little bit more about your file structure and what the Java files look like, but I will try to help you to the best of my ability right now. Here are a couple of things you might want to check:  
1. Are you in the right directory when you run the bash script? If you are running it from some other directory (i.e. using "bash <path>/test.sh"), the class path might not work as intended.
2. Is the path to your "lib" directory correct in your class path? If "lib" is in another directory than the one you run your bash script from, you might need to edit your class path.
3. Are there any typos in your Java files? If you get to this step, this is about the only thing I can think of without knowing more about your file structure.

I hope this helps! Please respond with more information if you're still stuck.

---
<span style="color:red">Peliz Hjelpmi</span>  
1 minute ago

Hi yes thank you so much for your help

Potential issue 1 didn't work but number 2 did. I managed to get it to work, look:
```
Peliz@Peliz-Laptop src % bash test.sh
JUnit version 4.13.2
.aaaa
bb

d

.

.




yay
!!!


Time: 0.007

OK (3 tests)
```

Turns out that when I was running the bash script from my "src" directory, it couldn't find a "lib" directory within it. What I needed to do was change my CPATH to put "../" before "lib" so that it went back a level to where the "lib" directory exists.

---
### Setup Description
This is a description of the setup needed to achieve this bug and then fix it.

File structure:

root  
  \tL--lib  
        L--hamcrest-core-1.3.jar  
        L--junit-4.13.2.jar  
    L--src  
        L--Main.java  
        L--MainTester.java  
        L--test.sh


