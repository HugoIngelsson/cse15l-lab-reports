# Lab Report 1

## Command: "cd"

### No arguments
```
[user@sahara ~]$ cd
[user@sahara ~]$
```
Working directory: /home/

### Using a directory as argument
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$
```

### Using a file as argument
```
[user@sahara ~]$ cd lecture1/Hello.java
bash: cd: lecture1/Hello.java: Not a directory
[user@sahara ~]$ 
```

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
