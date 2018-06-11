git learn
1.git init
当前目录变成Git可以管理的仓库
会生成.Git目录，git用于跟踪管理版本库

2.添加文件到版本库
所有版本控制系统都是跟踪文本文件的改动【txt文件，网页，程序代码等】可以
   显示出每一次的改动
  但二进制文件，比如图片，音乐文件，没有办法跟踪文件的变化
  Microsoft的word文件是二进制文件，尽量以纯文本形式保存文字	
  常用文本的编码：中文GBK，日文Shift_JIS
  建议同一使用UTF-8编码
  【不使用记事本编辑文本，记事本保存UTF-8文件会在文件开头加0xefbbbf(十六进制)】
  
   git add 需要添加的文件
   git commit -m <message> 提交文件
 
 3.修改提交
   git status ：修改完文件后，查看当前版本库的状态；提交后再次查看是否已经提交完了
   
   git diff ：查看修改的内容
   
 4.版本回退
   git log ：显示从最近到最远的提交日志
   git log --pretty=oneline ：简化log显示的内容
   git reflog ：记录每一次命令
   
   版本：
   HEAD   表示当前版本
   HEAD^  表示上一个版本
   HEAD^^ 表示上上一个版本
   以此类推
   HEAD~100 上100个版本
   
   git reset --hard HEAD^ ：回退到上一个版本
   git reset --hard commitId 部分 可以回退到相应的版本
   
   5.工作区和暂存区
    工作区：编辑文件所在目录
	版本库：工作区的.git文件夹，是git的版本库
	        版本库包含： stage（index）：暂存区
			             master（Git自动创建的第一个分支master，以及指向master的指针HEAD）
	git add操作，就是把文件添加到暂存区：stage
	git commit操作，把暂存区所有内容提交到当前分支，此时暂存区就是干净的了
	
	6.管理修改
	git 管理的是每次的修改
	如果第一次修改，git add将修改提交到暂存区；接着继续修改文件，接着用
	  git commit 只会将第一次add的修改提交到分支，第二次修改的部分因为没有add到
	  暂存区，所以不会被commit到分支上
	  
	7.撤销修改
	git checkout -- 文件 ：撤销工作区的修改
	如果修改后没有add到缓存区，那么撤销的就是当前修改的部分
	如果add到缓存区后又进行了修改，撤销的是add进缓存区后修改的部分
	总之，撤销的是工作区的修改
	
	git reset HEAD <file> 撤销缓存区的修改，清空缓存区数据
	HEAD 表示最新的版本
	此时工作区是有修改部分，缓存区没有
	
	8.删除
	
	
9.远程仓库	
10.分支管理
   1.创建dev分支，并切换到dev分支
     git checkout -b dev 
	     撤回工作区编辑后未提交，会撤回工作区的修改，使其保持和master一致
     
     git branch 查看当前所有分支，会在当前分支前出现*
   