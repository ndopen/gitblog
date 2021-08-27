# 这里用来测试学习git的技巧

Link:[git - 简明指南](https://rogerdudler.github.io/git-guide/index.zh.html)

## 创建仓库 or 克隆仓库

### `git init` 创建新仓库
> 在仓库中生成.git文件夹
![.git.PNG](:/6d97984c55a746acaf7b9e4e43198ad1)

### `git clone` 克隆仓库
```ssh
#本地仓库
git clone username@host:/path/to/repository
#仓库服务器
git clone /path/to/repository
```

## 工作流程
> 你的本地仓库由 git 维护的三棵“树”组成。第一个是你的 `工作目录`，它持有实际文件；第二个是 `暂存区（Index）`，它像个缓存区域，临时保存你的改动；最后是 `HEAD`，它指向你最后一次提交的结果。
![259087e70519cf0dc4786f91f6b1906e.png](:/3fb7525d4dcb44acbb9769f43d8d2e7f)

## git `add` & `commit` 来提交修改至 缓存区域和head区域
- add 到缓存取
```shell
# 提交单个文件
git add README.md
# 提交所有
git add -A
```

- commit 提交至HEAD，并且添加注释
```shell
/mnt/c/Users/Hairong/Documents/gitblog(master*) » git commit -m 'add bin and edit README'
[master a6a35b7] add bin and edit README
 1 file changed, 1 insertion(+)
 create mode 100644 bin/README.md
```

## `push`到远程服务器
- `remote` 关联到远程服务器
```shell
git remote add origin git@github.com:ndopen/gitblog.git
```

- `push`到远程仓库
> 你的改动现在已经在本地仓库的 HEAD 中了。可以把 master 换成你想要推送的任何分支。
```shell
git push origin master
```
## 分支
> 分支是用来将特性开发绝缘开来的。在你创建仓库的时候，master 是“默认的”。在其他分支上进行开发，完成后再将它们合并到主分支上。
![b88633a4fa71f4a009552dcc43257d56.png](:/c301e6a58ae74bc5b395d335f0c269d8)

- `checkout` 创建分支
```
git chechkout -b 1.0
```
- 切换分支
```
git checkout master
```
- 删除分支
```
git branch -d main
```
- 查看分支
```
git branch -l
```
- 流程
```shell
git checkout -b 1.0 #创建1.0 branch 并且切换,修改相关内容
git push origin 1.0  #push 1.0 到服务器
git checkout -b 1.0.1 #创建1.0.1 branch,添加相关内容
git merge 1.0.1 #合并1.0.1 到 1.0 分支
git push origin 1.0 #推送1.0 分支
git branch -d 1.0.1 #删除1.0.1 分支
```

### `deff` 查看两个分支合并前的改动情况
```
git diff master 1.0
diff --git a/bin/config/app.json b/bin/config/app.json
new file mode 100644
index 0000000..1a28c63
--- /dev/null
+++ b/bin/config/app.json
@@ -0,0 +1,4 @@
+{
+    'name':'testapp'
+}
+
diff --git a/bin/nginx.conf b/bin/nginx.conf
new file mode 100644
index 0000000..73a4220
--- /dev/null
+++ b/bin/nginx.conf
@@ -0,0 +1 @@
+root var/www/laravel/public
```




### `SSH` 公钥生成
> 许多 Git 服务器都使用 SSH 公钥进行认证。 为了向 Git 服务器提供 SSH 公钥，如果某系统用户尚未拥有密钥，必须事先为其生成一份。
- id_dsa 或 id_rsa 命名的文件，其中一个带有 .pub 扩展名。 .pub 文件是你的公钥，另一个则是与之对应的私钥。
- 文件位置于用户根目录下`~/.ssh`
- `ssh-keygen` 生成不需要密码的密钥，-o 参数生成需要密码的要密钥
```shell
» ssh-keygen
# -t 指定密钥加密类型 -C 指定用户标签
» ssh-keygen -t ed25519 -C "admin@gmail.com"
# 默认为 rsa 类型
ssh-keygen -C "admin@admin.com"
# 指定名称
ssh-keygen -t rsa -f ~/.ssh/github -C "admin@admin.c
om"
```
- link：[ssh-keygen命令 – 密钥认证](https://www.linuxcool.com/ssh-keygen) & [关于 SSH](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/about-ssh)
