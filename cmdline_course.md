---
layout: default
---

# Bits about the Command Line Tools course

I signed to the course because I knew only very basics of navigating \*nix type of system. I didn't know how command line can be useful for linguists and how much time command line tools can save. Here I've listed an overview of our 7-week long journey.

![xkcd linguistics](https://imgs.xkcd.com/comics/computational_linguists.png "xkcd comics on computational linguistics")

## **WEEK 1:** Introduction to Command Line Environments

We started by setting our environment. I did not have to bother about it since I had already been using Pop!\_OS. Then we tried our very first commands to navigate the system and work with files and directories.

### List of commands we learned

#### Navigating the system, system info
*	`ls`
*	`pwd`
*	`whoami`

#### Fetching files from internet
*	`wget`

#### Working with files
*	`mv`
*	`cat`
*	`less`
*	`cp`
*	`rm`
*	`mkdir`
*	`cd`

#### Quitting applications
*	`less` uses `q`
*	almost everything else uses `ESC`, `Ctrl-c` or `Ctrl-d`
*	(but `vim` uses `ESC :q` or `ESC :wq`)

We also covered the difference between text and binary files.

Last but not least, we learned how to compress a directory using `tar`:

```bash
tar -czvf COMPRESSED_DIRECTORY.tgz UNCOMPRESSED_DIRECTORY/
```

## **WEEK 2:** Navigating a UNIX System

We continued on learning more about the Unix System. We tried to copy, move and remove directories. We inspected standard system directories and their content. We discussed system permissions and how to change them. In the second part of that week, we learned about process management and how to control processes. In the last part, we worked with `ssh` and `scp` using a remote server.

### List of commands we learned

#### Directories
*	`cp -R`
*	`rm -R`
*	`rmdir`

#### File system
*	`which`

#### Processes
*	`top`
*	`&`
*	`fg`
*	`ps`
*	`kill`
*	`Ctrl-z`

#### Remote servers
*	`ssh`
*	`scp`


## **WEEK 3:** Basic Corpus Processing

In week 3, we were finally introduced to text processing tools. We learned about different encodings at first. Then we continued on structured text files.

### List of commands we learned

#### Converting encodings
*	`file`
*	`dos2unix`
*	`iconv`

#### Generating a word list
*	`tr`
*	`sort`
*	`uniq`

#### Searching in text files
*	`grep` or `egrep`

#### Basic comparison
*	`cut`
*	`sort`
*	`uniq`
*	`egrep -w -f`

## **WEEK 4:** Advanced Corpus Processing

Things started to get really tough in that week! We learned about `sed` command and how to use it to find patterns and replace them in a text file. UNIX pipelines were introduced as well.

### Command Examples

#### Frequency List

```
bash
cat life_of_bee.txt | tr -s '\n\r\t\ ' '\n' | tr -dc "A-Za-z0-9\n'" | sort | uniq -c | sort -nr > life_of_bee.freq
```

#### Sentence per Line Format

```
bash
cat life_of_bee.txt | dos2unix | sed 's/^$/#/' | tr '\n' ' ' | sed -E 's/([.?!]) ([A-Z])/\1# \2/g' | sed -E 's/([IVX][.])#/\1/g' | tr '#' '\n' | sed 's/^ *//' | grep -v "^$" > life_of_bee.sent
```

## **WEEK 5:** Scripting and Configuration Files

During week 5 we grabbed our commands and transformed them to scripts, so we would save time not typing them one by one over and over again. We used our knowledge of permissions and applied basic programming knowledge (such as variables and loops) on our scripts as well.

We looked around bash configuration files and modified them. But I didn't have to do that because I had had my .bashrc (.zshrc respectively) already modified since the beginning of using Pop!\_OS. 

### Example of a Bash Script

```
bash
#! /bin/bash

# The script does a basic maintenance of the system.
# Make sure to run it as a root.

echo -e "\nMaintenance starting\n"

apt update
apt -y upgrade

apt -y autoremove
apt autoclean

echo -e "\nJob done!\n"
```

## **WEEK 6:** Installing and Running Programs

We installed programs. This was more like a revision for me since I had used Linux before. Despite that I learned something new. I hadn't used `pip` to install Python packages before. 

### List of commands we learned

*	`sudo`
*	`passwd`
*	`whoami`
*	`apt-get`
*	`locate`

The second part of the week was about `make`. This was probably the hardest thing for me to grasp. The process of making a `Makefile` wasn't explained very well, so I don't know how to use it at all. I think `make` is still a bit overkill for the easy tasks we performed so I am satisfied with me writing scripts anyway.

## **WEEK 7:** Version Control

The last week was all about Git, GitHub and version control. I have used GitHub before but not profusely and I had always used GUI. It was great to try working with GitHub using command line. Now, I think I am prepared to use GitHub more and better :blush:

### List of commands we learned

#### Setting config values
*	`git --version`
*	`git config --global user.name "name"`
*	`git config --global user.email "email"`
*	`git config --list`

#### Start Tracking Code with Git
*	`git init`
*	`rm -rf .git`
*	`touch .gitignore`
*	`git clone <url> <where>`

#### Edit, Commit, Push!
*	`git status`
*	`git add -A`
*	`git commit -m "This is the commit message"`
*	`git pull origin master`
*	`git push origin master`
*	`git log`
*	`git revert HEAD`
*	`git reset`

#### Branches
*	`git branch <branch>`
*	`git push -u origin <branch>`
*	`git checkout <branch>`
*	`git branch --merged`
*	`git merge <branch>`
*	`git branch -d <branch>`
*	`git branch -a`
*	`git push origin --delete <branch>`

#### Info about repo
*	`git remote -v`
*	`git branch -a`
*	`git diff`

### Git Pushing Changes Timeline

| check untracked files | add all files to staging area | check status       | commit changes                  | pull any changes that were made | push changes                   |
|-----------------------|-------------------------------|--------------------|---------------------------------|---------------------------------|--------------------------------|
| ```git status```      | ```git add -A```              | ``` git status ``` | ``` git commit -m "Message" ``` | ``` git pull origin master ```  | ``` git push origin master ``` |

### Git Common Workflow

| create branch                  | begin working within the created branch | check status     | add all files to staging area | commit changes                | push branch to remote                  | checkout master           | pull all changes             | merge the branch              | push changes                 | delete branch locally             | delete branch from repository                |
|--------------------------------|-----------------------------------------|------------------|-------------------------------|-------------------------------|----------------------------------------|---------------------------|------------------------------|-------------------------------|------------------------------|-----------------------------------|----------------------------------------------|
| ```git branch <branch name>``` | ```git checkout <branch name>```        | ```git status``` | ```git add -A```              | ```git commit -m "Message"``` | ```git push -u origin <branch name>``` | ```git checkout master``` | ```git pull origin master``` | ```git merge <branch name>``` | ```git push origin master``` | ```git branch -d <branch name>``` | ```git push origin --delete <branch name>``` |


[back](./)

