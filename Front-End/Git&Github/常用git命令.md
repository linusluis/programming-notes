## 1、公司提交代码流程

1. `git clone SSH地址`：只在本地没有项目文件的时候使用

2. `cd 文件夹名称`：进入项目文件

3. `git branch -a`：查看所有分支，包括本地分支（绿色为本地分支，红色为远程分支）

4. `git checkout -b dev origin/dev`：在本地新建dev分支，关联远程origin/dev分支，并切换到本地的dev分支进行开发。

5. `git add .`：添加到暂存区

6. `git commit -m 描述`：添加到本地仓库

7. `git pull origin main:本地要合并的分支名称`：拉取远程更新

8. `git push origin dev` 推送到远程dev分支





推送到远程分支的其他方式

>1. 指定分支名称，无所谓是否关联
>
>git push origin 本地分支名称:远程分支名称

>2. 同名分支关联,如果远程没有该分支，则创建
>
>git push --set-upstream origin 分支名称

>3. 通用分支关联，后续提交，只需要git push origin即可
>
>git push --set-upstream origin 本地分支:远程分支



关联分支的方式

>通用分支关联，此操作仅关联，不提交
>
>git branch --set-upstream-to=origin/远程分支名称 本地分支名称



拉取的一些命令

>将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并
>
>git pull origin master:brantest
>
>如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
>
>git pull origin master