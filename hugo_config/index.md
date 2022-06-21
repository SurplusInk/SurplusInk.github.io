# 环境配置-Hugo


使用Hugo部署静态网站到Gitee的流程

<!--more-->

## 1 使用Hugo部署静态网站到Gitee

### 1.1 Hugo安装及搭建

到[官网Github地址](https://github.com/gohugoio/hugo)下载，我选择的版本如下图Fig. 1.所示。

{{< image src="1_1.png" caption="Fig. 1. hugo_extended_0.89.4" width="640" height="320" >}}

解压之后，命令行cd的此目录下，如图Fig. 2.所示。

{{< image src="1_2.png" caption="Fig. 2. hugo dir" width="640" height="320" >}}

{{< admonition >}}
这里my_website文件是后面创建的，不用在意。
{{< /admonition >}}

然后输入**hugo version**命令，如下图Fig. 3.所示即安装成功。

{{< image src="1_3.png" caption="Fig. 3. hugo version" width="640" height="320" >}}

输入**hugo new site my_website**命令，即可得到图Fig. 2.中的my_website文件。

之后就可以到[官方主题](https://themes.gohugo.io/)中选择主题进行安装，比如我这个[主题](https://themes.gohugo.io/themes/doit/)。他会教你后续的其它操作。

### 1.2 将本地博客推送到Gitee的命令流程

    1. hugo --theme=(主题名) --baseUrl="(网页地址)" --buildDrafts
        eg: hugo --theme=hugo-theme-stack --baseUrl="https://study777.gitee.io" --buildDrafts
        此步骤会生成public文件，里面就是后续要部署的博客。
    2. cd public
    3. git init                         
    4. git add .   
    5. git commit -m "(随便写)"                
    6. git remote add origin (仓库地址) 
        eg: git remote add origin https://gitee.com/study777/study777.git
        如果这一步输入之后提示出错信息： fatal: remote origin already exists.表示已经执行过这一步操作了，
        只需输入 git remote rm origin 之后再次输入即可。
    7. git push -u origin master    
        如果推送出错表示远程仓库有本地没有的文件。即，两个仓库不同步，这种情况下需要利用 git pull 命令合并两个仓库。
        只需输入 git pull --rebase origin master
        或者这一步可以直接强制推送,
        只需输入 git push -f origin master

### 1.3 后续更新博客的命令流程

在执行第二步之后不要把创建的public文件删除，如果删除了需重全部新执行第二步。

    1. hugo --theme=hugo-theme-stack --baseUrl="https://study777.gitee.io" --buildDrafts
    2. cd public                       
    3. git add .   
    4. git commit -m "(随便写)"                
    5. git push -f origin master    

{{< admonition >}}
如果部署实在不成功就把Gitee仓库清空重新再来就行了
{{< /admonition >}}

