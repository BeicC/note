# Linux
* man
    * 背景
    Linux里面有很多命令，如何了解一个命令该怎么使用？
    * 分类
    Linux将各种命令分为了9类，分别为：
    1、常见命令的说明
    2、可调用的系统
    3、函数库
    4、设备文件
    5、文件格式
    6、游戏说明
    7、杂项
    8、系统管理员可用的命令
    9、与内核相关的说明
    查看reboot命令在哪个分类下：`man -f reboot`；
    然后就可以使用`man 2 reboot`查看系统调用的reboot；
    使用`man 8 reboot`查看系统管理中的reboot
* `ll`是什么
`ll`是`ls -alF'`的别名（alias），可在Linux输入`type ll`查看；
也可通过`alias`命令查看有哪些别名
* `cp`:(copy)
```sh
cp a.txt /dev/a.txt # 将当前目录下的a.txt复制到dev目录下的a.txt
cp -r test1 test2 # 想要复制目录，需要加上-r
```
* `mv`(move)
```sh
mv a.txt /mnt/ # 会把当前目录中的a.txt移动到/mnt目录下；当前目录就没有a.txt了
mv a.txt a.doc # 把a.txt文件改名为a.doc
```
* `rm`:(remove)
```sh
rm a.txt # 删除a.txt文件
rm -r dir/ # 使用rm命令删除一个文件夹
rmdir dir/ # rmdir命令只能删除空文件夹
rm -rf dir/ # 使用rm命令删除一个文件夹，并且一路yes
```
* ssh
    * 通过windows远程连接：`ssh ubuntu@192.168.222.3`
    * 为什么需要xshell这种软件？
    如果同时操作多台服务器的话，在cmd中使用ssh就不太方便了；每次都要登录，退出。
    * 为什么需要xftp这种软件？
    如果涉及本电脑与服务器之间的文件传输，当然自己可以通过cmd通过ssh连接服务器，在通过scp命令进行文件传输。但是通过xftp，文件的传输只需要简单的拖拽
* gcc
    * `gcc --help`
# Idea
* 重写父类方法：CTRL+o
* 自动补全new Thread前面的 ：alt+enter
* 选中当前单词：ctrl+w
* 在当前行上面加一行：ctrl+alt+enter；在当前行下面加一行：shift+enter
* try-catch快捷键：选中代码，ctrl+alt+t
# VScode
|快捷键|作用|
|-|-|
|ctrl+L|选中当前行|
|shift+alt+↑|向下/上复制一整行|
|Ctrl+d|选中当前单词|
|Home|一键回到当前行的头部|
|End|一键回到当前行的尾部|
|Ctrl+enter|在当前行下插入一行|
|Ctrl+shift+enter|在当前行上插入一行|
|Ctrl+Alt+↓|选中多行|
* vscode逐个替换
[link](https://blog.csdn.net/fantasyYXQ/article/details/125607352)
* 代码自动对齐
shift+alt+f
# Markdown Preview Enhanced 
* [link](https://blog.csdn.net/while0/article/details/124677531?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-124677531-blog-94321593.pc_relevant_3mothn_strategy_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-124677531-blog-94321593.pc_relevant_3mothn_strategy_recovery&utm_relevant_index=10)
* esc：在vscode预览模式下显示目录

# Git
some questions
> 1、为什么git bash可以git clone，但cmd git clone却会failed？
## 本地
* `git status`
git status会比较工作区、暂存区、版本库
```bash
# 三者都一样
On branch master
nothing to commit, working tree clean
# 如果工作区和暂存区不一样
Changes not staged for commit:
# 如果暂存区和版本库不一样
Changes to be committed:
```
* `git add`
新创建的文件git是不会管理的，通过`git add`操作给这个文件‘打上标记’，git就可以管理了
* `git commit`
    * `git commit -m "输入简短的提交信息"`
* `git log`
```sh
git log --oneline # 将提交记录显示为一行
```
* 分支
    * 查看分支：`git branch`
    * 切换到feature1分支：`git switch feature1`
    * `git branch bugFix`:创建新的分支：bugFix
    * `git checkout bugFix`:切换到bugFix分支
    * `git checkout -b bugFix`:创建新的分支bugFix并切换到bugFix
    * `git merge newfeature`:将newfeature分支合并到当前所在的分支
    * `git branch --delete xx`:删除分支
* `git merge`
```bash
git merge feature1  # 此时我站在master分支上：将feature1分支 merge into master 分支
```
如果没有冲突，则自动合并，如果有冲突，显示如图,需要手动解决
<img src="./git/conflict.PNG">
* `git diff`
    * git diff是比较工作区和暂存区之间的区别
    * git diff 怎么看？
    ```shell
    $ git diff
    diff --git a/src/a.txt b/src/a.txt
    index a996bf8..41d731c 100644
    --- a/src/a.txt
    +++ b/src/a.txt
    @@ -1,3 +1,5 @@
    v1
    v2
    -v3
    \ No newline at end of file
    +v7
    +v4
    +v5
    \ No newline at end of file
    #============================================
    v1，v2前面没有-或者+，表示比较文件所共有的部分
    前面-，表示原来的文件独有的（在暂存区的）
    前面+，表示新修改文件独有的（在工作区的）
    所以：
    v1         v1
    v2  ->     v2
    v3         v7
               v4
               v5
    ```
* `git reset`
```sh
git reset # 在git add之后使用git reset，将被修改的暂存区恢复到git add之前的状态
git reset --hard # 撤销工作区中的所有修改，将工作区返回上一次刚刚commit之后的状态
git reset --hard <提交ID> #将工作区返回到某次commit之后的状态
```
* `git rm`
```bash
git rm a.c 
# 使用该条命令的前提是working tree clean
# 使用该条命令的结果是：暂存区中的文件被删除，工作区的文件也被删除，需要commit一下

# 如果只想删除暂存区中的文件，保留本地文件，需要加上--cached选项
git rm --cached a.c

# 常用的命令，直接删除对a.c文件的追踪，但保留本地文件
git rm -f --cached a.c
```
* `.gitignore`
直接在.git同级目录下新建`.gitignore`文件
怎么写：[link](https://www.w3schools.com/git/git_ignore.asp?remote=github)
.gitignore只能在文件untrack时有效，如果某个文件已经被`git add`了甚至`git commit`了，那需要先`git rm`后才会生效
* 当工作区与暂存区不一致是：`Changes not staged for commit:`,只有他俩一样才能commit
通过`git add`将工作区中的文件添加到暂存区
通过`git rm`将暂存区的文件删除
他们的目的都是使工作区和暂存区一致，然后好commit
* 我不小心把一些没有用的文件给add了，导致尽管已经在`.gitignore`文件中声明了，但是不生效
```bash
# 请使用git bash：windows下的terminal文件夹表示方法很奇怪
git rm --cached -r --ignore-unmatch **/**/.mvn
# git rm --cached 只删除暂存区中的文件，保留本地文件。如果不加--cached，就会导致本地文件也被删除掉
# -r git rm像rm命令一样，是不能直接rm folder删除文件夹的；想要删除文件夹，需要加上-r
# --ignore-unmatch：如果某个匹配文件夹中为空，git就会直接报错，结束命令，导致后面的文件夹都没法删除。--ignore-unmatch让git如果文件夹为空，也要继续执行，不要报错中断
# *.c匹配所有.c文件，**匹配所有文件夹
```
## 远程
* `git remote`
    * `git remote add git-demo https://xxx`：将链接取别名为git-demo
    为什么要这样做？
    请看git push操作，原始做法是`git push https://xxx master`,这样每次都要输入远程库的url，非常麻烦；通过取别名的方法，就可以用别名来代替url：`git push git-demo master`
    * `git remote -v`:查看有哪些别名
* `git push`
    * 使用背景：
    1、在GitHub上创建一个空仓库（repository）后，需要将本地代码上传到远程端
    * 详细使用
        * `git push url/别名 分支`
* `git pull`
    * 使用背景：由于种种原因，本地库和GitHub上的远程库已经不一样了
    * 详细使用
        * `git pull url/别名 分支`
    * 我写自己的代码功能写完了，需要将远程库中的代码先合并到本地，最后在将所有的代码一起push，但我不想将远程库的代码下载后，我修改的部分消失了。我该怎么做？
    先commit，在git pull
## 其他
* 查看git安装在哪了：`where git`
* `xxx.ignore`:通常为`git.ignore`
    * 使用背景：在idea的项目中，有一些与项目无关的代码：比如idea的配置文件:.iml、maven生成的target目录。这些文件是没有必要push上去的
    * 详细使用：
## Git的配置
* 用户信息
```shell
$ git config --global user.name "BeicC"
$ git config --global user.email 527609724@qq.com
```
* 查看配置信息：`$git config --list`
* 查看配置文件所在的位置：`$ git config --list --show-origin`
## git操作
* 分支
    * `git branch -a`：查看所有分支
    * ``
# VIM
## 移动
* 怎么快速回到文档首部：gg
## 插入
* 怎么在该行的上面直接插入：O
## 替换
* `s`
    * `:s/going/rolling`：当前行的第一个
    * `:s/going/rolling/g`:当前行的全部
    * `%s/going/rolling/g`:全部文件
# Postman
* Postman中的param与body中的form-data的区别？
get请求，可以在param中添加参数，会自动在url的后面加上?name=cbc&age=10
post请求，在form-data中添加数据，就相当于通过表单进行post提交
* 通过postman查看http请求报文
view-> postman console
# Maven
* [官网](https://mvnrepository.com/)
* 父子继承关系
要想让两个`pom.xml`成为父子：
父pom中要添加`<module>`标签
子pom中要添加`<parent>`标签
## [Dependency Management](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#dependency-management)
```xml
<dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring.cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>${spring.cloud.alibaba.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```
1、dependencyManagement通常写在parent pom.xml中，用来做版本管理
2、声明在dependencyManagement中的依赖是不会加入该项目的
3、声明dependencyManagement后，在声明dependencies，不需要加版本号了（无论是父项目还是子项目）
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.10</version>
        <scope>test</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
    </dependency>
</dependencies>
```
* 在DependencyManagement中，`<type>pom</type>`,`<scope>import</scope>`是什么鬼？
springboot项目中，我已经有了parent标签，但我自己在根`pom.xml`中维护了一个`DependencyManagement`；我想使用根pom中的版本管理，怎么办？

## 命令行命令
1、所有命令都是在`pom.xml`所在的目录下运行。
2、compile、test、package、install，某个命令执行前，都会把前面的命令都执行了
* clean:删除target目录
* compile：将项目编译到`/target/classes`目录下
* package：将`/target/classes`下面的文件打成jar包
* install：将项目打成jar包并且放到本地的repository里面
## pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>Real_Spring</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <!-- 该依赖只能src/test下的文件使用 -->
            <!-- 如果不写，默认为compile，main和test下的文件都能使用 -->
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```
## 插件
* maven-shade-plugin
直接`mvn package`打出来的jar包是没有manifest文件的，即不能运行。可通过该插件解决此问题
* maven-Archetype-plugin
自动创建maven约定的目录结构

* 为什么Maven要配置环境变量？我又不在命令行里面直接访问Maven..还要配置两个M2_HOME,Maven_HOME:说是可以让idea自动使别
* 在idea中，创建Maven项目时勾选模板与不勾选的区别？：勾选模板后的pom.xml文件里面的东西会更多，会预先导入一些包（Junit），而且文件目录有点不一样：勾选模板后会有个webapp目录，而不勾选就没有。
* Maven的高级之处：不在于它能自动导入Jar包，而在于它能自动导入Jar包所依赖的其他Jar包
* Maven中配置文件导不出的问题 【狂神p11 21min46s】
* Maven绑定Jar包的源代码:`mvn dependency:sources`
* Maven工程中的java和resources目录下的文件，在打包的时候会被放到哪？
java下的所有东西，编译后放到classes下（不包含java文件夹）
resources下的所有文件，也是放到classes下（可能有意外，发生意外时需要在pom.xml中配置一下）
```java
<build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>

    </build>
```
