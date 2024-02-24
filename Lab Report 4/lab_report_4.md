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

This is the same command as from before, but now when I run the `test.sh` script, it tells me that there are no failures. This shows me how the bug fix I did in the previous step worked.

## Committing and pushing the change to GitHub
![Adding, committing, and pushing](add_commit_push.png)
Keys pressed: `git add ListExamples.java<enter>`, then `git commit -m "Code fix<enter>"`, and then finally `git push<enter>`

Finally, I want to commit and push the changes I've made to GitHub. To do so, I first use `git add` to add `ListExamples.java` to the files that will be included in my next `commit`. Then, I use `git commit` with the message `"Code fix"` to get git ready to push the changes I want to GitHub. Anyone looking at the past commit history of this fork will be able to see the message I sent with it, so really I should have sent something more descriptive than "Code fix" so that people can understand what I did. Finally, I use `git push` to send this change to GitHub so that anyone else with access to the fork can download it.
