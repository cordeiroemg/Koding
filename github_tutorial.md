


> Tutorial for Github [github](https://github.com).

When I am stating a software project, how do I create a repository locally

    git init <newprojectname>
That will create a .git folder that will keep all directories you need for the basics git functions. You can assess this folder using the command 

    open .git
When you start to add remote destination by collaborating to somebody else of just access you files remotely at github or any other repository. First you have to create a new address in your config file by the command:

    git remote add origin http://github.com/cordeiroemg/repositoryname

You can check the remote address file in you .git file by typing:

    cat .git/config

the new address will be at *url* description

##Configuration

Set your user name and email correctly to guarantee ownership and access your collaborators works. 

    git config --global user.name "<username>"
    git config --global user.email "<email>"

Make sure to set the colors. That might be important to identify what is committed, add, removed, etc. much easier. 

    git config --global core.autocrlf true
    git config --global core.autocrlf input
    git config --global color.ui auto 
##how to initialize your new repository 

If you already have a project going on in your computer. When you in your project directory in the command line, just type

    git init

That will turn your local directory into a git repository in a completely non-destructive way. If you want the project in a source control before start the project, just type init command and the name of the new directory you want to create 

    git init newproject

This project will be created already initialized as a git repository

##commit in git

The commit is a they way we keep track on changes in the project. 

    git status 

will tell you what files might need to be committed. That's going to tell you about files that had changes or new files added since the last command. When you judge the changes are ready to be committed  use:

    git add <filename>
that command will make your file to move into the stage area, which you can check by using status command. To complete the process use command:

    git commit -m "Type your descriptive message here so people can tell in advance what kind of change you made"

The flag -m allows you to leave a message. If you do not include your message in your commit step, github will open the text editor for your to type a message before commit the file. 
   
##Dif command
This command is very handy to keep track on the modifications in your file and check what were those differences

    git diff

Gives you the description of how your working tree differs from your working area. But if you already staged your files, then you have to type

    git diff --staged
If you staged a file and want to modify the file, the command status will tell you that you have a staged file with unstaged modification. If you want to compare your change history with your most recent file version, use:

    git diff HEAD
Head is the command for the most recent change made. You can also use the color or word command to highlight the modifications with different colors 

    git diff --color-words
    git diff --word-diff

The stat command will tell you which file received changes

    git diff --stat 
##Log
To find out how your history looks like. You can use 

    git log --oneline

 
To see just the description of your commits with the short version of the commit ref (the log number on you left side). You can use

    git log --stat 

To have more information on which file was modified. 
##remove
You can easily remove a single file by using the command 

    git rm <filename>
To delete multiple files, you must you the command 

    git add -u .
. states that the command refers to you current work directory. If you want the file stop to be track by git without delete from your home directory, use the command 

    git rm --cached <filename>
##Branch
When starting out a new project or start to work in an existing one is important to start a new branch. A lot of people think the master branch is where the codes are, but commit to a new branch allows us to work safer . To create a new branch just type:

    git branch <nameofthenewbranch>

To delete a branch just type:

    git branch -d <branchname>

##Checkout 
You can find out which branch you are in by the commands 

    git status 

or

    git branch

The propose of the checkout is to change branches or contents wheres the upcoming commits will be made, and once you have made your commits to the branch you are checkouted to you can type switch 
 

    git checkout <branchname>

  








