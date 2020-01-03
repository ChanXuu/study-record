本地仓库操作

全局配置

git config --global user.name '用户名'

git config --global user.email '邮箱' 

创建仓库

1. 先创建个空文件夹
2. Git仓库初始化
   - 命令:git init
3. Git常用命令
   - git status --查看当前状态
   - git add '文件名'--添加到缓存区(可以添加一个,也可以添加多个文件)
     - git add '文件名' (单个文件)
     - git add '文件名1' '文件名2' (多个文件)
     - git add . (当前目录下)
   - git commit -m '注释内容' --提交至本地版本库
4. 版本回退
   1. 查看版本,确定回到的版本
      - git log
      - git log --pretty=oneline
   2. 回退操作
      - git reset --hard 版本id  回退版本
      - git reflog  获取没回退之前的版本id

远程仓库操作

    1.  在github先创建仓库

2. 提交方式
	1.  使用https
      	1.  复制仓库的https地址
      	2.  使用命令 git clone https地址
      	3.  开始操作(提交暂存区,提交本地仓库,提交线上仓库,拉取线上仓库)
      	4.  首次提交,需要配置权限,修改.git/config文件,将里面的 url的https:// 后里添加账号和密码和@符号,类似:https:abc:123@github.com/.....
      	5.  git push  提交到线上仓库
      	6.  git pull 拉取线上仓库
	2.  使用ssh协议
      	1.  先生成本地电脑的ssh秘钥
            	1.  ssh-keygen -t rsa -C '邮箱'
            	2.  把生成的秘钥保存到github中
            	3.  后续操作与https一样,先clone,然后操作

分支管理

相关指令: 

1. 查看分支 : git branch
2. 创建分支: git branch 分支名
3. 切换分支: git checkout 分支名
4. 删除分支: git branch -d 分支名 (删除前要退出需要删除的分支)
5. 合并分支: git merge 被合并的分支名

忽略文件

1. 新建一个叫.gitignore文件,该文件用来声明忽略文件或不忽略文件的规则,规则对当前目录和目录的子目录生效
2. 常见规则
       ./文件夹名/ 	 	过滤整个文件夹
       *.zip   	过滤所有.zip文件
       /文件夹名/文件名 	过滤某个具体文件
       !index.php 	不过滤某个具体文件
   
