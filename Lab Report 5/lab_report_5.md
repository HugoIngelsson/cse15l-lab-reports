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
