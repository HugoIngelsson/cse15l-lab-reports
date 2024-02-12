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
The `-i` option for `grep` makes it case-insensitive, which means that capitalization of words does not matter for finding them.

Example 1:
```
Hugo@Hugos-Laptop docsearch % grep -ilr dna technical
technical/government/About_LSC/Progress_report.txt
technical/government/About_LSC/commission_report.txt
technical/government/About_LSC/State_Planning_Special_Report.txt
technical/government/Media/New_funding_sources.txt
technical/government/Media/Making_a_case.txt
...
```
This examples shows me printing the names of files that contain any variation of "DNA", typing in only "dna". This is useful because it allows you to explore all cases (i.e. accounting for words at the start of sentences) without needing to type out things multiple times.

Example 2:
```
Hugo@Hugos-Laptop docsearch % grep -ilr DNA technical
technical/government/About_LSC/Progress_report.txt
technical/government/About_LSC/commission_report.txt
technical/government/About_LSC/State_Planning_Special_Report.txt
technical/government/Media/New_funding_sources.txt
technical/government/Media/Making_a_case.txt
...
```
This example has the exact same output as example 1, even though I typed in a different word for `grep`'s input. This is useful because it shows how `-i` allows you to be slightly more careless about typos when typing things fast, something that could save you time when running many commands.

I used the `man` command to find out how the `-i` option works.

### Option 3: -m
The `-m num` option for `grep` allows the user to stop looking for occurences of the input after `num` occurrences have been found in a file.

Example 1:
```
Hugo@Hugos-Laptop docsearch % grep -r -m 1 hi technical/plos
technical/plos/pmed.0020273.txt:        than 1 million cases in the US and Europe. The symptoms for both these conditions—which
technical/plos/journal.pbio.0030032.txt:        Applied Biosciences from the University of Arizona, who believes his PSM makes him more
technical/plos/pmed.0020065.txt:        For disease outbreak detection, the public-health community has historically relied on
technical/plos/pmed.0020071.txt:        children and adolescents [1]. According to the World Health Organization (WHO), mental and
technical/plos/pmed.0020059.txt:        adjusting for natural temporal and geographical variation, and dealing with the lack of
...
```
In this example, I look for the first occurrence of "hi" in each file within the `technical/plos` directory. This can be useful if you're trying to find the first time a string occurs in a text if you need to read from that spot onwards.

Example 2:
```
Hugo@Hugos-Laptop docsearch % grep -rm 3 "AND" technical/biomed
technical/biomed/1472-6882-3-3.txt:          AND (cervical vertebrae OR cervical
technical/biomed/1472-6882-3-3.txt:          AND (diagnosis OR manual OR
technical/biomed/1472-6882-3-3.txt:          AND (apophyseal OR asymmetry OR back
technical/biomed/gb-2001-2-7-research0025.txt:        CpG_ISLANDS
technical/biomed/1471-2288-2-4.txt:        correspond to AND rules, for example A>1 and B>1, as
...
```
In this example, I look for the first 3 occurrences of "AND" in each file within the `technical/biomed` directory. This can be useful because sometimes you want to find many occurrences of a string within a file but still don't want every occurrence (because that could lead to too much output).

I used the `man` command to find out how the `-m` option works.

### Option 4: -n
The `-n` option for `grep` makes each like print with the line number the input is found at in addition to what the surrounding text says.

Example 1:
```
Hugo@Hugos-Laptop docsearch % grep -n "molecule" technical/biomed/1471-2105-3-2.txt
26:        to predict the correct structure for an RNA molecule, given
32:        organism's rRNA, a molecule that encompasses two-thirds of
39:        single molecule, that included prokaryotes, protozoa,
105:        structure over this wide range of RNA molecules.
117:        RNA molecules ( 
168:            functionally equivalent molecule ( 
174:            sequences for a given molecule were determined, we
240:            representative for that molecule (Table 1); for
250:            seven different diagrams for that molecule: Nucleotide,
313:            unambiguously numbering each helix in a RNA molecule.
783:            group. For each of the three rRNA molecules (5S, 16S,
1414:            The two molecules (16S and 23S rRNA) show a
2009:            H-4C.1) displays the types of data (RNA molecules and
2052:        information for each RNA molecule under study, and our
2053:        interest in studying more RNA molecules beyond 16S and 23S
2057:        molecule are:
2073:        rRNA. The other RNA molecules we maintain (5S rRNA, tRNA,
2097:        the data; and 8) analyze more types of RNA molecules from a
2099:        formats utilized for the RNA molecules currently
```
In this example, I look for occurrences of "molecule" in the longest file in the `technical` directory. Clearly, the `-n` option is useful here because it allows us to quickly find where the input is in the file when we would otherwise need to do a lot of painful searching in a massive file to find it.

Example 2:
```
Hugo@Hugos-Laptop docsearch % grep -rn -m 1 "mRNA" technical/biomed/
technical/biomed//1471-2156-3-11.txt:39:        Tnfrh1 mRNA and discuss the
technical/biomed//gb-2002-4-1-r2.txt:122:          standard for each measurement, a pool of reference mRNA
technical/biomed//bcr620.txt:319:          This procedure allowed OPN, TSP-1 and TYRP-1 mRNA
technical/biomed//1471-2164-2-9.txt:39:        association with yPOP2, of the major yeast cytoplasmic mRNA
technical/biomed//gb-2001-2-4-research0010.txt:78:        gene length [ 44, 45, 46, 47], and mRNA secondary structure
...
```
In this example, I combined the use of `-n` and `-m` to find the first occurrence of "mRNA" in each file in `technical/biomed` and to locate where it was found. The combination of these two options can be very powerful to find exactly where in a directory you need to look to find something you're looking for.

I used the `man` command to find out how the `-n` option works.
