# GIT & GITHUB

## *Index*

>1. [New](https://gist.github.com/ctorstens/5375420#new)
1. Setup
  - Creating a new, local-only repo
  - Creating a github-based repo
  - [Moving a local-only repo into github](https://gist.github.com/ctorstens/5375420#creating-a-github-repo-from-a-pre-existing-local-repo)
2. Basics
  - Commit
  - [Branch](https://gist.github.com/ctorstens/5375420#branch)
1. Taking from others users' repositories:
  - [Clone](https://gist.github.com/ctorstens/5375420#clone)
  - [Fork](https://gist.github.com/ctorstens/5375420#fork)
  - Fetch
  - Pull
  - Prune
1. Giving back to others users' repositories:
  - Push
  - Pull Requests
2. [Remotes](https://gist.github.com/ctorstens/5375420#remotes)
2. [Getting around Git](https://gist.github.com/ctorstens/5375420#getting-around-git)
3. [Troubleshooting]()
1. [References](https://gist.github.com/ctorstens/5375420#references)

## SETUP
---
- #### Creating a new, local-only repo
  1. create the repo in the root directory of your project
  
    ``` git init ```
- #### Creating a github-based repo
  1. Create a new repo at [github](https://github.com/repositories/new)
    * include a ```README``` and an appropriate ```.gitignore``` file
  2. CLONE the repo to your computer
- #### Moving a local-only repo into github
  1. Create a new repo at [github](https://github.com/repositories/new)
  2. set your local repo to view the url from step one as remote

        git remote add origin <URL_from_your_newly_created_repo>



## BASICS
---
  * STATUS
  * ADD
  * COMMIT
  * BRANCH
  * disply repo history




## Getting Around Git
- Finding the current status of your project

         git status
- Adding files to your repo

         git add <file>
         
- Seeing your repo history *(any of these will do)*

  ``` gitk ```

  ``` git log --graph ```
  
  ``` git log --graph --oneline ```
        
  ``` git log --graph --full-history --all --color --pretty=format:"%x1b[31m%h%x09%x1b[32m%d%x1b[0m%x20%s" ```
  




4. Push your commit

  create a remote named 'origin' pointing at your github repo
  
        git remote add origin git@github.com:<creator-name>/<project-name>.git
  
  if you're changing your pre-existing origin use this instead
  
        git remote set-url origin git://new.url.here
  
  send your commits in the "master" branch to GitHub
  
        git push origin master 
  
  fetch a specific branch & merge it into your current local branch
  
        git pull <REMOTENAME> <BRANCHNAME>
 


## BRANCH
---

list branches

        git branch

Create a new branch

        git branch experiment
  
        git checkout -b experiment (switches to it at the same time)
  
Switch to a branch
  
        git checkout experiment
        git checkout master

if you want to push the branch

        git push origin experiment
  
Merging

        git checkout master
        git merge experiment

Deleting a branch

        git branch -d experiment # won't allow you to lose changes
        git branch -D experiment # will allow you to lose changes


## Remotes
---
- Which remote to use?
  - ``` https:// - HTTPS read-only and read/write ```

    >*The https:// clone URLs are available on all repos, public and private. They are smart, so they will offer either read-only or read/write access depending on your permissions to the repo. You will have to authenticate using your GitHub username and password to push to a repo you have write permission with and to read from any private repo you have access to.*

    >*Use these URLs for users that are behind a firewall or proxy. Many firewalls will block the git:// and ssh URLs from working.*

    >*You don't have to enter your password every time you use an HTTPS URL, check out [this guide](https://help.github.com/articles/set-up-git#password-caching) for more info.*

  - ``` git:// - Git read-only ```

    >*All git:// URLs are anonymous, public and read-only. Private repos do not have this URL type.*

    >*Use these URLs when cloning someone else's repo (where you don't have write access) and for submodules that point at public repos.*

  - ``` git@github.com - SSH read/write ```

    >*These URLs provide access to a git repo over SSH. To use these URLs, you must have write access to a public repo or any access to a private repo. These URLs will not work with a public repo you do not have write access to. You must also have an SSH keypair generated on your computer and attached to your GitHub account.*

    >*Use these URLs on your production servers for deployment. You can also use SSH agent forwarding with your deploy script to avoid managing keys on the server. Users that are familiar with SSH keys may prefer these URLs over HTTPS.*

- View existing remotes

        git remote -v
        
- Add a remote

        git remote add origin https://github.com/user/repo.git

- Tracking branch
>*This is useful if, when you have the master branch checked out, you want git pull to work without needing to do git pull origin master. Checking out a local branch from a remote branch automatically creates what is called a tracking branch. Also, when you clone a repository, it generally automatically creates a master branch that tracks origin/master.*

        git remote add --track master origin  https://github.com/user/repo.git

- Rename remote

        git remote rename '<orig_name>' '<new_name>'

- Change remote's URL

        git remote set-url origin https://github.com/user/repo2.git

- Delete remote

        git remote rm destination



## FORK
---

1. via [github](http://www.github.com), fork project to your account (click "fork" button)

2. [normal clone](https://gist.github.com/ctorstens/5375420#clone) from your own account

3. Configure remotes
  >When a repo is cloned, it has a default remote called origin that points to your fork on GitHub, not the original repo it was forked from. To keep track of the original repo, you need to add another remote named upstream:
  
    Assign the original repo to a remote called "upstream"

        git remote add upstream <URL-OF-ORIGINAL-GIT>
    
    Pull in changes not present in your local repository, without modifying your files

        git fetch upstream
    
    
4. Push commits

        git push origin master
  
5. Pull in upstream changes

        git fetch upstream
  
        git merge upstream/master


## Models of collaborative development on GitHub
---

- #### Fork & Pull
>The Fork & Pull Model lets anyone fork an existing repository and push changes to their personal fork without requiring access be granted to the source repository. The changes must then be pulled into the source repository by the project maintainer. This model reduces the amount of friction for new contributors and is popular with open source projects because it allows people to work independently without upfront coordination.

- #### Shared Repository Model
>The Shared Repository Model is more prevalent with small teams and organizations collaborating on private projects. Everyone is granted push access to a single shared repository and topic branches are used to isolate changes.

  >Pull requests are especially useful in the Fork & Pull Model because they provide a way to notify project maintainers about changes in your fork. However, they're also useful in the Shared Repository Model where they're used to initiate code review and general discussion about a set of changes before being merged into a mainline branch.


## *Taking from* others users' repositories:
---

- #### git clone
*To grab a complete copy of another user's repository when you do not have a local copy of the repository already established:*

  Go to the appropriate github repository and copy and past the command, e.g...

      git clone git@github.com:<creator-name>/<project-name>.git




- #### git fetch
  >If you already have a local repository with a remote set up for the desired project, you can grab all branches and tags for the existing remote using git fetch <REMOTENAME>. By default, git clone will create a remote named origin pointing to the URL you cloned from. Fetch does not make any changes to local branches, so you will need to merge a remote branch with a paired local branch to incorporate newly fetch changes.

- #### git pull
  > Similar to git fetch, you can use git pull <REMOTENAME> <BRANCHNAME> to fetch a specific branch and merge it into your current local branch. For one-time pulls from other users' repos, you can use a URL in place of a remote name.

  >Because pull potentially performs a merge on the retrieved changes, you should ensure that your working tree and index are clean before running the pull command. If you run into a merge conflict you cannot resolve, or if you decide to abort the merge, you can use git merge --abort to take the branch back to the state it was in before you pulled.



- #### git remote prune
  >Sometimes branches are deleted from an upstream repository, perhaps even by the recommendation of the user interface after a merged pull request. By default, git fetch will not remove any remote-tracking branches that have been deleted on the remote repo. Running git fetch --prune or git remote prune REMOTENAME will delete these tracking branches.



## *Giving back* to others users' repositories:
---

- #### Push
*Publish commits from your repository into a remote for other users to view and potentially fetch*

  To push a local branch to an established remote:

      git push <REMOTENAME> <BRANCHNAME>
*or, if you would like to give the branch a different name on the upstream side of the push:*

      git push <REMOTENAME> <LOCALBRANCHNAME>:<REMOTEBRANCHNAME>

- #### Pull Requests
  *Pull requests let you tell others about changes you've pushed to a GitHub repository. Once a pull request is sent, interested parties can review the set of changes, discuss potential modifications, and even push follow-up commits if necessary.*
  
  Check out [Using Pull Requests](https://help.github.com/articles/using-pull-requests) from the GitHub Help pages. For this action you must go to the [GitHub](http://www.github.com) itself.


## Undo

### Reset

#### hard

```
git reset --hard
```

>hard makes everything match the commit you've reset to. This is the easiest to understand, probably. All of your local changes get clobbered. One primary use is blowing away your work but not switching commits: git reset --hard means git reset --hard HEAD, i.e. don't change the branch but get rid of all local changes. The other is simply moving a branch from one place to another, and keeping index/work tree in sync. This is the one that can really make you lose work, because it modifies your work tree. Be very very sure you want to throw away local work before you run any reset --hard.


#### mixed

```
git reset --mixed
```

>mixed is the default. It resets the index, but not the work tree. This means all your files are intact, but any differences between the original commit and the one you reset to will show up as local modifications (or untracked files) with git status. Use this when you realize you made some bad commits, but you want to keep all the work you've done so you can fix it up and recommit. In order to commit, you'll have to add files to the index again (git add ...).

#### soft

```
git reset --soft
```

>soft doesn't touch the index or work tree. All your files are intact as with --mixed, but all the changes show up as changes to be committed with git status (i.e. checked in in preparation for committing). Use this when you realize you've made some bad commits, but the work's all good - all you need to do is recommit it differently. The index is untouched, so you can commit immediately if you want - the resulting commit will have all the same content as where you were before you reset.

#### merge

```
git reset --merge
```
>Merge was added recently, and is intended to help you abort a failed merge. This is necessary because git merge will actually let you attempt a merge with a dirty work tree (one with local modifications) as long as those modifications are in files unaffected by the merge. git reset --merge resets the index (like --mixed - all changes show up as local modifications), and resets the files affected by the merge, but leaves the others alone. This will hopefully restore everything to how it was before the bad merge. You'll usually use it as git reset --merge (meaning git reset --merge HEAD) because you only want to reset away the merge, not actually move the branch. (HEAD hasn't been updated yet, since the merge failed)




## TROUBLESHOOTING:
---

### Resolving merge conflicts

  **CAUSE:** Two branches have changed the same part of the same file, and then those branches are merged together. e.g. if you make a change on a particular line in a file, and your colleague working in a repository makes a change on the exact same line, a merge conflict occurs. Git has trouble understanding which change should be used, so it asks you to help out.

  In the affected file, you'll notice 'conflict markers' to the affected areas. A conflict-marked area begins with ```<<<<<<<``` and ends with ```>>>>>>>```, and the two conflicting blocks themselves are divided by ```=======```.

  **REMEDY:** 
  - **Manual:** 
    1. Open the file in a text editor
    2. Delete either the block above the ```=======``, the one below it, or create a new solution altogether. *make sure that you've removed all the remaining conflict markers*
    3. Save your changes. *If you've experienced a merge conflict while syncing, you can go ahead and click "Mark Resolved."* 
    4. If the conflict occurred locally:
      a. re-stage the file with ```git add```, which also marks it as resolved
      b. commit the change


### non-fast-forward errors

  ```
$ git push origin master
# To https://github.com/user/repo.git
#  ! [rejected]        master -> master (non-fast-forward)
# error: failed to push some refs to 'https://github.com/user/repo.git'
# To prevent you from losing history, non-fast-forward updates were rejected
# Merge the remote changes (e.g. 'git pull') before pushing again.  See the
# 'Note about fast-forwards' section of 'git push --help' for details.
```

  **MEANING:** Git cannot make the change on the remote without losing commits, so it refuses the push. 
  
  **CAUSE:** Another user pushing to the same branch. 

  **REMEDY:** Fetch & merge the remote branch, *or using ```git pull``` to perform both at once*.

  >*In some cases this error is a result of destructive changes made locally by using commands like ```git commit --amend``` or ```git rebase```. While you can override the remote by adding ```--force``` to the push command, you should only do so if you are absolutely certain this is what you want to do. Force-pushes can cause issues for other users that have fetched the remote branch, and is considered bad practice. When in doubt, don't force-push.*


## REFERENCES
---
- [Git Emmersion](http://gitimmersion.com/)
- [Learn Git Branching](http://pcottle.github.io/learnGitBranching/)
- GitHubHelp
  - [Dealing with non-fast-forward errors](https://help.github.com/articles/dealing-with-non-fast-forward-errors)
  - [Fetching a remote](https://help.github.com/articles/fetching-a-remote)
  - [Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys) *(only to be used on your personal computer)*
  - [Setup](https://help.github.com/articles/set-up-git)
  - [Updating credentials from the OSX Keychain](https://help.github.com/articles/updating-credentials-from-the-osx-keychain)
  - [Using Pull Requests](https://help.github.com/articles/using-pull-requests)
  - [Why is Git always asking for my password?](https://help.github.com/articles/why-is-git-always-asking-for-my-password)
- StackOverflow
  - [Can you explain what “git reset” does in plain english?](http://stackoverflow.com/questions/2530060/can-you-explain-what-git-reset-does-in-plain-english)
  - [Git push existing repo to a new and different remote repo server?](http://stackoverflow.com/questions/5181845/git-push-existing-repo-to-a-new-and-different-remote-repo-server)
  - [Import existing source code to github](http://stackoverflow.com/questions/4658606/import-existing-source-code-to-github)
  - [Move existing, uncommited work to a new branch in Git](http://stackoverflow.com/questions/1394797/move-existing-uncommited-work-to-a-new-branch-in-git)
  - [Visualizing branch topology](http://stackoverflow.com/questions/1838873/visualizing-branch-topology-in-git)
  - [How to change a remote repository URI using Git?](http://stackoverflow.com/questions/2432764/how-to-change-a-remote-repository-uri-using-git)