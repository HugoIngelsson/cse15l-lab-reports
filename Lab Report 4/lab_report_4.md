# Lab Report 4
For this lab, I'll be going through the steps I went through to fix a bug in a program.

## Logging into ieng6
![Log into ieng6](ssh.png)
Keys pressed: `ssh cingelsson@ieng6-201.ucsd.edu<enter>`

This is the `ssh` command we've learned how to do in previous labs; it connects us to the remote `ieng6` server using my account, `cingelsson`. Since we've already entered an RSA key into the account, there's no need to verify my identity when using this computer. Notably, I `ssh` into `ieng6-201` in particular here because there's otherwise a chance that I get sent into `ieng6-203`, which for some reason doesn't have access to `javac`.

## Cloning my fork
![Clone fork](git_clone.png)
Keys pressed: `cs15lwi24<enter>`, then `git clone git@github.com:HugoIngelsson/cse15l-lab7.git<enter>`
..Explanation..

## Running the tests, with failures
![Failed test](test_failure.png)
Keys pressed: `cd cse15l-lab7/<enter>`, then `bash test.sh<enter>`
..Explanation..

## Editing the code file
![Using vim](vim.png)
Keys pressed: `vim ListExamples.java<enter>`, then `?1<enter>nr2<esc>:wq<enter>`
..Explanation..

## Running the tests, without failures
![Successful tests](test_success.png)
Keys pressed: `bash test.sh<enter>`
..Explanation..

## Committing and pushing the change to GitHub
![Adding, committing, and pushing](add_commit_push.png)
Keys pressed: `git add ListExamples.java<enter>`, then `git commit -m "Code fix<enter>"`, and then finally `git push`
..Explanation..
