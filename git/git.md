
# git note
参考链接<https://www.liaoxuefeng.com/wiki/896043488029600>

## 本地仓库操作
* git config --global user.name "my_name" 配置名字
* git config --global user.email "my_email@test.com" 配置email
* git init 初始化（空目录下执行）
* git add README.md 加入暂存区 
* git commit -m "first commit" 本地提交
* git status 查看状态
* git diff 查看工作区文件修改内容
* git log 查看非删除的commit记录(--graph图方式查看)
* git reflog 查看所有分支所有操作记录
* git reset --hard commit_id 会退到某个指定版本号(HEAD^上个版本)
* git checkout -- file_name 丢弃某个文件在工作区的修改
* git checkout -- 还原工作区所有文件
* git reset HEAD file_name 丢弃某个文件工作区和暂存区修改
* git rm file_name 删除文件
* git checkout -b dev 创建dev分支并切换到dev分支
* git branch dev 创建dev分支
* git checkout dev 切换到dev分支
* git checkout -b issue-110 新建bug分支
* git branch 列出所有分支，*表示当前分支
* git merge dev 合并dev到当前分支(一般是合并到master)
* git merge --no-ff -m "tips" dev 哟功能非fast forward方式合并(推荐)
* git branch -d dev 删除dev分支(如果dev分支未合并不可删除)
* git stash 临时保存工作区和暂存区修改
* git stash list 列出临时保存到数据
* git stash pop 弹出临时保存数据(使用并删除保存)
* git stash apply 使用临时保存数据
* git stash drop 删除临时保存数据
* git stash apply stash@{0} 使用某份临时保存数据
* git branch -D feature 强制删除本地库feature分支
* git log --graph --pretty=oneline --abbrev-commit 查看日志
* git log --pretty=oneline --abbrev-commit 查看日志
* git rebase 变基，使日志信息变成一条线，简化查看提交变化
* git tag v1.0 打tag
* git tag 查看所有tag
* git tag v1.1 f12d663 指定办不好打tag
* git show v1.1 查看tag具体信息
* git tag -a v0.1 -m "version tips" 8848cbd 指定版本名和指定注释
* git tag -d v1.0 删除tag
* git push origin v1.0 推送tag到远程仓库
* git push origin --tags 推送所有tag到远程仓库
* git push origin :refs/tags/v1.0 删除远程tag(需要先删除本地tag)

## 远程仓库相关操作
* git remote add origin git@github.com:my_name/rep_name.git 设置远程仓库
* git push -u origin master 推送到远程仓库（-u设置后可以直接git push）
* git clone git@github.com:name/rep_name.git 克隆仓库
* git remote 查看远程仓库(加-v更详细)
* git push origin dev 推送到dev远程仓库
* git branch --set-upstream-to=origin/dev dev 设置dev和origin/dev链接(no tracking infomation)
* git fetch 从远程仓库拉取数据
* git pull 从远程仓库拉取数据并合并
* git branch 查看本地所有分支(-a查看所有 -r查看远程所有)
* git status 查看当前状态
* git checkout -b dev 建立一个新的本地分支dev
* git branch -D develop 删除本地库develop
* git remote show origin 显示缘商城哭origin里的资源

## 克隆支持协议
* https
* ssh
* git 

## 创建github远程仓库登陆key保存并设置免密码
* 生成key
ssh-keygen -t rsa -C "my_mail@test.com"
根据提示创建id_rsa名字的key并设置密码
创建后移动到～/./ssh/目录
* 复制公钥纸贴到github网站上设置的SSH Keys
* MacOs Sierra高版本添加agent
修改 ~/.ssh/config
Host * 
    AddKeysToAgent yes
    UseKeychain yes
    IdentifyFile ~/.ssh/id_rsa
* 启动ssh-agent并添加ssh key
eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/id_rsa

## 其他
* pull request 需要先克隆到自己仓库，后再pull
* git remote add 可以加多个远程仓库
* gitignore参考<https://github.com/github/gitignore>
* 仓库config路径。/git/config

## 配置别名
* git config --global alias.co checkout 配置别名
* git config --global alias.last 'log -l' 配置别名
* git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

