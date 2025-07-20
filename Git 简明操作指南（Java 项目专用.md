# Git 简明操作指南

1：初始化本地仓库（此时仓库只属于本地，与远程仓库还未建立联系）

```
git init
```

2: 通过SSH指令连接远程仓库-----》本地与远程建立连接

```java
// SSH方式
git remote add origin git@github.com:yourname/your-repo.git
// 注意：yourname为github用户名，your-repo为远程仓库名

// HTTPS方式
git remote add origin https://github.com/yourname/your-repo.git
```

3：查看远程地址----》可以检测第二步执行有没有成功

```java
git remote -v
```


4: 添加文件并提交

```Java
git add .
git commit -m "写清楚本次修改内容"
```

5: 推送代码到远程（第一次推送建立跟踪关系）----》这一步很重要，相当于本地的main分支和远程的main分支已经建立了联系。后续的推送操作，直接push就可以，而不需要指定本地和远程分支的关系。

```Java
git push -u origin main
```

6：后续直接将本地代码推送到远程

```java
git push
```

~~~
第一次提交前：

      本地                 远程
   ┌────────┐          ┌────────────┐
   │ main   │   ──x──▶│ origin/main│
   └────────┘          └────────────┘
（未建立跟踪关系）

你运行：
git push -u origin main

      本地                 远程
   ┌────────┐          ┌────────────┐
   │ main   │◄────────►│ origin/main│
   └────────┘ 跟踪关系  └────────────┘
（建立双向绑定）

后续可以直接使用：
git pull
git push
~~~


7：拉取远程更新并合并
```java
git pull
```

补充内容：合并分支

如果远程有main分支和test分支，并且test分支有对main分支的修改，那么你可以将test分支合并到main分支。

- 首先确保test分支内容已经进行修改，并且已经将本地修改内容推送到远端
- 切换到main分支，使用`git checkout main`语句
- 合并test分支到main分支，使用`git merge test`语句,此时会跳出可编辑的文件出来，直接在文件内保存此次修改即可，关闭文件本次合并结束。
- 需要注意的是现在本地代码已经合并了test分支的修改，但是没有将修改推送到远端，所以需要使用`git push origin main`语句将修改推送到远端。



8：相关命令集合
文档链接: https://www.mubu.com/doc/7TKf_YyDKUj 密码: 1234