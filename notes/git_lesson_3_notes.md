#github
repository 代码库
纯文本内容可以直接预览
##github开源项目
几个大型开源项目的例子

 - ipython :interactive shell
 - bootstrap:
 - jquery
 - atom

理论上任何人都可以对开源项目作出贡献，而且项目维护者必须接受任何更改（即使不被合并也可以选择自己保存）
##创建github账户
###Create a GitHub account
In this lesson, you'll be sharing changes on GitHub, so you'll need a GitHub account. If you don't already have one, you can create an account by visiting [github.com](https://github.com/) and clicking "Sign up for GitHub".
When you're asked to choose a plan, you can choose a free plan, since we won't be using any of the paid features in this course.

###Set up Password Caching
Every time you send changes to GitHub via the command line, you'll need to type your password to prove that you have permission to modify the repository. This can get annoying quickly, so many people like to set up password caching, which will let you type your password once and have it auto-filled on that computer in the future. To do this, follow the instructions [here](https://help.github.com/articles/caching-your-github-password-in-git/). If you're using Windows and you followed our Git installation instructions earlier, you're using msysgit, so you can follow the instructions for msysgit.

##与github同步
需要人工选择同步的时间和版本，并非自动同步
###在github新建新的repository
不能从本地clone到github，需要建立远程代码库（remotes）
###与remote之间的沟通
- push：只要push master（某个） branch，包含在这个branch上的所有commit都会被提交
- pull

新建github repository，如果本地文件已有commit则不需要勾选readme.md

####如何将已有commit，但没有remote的github文件夹与remote相连：

- 在terminal中使用git remote发现没有remote
- git remote add [存在本地的remote名，用来指代与之相连的remote，原则上默认使用origin] [url] `git add remote origin https://github.com/vivi3nli/reflections.git`（此处udacity视频内容出错，为使用SSH，对于一个已经形成的remote，[更改url的方法](https://help.github.com/articles/changing-a-remote-s-url/)）
- git remote -v :verbose 显示这个remote的详细信息，可以用来确认url是否正确
- git push origin master 也就是把master branch上的内容push到名字为“origin”的remote上

ps：如果是直接从网上clone的repository，git自动将来源url作为remote的url

### Copy the HTTPS URL, not the SSH URL!
At 1:29, Caroline copies the URL to the repository. The video mistakenly shows the URL to use if the repository is accessed over SSH. The course assumes that the student will use HTTPS, not SSH. Please click on the HTTPS button and copy the URL that shows up for HTTPS. It will begin with https:// rather than git@github.com.

If you are interested in using SSH instead, you can follow the instructions [here](https://help.github.com/articles/generating-an-ssh-key/), but this is not recommended unless you are already familiar with SSH keys.

### Sharing your reflections
We encourage you to be bold in sharing your reflections on GitHub. If you're not happy with any of your responses, the best solution is to update that response in one or more new commits. The previous response will still be visible in the commit history, but updating your perspective over time is part of the learning process! Having a commit history that shows your updating perspective will reflect well on you, not poorly.

That said, if you've written anything in your reflections repository that you are not comfortable sharing, you can checkout the commit before you introduced that change, create a new branch at that point, and commit any other changes you are willing to share to the new branch. Then, by only pushing your new branch, you can keep the changes on your original branch private.

### 在github直接添加内容（本地没有的）
可能出现在

- 直接在github上更改
- 从其他电脑向github添加文件
- 其他人向此repository添加文件

此时只要使用`git pull origin master`就可以将本地与github同步

##Forking
直接将某人的github repository复制到我的github上，不需要先clone到电脑再push到github。即将文件从github clone到github。作用：

- github可以记录fork人数
- 直接指向来源的repository
- 更容易向创始者提交建议

Where was your commit?
Before you ran `git push`, your change should have only existed locally via `git log`. Commits will not automatically be shared to remotes - you have to manually push your branch if you want to share changes.

After you ran `git push`, your change should have existed locally and on your fork. It should not have existed on Larry's repository, which is the repository you forked. The reason you forked in the first place is because you don't have permission to change Larry's repository!

##Conflict
如果同时在本地和remote端操作，会导致同一文件出现分歧，此时可以：

- `git fetch` 能够将remote的update更新为一个新的branch，同时可以保留原有的本地branch，此时可以通过git log和git different来看有什么变化
- `git merge`

或者直接：

- `git pull`

两者效力相同

###fast-forward merges
当两个中其中一个是ancestor，一般的pull（即为merge）是将更早的标签移动到更新的标签端：
you can reach a from b, so you can do a fast-forward merge.
a：merging into
b：merging from

##Workflow
###Pull Request
- `git branch <branchname>` 新建分支
- `git checkout <branchname>` 转移到那个分支，`git checkout`是用于在不同branch或者commit之间跳转
- make change（不一定要在这一步，也可以之前做改变）
- `git add`
- `git commit`
- `git push origin <branchname>` 推送到github的是这个特定的branch，此时在github可以看到新的branch和commit所做的更改，但下一步要做一个Pull request
- 点击特定branch，选择pull request，选择想要pull（也就是merge）的repository（可以是自己的fork，也可以是最初fork来源的repository）
- 查看pull request列表，可以看到diff
- （此时合作者可以查看pull request）并且在diff处留下comment。
- 没有问题即可merge


[这道题](https://classroom.udacity.com/courses/ud775/lessons/3105028581/concepts/33282286200923#) 是一个对理解的重要挑战，主要难点在于

- `git commit`之后，曾经在staging area的内容并没有被清除，只是不再改变了。
- `git pull origin master`之后local master branch改变了，同时local repository 以及 staging area也会随之改变 Sarah accidentally says that the local master is the only thing that changes when you run git pull origin master. However, the working directory and staging area will also update when you run git pull. That's why when you run git pull, you see your files update, not just the git log output.
- `git push origin master`之后只有GitHub master branch改变了
- 一个merge Pull Request的命令是完全在GitHub上完成的，类似于Fork

###Pull Conflict
如果对方也添加了pull request时，两个pull会形成冲突

- 进行一个pull request的merge （并删除该branch）
- 此时github会提示无法自动merge，需要将所有更改先pull到本地`git pull origin master` `git checkout <branchname>` `git merge master <branchname>`
- 看到conflict，解决conflict
- 再提交一个pull request `git push origin <branchname>`（如果直接merge并push会导致团队中其他成员不能审核并得到通知）

#### Commit merging a pull request
After running git log -n 1, you should have seen output something like this:

commit bc368511c6406028c77e2631f77c4d22a5da16d0
Merge: 79fff84 23d1775
Author: cbuckey 
Date:   Tue Sep 30 18:50:28 2014 -0400

    Merge pull request #1 from cbuckey-uda/different-oil

    Change vegetable oil to canola oil
Notice that the commit message:

Indicates that a pull request was merged
Gives the number of the pull request (#1 here)
Gives the branch the pull request was merged from (cbuckey-uda/different-oil here).
Contains the title of the pull request.
GitHub automatically creates a commit message like this whenever a pull request is merged to make it easy to see pull requests in the commit history. Even when the merge is a fast-forward merge, GitHub still creates this commit.

## Fork the repository and clone your fork
Now that you've learned how to fork a repository, push changes to your fork, and make a pull request, you’re ready to contribute to the create-your-own-adventure story that you saw at the beginning of the lesson. To do this, first you should fork this repository. Then clone your fork, and make a branch to make your changes in.

Note: You could make your changes directly to the master branch in your fork, but when contributing to a public repository, it’s standard practice to make the changes in a non-master branch within the fork. This way, you can easily keep your master branch up-to-date with master of the original repository, and merge changes from master into your branch when you are ready.

Note for Windows Users: The story has grown so large that it exceeds Windows' path length limit. If you encounter an error when cloning you can work around it by modifying a configuration setting. Run this command in git bash: git config --system core.longpaths true.

### Make a change to the story
Next, you should actually make a change to the story. For instructions on how to do so, please read the README in the create-your-own-adventure repository.

### Make a pull request
Next, you should make a pull request containing your changes to the original repository. To do this, click the "pull request" button from your branch like you did before, but this time, leave the original repository as the base.

### Ask for your pull request to be merged
You don't have permission to modify this repository, so you'll need someone at Udacity to merge your pull request. Our helpful bot Casey may be able to merge your pull request automatically. To have your pull request automatically merged, you'll need to follow the guidelines in the README of the repository, and in addition you won't be able to delete or modify lines. That restriction on deletions is because Casey doesn't want to merge a request that accidentally deletes part of the story, and she can't tell the difference between an accidental deletion and an intentional modification. To request auto-merging, leave a comment on the pull request containing "@casey-collab". For example "Please review this, @casey-collab". Make sure to leave the comment on the "Conversation" tab of the pull request, not the "Files changed" tab.

There are some valid pull requests that Casey won't be able to merge. For example, she won't accept a pull request that fixes a typo, since that modifies a line. If you'd like to make a pull request Casey can't merge, feel free to do so, and someone from Udacity will merge the pull request if we have time. However, we can't guarantee a response to these pull requests.

### If needed, update your pull request
If someone merges your pull request or leaves a comment, GitHub will email you and let you know. If you're asked to make some changes, push those changes to your fork to update the pull request. Make sure you let the reviewer know that they should take another look!

If your pull request would result in a merge conflict, and you're not sure how to resolve it, see the next video for instructions.

##向原始repository合并时出现的conflict
original repository has changed and your remote origin(fork) is not updated

- 此时需要增加一个remote指向最初的repository，可以命名为upstream
- 添加 `git pull upstream/master`
- merge 
- push

