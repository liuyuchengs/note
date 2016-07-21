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
  + checkout -- <fileName>：撤销还未添加到暂存区的修改

        $ git checkout -- readme.md
  + reset HEAD <fileName>：撤销添加到暂存区的修改，HEAD表示当前分支最新的版本(已经commit的)

        $ git reset HEAD readme.md
