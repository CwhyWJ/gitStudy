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
	 
	 git add git commit在dev分支上的修改后，git checkout master 切换回master分支
	 发现dev上修改的文件master上没有修改
	 
   2.合并分支
     git merge dev : 合并指定的dev分支当当前的mastter分支
	 Fast-forward 信息表明此次合并为“快进模式”，即直接把master只想dev当前的提交
     合并完了后，删除dev分支：
	 git branch -d dev
   
   分支管理策略：理解git分支的结构，merge，擦黄建分支工作
	 
	 
   3.解决冲突
     解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。   
	 
   4.分支管理策略
		必须commit才可以切换分支，否则会被覆盖
   
   5.bug分支
      【应用情景：当前dev分支正在开发，来了一个bug001，
	    理所当然想建立bug001分支对应bug，
		但是当前的dev开发正在进行不可提交（需要commit才可以切换分支）
		】
		Git的stash功能：将当前工作现场储藏起来
		git stash  后查看工作区，干净
		切换到建立新分支的分支上，建立新分支修改bug
		修改bug完成，提交到分支上
		切回创建新分支的分支上，比如master，merge合并分支，删除bug分支
		回dev分支干活：
		git checkout dev
		git stash list:查看之前存储工作现场的位置
		回复工作现场：|--方法一：git stash apply恢复后stash内容没有删除，用git stash drop 删除bug分支
		              |--方法二：git stash pop 恢复同时删除stash内容
		
		多次stash，恢复的时候就恢复指定的stash
		git stash apply stash@{0}

   6.Feature分支
        【git checkout -b mybranch 创建的新分支的基础是工作区还是缓存区？】 
		  实证：在过去没有add的记录在新分支中出现，所以基础是工作区？！】
		【再问：这样回到原先分支要合并feature分支时候，merge合并的应该是
		  两个缓存区的代码，那么当前分支的本地代码（之前未提交但是被新建到新分支的代码）可能和merge后的代码有冲突】
		    |--新分支没有修改基础代码的情况：merge到父节点时，工作区显示没有需要提交的记录
			|--新分支修改了原先的代码，
			
		创建新分支：s元分支没有add其工作区代码，新分支中有这部分没有add的代码，此时删除原先代码编辑新代码，提交
	    元分支merge新分支，工作区代码丢失，没有出现冲突
		创建新分支：元分支代码分别在  缓存区stage，master 上时，合并分支有没有影响？
		
		【应用情景：新功能开发，为不破坏当前dev分支新建分支（可能新功能后来还有变动）】
        git chheckout -b feature-vulcan
		
		
         		
	【git fetch : 会把远程服务器上的所有更新都拉取下来
	  git pull  ：远程分支上的代码拉取并合并到本地
	  git checkout -b new_branch origin/new_branch  拉去特定远程分支到本地（本地没有）
	 】	
	 7.多人协作

	   当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。
       git remote 查看远程库信息 
	   git remote -v
	       返回fetch:抓取分支 push:推送分支
		   
		   
		   
		git push 时出现错误，显示远程分支与自己提交部分有冲突
		git pull 获取远程分支新代码并merge时出现错误，打开文件解决错误   
	   git push origin master 推送本地master到远程
	   
	   
	   git 创建分支 分支的基础不是当前所属分支的master？
	   
	   
