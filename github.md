# GITHUB CHEAT SHEET

## STARTING A PROJECT

Forked projects or existing projects
```bash
cd ~/GITHUB/manolosolalinde
git clone <url>
git config credential.helper store
```

Create remote repository
```bash
cd ~/GITHUB/manolosolalinde
mkdir <reponame>
curl -u 'manolosolalinde@gmail.com' https://api.github.com/user/repos -d '{"name":"'"${PWD##*/}"'"}'
echo "# TODO Readme" >> README.md
```

Start Local Repository and push first commit
```bash
git init
git config credential.helper store
git add .
git commit -m "first commit"
git remote add origin https://github.com/manolosolalinde/${PWD##*/}.git
git push -u origin master
```
## DELETING ALL HISTORY
```bash
cd <localrepofolder>
rm -rf .git
Start Repository (as above)
git push -u --force origin master
```
## DELETING A FULL REMOTE REPO
```bash
cd <REPONAME>
curl -X DELETE -H 'Authorization: token replacewithtoken' https://api.github.com/repos/manolosolalinde/${PWD##*/}
```
Get Delete Auth token
```bash
curl -v -u 'manolosolalinde@gmail.com' -X POST https://api.github.com/authorizations -d '{"scopes":["delete_repo"], "note":"token with delete repo scope"}' >> token.json
```
## INITIAL GLOBAL SETUP
```bash
git config --global user.name "Manuel Solalinde"
git config --global user.email "manolosolalinde@gmail.com"
```

# UNTRACK FILES already added to git repository based on .gitignore
```bash
git rm -r --cached .
git add .
git commit -m ".gitignore fix"
```
    rm is the remove command
    -r will allow recursive removal
    --cached will only remove files from the index. Your files will still be there.
    The . indicates that all files will be untracked. 
    You can untrack a specific file with git rm --cached foo.txt (thanks @amadeann).



## GENERAL PURPOSE

http://www.cheat-sheets.org/saved-copy/github-git-cheat-sheet.pdf

`git config --global user.name "Manuel Solalinde"`\
Sets the name you want atached to your commit transactions

`git remote add origin git@github.com:manolosolalinde/newrepo.git`\
Add origin for existing repository

`git config --global user.email "manolosolalinde@gmail.com"`\
Sets the email you want atached to your commit transaction

`git init [project-name]`\
Creates a new local repository with the specified name

`git clone [url]`\
Downloads a project and its entire version history

`git status`\
Lists all new or modified files to be commited

`git add [file]`\
Snapshots the file in preparation for versioning

`git reset [file]`\
Unstages the file, but preserve its contents

`git diff`\
Shows file differences not yet staged

`git diff --staged`\
Shows file differences between staging and the last file version

`git commit -m "[descriptive message]"`\
Records file snapshots permanently in version history

`git branch`\
Lists all local branches in the current repository

`git branch [branch-name]`\
Creates a new branch

`git checkout [branch-name]`\
Switches to the specified branch and updates the working directory

`git merge [branch]`\
Combines the specified branch’s history into the current branch

`git branch -d [branch-name]`\
Deletes the specified branch

