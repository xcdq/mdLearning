## 概述

<table><caption>本文内容简述</caption><tbody><tr><td rowspan="3">Git 概述</td><td>① 什么是版本管理系统</td><td>② Git 和 SVN 的区别</td></tr><tr><td>③ Git 的四个组成部分</td><td>④ Git 中文件的几个状态</td></tr><tr><td colspan="2">⑤ Git 中的四类对象</td></tr><tr><td colspan="3">Git 下载安装配置</td></tr><tr><td rowspan="11">Git 本地基本操作</td><td>① 配置「git config」</td><td>② 获取帮助「git help」</td></tr><tr><td colspan="2">③ 创建 Git 仓库「git init」</td></tr><tr><td colspan="2">④ 添加文件到暂存区「git add」</td></tr><tr><td colspan="2">⑤ 让 Git 不跟踪特定文件「.gitignore 文件」</td></tr><tr><td colspan="2">⑥ 暂存区内容提交到本地仓库「git commit」</td></tr><tr><td colspan="2">⑦ 查看工作区与暂存区状态「git status」</td></tr><tr><td colspan="2">⑧ 内容变化，差异对比「git diff」</td></tr><tr><td colspan="2">⑨ 查看历史提交记录「git log」</td></tr><tr><td colspan="2">⑩ 查看某个文件的改动记录「git blame」</td></tr><tr><td colspan="2">⑪ 设置 Git 命令别名「git config --global alias」</td></tr><tr><td colspan="2">⑫ 为重要提交打标签「git tag」</td></tr><tr><td rowspan="8">Git 文件恢复与版本回退</td><td colspan="2">① 文件恢复，未 add「git checkout」</td></tr><tr><td colspan="2">② 文件恢复，已 add 未 commit「git reset HEAD」</td></tr><tr><td colspan="2">③ 版本回退，已 commit「git reset --hard」</td></tr><tr><td colspan="2">④ 查看输入过的指令记录「git reflog」</td></tr><tr><td colspan="2">⑤ 撤销某次提交「git revert」</td></tr><tr><td colspan="2">⑥ 查看某次提交的修改内容「git show」</td></tr><tr><td colspan="2">⑦ 查看分支最新 commit 的 Hash 值「git rev-parse」</td></tr><tr><td colspan="2">⑧ 找回丢失对象的最后一点希望「git fsck」</td></tr><tr><td rowspan="8">Git 本地分支</td><td>① 分支的概念</td><td>② 创建其他分支的原因</td></tr><tr><td colspan="2">③ 一个简单的分支管理策略</td></tr><tr><td colspan="2">④ 分支的创建于切换「git branch」</td></tr><tr><td colspan="2">⑤ 分支合并「git merge」 VS 「git rebase」</td></tr><tr><td>⑥ 解决合并冲突</td><td>⑦ 删除分支</td></tr><tr><td>⑧ 恢复误删分支「git log --branches」</td><td>⑨ 分支重命名</td></tr><tr><td colspan="2">⑩ 切换分支时暂存未 commit 的更改「git stash」</td></tr><tr><td colspan="2">⑪ 把 commit 从一个分支挪到另一个分支「git cherry-pick」</td></tr><tr><td rowspan="7">Git 远程仓库</td><td colspan="2">① 远程仓库概述</td></tr><tr><td colspan="2">② 本地仓库与远程仓库建立关联「git remote」</td></tr><tr><td colspan="2">③ 推送本地仓库到远程仓库「git push」</td></tr><tr><td colspan="2">④ 克隆远程仓库「git clone」</td></tr><tr><td colspan="2">⑤ 同步远程仓库更新「git fetch」VS「git pull」</td></tr><tr><td colspan="2">⑥ git push 时的 unrelated history 问题</td></tr><tr><td colspan="2">⑦ SSH Key 避免每次 push 重复输入账号密码</td></tr><tr><td rowspan="3">Git 工作流</td><td>① 集中式工作流</td><td>② 功能分支工作流</td></tr><tr><td>③ Gitflow 工作流</td><td>④ Forking 工作流</td></tr><tr><td colspan="2">⑤ Pull Request 工作流</td></tr><tr><td rowspan="1">其他杂项</td><td>① 为开源项目贡献代码</td><td>② SourceTree 使用详解</td></tr></tbody></table>

* * *

0x1、Git 概述——分布式版本控制系统
---------------------

* * *

了解 Git 相关的概念，有助于后续命令的掌握~

* * *

### 1. 什么是版本管理系统

**VCS**（Version Control System），一种用于记录一个或多个文件内容变化  
历史，以便将来能对特定版本的历史记录进行查看，更改，备份还原的系统。  
可以简单类比为「**游戏存档**」，打 Boss 前存下档，没过关，重新读档；  
分支剧情，想体验不同选择触发的不同剧情，可以存多个档， 想玩哪个读哪个。

VCS 一般分为下述三类：

* * *

*   1. **本地 VCS**

> 使用简单的数据库来记录文件的历史更新差异，比如 RCS。
> 
> ![](http://static.zybuluo.com/coder-pig/1yloqw07te8l143g4xrqrbdt/1.png)

*   2. **集中式 VCS**

> 用一个服务器来保存所有文件的修订版本，协同工作的人连接这个服务器，  
> 获取或提交文件更新，比如 SVN。
> 
> ![](http://static.zybuluo.com/coder-pig/1qb5eciuuqxxk9kyijphskb7/2.png)
> 
> 这种协同方式有个两个明显的缺点：  
> 1.「**需要联网**」：同步和推送更新速度受带宽限制，内网还好，外网可能会有点慢了（大文件）；  
> 2.「**依赖中央服务器**」：每个人的本地只有以前所同步的版本，如果服务器宕 (dang) 机了，谁都无法获取或提交更新。

*   3. **分布式 VCS**

> 每个用户拥有完整的提交历史，支持离线提交更改，查看历史提交记录等。中央服务器更多的只是用作更改合并，同步的工具，比如 Git。
> 
> ![](http://static.zybuluo.com/coder-pig/737bf0y01d20nr89hqw81xfe/3.png)
> 
> 从根本上来说，Git 是一个**内存寻址的文件系统**，根据文件的 Hash 值来定位文件。  
> 这个 40 位的 Hash 值使用 SHA1 算法生成，由两部分拼接：  
> **header = “<type>” + content.length + "\0"**  
> (参数依次为：对象类型，数据字节长度，空字节 (用于分隔 header 与 content)  
> **hash = sha1(header+content)**，这里的拼接是二进制级别的拼接，而非字符串拼接。

* * *

### 2. Git 与 SVN 的区别

Git 和 SVN 除了上面说的联网需求不同外，还有「**存储差异**」：

> SVN 关心：**文件内容的具体差异**；而 Git 关心：**文件整体是否发生改变**。  
> SVN 每次提交记录的是：「**哪些文件进行了修改，修改了哪些行的哪些内容**」。
> 
> ![](http://static.zybuluo.com/coder-pig/op0rxe23xtvn30pkkoskw4e9/2.png)
> 
> 如图，Version 2 中记录的是文件 A 和 C 的变化，而 Version 3 中记录文件 C 的变化，以此类推；  
> 而 Git 中，并不保存这些前后变换的差异数据，而是保存整个缓存区中的所有文件，  
> 又称**快照**，「**有变化的文件保存，没变化的文件不保存，而是对上次保存的快照做一个链接**」，  
> 因为这种不同的保存方式，使得 Git 切换分支的速度比 SVN 快上不少。
> 
> ![](http://static.zybuluo.com/coder-pig/cw124ird2emdh8bysh4uu7ey/3.png)

当然 SVN 也有它的优点，比如「**权限控制**」，可以设定每个账户的读写权限，而 Git 中  
则没有响应的权限控制。至于用哪个的，还是看公司要求吧~

* * *

### 3. Git 的四个组成部分

![](http://static.zybuluo.com/coder-pig/spfndr6nbi1a69nmmbdehqcb/1.png)

简单说下 Git 的四个组成部分：

*   **工作区**：不包含. git 文件夹在内的整个项目目录，所有修改都在工作区内进行。
*   **暂存区**：又称索引区，本地文件修改后，执行 add 操作会把工作区的修改添加到缓存区。
*   **本地仓库**：当执行 commit 操作时，暂存区的数据被记录到本地仓库中。
*   **远程仓库**：托管项目代码的服务器，多人协作时通过远程仓库进行代码同合并与同步。

接下来说下这几个部分是如何协同工作的：

**工作区与暂存区**：工作区更改，通过 git add 命令可以把更改提交到暂存区；  
也可以 git checkout 命令使用暂存区内容覆盖当前的工作区的内容。

**暂存区与本地仓库**：可以通过 git commit 命令把暂存区的内容提交到本地仓库，  
每次 commit 都会生成一个快照，快照使用 Hash 值编号。可以通过 git reset Hash 值，  
把某个快照还原到暂存区中。

**工作区和本地仓库**：通过 git checkout 快照编号，直接把某个快照还原到工作区中。

**本地仓库和远程仓库**：可以通过 git push 命令把 commit 推送到远程仓库，多人协作的  
时候可能还需要进行一些冲突处理；还有通过 git clone 拉取某个远程仓库的项目到本地，  
或通过 git fetch 拉取远程仓库的最新内容，检查后决定是否合并到本地仓库中。

**工作区和远程仓库**：这里两者的协作一般是 git pull，即把远程主机的最新内容拉取下来后直接合并。

* * *

### 4. Git 中文件的几个状态

按照大类划分，可以分为两种状态：**Tracked**(已跟踪) 和 **Untracked**(未跟踪)，  
依据是：「**该文件是否已加入版本控制**」？

**文件状态变化周期流程图**：

![](http://static.zybuluo.com/coder-pig/h0ohvbtxdhyb7ll59ruqmaen/4.png)

**流程简述**：

假设某个项目已加入 Git 版本控制系统

*   1. 新建一个文件，该文件处于 **`Untracked`** 状态；
*   2. 通过 git add 命令添加到缓存区，此时文件处于 **`Tracked`**状态又或者说  
    此时这个文件已经被版本控制系统所跟踪，而且他处于**`Staged`**(暂存) 状态；
*   3. 通过 git commit 命令把暂存区的文件提交提交到本地仓库，此时文件处于  
    **`Unmodified`**(未修改) 状态；
*   4. 此时如果去编辑这个文件，文件又会变成 **`Modified`**(修改) 状态；

### 5. Git 中的四类对象

在 Git 系统中有四种类型的对象，几乎所有的 Git 操作都是在这四种对象上进行的，依次为：  
**`Blob`（块）对象，`Tree`（树）对象，`Commit`（提交）对象，`Tag`（标签）对象。**  
前三者的关系如图所示：

![](http://static.zybuluo.com/coder-pig/8dvmokvpa9p3f80n2ld0gcn5/5.png)

接着我们来详解的讲解这四类对象：

① **块对象（Blob）**

> 一块二进制数据，「**仅存放文件内容**」，不包括文件名、权限等信息。Git 会根据文件内容计算  
> 出一个 **Hash 值**，以这个 Hash 值作为文件索引保存起来。意味着，相同文件内容的文件，只会保存  
> 一个，即共享同一个 Blob 对象。可以使用：**`git hash-object 文件名`** 来计算文件内容的 Hash 值。  
> 如果你知道已经添加到 Git 中的某个文件的 hash 值，还可以通过 **`git cat-file hash值`** 来读取数据  
> 对象，可选参数：**`-p`**（查看 Git 对象内容） ，**`-t`**（查看 Git 对象类型），示例如下：

![](http://static.zybuluo.com/coder-pig/k2kxevthfnvcsezhfloqa0mt/1.png)

② **树对象（Tree）**

> **保存一个或多个块对象的引用**，每次 commit 对应一个树对象，这里生成一个 commit，  
> 然后调用 **`git ls-tree Hash值`** 查看树对象的内容：

![](http://static.zybuluo.com/coder-pig/mo7z34uw7lqsyznt9g9t20uo/2.png)

利用上面的 **`git cat-file -p hash值`** 来查看 blob 块的具体内容：

![](http://static.zybuluo.com/coder-pig/us1prn2tbdj1icdml4o0w6l6/3.png)

除了保存块对象的引用外，树对象还可以引用「**其他树对象**」，从而构成一个「**目录层次结构**」。  
新建一个 test 目录，复制一个 1.txt 文件到这个路径下，提交一个 commit，然后查看树对象的内容：

![](http://static.zybuluo.com/coder-pig/gvps5u0t0xve6n4w4da7o57r/4.png)

可以指向了另一个 tree 对象，这个 tree 对象指向另一个 1.txt 文件，树对象解决了**文件名**的问题。  
而对于提交的人、时间、说明信息等，我们还需要通过提交对象进行了解。

③ **提交对象（Commit）**

> **保存树对象的 Hash 值，父 Commit 的 Hash 值，提交作者、时间、说明信息**。  
> 同样可以使用 **`git cat-file`** 命令查看 commit 对象：

![](http://static.zybuluo.com/coder-pig/2drhh4ftvlvxwcqav7cebxod/5.png)

④ **标签对象（Tag）**

一般会对某次重要的 commit 加 TAG，以示重要，分为两种情况：

*   **轻量级标签**：不会创建真正的 TAG 对象，而是直接引用 commit 对象的 Hash 值。
*   **附加标签**：会创建 TAG 对象，TAG 对象中包含 commit 对象的引用，除此之外会创建  
    一个文件：**`.git/refs/tags/标签名`**，里面保存 TAG 对象的引用。

这里为我们上面的两个 commit 一次打上两种标签，然后看下具体的结果：

![](http://static.zybuluo.com/coder-pig/nxsr8hi72fjtbptiq9xy2gt3/6.png)

* * *

0x2、Git 下载安装配置
--------------

* * *

*   **Windows 系统**：到 [Git For Windows](https://git-scm.com/download/win) 或 [git-for-windows.github.io](https://gitforwindows.org/) 下载，傻瓜式下一步。
*   **Linux 系统**：到 [Download for Linux and Unix](https://git-scm.com/download/linux) 下载，如果是 Ubuntu 的话，直接 Terminal 键入：  
    **`sudo apt-get install git`** 安装即可。
*   **Mac 系统**：到 [Installing on Mac](https://git-scm.com/download/mac) 下载，不过新系统貌似默认已经带有 Git 了，另外如果安装了  
    Homebrew 的话可以直接命令行键入：**`brew install git`** 进行安装。

* * *

0x3、Git 本地基本操作
--------------

* * *

### 1. 相关配置「git config」

安装完后，使用 Git 还需要进行环境的配置，配置信息保存在 gitconfig 文件中，有三种级别：

*   **system**（系统）：**系统中所有用户**都会生效，配置文件：`C:\Program Files\Git\mingw64\etc\gitconfig`，  
    不同的系统可能不一样，你可以通过：`git config -e --system`，底部可以找到配置文件的路径：  
    ![](http://static.zybuluo.com/coder-pig/jugbwh6476nk0bzbsy2u080a/1.png)
*   **global**（全局）：**当前系统用户下生效**，配置文件：`C:/Users/当前用户/.gitconfig`，  
    同样可以采用上面的：`git config -e --global` 查看配置文件的位置。
*   **local**（本地）：**配置仅在当前项目生效**，配置文件：`项目路径/.git/config`

**配置生效优先级**：local > global > system，**常用命令**：

```
# 配置
git config --global user.name "用户名"          # 配置用户名
git config --global user.email "用户邮箱"       # 配置邮箱
git config --global core.editor 编辑器          # 配置编辑器，模式使用vi或者vim

# 查看配置
git config --global user.name       # 查看配置的用户名
git config --global user.email      # 查看配置的邮箱

# 查看所有配置列表
git config --global --list      # 查看全局设置相关参数列表
git config --local --list       # 查看本地设置相关参数列表
git config --system --list      # 查看系统配置参数列表
git config --list               # 查看所有Git的配置(全局+本地+系统)
```

除了命令行的方式外，你还可以直接去编辑对应的配置文件。

### 2. 获取帮助「git help」

```
git help 命令       # 查看某个git命令的介绍，用法
git 命令 --help     # 另一种写法
```

### 3. 创建本地仓库「git init」

```
git init 仓库名     # 创建一个新的带Git仓库的项目
git init           # 为已存在的项目生成一个Git仓库
```

### 4. 添加文件到暂存区「git add」

```
git add 文件名  # 将工作区的某个文件添加到暂存区。
git add -u     # 添加所有被tracked文件中被修改或删除的文件信息到暂存区，不处理untracked的文件
git add -A     # 添加所有被tracked文件中被修改或删除的文件信息到暂存区，包括untracked的文件
git add .      # 将当前工作区的所有文件都加入暂存区
git add -i     # 进入交互界面模式，按需添加文件到缓存区
```

很多人应该没用过交互界面模式，这里演示下用法：

![](http://static.zybuluo.com/coder-pig/4qgt0e4dlmyorgc98ojue1q1/2.png)

流程简述：

*   在 GitTest 文件夹中新建两个文件；
*   键入 git add -i，进入交互界面模式，键入 4，选择添加 untracked（未标记）的文件；
*   根据未标记文件的序号来添加文件，输入？会弹出相关提示，直接回车，结束选择；
*   键入 4，可以看到已经不存在 untracked 的文件了。

### 5. 让 Git 不 Tracked 特定文件「.gitignore 文件配置」

当我们使用 git add 命令把未标记的文件添加到缓存区后，Git 就会开始跟踪这个文件。  
对于一些比如：**自动生成的文件**，**日志**，**临时编译文件**，**应用签名文件等**，就没必要进行跟踪了，  
我们可以编写一个 **「.gitignore 文件」**，把不需要跟踪的文件和文件夹写上，git 就不会去  
跟踪这些文件了，另外：**.gitignore 文件与. git 文件夹在同级目录下 **。

如果不想自己写这个文件，可以到 [https://github.com/github/gitignore](https://github.com/github/gitignore) 选择对应的模板，复制粘贴。  
也可以自行编写，支持简化了的真这个表达式（规范与示例模板摘自：[Git 王者超神之路](http://www.jianshu.com/p/f4cd5f2d1a5f)）

*   `*` ： 匹配零个或多个任意字符
*   `[abc]`：只匹配括号内中的任意一个字符
*   `[0-9]`：代表范围，匹配 0-9 之间的任何字符
*   `?`：匹配任意一个字符
*   `**`：匹配任意的中间目录，例如 a/*/z 可以匹配: a/z,a/b/z,a/b/c/z 等

**模板示例**：

```
# 忽略所有以 .c结尾的文件
*.c

# 但是 stream.c 会被git追踪
!stream.c

# 只忽略当前文件夹下的TODO文件, 不包括其他文件夹下的TODO例如: subdir/TODO
/TODO

# 忽略所有在build文件夹下的文件
build/

# 忽略 doc/notes.txt, 但不包括多层下.txt例如: doc/server/arch.txt
doc/*.txt

# 忽略所有在doc目录下的.pdf文件
doc/**/*.pdf
```

**有一点要特别注意**！！！！

**配置. gitignore** 只对那些**没有添加到版本控制系统的文件生效** (**未 Tracked** 的文件)！

举个简单的例子：

有 A，B 两个文件，你先把他两个 add 了，然后在. gitignore 文件中  
配置了不跟踪这两个文件，但是你会发现根本不会生效。

```
git add A
git add B
# 配置不跟踪A和B
git add .gitignore
```

所以，最好的做法就是在项目刚开始的时候，先添加. gitignore 文件。  
当然，即使是发生了，还是有解决方法的，可以键入下述命令清除标  
记状态，然后先添加. gitignore，再添加文件即可：

```
git rm -r --cached .    # 清除版本控制标记，.代表所有文件，也可指定具体文件
```

另外，如果你用的 IDEA 系列的代码编辑器，可以安装一个「.ignore」的插件，手动  
勾选不需要跟踪的文件，直接生成. gitignore 文件。

### 6. 将暂存区的内容提交到本地仓库「git commit」

```
git commit -m "提交说明"    # 将暂存区内容提交到本地仓库
git commit -a -m "提交说明" # 跳过缓存区操作，直接把工作区内容提交到本地仓库
```

如果不加 - m “提交说明”，git 会让用你让默认编辑器 (vi 或 vim) 来编写提交说明。  
除此之外，有时可能想修改上次提交的内容：提交说明，修改文件等：

```
# 合并暂存区和最近的一次commit，生成新的commit并替换掉老的。如果缓存区没内容，
# 利用amend可以修改上次commit的提交说明。
# 
# 注：因为amend后生成的commit是一个全新的commit，旧的会被删除，所以别在公共的
# commit上使用amend！切记！！！

git commit --amend 
git commit --amend --no-edit # 沿用上次commit的提交说明
```

### 7. 查看工作区与缓存区的状态「git status」

```
git status      # 查看工作区与暂存区的当前情况
git status -s   # 让结果以更简短的形式输出
```

### 8. 差异对比（内容变化）「git diff」

```
git diff                     # 工作区与缓存区的差异
git diff 分支名              # 工作区与某分支的差异，远程分支这样写：remotes/origin/分支名
git diff HEAD               # 工作区与HEAD指针指向的内容差异
git diff 提交id 文件路径     # 工作区某文件当前版本与历史版本的差异
git diff --stage           # 工作区文件与上次提交的差异(1.6 版本前用 --cached)
git diff 版本TAG           # 查看从某个版本后都改动内容
git diff 分支A 分支B       # 比较从分支A和分支B的差异(也支持比较两个TAG)
git diff 分支A...分支B    # 比较两分支在分开后各自的改动

# 注：如果只想统计哪些文件被改动，多少行被改动，可以添加--stat参数
```

### 9. 查看历史提交记录「git log」

```
git log                 # 查看所有commit记录(SHA-A校验和，作者名称，邮箱，提交时间，提交说明)
git log -p -次数                # 查看最近多少次的提交记录
git log --stat                  # 简略显示每次提交的内容更改
git log --name-only             # 仅显示已修改的文件清单
git log --name-status           # 显示新增，修改，删除的文件清单
git log --oneline               # 让提交记录以精简的一行输出
git log –graph –all --online    # 图形展示分支的合并历史
git log --author=作者           # 查询作者的提交记录(和grep同时使用要加一个--all--match参数)
git log --grep=过滤信息         # 列出提交信息中包含过滤信息的提交记录
git log -S查询内容              # 和--grep类似，S和查询内容间没有空格
git log fileName              # 查看某文件的修改记录，找背锅专用
```

除此之外，还可以通过 –pretty 对提交信息进行定制，比如：

![](http://static.zybuluo.com/coder-pig/jhd3rupqiizkuc3ij4e9hnrg/3.png)

更多规则与定制如下（更多可参见：[Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)）  
format 对应的**常用占位符**：(注：作者是指最后一次修改文件的人，提交者是提交该文件的人)

```
提交对象（commit）的完整哈希字串
```

一些其他操作：

```
按补丁格式显示每个更新之间的差异
```

还有一些限制 log 输出的选项：

```
仅显示最近的 n 条提交
```

### 10. 查看某个文件是谁改动的「git blame」

```
git blame 文件名 # 查看某文件的每一行内容的作者，最新commit和提交时间
```

这里为了演示，先修改一波作者用户名和邮箱，然后往 1.txt 中新增内容：

![](http://static.zybuluo.com/coder-pig/yutey6uc60nzmjtyw3ax42if/4.png)

**Tip**：如果你用的 IDEA 系列的编译器，右键行号，选择 Annotate 也可以实现同样的效果。如：  
![](http://static.zybuluo.com/coder-pig/tpog2nudqnjy0fzyfcqe0nzg/image_1bp0rfk3s60k2g51cm61tuk1r5j2v.png)

### 11. 设置 Git 命令别名「git config –global alias」

在终端使用 Git 命令的时候，虽然可以通过按两次 tab 来自动补全。但是有些命令比较常用，  
每次都要敲完就显得有些繁琐了，可以为这些命令起一个简单的别名，比如：  
status 为 st，checkout 为 co ; commit 为 ci ; branch 为 br 等，设置示例如下：

```
git config --global alias.st status
```

![](http://static.zybuluo.com/coder-pig/zl9uex0yo6cpwnycslkauiu2/4.png)

别名的设置保存在 git 的配置文件中：

![](http://static.zybuluo.com/coder-pig/plbuftl3sutzehcpzd1vx4b1/6.png)

### 12. 为重要的提交打标签「git tag」

对于某些提交，我们可以为它打上 Tag，表示这次提交很重要， 比如为一些正式发布大版本的  
commit，打上 TAG，当某个版本出问题了，通过 TAG 可以快速找到此次提交对应的 Hash 值，  
直接切换到此次版本的代码去查找问题，比起一个个 commit 找省事多了。

Git 中的标签分为两种：**轻量级标签** 和 **附加标签**，命令如下：

```
git tag 标记内容                    # 轻量级标签
git tag -a 标记内容 -m "附加信息"    # 附加标签
```

如果想为之前某次 commit 打 TAG，可以找出此次提交的 Hash 值，添加 - a 选项，示例如下：

```
git tag -a 标记内容 版本id      # 比如：git tag -a v1.1 bcfed96
```

另外，git push 的时候默认不会把标签推送到远程仓库，如果想把标签页推送到远程仓库，可以：

```
git push origin 标记内容    # 推送某标签到远程仓库
git push origin --tags     # 删除所有本地仓库中不存在的TAG
```

除此之外还有下述常规操作：

```
git checkout -b 分支名 标记内容          # 新建分支的时候打上TAG
git show 标记内容                       # 查看标签对应的信息
git tag -d 标记内容                     # 删除本地TAG
git push origin --delete tag 标记内容   # 删除远程TAG
```

* * *

Git 文件恢复与版本回退
-------------

* * *

### 1. 文件恢复（未 commit）「git checkout」

如果在工作区直接删除已经被 Git Tracked 的文件，暂存区中还会存在此文件：

![](http://static.zybuluo.com/coder-pig/mrrbux6w7kt03tji2csf1jtc/2.png)

Git 告诉你，工作区的文件被删除了，你有两种可选操作：「**删除缓存区文件**」 或 「**恢复被删文件**」：

```
# 删除暂存区中的文件：
git rm 文件名
git commit -m "提交说明"

# 误删恢复文件（用暂存区的文件覆盖工作区的文件）
git checkout -- 文件名

# Tip：git rm 等价于 git rm --cached 文件名 + rm 文件名
# 务必注意：git checkout会抛弃当前工作区的更改!!!不可恢复！！！务必小心！！！
```

### 2. 文件恢复（已 add 未 commit）「git reset HEAD」

如果更改已经 add 到暂存区中，想恢复原状，可以执行下述命令：

```
git reset HEAD 文件名   
git checkout 文件名
```

### 3. 版本回退（已 commit）【git reset –hard】

文件已经 commit，想恢复未上次 commit 的版本或者上上次，可以：

```
git reset HEAD^             # 恢复成上次提交的版本
git reset HEAD^^            # 恢复成上上次提交的版本，就是多个^，以此类推或用
git reset HEAD~3            # 也可以直接~次数
git reset --hard 版本号      # git log查看到的Hash值，取前七位即可，根据版本号回退
```

reset 命令的作用其实就是：**重置 HEAD 指针，让其指向另一个 commit**，而这个动作可能会对  
缓存区造成影响，举个例子：

本来的分支线：**- A - B - C (HEAD, master)**，git reset B 后：**- A - B (HEAD, master)**  
解释：看不到 C 了，但是他还是存在的，可以通过 git reset C 版本号找回，前提是  
C 没有被 Git 当做垃圾处理掉 (一般是 30 天)。

**reset 提供了三个可选参数**：

*   **soft**：只是改变 HEAD 指针指向，缓存区和工作区不变；
*   **mixed**：修改 HEAD 指针指向，暂存区内容丢失，工作区不变；
*   **hard**：修改 HEAD 指针指向，暂存区内容丢失，工作区恢复以前状态；

### 4. 查看输入过的指令记录「git reflog」

Git 会记住你输入的每个 Git 指令，比如上面的 git reset 切换成一个旧的 commit，然后  
git log 后发现新提交的记录没了，想切换回新的那次 commit， 可以先调 git reflog  
获取新 commit 的 Hash 值，然后 git reset 回去。

```
git reflog
```

![](http://static.zybuluo.com/coder-pig/poc5yulnsj258h7xw4it10ip/1.png)

**注**：指令记录不会永久保存！Git 会定时清理用不到的对象！！！

### 5. 撤销某次提交「git revert」

有时可能我们想撤销某次提交所做的更改，可以使用 revert 命令

```
git revert HEAD             # 撤销最近的一个提交
git revert 提交的Hash值     # 撤销某次commit
```

![](http://static.zybuluo.com/coder-pig/uljdgp8z1hy35qlkinx0ry4r/2.png)

**注意**！！！

不是真的把提交给撤销了，而是生成一个新的提交来覆盖旧的提交，被撤销的提交  
和新的提交记录都会保存！！！如果不信的话，你可以再键入 git revert HEAD，  
会发现被撤销的更改又变回来了。简单点说：「**撤销的只是文件变化，提交记录依旧存在**」。

### 6. 查看某次提交的修改内容「git show」

```
git show 提交Hash值     # 查看某次commit的修改内容
```

### 7. 查看分支最新 commit 的 Hash 值「git rev-parse」

```
git rev-parse 分支名    # 查看分支最新commit的Hash值，也可以直接写HEAD
```

### 8. 找回丢失对象的最后一点希望「git fsck」

因为你的某次误操作导致 commit 丢失，如果 git reflog 都找不到，你可以使用 **git fsck**，找到丢失  
的对象的版本 Hash 值，然后恢复即可。

```
git fsck --lost-found
```

![](http://static.zybuluo.com/coder-pig/1fvcdmqolanlgsn1oyhjsjml/3.png)

* * *

0x4、Git 本地分支
------------

* * *

### 1. 分支的概念

分支并不是 Git 对象，和轻量级的 TAG 对象类似，只包含对 commit 对象的索引。只是分支更新后，  
索引会替换为最新的 commit，而 TAG 对象创建后索引就不在变化。分支文件保存与下述两个路径：

*   **本地分支**：`当前项目/.git/refs/heads/`
*   **远程分支**：`当前项目/.git/refs/remotes/`

说到分支，必然会提及 **HEAD**，它指向「**当前工作的本地分支**」，对应文件：`当前项目/.git/HEAD`

![](http://static.zybuluo.com/coder-pig/vcwj6c0h5hb6xpjzbyr1s3n8/4.png)

下面通过示例和图解的方式帮大家理解分支：

![](http://static.zybuluo.com/coder-pig/5ozf28vnfz7376x4u6tfa6ec/11.png)

![](http://static.zybuluo.com/coder-pig/7elzmle1q6svxjov0gjzg8hu/22.png)

如法炮制，提交两次：

![](http://static.zybuluo.com/coder-pig/t8v68thkiigqh8u3tcqsp4f6/33.png)

从上面的图中不难发现这样的规律：**每次 commit，master 都会向前移动，指向最新提交**。  
这个时候可能有些童鞋会问：**commit 之间的箭头哪来的**？**或者说 commit 怎么串成一条线的**？

> 答：还记得一开始介绍的 **commit 对象**吗？里面**有一个 parent 的值**，**指向父 commit 的 Hash 值**。

### 2. 创建其他分支的原因

通过两个常见的场景来体会创建其他分支的必要性：

*   **场景一**：

项目一般都是一步步迭代升级的，有大版本和小版本的更新： 大版本一般是改头换面的更新，比如  
UI 大改，架构大改，版本是： v2.0.0 这样；小版本的更新一般是 UI 小改，Bug 修复优化等，版本是：  
v2.0.11 这样；只有一条 master 分支，意味着：你的分支线会 非常非常的长，假如你已经发布到了  
第二个大版本，然后用户反馈第一个版本有很严重的 BUG，这时候想切回第一个版本改 BUG，  
然后改完 BUG 切回第二个大版本，想想也是够呛的。 (PS：可能你说我可以对重要的 commit 打 tag，  
然后找到这个 tag 切回去，当然也行这里是想告诉你引入其他分支会给你带来的便利)

*   **场景二**：

如果只有一个 master 分支的话，假如某次 commit 冲突了，而这个冲突很难解决或者解决不了，  
那么整个开发就卡在这里，无法继续向后进行了。

### 3. 一个简单的分支管理策略

为了解决只有一个 master 分支引起的问题，可以引入分支管理，最简单的一种策略如下：

在 **master 分支**上开辟一个新的 **develop 分支**，然后我们根据功能或者业务，再在 develop  
分支上另外**开辟其他分支**，完成分支上的任务后，再将这个分支合并到 develop 分支上！  
然后这个功能分支的任务也到此结束，可以删掉，而当发布正式版后，再把 develop 分支  
合并到 master 分支上，并打上 TAG。

**master 与 develop** 分支都作为**长期分支**，而其他创建的分支作为**临时性分支**！  
简述各个分支的划分：

*   **master 分支**：可直接用于产品发布的代码，就是正式版的代码
*   **develop 分支**：日常开发用的分支，团队中的人都在这个分支上进行开发
*   **临时性分支**：根据特定目的开辟的分支，包括**功能 (feature) 分支**，或者**预发布 (release) 分支**，  
    又或者是**修复 bug （fixbug）分支**，当完成目的后，把该分支合并到 develop 分支，  
    然后删除该分支，使得仓库中的常用分支始终只有：**master 和 develop 两个长期分支**！

### 4. 分支创建与切换「git branch」

```
git branch 分支名    # 创建分支
git branch          # 查看本地分支
```

我们在 master 分支上创建一个 develop 分支，此时的版本线变成了这样：

![](http://static.zybuluo.com/coder-pig/l3i5vh3lcyewrncuhvynobf6/44.png)

此时虽然已经创建了 develop 分支，但是 HEAD 还是指向 master，接着我们来切换分支：

```
git checkout 分支名         # 切换分支
git checkout -b 分支名      # 创建分支同时切换到这个分支
```

![](http://static.zybuluo.com/coder-pig/kufxtbnye17n402ms7n7abo3/55.png)

切换到 develop 后，提交一次，此时的版本线：

![](http://static.zybuluo.com/coder-pig/aljd611odsysbyffa2wktieq/66.png)

再提交一次，然后切换为 master 分支，此时的版本线：

![](http://static.zybuluo.com/coder-pig/qqadeudplluaf1t6xjmel09j/77.png)

切换回 master 后，提交一次，此时的版本线：

![](http://static.zybuluo.com/coder-pig/lphi996ig8rhw300wvxo4yum/111.png)

行吧，讲到这里，相信各位童鞋对 Git 中的分支已经有所了解了。

### 5. 分支合并「git merge」 VS 「git rebase」

Git 中，可以使用「**git merge**」和「**git rebase**」两个命令来进行分支的合并。

**git merge 合并分支**

合并的方式分为两种：**快速合并** 和 **普通合并**，两者的区别在于：  
「**前者合并后看不出曾经做过合并，而后合并后的历史会有分支记录**」  
如图所示：

![](http://static.zybuluo.com/coder-pig/aaou8a7t834nsuh25fqwu467/9.png)

**快速合并**，默认，快速合并有一个前提：「**当前分支的每个提交都在另一个分支中**」，  
Git 不创建任何新的 commit，只是将当前分支指向合并进来的分支。下面演示下快速合并，  
执行 git reset 切换到第四次 commit，然后执行 git merge develop 合并 master 分支。

![](http://static.zybuluo.com/coder-pig/hgysoc5o7nlck07t45pfu3p7/1.png)

**普通合并**，添加 **–no-ff** 参数表示禁用快速合并。

![](http://static.zybuluo.com/coder-pig/we3grpf0jb6eeakwb7abw4x8/2.png)

另外有时会有这样的场景：合并的分支中有很多 commit 记录是无需在分支中体现的，一个 commit  
就够了。可以借助 **–squash** 参数来压缩提交，示例如下：

![](http://static.zybuluo.com/coder-pig/qpqs0638r97wwf594mzvhfn3/4.png)

附：git merge 的常用参数：

```
git merge -ff           # 快速合并，默认参数
git merge -ff-only      # 只有快速合并的情况才合并
git merge --no-ff       # 不使用快速合并
git merge -n 分支名     # 合并分支，不会在合并后显示合并前后的不同状态
git merge -stat 分支名  # 合并分支，合并结束后显示合并前后的不同状态
git merge -e 分支名     # 合并分支，合并前调用编辑器，可自行编写commit
```

> **Tips**: git-merge 除了用来合并分支外，拉取远程仓库更新时也可用到（git fetch + git merge）

**git reabse 合并分支**

rebase（衍合，变基），网上很多教程写得很高深莫测，其实并没有那么复杂，  
只是这种合并会让树整洁，易于跟踪。以上面 4 中的结果为例，先把 master 分支  
和 develop 分支重置到最新的 commit。

![](http://static.zybuluo.com/coder-pig/c9cxpbdk60gvuhxlqw2e7htn/1.png)

先走一波前面的 merge 合并方式：

![](http://static.zybuluo.com/coder-pig/28gre12ik08eeau8limj4qou/1.png)

接着再试试 rebase 合并方式：

![](http://static.zybuluo.com/coder-pig/k3eqo0ydz48cwwowuvcnm1iq/2.png)

Git 会把每个提交都取消掉，并把他们临时保存为补丁，比如经过一些冲突解决，生成新的 commit，  
旧的 commit 会被丢弃，还会被 git 的 gc 回收，这样的结果就是一条直线的树。

### 6. 解决合并冲突

在分支的合并的时候，并不是每次都能直接合并的，有时会遇到合并冲突，特别是在多人协作的时候。  
出现合并冲突后，需要解决完冲突，才能继续合并。

举个简单的例子，A 和 B 在 master 分支上开辟出两个分支来完成相关的功能，  
A 做完了，把自己的分支合并到 master 分支，此时 master 分支向前移动了几次 commit，  
接着 B 也完成了他的功能，想把自己分支合并到 master 分支，如果改动的文件和和 A 改动  
的文件相同的话，此时就会合并失败，然后需要处理完冲突，才能够继续合并！

接下来我们来简单的模拟合并冲突，先来试试 merge：

**merge 分支后处理冲突**

![](http://static.zybuluo.com/coder-pig/eh920smf7p083fuuqwjs85qh/1.png)

如图，合并完 A 分支后合并 B 分支出现了冲突，接着键入：git status 查看冲突的文件：

![](http://static.zybuluo.com/coder-pig/0fqfo6q6m3yemw4fhy3yffma/2.png)

可以看到未合并的两个文件，1.txt 和 2.txt，打开其中一个文件：

![](http://static.zybuluo.com/coder-pig/l8aoa2athrxcyhomjildvccd/2.png)

<<<和>>> 包裹着的就是冲突内容，保留自己想要的内容，处理完后删掉 <<< 和 >>>，修改完后：

![](http://static.zybuluo.com/coder-pig/dmb34s45ver4u3bvmmvvc530/3.png)

2.txt 文件也如法炮制，接着 add，然后 commit 即可，合并结束。

![](http://static.zybuluo.com/coder-pig/uzkrr7k23r02ekkhjqovop6h/3.png)

**rebase 分支后处理冲突**

![](http://static.zybuluo.com/coder-pig/cizigcyjry44xgpnlpb3zjpl/1.png)

如图，A 合并成功，在合并 B 的时候，出现了合并冲突，有三个可选的操作：

```
git rebase --continue # 处理完冲突后，继续处理下一个补丁
git rebase --abort # 放弃所有的冲突处理，恢复rebase前的情况
git rebase --skip # 跳过当前的补丁，处理下一个补丁，不建议使用，补丁部分的commit会丢失！
```

键入 git status 查看冲突文件：

![](http://static.zybuluo.com/coder-pig/08dfzmviuczpykztlxiukes0/1.png)

接着处理 1.txt 文件中的冲突，解决完成后，先键入 git add，接着键入 **git rebase --continue**  
处理下一个冲突：

![](http://static.zybuluo.com/coder-pig/61xondo6mgfuv618x63pbxte/2.png)

处理接下来的冲突，直到没有冲突为止：

![](http://static.zybuluo.com/coder-pig/aib8lwxf8k91kgrngi7ij4y9/3.png)

可以看到使用 rebase 合并，最后的分支线是一条直线。另外，使用 rebase 合并中途出差错，  
可以使用 git rebase --abort 恢复 rebase 前的状态。

### 7. 删除分支

合并完的分支，基本没什么用了，可以使用下述命令删除：

```
git branch -d 分支名    # 删除分支，分支上有未提交更改是不能删除的
git branch -D 分支名    # 强行删除分支，尽管这个分支上有未提交的更改
```

### 8. 恢复误删分支

两步：找出被删分支最新的 commit 的 Hash 值，然后恢复分支：

```
git log --branches="被删除的分支名"     # 找到被删分支最新的commit版本号
git branch 分支名 版本号(前七位即可)    # 恢复被删分支
```

### 9. 切换分支时暂存未 commit 的更改「git stash」

有时我们可能在某个分支上正编写着代码，然后有一些突发的情况，需要 我们暂时切换到  
其他分支上，比如要紧急修复 bug，或者切换分支给同事 review 代码，此时如果直接切换  
分支是会提示切换失败的，因为这个分支 上做的更改还没有提交，你可以直接 add 后 commit，  
然后再切换，不过我们习惯写完某个功能再提交，我们想：

> **先暂存这个分支上的改动**，切去其他分支上搞完事，然后回来继续  
> 继续在之前的改动上写代码。

那么可以使用：

```
git stash   # 保存当前的改动
```

然后放心的切换分支，然后再切换回来，接着使用：

```
git stash apply     # 恢复保存改动
```

另外有一点一定要注意！！！可以 stash 多个改动！！如果你切换到另一个分支  
又 stash 了，然后切换回来 stash apply 是恢复成另一个分支的 stash！！！  
如果你这样 stash 了多次的话，我建议你先键入：

```
git stash list      # 查看stash列表
```

找到自己想恢复的那个

![](http://static.zybuluo.com/coder-pig/wrz9x1032skwg2fo8zvbqqbv/1.png)

比如这里恢复的应该是 master 上的 stash，可以使用下述命令进行恢复：

```
git stash apply stash@{1}
```

### 10. 分支重命名

```
git branch -m 老分支名 新分支名     # 分支重命名
```

### 11. 把提交的 commit 从一个分支放到另一个分支「git cherry-pick」

有时我们可能需要把某个分支上的一次 commit 放到另一个分支上，此时可以使用 **git cherry-pick**，  
比如下面这样两个分支：

master 分支：A -> B -> C  
feature 分支：a -> b

现在想把 feature 分支上的 b，放到 master 的后，可以这样操作：

*   **Step 1**：切换到 feature 分支上，git log 拿到 b commit 的版本号 (SHA1)。
*   **Step 2**：切换到 master 分支，键入：git cherry-pick 版本号。

![](http://static.zybuluo.com/coder-pig/ojh7sqqaxnn2pguwxpbae3ha/2.png)

* * *

0x5、Git 远程仓库
------------

* * *

### 1. 远程仓库概述

在实际开发过程中，基本都是团队协作的形式进行，即多人一起负责同一个项目，那如何共享同一份代码并进行管理呢？可以用到「**Git 远程仓库**」。可以自己搭建，或选择专业的代码托管平台，比如：**Github，Git@OSC，GitCafe，GitLab，coding.net，gitc，BitBucket，Geakit，Douban CODE 等**。当然，如果有条件的话，肯定是自己搭建的爽一些，可控，还可以做一些订制 (集成编译，机器人提醒等)，简单点的可以试试「**Gogs**」，可玩性更高的可以试试「**GitLab**」。

### 2. 本地仓库与远程仓库建立关联「git remote」

在 Github 上新建了一个项目仓库，会生成对应的仓库链接，如：

![](http://static.zybuluo.com/coder-pig/sja2klqrocavj2arnhwcqgz9/image_1e45lk08ccmoe8geabbvctco9.png)

键入下述命令进行关联：

```
git remote add origin 远程仓库地址
```

接着可键入下述命令查看关联情况：

```
git remote      # 列出已经存在的远程分支
git remote -v   # 查看远程仓库的地址
```

![](http://static.zybuluo.com/coder-pig/yekmvhkss1wlqv09g36lbyuf/image_1e45m4fgipbntnsfeq87aiq16.png)

### 3. 推送本地仓库到远程仓库「git push」

建立完关联后，我们可以使用 git push 命令把本地更改推送到远程仓库

```
git push -u origin master
```

**-u 参数**：作为第一次提交使用，作用是把**本地 master 分支和远程 master 分支**关联起来 (设置默认远程主机)，后续提交不需要这个参数！

![](http://static.zybuluo.com/coder-pig/w6cdddvfhzcm2k7sfmbv6xei/image_1e45mbkm5cph12kdqoo6s18vu1j.png)

另外，如果想修改远程仓库地址，可通过下述命令：

```
# 直接修改远程仓库地址
git remote set-url origin 远程仓库地址

# 也可以先删除origin后再添加
git remote rm origin               # 删除仓库关联
git remote add origin 远程仓库地址   # 添加仓库关联
```

你还可以直接修改「**.git 文件夹中的 config 文件**」，直接替换圈住位置内容即可：

![](http://static.zybuluo.com/coder-pig/vo67g5e8k77zrkt35ga6kv1p/image_1e45mfvgk1vrh1gb1o801tgmhe820.png)

还有一点：「**origin**」并不是固定的东西，只是后面「**仓库地址的一个别名**」！！可以写成其他的东西，然后你也**可以设置多个仓库关联**，用不同的别名标志，比如：

```
git remote add github https://github.com/coder-pig/SimpleTea.git
git remote add osc git@git.oschina.net:coder-pig/SimpleTea.git
```

### 4. 克隆远程仓库「git clone」

把项目推送到远程仓库后，其他开发者就可以通过 git clone 命令把项目克隆到本地

```
git clone 仓库地址          # 克隆项目到当前文件夹下
git clone 仓库地址 目录名    # 克隆项目到特定目录下

# 注：git clone命令只会建立master分支，如果想克隆特定远程分支，可在克隆后：
git checkout -t origin/dev 

# 该命令等同于
git checkout -b dev origin/dev

# 除此之外，还可以：
git fetch origin 远程分支:本地分支 # 会在本地新建分支，但不会自动切换，还需checkout
git branch --set-upstream 本地分支 远程分支 # 建立本地分支与远程分支的链接
```

### 5. 同步远程仓库更新「git fetch」VS 「git pull」

获取远程仓库更新的方法有两种：**fetch** 和 **pull**，简要讲解下两者的区别：

*   **git fetch**

> 仅仅只是从远处服务器获取到**最新版本到本地**，假如你不去合并 (**merge**)，本地工作空间是不会发生变化的！比如：在 Github 上创建一个 README.md 文件，然后调 **git fetch** 去获取远程仓库的更新。

![](http://static.zybuluo.com/coder-pig/ryvaxobvgt6badn0zvcesetl/image_1e45qp7na1hd61jmi1ho9uph1kht2d.png)

*   **git pull**

> 一步到位，**pull = fetch + merge**，比如：同样修改 Github 上的 README.md 文件，然后 git pull 同步远程仓库的更新:

![](http://static.zybuluo.com/coder-pig/f1a0fz92itadtmbumcepq4y3/image_1e45qqs6n1aun55n7v9seg5kl2q.png)

区别显而易见，使用 git fetch 会更安全一些，毕竟 merge 的时候，查看更新的情况，再决定是否进行合并。

### 6.git push 时的 unrelated history 问题

在 Github 创建新项目后，在 repo 处创建了 README.md 或其他文件，然后关联本地仓库，push 时会报错：  
Push rejected: Push to origin/master was rejected，然后提示你 pull 一下，当你 pull 时又会报错：  
「**refusing to merge unrelated histories**」，原因是两个仓库不同导致的，可使用下述命令解决：

```
git pull origin master --allow-unrelated-histories
```

除此之外，你还可以粗暴一点，直接用本地仓库「**强制覆盖远程仓库**」，但是 **慎用**！！！如果出问题了，只能看下其他人的电脑中是否有原始的本地仓库进行还原！！！

```
git push -f origin  # 慎用！！！
```

### 7.SSH Key 避免每次 push 重复输入账号密码

私有项目，使用 Https 协议 pull 或 push，都需要验证账号和密码，有点繁琐，如果想避免这种重复输入的情况，可以考虑使用 **SSH** 协议。SSH，Secureshell(安全外壳协议)，专为远程登陆会话与其他网络服务提供安全性的协议，而 SSH 传输的数据是可以经过压缩的，可以加快传输的速度，出于安全性与速度，优先考虑使用 SSH 协议，而 SSH 的安全验证规则又分为基于**密码**和基于**密钥**两种！这里使用的是第二种，即在本地创建一对密钥「**公钥 (id_rsa.pub) 和私钥(id_rsa)**」然后把公钥内容贴到远程仓库设置中的 ssh keys 中，从而建立本地与远程的认证关系。配置 SSH Key 的流程如下：

*   ① 来到电脑的根目录下 (假设还没创建过 SSH key)：

![](http://static.zybuluo.com/coder-pig/0wtobc65tfrgpc1ir9l7zryk/image_1e45sobhv16o316mjoqfs49cku37.png)

执行完 **ssh-keygen** 那个指令后，后面依次要你输入文件名  
**直接回车** → 会生成两个默认的秘钥文件，接着提示输入密码，  
**直接回车** → 如果这里你输入密码了的话，那么 push 的时候你还是需要输入密码，接着又输多一次密码  
**直接回车** → 出现最下面的这串东西就说明 ssh key 已经创建成功了！  
接着可以用编辑器打开 **id_rsa.pub** 文件或者键入下述命令复制内容:

```
clip <id_rsa.pub
```

打开 Github，点击头像，选择：**Settings**，然后点击左侧 **SSH Keys**, 然后 **New SSH Key**

![](http://static.zybuluo.com/coder-pig/0kx50nrxa79xk3pxnvawc1mh/image_1e45suj5clko4j0f8jt9o1fmt3k.png)

然后 Github 会给你发来一个提示创建了一个新 ssh key 的邮件，无视就好，接下来我们可以键入:

```
**ssh -T git@github.com**
```

然后如果上面设置过密码则需要输入密码，否则直接输入 yes 然后一直按回车就好！，最后出现 Hi xxx 那句话就说明 ssh key 配置成功了！

![](http://static.zybuluo.com/coder-pig/9h36gjhy66i3bakw4ethvct6/image_1e45t0pe015j5und1i9mmo51cc041.png)

其他远程仓库配置方法类似，另外如果想一个电脑管理多个 SSH-Key，可移步至：

[《Git 拾遗：一机多 SSH-Key 管理》](https://juejin.im/post/5ae9cb26f265da0b873a5185)

* * *

0x6、Git 工作流
-----------

* * *

关于 Git 工作流，Github 上有一篇图文并茂写得很好的文章，就不细说了，只是简单介绍下，更多详情可见：[《Git Workflows and Tutorials》](https://github.com/oldratlee/translations/tree/master/git-workflows-and-tutorials)

### 1. 集中式工作流

类似于 SVN，不过只有一条 master 分支，然后一群人就在这条分支上嗨，比如有小 A 和小 B：

*   1. 项目管理者初始化仓库，然后推到远程仓库
*   2. 其他人克隆远程仓库项目到本地
*   3. 小 A 和小 B 完成各自的工作
*   4. 小 A 先完成了，git push origin master 把代码推送到远程仓库
*   5. 小 B 后完成了，此时推送代码到远程仓库，出现文件修改冲突
*   6. 小 B 需要先解决冲突，git pull –rebase origin master，然后 rebase 慢慢玩
*   7. 小 B 把冲突解决后，git push origin master 把代码推送到远程仓库

### 2. 功能分支工作流

和集中式分部流相比只是分支再不是只有 master，而是根据功能开辟新的分支而已，示例如下：

> *   1. 小 A 要开发新功能，git branch -b new-feature 开辟新分支

*   2. 小 A 在 new-feature 上新功能相关的编写，他可以这个分支推到远程仓库
*   3. 功能完成后，发起请求 pull request(合并请求)，把 new-feature 合并到 master 分支
*   4. 仓库管理员可以看到小 A 的更改，可以进行一些评注，让小 A 做某些更改，  
    然后再发起 pull request，或者把 pull request 拉到本地自行修改。
*   5. 仓库管理员觉得可以了，合并分支到 master 上，然后把 new-feature 分支删掉

**注**：这里的仓库管理者是拥有仓库管理权限的人

### 3.Gitflow 工作流

其实就是功能分支工作流做了一些规范而已，大概流程参见上面「**一个简单的分支管理策略**」

### 4.Forking 工作流

分布式工作流，每个开发者都拥有自己独立的仓库，为开源项目贡献代码常用，把项目 fork 到自己的远程仓库，完成相应更改，然后 pull request 到源仓库，源仓库管理者可以决定是否合并。

### 5.Pull Request 工作流

和 Forking 工作流类似，Pull Requests 是 Bitbucket 上方便开发者之间协作的功能

* * *

0x7、其他杂项
--------

* * *

### 1. 为开源项目贡献代码

你可以 Clone 别人的开源项目，在看别人代码的时候，觉得作者某些地方写得不好，写错，或者你有更好的想法，在本地修改后，想把修改 push 推送到开源项目上，是无法直接 Push 推送更改的。参与开源项目的方式有两种：

*   **方法一**：  
    是让作者把你加为写作者，添加协作者流程：  
    点击仓库的 **Settings** → **Collaborators** 然后输入想添加的人的用户名或者邮箱，点击  
    添加即可。
    
*   **方法二**：  
    点击 Fork 按钮，把这个项目 **fork** 到自己的账号下，然后 **Clone** 到本地，然后做你想做的修改，**commit** 提交，然后 **push** 到自己账号里的仓库，然后打开开源项目，点击，然后新建一个「**pull request**」，接着设置自己的仓库为源仓库，**设置源分支，目标仓库与目标分**支，然后还有 **pull request 的标题和描述信息**，填写完毕后，确定。  
    这个时候开源项目的作者就会收到一个 pullrequest 的请求，由他来进行审核，作者审查完代码觉得没问题的话，他可以点击一下 **merge** 按钮即可将这个 pull request 合并到自己的项目中，假如作者发现了你代码中还有些 bug，他可以通过 Pull Request 跟你说明，要修复了 xxBUG 才允许合并，那么你再修改下 BUG，提交，更改后的提交会进入 Pull Request，然后作者再审核这样！
    

**Tips**：o(╯□╰)o 假如作者不关闭或者 merge 你的这个 Pull Request，你可以一直 commit 骚扰主项目…

### 2.SourceTree 使用详解

命令行虽酷炫可装逼，但是有时用图形化工具还是能提高不少效率的，安利个巨好用的 Git 图形化工具 **SourceTree**，官网下载地址：[https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/)，网上教程满天飞，笔者也不粘贴复制了，找到个写得还行的，有兴趣可移步至：[《用 SourceTree 轻松 Git 项目图解》](https://blog.csdn.net/zcube/article/details/47841175)。

* * *

后面有新的会更新，待续…

* * *

**参考文献与更多 Git 学习资料**：

*   [Pro Git 中文版](https://0532.gitbooks.io/progit/content/ff1ccf57e98c817df1efcd9fe44a8aeb/c3c2acea22ea3f6a535ba0d2c45980bb.html)
*   [Git 背后的 object](https://blog.csdn.net/i_enum/article/details/50557367)

* * *