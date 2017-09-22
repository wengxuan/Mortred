## git常用命令

### 初始化仓库的两种方式

`git init`
`git clone`

### 添加文件到暂存区

`git add git-base_command.md`

`git add`添加到暂存区的文件又进行了修改的话，需要重新add

### 查看当前文件状态

`git status`输出的信息比较繁琐

`git status -s` 更为紧凑的输出格式

	$ git status -s
	 M README               // 右M，修改了，未放入暂存区
	MM Rakefile             // 左右M，修改放入暂存区后又进行了修改
	A  lib/git.rb           // A，新添加到暂存区的文件
	M  lib/simplegit.rb     // 左M，修改并放入暂存区了
	?? LICENSE.txt          // ??，新添加未跟踪的文件

### 提交更新

`git commit -m "commit message"`

### 跳过使用暂存区

觉得使用暂存区繁琐，想要直接提交，给 git commit 加上 -a 选项，Git 就会自动把所有**已经跟踪过的文件**暂存起来一并提交

`git commit -a -m "commit message"`

### 移除文件

`git rm log/\*.log`

注意到星号 * 之前的反斜杠 \， 因为 Git 有它自己的文件模式扩展匹配方式，所以我们不用 shell 来帮忙展开。 此命令删除 log/ 目录下扩展名为 .log 的所有文件。

`git rm \*~`

删除以 ~ 结尾的所有文件



