
![](Attachments/Pasted%20image%2020260922020556.png)

| part                  | meaning                                  |
| --------------------- | ---------------------------------------- |
| **Working Directory** | الملفات التي تعمل عليها حاليًا           |
| **Staging Area**      | الملفات التي جهزتها لتدخل في الـ Commit  |
| **Local Repository**  | مستودع Git الموجود على جهازك             |
| **Remote Repository** | المستودع الموجود على الإنترنت مثل GitHub |

Working Directory
       │
       │ git add
       ▼
Staging Area
       │
       │ git commit >> What changed? When? And who made the change?
       ▼
Local Repository  >> The Local Repository is a Git repository located on your machine.
       │
       │ git push >> Send the Commits located on your device to the Remote Repository.
       ▼
Remote Repository


## What happens when there are changes to Remote?

magine that your colleague modified the project and uploaded the changes to GitHub.
```
git fetch
```



____
____
___
## The steps To master GitHub ? 
1.  copy the link of repo 
 ![](Attachments/Pasted%20image%2020260904154606.png)
 2.  open terminal   and enter to directory  and  paste this is .... 
```
    *.git clone https://github.com/Qusai-Abdullah/Cybersecurity-Writeups.git
    *.cd Cybersecurity-Writeups
    *. git status 
   
```
![](Attachments/Pasted%20image%2020260904161205.png)

___
___

####  1) Now  the red files are  need to transform to (staging area)  ?
```
git add qusai/  or  git add * for add all things 
```
![](Attachments/Pasted%20image%2020260904161606.png)

## To return the file from the (staging area  )
```
	git reset head css.css 
```
![](Attachments/Pasted%20image%2020260904162125.png)


## 2) To transform the files to the (Local repo) ?
 ```
 git commit -m "........." <<  the description for what you made ..
 ```
## 3)To transform the files to the (remote repo) ?
```
git push remoteName BranchName   it will make you sigin in 



to know the remoteName >> git remote -v 
to know the BranchName >> git branch 
```
 ![](Attachments/Pasted%20image%2020260904170245.png)

![](Attachments/Pasted%20image%2020260904170901.png)
![](Attachments/Pasted%20image%2020260904171747.png)



___
___
### NOW Will add another file or modified the file 
1.   ![](Attachments/Pasted%20image%2020260904172228.png)
    2. ![](Attachments/Pasted%20image%2020260904172345.png)
____
___
___
## Now To get from Remote repo ?
  ```
  git pull remotename 
  git pull origin >>
  this command doing two thing 
  1. git fetch 
  2.git marge
  ```

___
___

# Github public Key ?
```
ssh-keygen -t rsa -b 4096 -C ypurgmail@gmail.com
```


![](Attachments/Pasted%20image%2020260904180315.png)

![](Attachments/Pasted%20image%2020260904184403.png)

done 
 ![](Attachments/Pasted%20image%2020260904184446.png)
 To test 
 ```
  ssh -T git@github.com 
  and enter the password 
 ```
 ![](Attachments/Pasted%20image%2020260904184629.png)



----
----
----





## To add our Writes up into GitHub ?
1.  cd C:\Users\HP\Documents\Obsidian Vault
2.  *git ststus *
3.  to now git location >> *git rev-parse --show-toplevel*
4.  <mark style="background: #FF5582A6;">(git init) if we have no git</mark>
5. (New-Item -Path ".gitignore" -ItemType File) to avoid the useless file to upload into GitHub
6. (notepad .gitignore)
7. (Get-Content .gitignore)
8. <mark style="background: #FF5582A6;">(git add .)</mark>
9. <mark style="background: #FF5582A6;">(git status)</mark>
10. <mark style="background: #FF5582A6;">(git commit -m "Initial commit - Obsidian Vault")</mark>
11. 






![](Attachments/Pasted%20image%2020260922035031.png)
```
git add GitHub.md
```
