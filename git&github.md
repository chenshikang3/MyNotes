***www.git-scm.com***

#### CMD常用命令行

- cls：清屏

- dir：显示当前路径下的文件

- mkdir：新建文件

  ```
  mkdir d:\GAME\test_b #在d:\GAME\中创建子目录test_b
  ```

- rename：重命名文件

  ```
  rename d:\GAME\test_b\test.txt dashabi.txt
  ```

#### Unix常用命令行（Git Bash）

- clear：清屏或者==***ctrl+l***==

- rm -rf [path/filename]：递归删除该路径下的所有文件

- pwd：当前目录

- ls：列出当前目录下的所有文件

- ls -a：显示隐藏文件

- touch：新建文件

  ```
  touch a1.txt
  ```

- vim [filename]：编辑文件
  - 刚进入的时候是命令模式，输入i进入编辑模式，编辑完Esc进入命令模式，==**输入：**==wq保存并退出;
  - shift+a,进入编辑模式并跳入行尾；
  - d删除
  - vi下删除：输入":"，再输入2,3d，前两个数字分别为起始行号和结束行号
  - ：set number，添加行号
  
- cat [filename]：查看文件内容

- cp [file] [file]：拷贝

- mv [file] [file]：改名

- ctrl+ins：复制

- shift+ins：粘贴

- ctrl+c：跳过该条命令

- echo：重定向

  ```
  #把hello World输入到test2.txt
  echo 'hello World' > test2.txt
  #追加
  echo '[context]' >> [filename]
  ```

- ctrl+a：光标回到一行的头部

- ctrl+e：光标回到一行的尾部

- shift+t：到最后一行

- &&：连续执行两个命令

  ```
  #先执行mkdir mydir，再执行cd mydir
  mkdir mydir && cd mydir
  ```

- cd -：进入上次的目录

#### 概念

- *repository*：存储整个项目的整个历史，存储在本地，不用联网就可以访问

- *unmodified* ：没有改变

- *modified* ：发生改变

- *staged* ：已经被*git add*

- *committed*：已提交

- *HEAD*： A special branch pointer， references the branch you currently have as your working directory ,指向当前所在分支的标识符，并不包含SHA-1值，而是一个指向另外一个引用的指针。

  当使用commit命令时，会将新创建的commit的parent指针指向HEAD所指向的SHA-1值

  对于HEAD修改的任何操作都会被git reflog完整记录下来

- ORIG_HEAD：远程的head
- FETCH_HEAD：从远程拉取完代码后，处于什么点

- *master* : your initial branch 
- git文件：已被版本库管理的文件

#### 本地操作

- 配置信息

  ```
  git config --global user.name 'username'
  git config --global user.email 'xxx@xxx.com'
  ```

  常见的设置位置

  - ~/.gitconfig：设置该用户的信息

    ```
    git config --global
    ```

  - .git/config：针对特定项目

    ```
    git config --local
    ```

- ==git init==打开文件夹初始化

  ```
  cd /users/sandra/recipes
  git init
  ```

- ==git add==操作，把文件添加到tarack list，add command tells git which ones it should be tracking ，**文件修改之后需要再次add**

  ```
  git add ./tofu/kung_pao_tofu.txt
  
  #将所有文件add
  git add .
  ```

- ==git status==操作，查看当前文件夹的情况，包括track的和untrack的

  ```
  git status
  ```

  ```
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
  
      new file:   tofu/basil_ginger_tofu.txt
      new file:   tofu/kung_pao_tofu.txt
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
  
      seitan/
  ```

- ==git commit==操作，commit添加到仓库，-m添加提交信息

  ```
  git commit -m 'added tofu recipes'
  
  #添加并提交当前已修改的文件,用-am
  git commit -am 'message'
  ```

- ==git log==操作，查看提交日志（除了提交日志还有操作日志）

  ```
  git log
  ```

  ```
  commit 9f955d85359fc8e4504d7220f13fad34f8f2c62b
  Author: Sandra Upson <sandra@Sandras-MacBook-Air.local>
  Date:   Sun Jan 17 19:06:48 2016 -0800
  
      added tofu recipes
  ```

  常见操作

  ```
  #查看最近n条操作
  git log -n
  
  #把每条信息用一行显示出来(还可以定制格式)
  git log --pretty=oneline
  /**
    *7eb6c9145a1402cabcfda54a0d81c8dad5aaf922 (HEAD) delete
    *c79bf4447bfc93d8b5fefa977b5a4052fd08ae40 commit test.txt
  */
  
  #以图形化显示log信息
  git log --graph
  
  #缩写
  git log --graph --abbrev-commit
  git log --graph --pretty=oneline --abbrev-commit
  ```

  

- ==git reflog==查看操作日志

  ```
  git reflog
  ```

  
  
- ==git show==操作，查看commit内部信息，需要commit的ID

  ```
  git show 9f955d85359fc8e4504d7220f13fad34f8f2c62b
  ```

  ```
  commit 9f955d85359fc8e4504d7220f13fad34f8f2c62b
  Author: Sandra Upson <sandra@Sandras-MacBook-Air.local>
  Date:   Sun Jan 17 19:06:48 2016 -0800
  
      added tofu recipes
  
  diff --git a/tofu/basil_ginger_tofu.txt b/tofu/basil_ginger_tofu.txt
  new file mode 100644
  index 0000000..9a56e7a
  --- /dev/null
  +++ b/tofu/basil_ginger_tofu.txt
  @@ -0,0 +1,3 @@
  +basil
  +ginger
  +tofu
  diff --git a/tofu/kung_pao_tofu.txt b/tofu/kung_pao_tofu.txt
  new file mode 100644 index
  0000000..dad9bd9
  --- /dev/null
  +++ b/tofu/kung_pao_tofu.txt
  @@ -0,0 +1,3 @@
  +szechuan peppers
  +tofu
  +peanuts
  +kung
  +pao
  ```

- ==git checkout==操作，把内容变成某ID下的内容，**checkout不会改变commit的历史**，**Make sure to specify a file (or directory) when you use checkout.** 不加路径会改变commit历史。可怕。。补救措施： https://sp19.datastructur.es/materials/guides/git-wtfs.html 

  ```
  git checkout 9f955d85359fc8e4504d7220f13fad34f8f2c62b ./recipes/tofu
  ```

- 删除文件

  ```
  rm -rf a1.php
  git rm a1.php
  git commit -m 'delete'
  ```

- gitk 图形化界面查看提交信息

  ```
  gitk
  ```

- git gui 图形化界面

  ```
  git gui
  ```

- 别名

  ```
  #例：用br代表branch
  git config --global alias.br branch
  #例：用unstage代表reset HEAD，两个单词要用引号
  git config --global alias.unstage 'reset HEAD'
  #例：用ui代表gitk，因为gitk是外部命令，所以要加感叹号
  git config --global alias.ui '!gitk'
  ```

- 对HEAD操作（底层操作）

  ```
  #读取HEAD
  git symbolic-ref HEAD
  #修改HEAD,不会修改reflog
  git symbolic-ref HEAD refs/heads/[branch_name] 
  ```

  

#### Undoing Changes（撤销更改）

- checkout和reset的区别

  ```
  #丢弃在工作区的操作，回到上一次暂存区的内容
  git checkout -- [file]
  #回到某个提交点
  git checkout [ID的前几位]
  会处于游离状态，做了变更之后要提交，提交完需要新建一个分支保存
  git branch [branch name] [ID的前几位]
  
  #从暂存区移到工作区
  git reset HEAD [file]
  ```

  

- 回退到之前的提交版本

  ```
  #回退一个版本
  git reset --hard HEAD^
  #回退两个版本
  git reset --hard HEAD^^
  #回退到某一指定版本
  git reset --hard [ID的前几位]
  #回到第n个版本
  git reset --hard HEAD~n
  ```

- Unstage a file that you haven't yet committed,使文件回到modified状态（==从暂存区恢复到工作区==）

  ```
  git reset HEAD [file]
  ```

- Amend latest commit  (changing commit message or add forgotten files) 

  ```
  git add [forgotten-file]
  #把上次提交的message修正
  git commit --amend -m 'message content'
  ```

-  Revert a file to its state at the time of the most recent commit:丢弃modified的内容，和暂存区保持一致，注意：**丢了就找不回来了**（==在工作区，丢弃删除操作==）

  ```
  git checkout -- [file]
  ```

- 撤销git add，等同于第一个

  ```
  git rm --cached [file]
  ```

- 删除&修改
  - 误提交文件到版本库之后（==必须commit之后==），删除

  ```
  git rm [file]
  ```

  ​	删除之后可以使用git reset HEAD [file]（==从暂存区恢复到工作区==），再使用git checkout -- [file]恢复 （==丢弃删除操作==）

  ​	删除一个文件之后也需要commit（提交）

  ​	==但是==，如果使用rm删除，只需要使用git checkout -- [file]恢复即可，但无法提交，提交还需git add

  rm与git rm对比：

  ​	git rm有以下两步：1、删除文件；2、把删除操作提交到暂存区

  ​	rm有以下一步：1、删除文件

- 修改文件名（git mv和mv的关系同上）

  ```
  git mv [file] [file]
  ```

#### .gitignore

jar包不用放入版本控制系统中，只要把它的配置文件放进去

IDE所需的配置文件不用放入版本控制系统中

1. 操作步骤

```
#创建'.gitignore'文件
vi .gitignore
#把需要忽略的文件名加入'.gitignore'
```

2. ***支持正则表达式***

   ```
   #'*.b'表示忽略所有后缀为b的文件
   
   #'！a.b'表示a.b文件除外
   
   #'/test3.txt'表示忽略根目录下的test3.txt，不忽略子目录下的test3.txt
   
   #'/*/test3.txt'表示忽略一层目录下的test3.txt,'/**/test3.txt'表示忽略所有层目录下的test3.txt
   
   #'build/'忽略掉build下的所有文件
   ```

#### git branching分支

- 概念

  - 一个commit对象链：一条工作记录线，用链表存储每次commit，每个commit有一个parent为上一个commit的ID

  - HEAD指向的是当前分支，master指向的是提交，相当于HEAD指向master，master指向具体的提交

    

- 写在前面

  - 不同分支的文件是相互独立的
  - 未被commit的文件会在所有的分支上显示
  - 在哪个分支上commit的文件就会显示在哪个分支上
  - 在哪个分支上新建的分支，拷贝的就是哪个分支上的内容
  - 当发生冲突，手动修复之后需要调用git add告诉git已经修复了，再使用‘git commit’，后面需要加东西，结束merge

- 使用理由

  - 你想对代码做出戏剧性改变，但你这部分代码正被另一个project使用
  - 你想开始project的新部分，但不确定这部分是否是有用的
  - 你和你的伙伴合作，但你目前还不想把自己的代码和他们的混合

  branch可以更好地跟踪多版本代码

- 常见命令

  - 查看所有分支，带*表示当前分支

    ```
    git branch
    
    #如果要查看远程分支origin/master
    git branch -a
    
    #查看远程分支并列出提交信息
    git branch -av
    ```
    
  - 创建 create a branch

  ```
  git branch [new-branch-name]
  ```

  - 切换 switch branch, your initial branch is called `master`. 

  ```
  git checkout [destination-branch]
  ```

  - 结合新建并 切换branch

  ```
  git checkout -b [new-branch-name]
  ```

  - 删除 branch（不能删除当前所处的分支）

  ```
  git branch -d [branch-to-delete]
  
  #删除没有合并过的分支
  git branch -D [branch-to-delete]
  ```

  - 分支改名

    ```
    git branch -m [branch name] [new branch name]
    ```

  - 查看当前分支最新的提交消息

  ```
  git branch -v
  ```

- Merging

  you should checkout the `master` branch and merge `fixing-ai-heuristics` into `master`. 

  ```
  git checkout master
  git merge [branch_to_merge]
  
  #禁用fast-forward模式
  git merge --no-ff [branch_to_merge]
  ```

- Resolving Merge Conflicts

   Git will tell you which files have conflicts. You need to open the files that have conflicts and **resolve them manually**. After doing this, you must **commit to complete the merge of the two branches** 

#### stash 临时保存信息

```
#保存
git stash
#加说明的保存
git stash save 'message'
#查看保存列表
git stash list
#恢复状态
git stash pop（会自动删除）
或
git stash apply（需要手动删除）
#手动删除第n条
git stash drop stash@{n}
#恢复第n个版本
git stash apply stash@{n}
```

#### 标签

- 作用：标签可以记录commit ID

  发布版本时打上标签，做标记。有两种标签，1）轻量级标签（lightweight），只有标签名；2）带有附注的标签（annotated）

  标签不依赖于分支

  ```
  git tag [tag name]
  git tag -a [tag name] -m 'message'
  
  #查看标签
  git tag
  #查看标签详信息(commit id)
  git show [tag_name]
  #搜索标签
  git tag -l '[可以使用正则表达式]'
  #删除标签
  git tag -d [tag_name]
  
  #将标签推送到远程
  git push origin [tag_name]
  git push origin [tag_name] ... [tag_name]
  #将本地所有标签一次性推送到远程
  git push origin --tags
  #[完整写法]将本地标签推送到远程
  git push origin refs/tags/v7.0:refs/tags/v7.0
  
  #仅仅将标签从远程拉取回来
  git fetch origin tag v7.0
  #将远程标签拉取到本地
  git pull
  
  #删除远程标签
  #删除远程的V6.0标签
  git push origin :refs/tags/v6.0
  #另一种方法
  git push origin --delete tag v6.0
  ```

#### diff&blame

- blame查看该文件上一次被谁修改过

  ```
  git blame [file name]
  ```

- diff比较两个文件的不同

  - linux自带的diff

    ```
    diff [fileName] [fileName]
    diff -u [fileName] [fileName] #-对应第一个文件，+对应第二个文件
    ```

  - git的diff

    - 工作区和暂存区之间的差别

      ```
      git diff #暂存区为原始文件，工作区为目标文件
      ```

    - 工作区与版本库的差别

      ```
      #比较工作区和当前提交的差别
      git diff HEAD
      #比较工作区和特定版本的差别
      git diff [commit_id]
      #版本库为原始文件，工作区为目标文件
      ```

    - 暂存区和版本库之间的差别

      ```
      #比较暂存区和特定版本的区别
      git diff --cached [commit_id]
      #比较暂存区和最新版本的区别
      git diff --cached
      ##版本库为原始文件，暂存区为目标文件
      ```

      

#### other git features

- stash： Stashing allows you to save your changes onto a stack without making a more permanent commit.  picking up your work-in-progress and placing it in a box to get back to later. 
  - 什么时候使用
    - file in  disorganized state，不想commit，也不想get rid of
    - 修改了很多，发现不喜欢，想回到从前
    - 在错误的分支上修改了
- rewriting history：想修改更之前的commit
- rabasing：
- reset：确定不想要最后几次的commit了
- revert： a safer option that simply throwing away past commits. 
- cherry pick：



#### github 远程仓库

- `git clone [remote-repo-URL]`: Makes a copy of the specified repository, but on your local computer. Also creates a working directory that has files arranged exactly like the most recent snapshot in the download repository. Also records the URL of the remote repository for subsequent network data transfers, and gives it the special remote-repo-name “origin”. 

- `git remote add [remote-repo-name] [remote-repo-URL]`: Records a new location for network data transfers. 

- `git remote -v`: Lists all locations for network data transfers. 

- `git pull [remote-repo-name] master`: Get the most recent copy of the files as seen in remote-repo-name 

- `git push [remote-repo-name] master`: Pushes the most recent copy of your files to the remote-repo-name. 

- 命令

  - pull 拉取，同时会执行合并merge，pull == fetch+merge

  - clone：在github上复制地址，然后

    ```
    git clone '地址'
    ```

  - 显示所有与当前仓库关联的远程仓库的别名

    ```
    git remote show #默认都叫origin,如果有两个以上就得叫别的名字
    ```

  - 显示远程仓库的详细信息

    ```
    git remote show [remote_name]
    ```
    
  - push，同步到远程仓库，同时更新origin/master分支

    ```
    git push
    ```


- 步骤

  - 在github上新建一个repo

  - 使用以下命令在git bash上将文件推送到远程

    ```
    #首次推送
    git remote add origin https://github.com/chenshikang3/Test.git
    git push -u origin master
    
    #再次推送，直接使用
    git push
    ```

- 使用SSH，以下是给repo设置ssh，也可以给整个git账号设置ssh，在git的setting里

  ```
  git remote add origin [ssh]
  git remote show origin #不能建立，需要生成公钥和私钥，再把公钥部署到github上，输入yes
  ssh-keygen #会问保存在哪里，密码是什么，都直接回车
  #进入目录
  cd ~
  cd .shh #id_rsa是私钥,id_rsa.pub是公钥
  #查看公钥内容并复制到github上
  cat id_rsa.pub
  #仓库界面->setting->Deploy kesys-> Add deploy key
  #名字随便起
  #再次执行git remote show origin就可以正常使用了
  #做一次远程分支的关联
  git push -u origin master 
  ```

- git协作，每次push前先pull，pull的时候要是merge失败了，需要手动修改，再次push到远程

  ```
  Local branch configured for 'git pull':
      master merges with remote master
    Local ref configured for 'git push':
      master pushes to master (up to date)
  ```

  另一个协作者参与协作

  ```
  git clone [ssh/https]
  
  #克隆并制定文件名
  git clone [ssh/https] [filename]
  ```

#### 远程分支

- 创建远程分支并对应

  ```
  方法一：
  #在远程创建develop分支，并将develop分支推送到远程develop分支
  git push --set-upstream origin develop
  #远程的名字和本地的不同的话
  git push --set-upstream origin develop:develop2
  
  方法二：
  git push -u origin develop
  ```

- git pull会直接将远程的所有分支拉回到本地，但本地并没有相应分支，也就是李四在远程创建了develop分支，张三可以拉取到本地，得到origin develop分支，但张三的本地并没有develop分支

- 需要基于该远程分支创建新分支

  ```
  方法一：
  #基于origin/develop创建develop分支
  git checkout -b develop origin/develop
  
  方法二：
  #基于origin/test创建分支，会把test作为分支名
  git checkout --track origin/test
  ```

- git pull 的完整写法

  ```
  git pull origin src:dest
  ```

- git push的完整写法

  ```
  git push origin src:dest
  ```

- 删除远程分支

  ```
  #方法一
  #把一个空推到远程分支
  #删除远程的develop分支
  git push origin :develop
  
  #方法二
  #删除远程的develop分支
  git push origin --delete develop
  
  #李四在他的本地仓库删除了远程仓库的分支，但是在张三的本地仓库仍然会保留删除前的分支，需要裁减
  git remote prune origin
  ```

- 远程分支重命名步骤：
  1. 删除远程分支
  2. 重命名本地分支
  3. 把改名后的本地分支推到远程

- 

#### Git分支最佳实践

1. Git分支有如下几种
   1. develop分支，开发人员之间，频繁变化
   2. test分支，供测试与产品，变化不是特别频繁，develop->test
   3. master分支，生产发布分支，变化非常不频繁的一个分支，test->master
   4. bugfix（hotfix）分支，生产系统中出现紧急bug，用于紧急修复的分支

#### submodule

- git裸库：没有工作区的库，通常在服务器

  ```
  #创建裸库
  git init --bare
  ```

- submodule：你在维护一个git项目a，有另一个团队维护另一个git项目b，你想把b的源码引入a，那么就在你的git仓库里又有一个git仓库

- 步骤

  1. 在github上创建两个仓库(可以称作git_parent，git_child)

  2. 在parent库中

     ```
     #filename放置拉取过来的文件，事先不能存在
     git submodule add [child_ssh] [filename]
     ```

  3. add、commit，然后push

  4. 当child修改时，只需要cd mymodule，然后执行一次git pull

  5. 如果有多个submodule，想要一次把所有的都更新，可以在git_parent目录下执行

     ```
     git submodule foreach git pull
     ```

  6. add、commit,push

- clone父模块

  ```
  #方法一
  #步骤一：先正常clone
  git clone [parent_ssh] [filename]
  #步骤二：在git_parent2上init
  git submodule init
  #步骤三：递归更新
  git submodule update --recursive
  
  #方法二
  git clone [parent_ssh] [filename] --recursive
  ```

- 删除submodule

  ```
  #步骤一:从暂存区移除
  git rm --cached mymodule
  #步骤二：从工作区删除
  rm -rf mymodule
  #步骤三
  rm .gitmodules
  #步骤四：add、commit、push
  ```

#### subtree

解决的问题和submodule相似，推荐使用。

- 查看subtree命令

  ```
  git subtree
  ```

- 使用步骤

  1. 在parent库中添加child的远程连接

     ```
     git remote add subtree-origin [child_ssh]
     ```

  2. 拉取子库

     ```
     git subtree add --prefix=subtree subtree-origin master --squash
     #git subtree add --prefix=[filename] [remote] [branch],--squash表示把子库之前提交的记录压缩成一条 
     git push
     ```

  3. child变动后，parent库更新

     ```
     git subtree pull --prefix=subtree subtree-origin master --squash
     git push
     ```

  4. 使用‘--squash’会导致child库的提交历史被压缩，在parent库中更新child库的内容，然后推给child库时，可能会导致merge冲突，解决办法是从一开始，所有的命令都需要使用‘--squash’

     不使用则会导致child库的提交历史都进入parent的提交历史中，污染了parent的提交历史

     综上，在add、pull使用‘--squash’，要么就不用，要么就一直用。

     有时会出现本不会冲突的地方发生了冲突的情况，也是由于‘--squash’造成的

  5. 在parent中改动child，再推回child

     ```
     git push
     git subtree push --prefix=subtree subtree-origin master
     ```

  6. git clone，可以直接把整个仓库的代码更新下来
  7. git split 将子模块及其提交历史分割出去成为一个新的项目

#### git cherry-pick

将在一个分支上的commit应用到领一个分支上

```
#先切换到需要应用的分支
#再使用cherry-pick
git cherry-pick [commit_id](前几位即可)
#在使用cherry-pick时，如果跳过commit去pick，可能会发生冲突
```

先checkout到一个commit_id上，然后把branch删掉，再基于该commit_id创建一个新的branch，使用git switch -c [new_branch_name]，就可以消除对一个branch的改动

#### git rebase 变基/衍合

改变分支的根基，功能类似于merge

```
#在test分支上，将develop为基
git rebase develop
#如果出现冲突
#使用git rebase --skip就会忽略掉当前补丁，以develop上的为准
#使用git rebase --abord就会回到rebase之前
#或者手动修改冲突，然后git add test.txt 然后 git rebase --continue
```

merge会产生一个新的提交，这个提交会指向之前提交的两个分支

![](D:\数据\学习笔记\git&github\merge.png)

rebase会将历史变为一条直线，它其实是将一个分支的提交不断应用到另一个分支上，会修改git的提交历史，rebase可以终止，会回到rebase之前

不要对master分支执行rebase；执行rebase分支都是自己的本地分支，没有推送到远程版本库

==不要在与他人共享的分支上用git rebase==

==不要在master分支上使用git rebase，因为master分支一定是一个与他人共享的分支==

假设当前在test分支，merge是将dev合到test上，rebase是以dev为基，把test往上合

![](D:\数据\学习笔记\git&github\rebase.png)

#### 其他

- commit id是一个摘要值，通过sha1计算出来

- git维护的是全量不是增量

- git不识别空文件夹

- 开发规范
  
- Gitflow
  
- git合并原则：三方合并原则

- 在缺省情况下，refspec会被git remote add命令所自动生成，Git会获取远端上refs/heads下的所有引用，并将它们写到本地的refs/remotes/origin目录下。所以，如果远端有一个master分支，你在本地就可以通过以下几种方式来访问它们的历史记录：

  查看origin/master分支的提交记录

  ```
  #方法一
  git log origin/master
  #方法二
  git log remotes/origin/master
  #方法三
  git log refs/remotes/origin/master
  ```

- gc垃圾收集机制

- gradle官网：www.gradle.org

