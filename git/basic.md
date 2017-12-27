

#git init 
#创建新仓库   

#git clone /path/to/repository 
#创建本地仓库的克隆版本  


#git clone username@host:/path/to/repository 
#创建远端服务器上的仓库的克隆版本  


#git add <filename>  
#将工作区内的某文件修改存到暂存区


#git add .  
#将工作区内所有修改存到暂存区

#git commit -m "代码提交信息"   
#将暂存区内代码提交到本地仓库

#git push origin master     
#将本地仓库代码提交到远程仓库

#git remote add origin <server>
#还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器.

#git checkout -b feature_x
#创建一个叫做“feature_x”的分支，并切换过去

#git checkout master
#切换回主分支

#git branch -d feature_x
#删除feature_x分支

#git push origin branchName
#将本地仓库代码推送到远端仓库，才能为他人所见

#git pull
#更新你的本地仓库至最新改动

#git merge branchName
#合并其他分支到你的当前分支

#git merge branchName
#合并其他分支到你的当前分支

#git diff <source_branch> <target_branch>
#查看两个分支之间的差异...1b2e1d63ff 是你想要标记的提交 ID 的前 10 位字符

#git tag 1.0.0 1b2e1d63ff
#创建一个叫做 1.0.0 的标签

#git log 
#获取提交ID,了解本地仓库的本地纪录

#git log --author=bob
# 只看某一个人的提交记录

#看看哪些文件改变了: 
#git log --name-status


#使用HEAD中的最新内容替换掉工作目录中的文件（暂存区的改动不受影响）
#git checkout -- <filename>

#丢弃本地的所有改动与提交
#git fetch origin
#git reset --hard origin/master



# 删除工作区文件，并且将这次删除放入暂存区
# git rm file1 file2 ...

# 改名文件，并且将这个改名放入暂存区
# git mv file-original file-renamed

# 提交时显示所有diff信息
# git commit -v

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
# git commit --amend -m [message]

# 列出所有远程分支
# git branch -r

# 列出所有本地分支和远程分支
# git branch -a

# 切换到上一个分支
# git checkout -

# 列出所有tag
# git tag

# 显示有变更的文件
# git status


# 显示暂存区和工作区的差异
# git diff


# 显示暂存区和上一个commit的差异
# git diff --cached [file]


# 显示工作区与当前分支最新commit之间的差异
# git diff HEAD

# 显示今天你写了多少行代码
# git diff --shortstat "@{0 day ago}"

# 显示当前分支的最近几次提交
# git reflog


















