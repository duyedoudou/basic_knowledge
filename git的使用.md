## github

#### 基本概念：

`repository（仓库）`   `star(收藏)`   `fork（复制克隆项目）`  

 `pull request(发起请求)`   `watch(关注)`  `issue(发消息一起讨论是否是bug)`

#### git初始化：

```
1设置用户名：
git config --global user.name 'duyedoudou'
2设置用户邮箱：
git config --global user.emailb '1019737754@qq.com'
```

在建好的文件夹下执行git init，会在该文件夹下生成.git文件，是来存储仓库的所有信息的。

```
git init
```

```
git status                      # 查看当前工作区和暂存区文件的状态
git add 文件名                   # 提交到暂存区
git commit -m '这里写描述内容'    # 提交到本地仓
```

==修改文件后==，依然要重复：git add ..之后的步骤。

删除：假设此时`删除`了某文件，然后需要将它从暂存区删除：

```
git rm 文件名
git commit -m '描述'
```

#### 如何将本地仓库git到远程仓库：

git克隆操作：

```
git clone 仓库地址 
```

本地同步到远程仓库：

```
git push 
```

```
查看config信息：
git config --list
```

