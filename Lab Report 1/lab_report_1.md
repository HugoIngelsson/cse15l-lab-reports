# Lab Report 1

## Command: "cd"

### No arguments
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ 
```
Working directory: /home/lecture1/

There was technically no output, thought it's important to look at the command prompt after the command finished executing. More precisely, the command prompt changed to be blank, with only a ~, which shows that the current working directory has been set to our root directory. This is because the "cd" command sets your current directory to the root directory when there is no input.

This output is not an error.

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
Working directory: /home/

When run with no inputs, the "ls" command lists the files in our current directory. This makes sense because combining our working directory ("/home/") with empty text yields our working directory again; really, having no arguments works exactly the same as having a path to another directory.

This output is not an error.

### Using a directory as argument
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
[user@sahara ~]$ 
```
Working directory: /home/

The output is a list of all the files in the folder "lecture1". This happens because "ls" combines our working directory ("/home/") with the input ("lecture1") into a new file path ("/home/lecture1"); because this file path is a directory, it then prints all of the files in that directory.

This output is not an error.

### Using a file as argument
```
[user@sahara ~]$ ls lecture1/Hello.java
lecture1/Hello.java
[user@sahara ~]$ 
```
Working directory: /home/

The output this time is the absolute file path of the input file in our directory. The "ls" command combines our working directory with the input into "/home/lecture1/Hello.java", which it recognizes as a file and not a directory. Therefore, it only prints the path and doesn't try to print any of its contents.

This output is not an error.

## Command: "cat"

### No arguments
```
[user@sahara ~]$ cat
HI
HI
echo... echo.. echo
echo... echo.. echo
not an error!
not an error!
^C
[user@sahara ~]$ 
```
Working directory: /home/

When running the "cat" command with no inputs, the terminal enters into a loop where it prints out whatever you type into it until you exit with control-C. This happens because when the "cat" command has no inputs, it automatically sets the "file" it should print out to be the terminal; thus, anything typed into the terminal instantly gets printed out again. Since the terminal technically never "ends", the only way to stop the cat command from looking for things to print is to force it to stop.

This output is actually not an error, despite it seeming like it is.

### Using a directory as argument
```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
[user@sahara ~]$ 
```
Working directory: /home/

The output is an error message telling the user that their input isn't valid. This is because the "cat" command is meant to output the contents of files, but "/home/lecture1" is a directory (not a file). This means that the command can't print any contents, so it prints an error message instead.

This is an error because the "cat" command is only meant to have files as input.

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
Working directory: /home/

The output is the contents of "/home/lecture1/Hello.java", which got printed because that's the absolute filepath you get after combining our working directory and the command input. Interestingly, there is no new line at the end of the output, so our next command prompt gets printed on the same line as the last closing curly bracket.

This output is not an error.
