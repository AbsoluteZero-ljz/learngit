# git入门
## git工作流程
![](https://gitee.com/AbsoluteZero-ljz/BlogImageLibs/raw/master/img/20210102172351.png)

![](./image/2021-01-02-17-29-09.png)

## git配置
> \$ git config --global user.name "Your Name"
> \$ git config --global user.email "email@example.com"


## 常用命令行
1. <kbd>git init</kbd>：把当前目录变成Git可以管理的仓库
2. <kbd>git add</kbd>：把文件添加到暂存区
3. <kbd>git commit</kbd>：把暂存区内容提交到当前分支
   ```git
   git commit -m "add a new file"
   ```
4. <kbd>git status</kbd>：查看工作目录状态
5. <kbd>git diff</kbd>：查看文件差异
   > git diff比较的是工作目录中当前文件和暂存区域快照之间的差异， 也就是修改之后还没有暂存起来的变化内容。若要查看已暂存的将要添加到下次提交里的内容，可以用 git diff --cached 命令。

   > 请注意，git diff 本身只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。 所以有时候你一下子暂存了所有更新过的文件后，运行 git diff 后却什么也没有，就是这个原因。

   > gitdiff HEAD -- filename：工作区和库(HEAD)之间差异

   > git add的反向命令git checkout
   > git commit的反向命令git reset HEAD

6. <kbd>git log</kbd>：查看commit记录
   注：
   - 记录中`HEAD`表示当前版本
   - 如果要表示上一个版本，可以使用`HEAD^`。同理上上一个版本，可以使用`HEAD^^`表示。
   - 如果要表示往上10个版本，10个`^`不但不方便书写，也不方便查看。往上10个版本，可以使用`HEAD~10`表示。
   - `git log --pretty=oneline` 查看简要信息
7. <kbd>git reflog</kbd>：查看包含git reset回退到某一版本的记录，可用于查看回退版本之前的commit id。
8. <kbd>git reset --hard <></kbd>：回到某一版本
   ```git
   git reset --hard HEAD^    # 回退上一版本
   ```
   ```git
   git reset --hard <commit id>    # 回退到某一指定版本
   ```
9. <kbd>git checkout -- file</kbd>：让这个文件回到最近一次git commit或git add时的状态。
    注：新版本使用git restore代替
10. <kbd>git reset HEAD file</kbd>：撤销暂存区的修改，与HEAD保持一致
    注：新版本使用git restore --staged代替
11. <kbd>git remote add</kbd>：添加远程库。适用于先有本地库，后有远程库。
    例：
    `git remote add origin git@server-name:path/repo-name.git`
    `origin`：关联远程库时给远程库所指定的名字，origin默认习惯命名。
12. <kbd>git remote -v</kbd>：查看远程库信息
13. <kbd>git remote rm</kbd>：删除远程库
    例：`git remote rm origin`
14. <kbd>git clone</kbd>：从远程库克隆。适用于先有远程库。
15. <kbd>git branch dev</kbd>：创建dev分支
16. <kbd>git branch</kbd>：查看当前存在哪些分支
17. <kbd>git switch -c dev</kbd>：创建dev分支，并切换到dev分支。
    注：
    - <kbd>git switch</kbd>命令加上`-c`参数表示创建并切换。上述命令相当于下面两条命令。
      > git branch dev     创建dev分支
      > git switch dev     切换到dev分支
    - 旧版本使用 `git checkout -b dev` 表示创建dev分支，并切换到dev分支。
    - 旧版本使用 `git checkout dev` 表示切换到dev分支。
18. <kbd>git merge</kbd>：合并指定分支到当前分支。
19. <kbd>git branch -d</kbd>：删除指定分支
20. <kbd>git stash</kbd>：把当前工作现场“储藏”起来，等以后恢复现场后继续工作
21. <kbd>git stash list</kbd>：查看被“储藏”的工作现场
22. <kbd>git stash apply</kbd>：恢复现场，但是stash内容不删除
23. <kbd>git stash drop</kbd>：删除stash内容
24. <kbd>git stash pop</kbd>：恢复现场，并删除stash内容
    注：
    可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash
25. <kbd>git push</kbd>：推送分支
    例：
    `git push origin master`
    `git push -u origin master`
    注：
    第一次推送master分支时，加上-u参数，Git不但会把本地的master分支内容推送到远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
26. <kbd>git branch --set-upstream-to=origin/dev dev</kbd>：指定本地`dev`分支与远程`origin/dev`分支的链接
27. <kbd>git pull</kbd>：抓取分支
28. <kbd>git rebase</kbd>：把本地未push的分叉提交历史整理成直线
29. <kbd>git tag \<tagname></kbd>：打一个新的标签。默认标签是打在最新提交的commit上。
30. <kbd>git tag \<name> \<commit id></kbd>：打一个新的标签。指定某一commit。
31. <kbd>git tag -a \<tagname> -m "massage" \<commit id></kbd>：创建带有说明的标签。`-a`指定标签名，`-m`指定说明信息。
32. <kbd>git tag</kbd>：查看所有标签。
33. <kbd>git show \<tagname></kbd>：查看标签信息
34. <kbd>git tag -d \<tagname></kbd>：删除本地某一标签
35. <kbd>git push origin \<tagname></kbd>：推送某一标签到远程
36. <kbd>git push origin --tags</kbd>：推送全部尚未推送到远程的本地标签
37. <kbd>git push origin :refs/tags/\<tagname></kbd>：删除一个远程标签
38. 忽略某些文件时，需要编写`.gitignore`。参考[https://github.com/github/gitignore](https://github.com/github/gitignore)
39. `.gitignore`文件本身要放到版本库里
40. 把指定文件排除在`.gitignore`规则外的写法就是`!`+文件名。例：`!.gitignore`
41. <kbd>git check-ignore -v \<file></kbd>：检查指定文件匹配到哪一个忽略规则。
42. 配置别名。例：`git config --global alias.ci commit`