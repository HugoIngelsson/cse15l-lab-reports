# Lab Report 1

## Command: "cd"

### No arguments
```
[user@sahara ~]$ cd
[user@sahara ~]$
```
Working directory: /home/

There was technically no output, thought it's important to look at the command prompt after the command finished executing. More precisely, the command prompt hasn't changed, which is because the "cd" command can't change the directory if you don't give it a directory to change to.

This probably isn't considered an error because there weren't any errors printed for not giving the command any arguments.

### Using a directory as argument
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$
```
Working directory: /home/

Again, there technically isn't any output. However, this time we can see that the command prompt changed, which is because the "cd" command took our working directory ("/home/"), appended the argument we gave it ("lecture1") to that, and set the working directory to their combination ("/home/lecture1"). 

Since the folder "lecture1" existed in our working directory, it didn't have any errors.

### Using a file as argument
```
[user@sahara ~]$ cd lecture1/Hello.java
bash: cd: lecture1/Hello.java: Not a directory
[user@sahara ~]$ 
```
Working directory: /home/

This time, there was an actual output, which describes an error in how we used the "cd" command. Specifically, it can't take a file as an input because it doesn't make any sense to have our directory be a file.

This output is an error because the "cd" command doesn't work with files as input; even though the file exists in our current directory, "cd" can't make it our working directory so it creates an error.

## Command: "ls"

### No arguments
```
[user@sahara ~]$ ls
lecture1
[user@sahara ~]$ 
```

### Using a directory as argument
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
[user@sahara ~]$ 
```

### Using a file as argument
```
[user@sahara ~]$ ls lecture1/Hello.java
lecture1/Hello.java
[user@sahara ~]$ 
```

## Command: "cat"

### No arguments
```
[user@sahara ~]$ cat
```

### Using a directory as argument
```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
[user@sahara ~]$ 
```

### Using a file as argument
```
[user@sahara ~]$ cat lecture1/Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}[user@sahara ~]$ 
```
