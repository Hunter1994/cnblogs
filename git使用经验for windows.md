<p><a href="#a1"><strong>一、本地同步fork的最新版本</strong></a></p>
<p><a href="#a2"><strong>二、git命令</strong></a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、本地同步fork的最新版本</span></strong></span></p>
<p>①打开Git CMD工具，进入git的主目录</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201804/741594-20180404133713534-414849831.png" alt="" /></p>
<p>②使用&nbsp;<span class="cnblogs_code">git remote -v</span>&nbsp;查看fork的远程仓库地址</p>
<p>&nbsp;<img src="https://images2018.cnblogs.com/blog/741594/201804/741594-20180404133730392-299893167.png" alt="" /></p>
<p>origin：为我fork的远程仓储的名字</p>
<p>paySource：为原项目github地址（需要使用命令&nbsp;<span class="cnblogs_code">git remote add paySource git@github.com:octocat/Spoon-Knife.git</span>&nbsp;添加进来）</p>
<p>③执行&nbsp;<span class="cnblogs_code">git fetch paySource</span>&nbsp;命令，检出paySource分支以及各自的更新</p>
<p>④切换到你的本地分支主干&nbsp;<span class="cnblogs_code">git checkout master</span>&nbsp;</p>
<p>⑤合并paySource/master分支和master分支,将原项目中的更改更新到本地分支，这样就能使你的本地的fork分支与原项目保持同步，命令:&nbsp;<span class="cnblogs_code">git merge paySource/master</span>&nbsp;</p>
<p>⑥执行&nbsp;<span class="cnblogs_code">git push</span>&nbsp;将本地分支的修改推送到远端fork的项目</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、git命令</span></strong></span></p>
<p>&nbsp;</p>
<p>设置用户名和email<br />$ git config --global user.name "Your Name"<br />$ git config --global user.email "email@example.com"</p>
<p>-------------------<br />将目录变成Git可以管理的仓库<br />$ git init<br />-------------------<br />把文件添加到版本库<br />$ git add readme.txt<br />-------------------<br />把文件提交到仓库<br />$ git commit -m "wrote a readme file"<br />-------------------<br />status与diff<br />要随时掌握工作区的状态，使用git status命令。<br />如果git status告诉你有文件被修改过，用git diff可以查看修改内容</p>
<p>-------------------<br />查看状态<br />$ git log <br />-------------------<br />回退上一个版本，或者将暂存区修改回退到工作区<br />$ git reset --hard HEAD^ <br />-------------------<br />撤销工作区的修改<br />git checkout -- file<br />-------------------<br />生产ssh<br />$ ssh-keygen -t rsa -C "youremail@example.com"<br />-------------------<br />现有本地库，后有远程仓库<br />添加远程仓储<br />git remote add origin git@github.com:michaelliao/learngit.git<br />将本地库所有内容推送到远程库上，并将本地master和远程maste关联<br />git push -u origin master<br />-------------------<br />最好是先创建远程库，然后从远程库克隆<br />git clone git@github.com:michaelliao/gitskills.git<br />-------------------<br />创建与合并分支<br />$ git checkout -b dev	创建并切换分支<br />$ git branch dev	创建分支<br />$ git checkout dev	切换分支<br />$ git branch	查看分支<br />$ git merge dev	合并dev分支（需要切换到master分支）<br />$ git branch -d dev	删除分支<br />$ git branch -D &lt;name&gt;强行删除分支<br />-------------------<br />将未提交的工作区变干净（把当前工作现场&ldquo;储藏&rdquo;起来）<br />$ git stash		储藏<br />$ git stash list	查看储藏哪里了<br />$ git stash pop	恢复储藏的内容并删除储藏备份<br />$git stash drop	删除储藏备份<br />-------------------<br />多人协作<br />$ git remote	查看远程仓库信息<br />$ git push origin master	推送分支<br />$ git checkout -b dev origin/dev	创建本地dev分支获取远程dev分支<br />$ git branch --set-upstream-to=origin/dev dev	设置dev和origin/dev的链接<br />-------------------<br />$ git tag v1.0	创建标签<br />$ git tag		查看所有标签<br />$ git tag -d v0.1	删除标签</p>
<p>&nbsp;</p>