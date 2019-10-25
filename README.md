# miaomiao

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## 与远程仓库相连接

创建项目后，会生成一个连接，有http 和 ssh 格式的，我们选择ssh 格式的，这个每次操作仓库的时候就不要登录密码了

将本地的文件与远程仓库连接根据创建仓库后出现的提示做就好了，初次会有问题，我们，需要给GitHub设置本地ssh-key,然后文件名呢就是id_rsa.pub,可以自己找到然后添加就好了 <https://www.runoob.com/w3cnote/view-ssh-public-key.html>  如何查看和创建ssh-key

git remote  查看仓库

git push origin master  将代码push 到远程仓库

在进行项目开发的时候我们不要直接在主分支上进行开发，我们应该创建一个分支，完成工作后在进行文件的汇总

git  checkout -b dev     -b 可以直接创建后选择到分支上  dev是分支的名称

然后我们将分支也push到仓库中

git push origin dev   

当完成今天的任务后，我们将代码push到github上并合并

git status   查看改动的代码

git add .    全部提交

git commit -m "注释内容"      创建一个版本注释

这个时候这个分支就没有用了

我们可以切换到dev分支上

git checkout dev

我们将今天做的东西合并到dev的分支上

git merge createComponents --no-ff      

然后我们推出

打出   ：q   便可以退出

然后  查看日志

git log

然后将代码推送到远程仓库

git push origin dev

然后我们这个时候createComponent分支已经没用了

我们  git branch    查看目前存在的分支

然后   git branch -d createComponent  删除分支就好了