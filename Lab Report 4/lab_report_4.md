# Lab Report 4
For this lab, I'll be going through the steps I went through to fix a bug in a program.

## Logging into ieng6
![Log into ieng6](ssh.png)
Keys pressed: `ssh cingelsson@ieng6-201.ucsd.edu<enter>`

This is the `ssh` command we've learned how to do in previous labs; it connects us to the remote `ieng6` server using my account, `cingelsson`. Since we've already entered an RSA key into the account, there's no need to verify my identity when using this computer. Notably, I `ssh` into `ieng6-201` in particular here because there's otherwise a chance that I get sent into `ieng6-203`, which for some reason doesn't have access to `javac`.

## Cloning my fork
![Clone fork](git_clone.png)
Keys pressed: `cs15lwi24<enter>`, then `git clone git@github.com:HugoIngelsson/cse15l-lab7.git<enter>`

The first command I ran simply put me into the correct workspace since I want anything I download for this class to be contained in this class's workspace, `cs15lwi24`. The second command cloned my fork using the SSH key that I connected to GitHub from my `ieng6` account. 

## Running the tests, with failures
![Failed test](test_failure.png)
Keys pressed: `cd cse15l-lab7/<enter>`, then `bash test.sh<enter>`

The first command put me into the correct working directory, `cse15l-lab7/`, which will be helpful because it cuts out typing the directory every time I want to run a command in it. The second command ran the bash file `test.sh`, which compiles and runs `ListExamples.java` using `javac` then `java`. As a result of running this command, I can now see that there's a bug in `ListExamples.java`.

## Editing the code file
![Using vim](vim.png)
Keys pressed: `vim ListExamples.java<enter>`, then `?1<enter>nr2<esc>:wq<enter>`

Running `vim` on `ListExamples.java` put me into the terminal editor, editing `ListExamples.java`. The next series of key-presses are cryptic, but they're also a very efficient way of fixing the bug.

First, typing in `?` tells `vim` I want to search for something from the back (as opposed to `/`, which searches from the front). Then, typing in `1` and pressing enter means that I want to search for all occurrences of `1`, starting from the back.

I then press `n` once to skip the first occurrence of `1` and go to the second one. There, I press `r`, which means to replace the character the cursor is currently on, and then `2`. In all, this replaces the second-to-last `1` with a `2`, fixing the variable name in the file.

Finally, we want to exit `vim`. To do that, I first press `<esc>` to exit insertion mode, then I press `:wq`, which tells `vim` to first write to file (i.e. save) and then quit, returning me back to the terminal.

## Running the tests, without failures
![Successful tests](test_success.png)
Keys pressed: `bash test.sh<enter>`
..Explanation..

## Committing and pushing the change to GitHub
![Adding, committing, and pushing](add_commit_push.png)
Keys pressed: `git add ListExamples.java<enter>`, then `git commit -m "Code fix<enter>"`, and then finally `git push`
..Explanation..
