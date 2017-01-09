# 快速脚本

## init
初始化脚本，在GitHub创建空repository后执行脚本，将在脚本存放路径生成gitbook项目。
如`./initbook.sh GitbookGuide`
```shell
#!/bin/bash
#usage ./initbook.sh GitbookGuide
echo Your gitbook name is $1
mkdir $1
mkdir "${1}_pages"

cd $1
echo ".DS_Store" > .gitignore
git init
git add .
git commit -m "init gitbook"
git remote add origin "git@github.com:AlexanderWangsgithub/${1}.git"
git push -u origin master

cd ../
git clone "git@github.com:AlexanderWangsgithub/${1}.git" "${1}_pages"
cd "${1}_pages"
git checkout -b gh-pages
git push -u origin gh-pages

echo gitbook was inited!
```
## deploy
发布脚本，每一次更改后运行此脚本，自动push master和gh-pages分支

```shell
#!/bin/bash
#usage ./deploybook.sh GitbookGuide
projectName=$1
echo Your gitbook name is $projectName

#push master分支
cd $projectName
git add .
git commit -m `date|awk '{print $3}'`
git push -u origin master
cd ../

#编译gitbook
gitbook init $projectName
gitbook build $projectName "${projectName}/_book"

#复制网页
pathAbs=`pwd`
dir1="$pathAbs/$projectName/_book/"
dir2="${projectName}_pages"

for file in `ls $dir1`
do cp -r "$dir1$file" $dir2
done

cd "${projectName}_pages"
#push gh-pages分支
git add .
git commit -m `date|awk '{print $3}'`
git push -u origin gh-pages

echo Your gitbook $1 was deployed!
```

> 采用两个文件夹并通过复制的方式，保证了每次修改是增量的
