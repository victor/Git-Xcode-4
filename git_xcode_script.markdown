NOTE: As long as no project has been selected, I'll call the project XXX.

# Demo 1 Working on a team without central repo

NOTE: go drawing on a board as the demo goes.

## Step 1 - User 1 - adding to git

The user has already a project so he forget to include it in git so he does it now:

       cd ~/Documents/repos/XXX
       git add .
       touch .gitignore
       mate or mvim or edit .gitignore -> to cmodify the file

On the git ignore we add:

       build
       xcuserdata
       */xcuserdata/*
       .DS_Store

 *Suggestion: Make a few more commits to later show that, when cloning a repo, the full history goes with it.*
 
## Step 2 - User 1 - Sharing

The user wants to share its work with the world so he creates a bare repo on its public folder and push its project to it.

       cd ~/Public/josealobato-gitrepos/
       git init --bare XXX  <- explain --bare

Move to the location of the project and push to the bare repo

       cd ~/Documents/repos/XXX
 git remote add origin ~/Public/josealobato-gitrepos/
       cd push origin master

Call your team mate and tell him about the path of the bare public repo, and tell him to work on the project

## Step 3 - User 2 - getting the project

Connect to the user 1 public repo (mount a unit) and clone from the repo.

       git clone /Volumes/josealobato/Public/josealobato-gitrepos.git  <- test this, not sure about the path.

## Step 4 - User 2 - Create your own Public Bare to share

Here the user have to create a share the bare as before.

       cd ~/Public/victorjalencas-gitrepos/
       git init --bare XXX

Add your public as your remote and push to it.

       cd ~/Documents/repos/XXX
 git remote add origin ~/Public/victorjalencas-gitrepos/
       cd push origin master


Inform User 1 about your repo


## Step 5 - User 2 - Review remotes.

You want to make sure that your origin is your public repo and add the other user public as another remote with the name of the user. To do this you will need to edit the .git/config file and modify the current origin (the one created on clone) by the other user name.

(add here .git/config code demo)

Add your public as your remote and push to it.

       cd ~/Documents/repos/XXX
 git remote add origin ~/Public/victorjalencas-gitrepos/
       cd push origin master


Inform User 1 about your repo public folder

## Step 6 - Working

Now every developer can modify its code, add, commit and push to its own public repo (origin). It can as well pull from the other developers remotes. If it pulls the changes will be commited, but it is better to fetch and compare the remote with your branch or create a new branch from the remote to make changes. Remember that you can not commit to to a remote repo, in case you want to make changes you can branch or create a patch.


## Step 7 - Parallel commits

Each developer introduces changes and commits them, in a few commits

## Step 8 - Fetch/Merge and Pull

One of the developers does a pull, while the other shows the steps separately: fetch and merge. No conflict arises as they are in different parts

## Step 9 - More parallel commits

Now both developers add a method to the same class, at the end, thus ensuring a conflict at merge time

## Step 10 - Solving conflicts

Both devs do a fetch, and attempt to merge. A conflict pops up, and each one resolves it and pushes back the fix

## Step 11 - Just some more commits

Both devs go on adding changes and committing them. This could be a good time to introduce partial commits.

## Step 12 - Rebase

This time, instead of merging changes, to avoid gratuitous forks in the history tree, the changes are incorporated with a rebase


# Demo 2 A good process to follow (Git Flow like process)

With git you can do whatever you want, but it is a good idea to follow some rules to have a very clean, and useful environment to never loose track. Here are some rules:

* Master is clean. Never work in the master branch. The branch always contains the last working and tested app version with its corresponding tag. If a customer ask for the latest version we will use the one on Master.

* Develop is the integration area. The develop branch is the the place from where we will start new branches to work on and where we will integrate all the changes.



# Demo 3 ...


# Trick - Create a pacth to send by e-mail

A nice feature is that you can modify some code, create a patch and send to another person by e-mail. There are lots of ways to do that. Here are somes:

## Using diff

## Using format-patch


# Trick - a nice changes log

To fast view of the latest we can use git log, but the view is not very nice. We can use the --pretty config to make the view more

lgnr = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative -n8

lgs = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative --all -n8

lgs = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative

lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative --all.

#
# Trick - The correct way to comment commits.

Refer to Pro Git (free book by @schacon):

    As a general rule, your messages should start with a single line that’s no more than about 50 characters and that describes the changeset concisely, followed by a blank line, followed by a more detailed explanation. The Git project requires that the more detailed explanation include your motivation for the change and contrast its implementation with previous behavior — this is a good guideline to follow. It’s also a good idea to use the imperative present tense in these messages. In other words, use commands. Instead of “I added tests for” or “Adding tests for,” use “Add tests for.”

Here’s a template:

    Short (50 chars or less) summary of changes

	More detailed explanatory text, if necessary.  Wrap it to about 72
	characters or so.  In some contexts, the first line is treated as the
	subject of an email and the rest of the text as the body.  The blank
	line separating the summary from the body is critical (unless you omit
	the body entirely); tools like rebase can get confused if you run the
	two together.

	Further paragraphs come after blank lines.

	- Bullet points are okay, too

	- Typically a hyphen or asterisk is used for the bullet, preceded by a
	  single space, with blank lines in between, but conventions vary here