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
