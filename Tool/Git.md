+ 工作区和版本库
  + 工作区：自己工作的文件及目录
  + 版本库：版本控制信息，建立在工作区内的.git隐藏文件中
  + stage/index文件：暂存区，git add把文件修改添加到该暂存区
  + head文件：分支，git commit把文件提交到当前分支文件中

	  	//文件提交流程
	  	文件修改->(git add)->暂存区->(git commit)->分支文件中->(git push)->Git Server
+ 管理修改
  + add <fileName>/add -A：提交指定文件的修改或者提交所有文件的修改到暂存区

	  	$ git add readme.md
	  	$ git add -A
  + commit -m<message>：将暂存区的文件全部提交到分支文件中

	  	$ git commit -m"add readme.md"
+ 撤销修改
  + checkout -- <fileName>：撤销还未添加到暂存区的修改和删除,将文件保持与当前分支最新版本一致

	  	$ git checkout -- readme.md
  + reset HEAD <fileName>：撤销添加到暂存区的修改(删除无法恢复)，HEAD表示当前分支最新的版本(已经commit的)

	  	$ git reset HEAD readme.md
+ 版本回退
  + log：查看历史版本信息

	  	$ git log
  + reset --hard <version>：切换到指定版本

	  	$ git reset --hard ff0b02e5056378c7ec2b2af89b643857d6ac8a13
  + reset --hard HEAD^：跳转到上一个版本

	  	$ git reset --hard HEAD^; //上一个版本
	  	$ git reset --hard HEAD^^; //上两个版本
+ 远程仓库
  + 配置ssh：先使用gui brash生成私钥和公钥，然后将公钥内容添加进个人信息中

		// 生成密钥
		$ ssh-keygen -t rsa -C "gudujianjsk@gmail.com"
		// 将id_rsa.pub文件中公钥添加进账户信息
  + clone ：克隆现有的远程仓库

  		$ git clone git@github.com:liuyuchengs/note.git
