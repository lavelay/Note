##  版本控制

常用的版本控制系统

- cvs / svn : 集中式版本控制系统
- git : 分布式版本控制系统

SVN弊端

- 需要连网才能回退或查看历史版本信息
- 中央服务器坏了，一切over
- 所有的上传和下载都是基于文件传输方式，速度慢

git 优势

- 无需连网也能记录和查看历史版本信息
- 无需过多依赖中央仓库，每个人本地也有全部的信息
- 向中央仓库传输内容依托的是文件流传输，速度比svn快很多




## 常用的DOS命令

```bash
ping www.baidu.com -t     测试网速
ctrl+c           结束当前正在运行的操作
exit             退出当前窗口
ipconfig -all    查看当前电脑的物理地址/IP地址/子网掩码/DNS等信息
cls              清屏
cd      	     进入到指定的文件目录（window电脑要先进入到对应的磁盘）
dir     		 查看当前目录下所有的文件
copy con xxx.xx  创建文件并且给文件中输入内容，完成后用ctrl+c结束
rm xxx.xx  	  	 删除文件
rmdir xx      	 删除文件夹
```

## gitbash 常用命令

```bash
$ mkdir 目录1 目录2 ..     # 新建目录
$ cd dir          # 进入目录
$ cd ..             # 返回上级目录
$ rm -rf 目录名1 目录名1 .. # 删除目录
$ touch 文件名1 文件名2 ..  # 新建文件
$ rm 文件1 文件2 ..      # 删除文件
$ cat 文件名         # 查看文件内容
$ less 文件名        # 查看文件内容 需要按q退出
$ vi 文件名        # 创建并进入文件编辑模式
$ i             # 进入插入编辑模式 
# esc退出插入编辑模式
$ :q            # 退出编辑模式 但是不保存
$ :wq           # 保存并退出编辑模式
$ :q!           # 强制退出但不保存编辑模式
```

## git命令

```bash
$ git config --global user.email "you@example.com"
$ git config --global user.name "yourname"
$ git init	           # 生成一个隐藏文件夹“.git”（暂存区和历史区的部分信息在，不可删除）
$ git add xxx	       # 把某一个文件提交到暂存区
$ git add .			   # 把当前仓库中所有文件提交到暂存区
$ git add -A 		   # 把当前仓库中所有文件提交到暂存区
$ git status		   # 查看文件状态（红色代表在工作区，绿色是在暂存区，没东西说明已提交到历史区）
$ git commit -m'描述'	  # 把暂存区内容提交到历史区
$ git log
$ git reflog
$ git log --oneline     # 查看提交的简略信息
$ git reset --hard 版本号   # 版本穿梭，回退到某个版本

$ git branch                # 列出所有本地分支
$ git branch 分支名称    	 # 新建一个分支
$ git checkout 分支名称 	 # 切换到指定分支
$ git checkout -b 分支名称	 # 新建分支并切换到该分支 （相当于同时进行前面两步操作）
$ git branch -d 分支名称  	 # 删除分支 

$ git merge 分支名           # 把指定的分支中的代码合并到当前分支

$ git clone 地址			  # 将远程仓库的文件克隆下来
...编辑过后
$ git pull 				   # 推送之前最好从远程仓库拉取最新的代码
$ git push				   # 推送到远程github
```



## npm

```powershell
$ npm install xxx	把模块安装在当前项目中
$ npm install xxx -g	把模块安装在全局环境中
$ npm i xxx@1.0.0	安装指定版本号的模块
$ npm view xxx versions > xxx.version.json	查看某个模块的版本信息（输出到指定JSON文件中）
$ npm init -y	初始化当前项目的配置依赖清单
$ npm i xxx --save	把模块保存在清单生产依赖中
$ npm i xxx --save-dev	把模块保存在清单开发依赖中
$ npm install	跑环境，按照清单安装所需的模块
$ npm root -g	查看全局安装模块的目录
$ npm uninstall xxx
$ npm uninstall xxx -g	卸载安装过的模块
```



