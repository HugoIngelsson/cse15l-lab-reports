# Lab Report 3

## Part 1
For this part, I decided to use the `filter` method in ListExamples.java.

Before getting into any of the bugs, I want to show the filter that I used in the tests. It looks through a String and only returns true if it contains the character `A`:
```
class CheckHasA implements StringChecker {
    @Override
    public boolean checkString(String s) {
        for (int i=0; i<s.length(); i++) {
            if (s.charAt(i) == 'A')
                return true;
        }

        return false;
    }
}
```

### Failure-Inducing Input
```
@Test
public void testFilter1() {
    List<String> list = Arrays.asList("aA", "aBa", "not in the list!", "aA", "uh oh A");
    List<String> expected = Arrays.asList("aA", "aA", "uh oh A");

    assertEquals(expected, ListExamples.filter(list, new CheckHasA()));
}
```

### Non-Failing Input
```
@Test
public void testFilter2() {
    List<String> list = Arrays.asList("aA", "aBa", "not in the list!", "uh oh A", "aA");
    List<String> expected = Arrays.asList("aA", "uh oh A", "aA");

    assertEquals(expected, ListExamples.filter(list, new CheckHasA()));
}
```

### Symptom

![Symptom](symptom.png)
As you can see, only testFilter1 runs into an error (there are also some test cases for other methods that pass), ending up with the reverse list of what we'd expect.

### The Bug

Code before:
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
        if(sc.checkString(s)) {
            result.add(0, s);
        }
    }
    return result;
}
```

Code after:
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
        if(sc.checkString(s)) {
            result.add(s);
        }
    }
    return result;
}
```

The bug fix was to change `result.add(0, s)` into `result.add(s)`, which makes the filter add each item to the end of the list instead of the start. This fixes the issue because we want the returned list to have each item in the order they originally occurred in the input list; adding items to the start of the list wrongly reverses the order. The non-failing input still gave the correct answer because its result is a palindrome.

## Part 2
For this, I'll be showcasing different command-line options for the `grep` command.

### Option 1: -w
The `-w` option for `grep` only finds occurrences that contain the exact word provided, not things that contain the word within them.

Example 1:
```
Hugo@Hugos-Laptop docsearch % grep -wr ie technical
technical/government/Env_Prot_Agen/atx1-6.txt:type were outside of the test concentration range (ie.,
technical/government/Gen_Account_Office/og96014.txt:licensees in order to obtain special consideration (ie. an extended
technical/biomed/ar130.txt:          DMEM-20% FCS without added growth factors (ie <1% of
technical/biomed/cc4.txt:          side port of the Mallinckrodt endotracheal tube, ie 162
technical/biomed/cc4.txt:          grouping factor, ie factor `group (absence or presence of
...
```
In this example, I search for all occurrences of exactly `ie` in the `technical` directory. I use the `-r` option in addition to `-w` to look at all files in the directory. This is useful because it allows me to look for only examples and filter out extraneous words like "field".

Example 2:
```
Hugo@Hugos-Laptop docsearch % grep -wr edu technical/biomed
technical/biomed/1471-2156-2-3.txt:          http://sequence.aecom.yu.edu/chr12/QARM1.pdfand
technical/biomed/1471-2156-2-3.txt:          http://sequence.aecom.yu.edu/chr12/Parm2.pdf) were
technical/biomed/1471-2156-2-3.txt:          http://sequence.aecom.yu.edu/chr12/Parm2.pdf). These BACs
technical/biomed/1471-2156-2-3.txt:          http://sequence.aecom.yu.edu/chr12/Parm2.pdfand
technical/biomed/1471-2156-2-3.txt:          http://sequence.aecom.yu.edu/chr12/QARM1.pdf), thus
technical/biomed/ar319.txt:          (http://genome.ucsc.edu), was the primary source used to
...
```
In this example, I search for all occurrences of exactly `edu` in the `technical/biomed` directory. This is useful because it allows me to find links containing "edu" without including words like "education", which might pop up in research articles.

I used the `man` command to find out how the `-w` option works.

### Option 2: -i

### Option 3: -C

### Option 4: -n
