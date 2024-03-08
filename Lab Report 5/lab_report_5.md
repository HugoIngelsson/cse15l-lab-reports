# Lab Report 5
In this lab report, I'll be creating an imaginary scenario where a student has a bug in their code and gets help from EdStem. Then I'll describe something I've learned in CSE 15L.

## Debugging Scenario
---  
<span style="color:red">Peliz Hjelpme</span>  
3 hours ago in <span style="color:blue">General</span>

Hello,  
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
