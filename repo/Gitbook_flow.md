# Gitbook正常流程

## 安装GitBook
```
npm install gitbook -g
npm install -g gitbook-cli
```

## 使用GitBook
### 生成静态网页
命令`gitbook init $projectName`
会在`$projectName`目录下生成一个`_book`目录，该目录下是编译好的静态网页
### 启动本地端口
命令`gitbook init $projectName`
会启动服务，通过本地`localhost:4000`访问工程

## 使用GitHub Pages服务
1. Create New Repository
2. 创建分支`gh-pages`，将静态网页放到该分支下。
3. push分支`gh-pages`，访问`https://alexanderwangsgithub.github.io/$projectName`，如：
https://alexanderwangsgithub.github.io/GitbookGuide
