# GIT

#### 어떤 Branch를 Local과 Remote 동시에 삭제하려면?
```bash
# https://koukia.ca/delete-a-local-and-a-remote-git-branch-61df0b10d323
# Delete local branch
$ git branch -d branch_name
$ git branch -D branch_name     # Forcibly

# Delete remote branch
$ git push <remote_name> --delete <branch_name>
$ git push <remote_name> :<branch_name>

# If u want delete multiple branches...
$ git push <remote_name> --delete <branch_name1> <branch_name2> ...
```
