# Git 简明操作指南

1：初始化本地仓库
```
git init
```

2: 通过SSH指令连接远程仓库-----》本地与远程建立连接
```java
git remote add origin git@github.com:yourname/your-repo.git
// 注意：yourname为github用户名，your-repo为远程仓库名
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

8：相关命令集合
文档链接: https://www.mubu.com/doc/7TKf_YyDKUj 密码: 1234