# Websites for you and your projects

地址：https://pages.github.com/

## Github上创建repository；本地push

在你的项目目录中，

```
git init

git add --all

git commit -m 'add all and commit'

// 创建连接别名origin
git remote add origin git@github.com:baibaibai66/baidu.git
// origin下面master分支
git push -u origin master
```

以上步骤其实就是在Github上面创建一个repository时候上面教给你怎么操作的

## 创建分支：gh-pages（这个名字是固定的）

```
git branch gh-pages

git checkout gh-pages

git push -u origin gh-pages
```

当然也可以在创建Github仓库时候，直接创建github.io

## github上就可以展示你的项目了

![](http://i1.piimg.com/567571/f443b14658f3705c.png)


## 如何绑定自己的域名 －－ 到域名解析进行绑定即可

![](http://i1.piimg.com/567571/be6741f470e5d343.png)

1. 本地创建CNAME

```
$ vim CNAME
baidu.luckybai.top

git add --all

git commit -m 'add domain name'

git push -u origin gh-pages
```

2. 绑定域名解析

![](http://i1.piimg.com/567571/e5cf29d5ce8bf95b.png)

OK

![](http://i2.muimg.com/567571/03dbc72b43137e01.png)