# gitolite自动部署

> 安装好 gitolite
> 本教程是结合`rsync`完成的自动部署

## 修改.gitolite.rc(服务器)

找到下边这两行,将这两行的注释去掉

```
LOCAL_CODE => "$rc{GL_ADMIN_BASE}/local",

repo-specific-hooks
```

## 克隆准备自动部置的代码库,并指定目录为 `/test.git/repo/`

```
git clone git@127.0.0.1:xxxx.git /test.git/repo/
```


## 克隆管理代码(gitolite-admin)

> 以下修改都在本地开发机上操作

```
git clone git@host:gitolite-admin.git 
```

### 修改 conf/gitolite.conf

增加`option hook.post-receive= deploy`

```
@devs = admin

repo mysite
    option hook.post-receive= deploy 
    RW+     =   @devs

```

### 创建自动部署脚本

* 先在本地 `gitolite-admin` 根目录创建 `local/hooks/repo-specific/` 目录
* 在上一步创建的目录下创建文件名为`deploy`的脚本

deploy 内容如下:

```
#!/bin/sh

set -x
unset GIT_DIR
NowPath=`pwd`

GIT_REPO="/test.git/repo/"
DEV_DEST="/dest/dev/"
WWW_DEST="/dest/www/"

while read oldrev newrev ref
do
	branch=`echo $ref | cut -d/ -f3`
	echo "--- Current branch is : "$branch	
	if [ "master" == "$branch" ]; then
		dest=$WWW_DEST
	fi
	
	if [ "dev" == "$branch" ]; then
		dest=$DEV_DEST
	fi

	if [[ "dev" == "$branch" || "master" == "$branch" ]]; then
		cd $GIT_REPO
		git checkout $branch
		git pull origin $branch
		sudo /usr/bin/rsync -av --delete $GIT_REPO $dest --chown=www:www --exclude=.git
	fi
done

cd $NowPath
exit 0
```

