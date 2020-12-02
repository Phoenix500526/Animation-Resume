# Animation Resume

## 使用方法
```bash
git clone git@github.com:Phoenix500526/anires.git
cd anires
npm install
npm run build
npm run dev
```
编译成功后，执行 `npm run dev` 会自动打开浏览器(地址默认为 http://localhost:8080/)。


## 定制化方法
修改位于 anires/src/App.vue 文件, 将相关的 markdown 文本修改为你想要写的简历内容即可

## 部署方法
1. fork 该代码仓库至自己的 github 账户，并将其 clone 到本地【注：请保留项目名称 anires】
2. 完成自己的定制化需求后，执行 `npm run build` 目录重新编译代码，并通过 `npm run dev` 进行本地调试
3. 完成第 2 步后，将生成的 public/\* 文件提交至自己的 github 仓库 anires 当中，如下
```bash
npm run build
git add .
git commit -m "Customization"
git push origin master
```
4. 为自己 github 账户下的 anires 仓库启动 **Github Pages** 功能，并在 Source 处设置 Branch 为 master，然后保存
5. 完成第 4 步以后，会产生一个 url 地址，如：https://www.hacker-cube.com/anires/ 。访问地址：https://www.hacker-cube.com/anires/public/index.html 即可看到自己的动态简历。
PS：在第 5 步中www.hacker-cube.com 是我的个人域名。如果你没有设置域名的话，则默认是 https://username.github.io/anires 其中 username 是你的 GitHub 账户名称。


# 关于我
- [个人博客](https://hacker-cube.com)
- [GitHub](https://github.com/Phoenix500526)
- [Stackflow](https://stackoverflow.com/users/8557622/phoenix-chao?tab=profile)
- **主要涉及技术：`C++ 网络编程`、`Go 语言`、`lua 语言`、`Linux系统开发`**

## License

[Apache License](./LICENSE)

## 致谢
**本项目源于：[https://github.com/jirengu-inc/animating-resume](https://github.com/jirengu-inc/animating-resume "https://github.com/jirengu-inc/animating-resume") 。我在原始代码的基础上，删除了一些冗余代码，填平了一些编译及部署上的坑，在此向作者表示深深的敬意。**