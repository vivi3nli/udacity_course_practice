#How to manage a git repository within another repository?
2017-1-4
如何在一个git文件夹下包含其他路径的git文件夹

问题描述：我的2017新年愿望是：每天都能在github上更新文件，我1月1日晚上将我现在正在学习的udacity git课程文件夹push到了github上，但问题是这里面的三个文件都是位于udacity的git上的，也就是说是其他路径下的git文件夹，所以从github上查看，只能看到这三个文件夹的名字，但不能操作和追踪这些文件。针对此问题进行搜索。

##my attempt
tried to `git remote add [url] github`
after that, use `git remote -v`
	github	https://github.com/vivi3nli/udacity_course_practice.git (fetch)
	github	https://github.com/vivi3nli/udacity_course_practice.git (push)
	origin	https://github.com/udacity/pappu-pakia.git (fetch)
	origin	https://github.com/udacity/pappu-pakia.git (push)
and don't know what can be done next, cause when I do `git status` it is 
	On branch master
	Your branch is up-to-date with 'origin/master'.
	nothing to commit, working tree clean
cause at this time 
##remove all the ./git (brutal)
##use git submodule 子模块
###add as a submodule
use `git submodule add` like this:
`$ git submodule add [url] [name]`
