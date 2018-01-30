# git-tutor
my git tutor

如何有效地使用git进行代码管理

Git优势: 分布式源码管理，代码库就存在于本地, 速度更快

一、 获取版本库
git clone path

二、 设置 用户名和密码
git config --global user.name "leon"
git config --global user.email "leon@xxx.com"

三、 生成本机公钥
ssh-keygen -t rsa -C "leon@xxx.com"

四、忽略不纳入版本库的文件或目录
1. 在项目根目录，新建.gitignore 文件，并增加忽略的文件或目录 (只作用于当前项目)
2. 设置全局忽略文件 git config --global core.excludesfile ~/.gitignore (作用于所有项目)

五. 提交代码

1. 将工作目录所有修改或增加的文件提交到版本库
git add . 将工作目录修改加入暂存区
git commit  提交暂存区的代码，并填写提交记录

2. 提交部分代码到暂存区
git add -- filepath

3. 将暂存区代码撤销到工作目录 (放弃提交 - 可逆)
git reset HEAD filepath

4. 撤销工作目录的文件修改 （放弃修改 - 不可逆)
git checkout -- filepath

5. 撤销工作目录以及暂存区的修改(同时作用于暂存区以及工作目录 - 不可逆)
git reset --hard HEAD

5. 保存工作目录的修改 ( 保存修改，可随时恢复）
git stash list  查看所有保存的修改列表
git stash save 'description' 保存当前的修改并添加说明

6. 恢复保存的修改记录 (保持工作目录为clean状态，并确认在正确的分支)
git stash apply 恢复最近一次的保存
git stash apply stash@{0}  指定某次的保存进行代码恢复

git stash pop  恢复并删除最近一次的保存
git stash pop stash@{0} 恢复并删除某一次的保存记录 

7. 删除保存记录
git stash drop stash@{0} 删除某一次的保存记录
git stash clear  删除所有暂存记录

六、更新和共享代码

1. 设置版本库地址
git remote -v  查看所有版本库地址
git remote add main url  增加版本库地址
git remote set-url origin newUrl 修改版本库地址

2. 从主库更新代码
git fetch main master 从主库拉取master分支最新代码 
git merge main/master 合并拉取后的代码到当前分支

3. 将提交推送到自己的版本库
git push origin master 将master分支上的提交推送到远程自己的版本库

4. 两个人如何共享代码
git push origin myBranch 将自己的私有分支推送到远程仓库

git fetch repName myBranch 拉取他人的私有分支
git checkout -b myBranch repName/myBranch   基于他人私有分支新建分支
git merge repName/myBranch   合并他人的分支到自己当前分支

git push origin :myBranch 删除不再需要的远程私有分支
git branch -d myBranch 删除本地分支

5. 解决冲突 

冲突发生在多人修改文件同一部分, 从主库更新文件到本地时
第一步：冲突时git会提示哪些文件冲突了，打开相应的文件，进行手动解决，删除哪些，保留哪些。
对于前端dist目录下的文件可以进行重新编译即可.
第二步:  解决冲突后，利用git add 命令加入暂存区，然后利用git commit进行提交，会自动生成提交记录
第三步： 如果需要推送代码到远程仓库，利用git push 同步代码到远程仓库

七、同时工作多个任务, 在私有分支上工作
1.  查看分支
git branch  查看本地分支
git branch -a  查看所有分支

2.  基于某个分支建立新分支并切换到新分支
git checkout -b branchName

3. 切换分支
git checkout branchName

4. 合并私有分支到公共分支
git merge myBranch

5. 删除确定不用的分支
git branch -d branchName
git branch -D branchName   // 强制删除

八、追踪之前的提交记录 

1. git log  查看某个分支上的提交记录

2. git log -p filePath 查看某个文件的修改历史记录  

应用场景：文件某处代码是否被某人曾经修改过
3. git log -L start:end:filePath 查看某个文件的某几行的修改历史

4. git log --author='xxxx' 查看某个人的提交历史

应用场景：查找曾经做的某个功能或者问题单修改的提交记录
5. git log --grep='xxxx' 根据提交记录关键字搜索提交历史

6. git show --stat commitId 查看某次提交都修改了哪些文件

九、合并过去某一次提交到另一个分支
git cherry-pick commitId

十、撤销过去某一次提交
git revert commitId

十、文件对比
1. git diff filepath  查看某个文件工作区与暂存区的差异
2. git diff HEAD filepath 查看文件工作区与最近一次提交的差异
3. git diff --cached filepath 查看暂存区与最近一次提交的差异
4. git diff branchName filepath 当前分支与其他分支进行比较
5. git diff commitId filepath 与某一次提交进行文件比较

十一、时空旅行 (谨慎驾驶)
1. git reset --hard commitId 将代码重置到过去某一次提交

2. git reflog 查看git操作记录, 回到未来








