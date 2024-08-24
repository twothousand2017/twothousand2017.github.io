# 一网盟 Hexo 仓库使用说明
本仓库为hexo网站源码，其中可能包含私密信息，请务必设置仓库可见性为 `Private` 。
## 功能简介
1. 本仓库有提交变更则自动触发渲染 HTML
2. 本地端不需要渲染和发布工序，只需要维护 MarkDown 源文档，提交同步到 GitHub 云端仓库即可
3. HTML 静态页自动发布到：`owner.github.io` 「需自行建立 pages 仓库和配置授权」，分支：`pages-hexo`
4. 如果网址非 `github.io`，则自动生成 `CNAME` 「需自行在DNS托管商处做好cname解析」
   
![本仓库方案](https://cdn.jsdelivr.net/gh/828767/static/images/github_page_free.png)

## 本地预览环境
为更好地预览即将发布的内容，建议将本仓库克隆到本地电脑维护 MarkDown 源码，那么本地就需要安装一个预览环境。

> 到以下涉及软件官网下载如果速度慢，可以从 [墙内淘宝源下载](https://registry.npmmirror.com/binary.html)。

### **git**
大名鼎鼎的代码项目管理工具，到 [Git-SCM官网](https://git-scm.com/downloads) 或者 [墙内淘宝源](https://registry.npmmirror.com/binary.html?path=git-for-windows/ "Windows版，其他系统自带或直接命令安装") 下载安装包或者软件源默认安装完成即可。

仓库同步就需要通过 `git` 客户端，Windows 系统安装完成后，会在右键菜单添加 `Git Bash Here` 入口，方便后续使用。

![Git Bash Here](https://cdn.jsdelivr.net/gh/828767/static/images/git_menu_gitbashhere.png)

如果以前未使用过 Git，一般都需要设置用户名和邮箱，随便一个目录空白地方 点右键「Windows系统，其他系统打开系统终端输命令」》 `Git Bash Here` ，运行以下命令设置：
```bash
git config --global user.name name #设置Git用户名
git config --global user.email "email" #设置Git邮箱
```
> 这里只是最基本的Git信息设置，后续提交同步 GitHub 等需要额外授权另外教程再说，或者自行求助战略合作伙伴 Google 或百度。


### **nodejs**
`nodejs` 是跨平台的 JavaScript 运行环境和包管理工具。一样的，到 [Nodejs官网](https://nodejs.org/zh-cn/) 或者 [墙内淘宝源](https://registry.npmmirror.com/binary.html?path=node/) 下载安装包，建议选择长期维护版，默认安装完成即可。

安装完成后，在前文安装完成的 `Git Bash` 或者系统终端中输入命令 `npm version` 验证安装结果：
```bash
$ npm version
{
  npm: '8.5.5',
  node: '16.15.0',
  ……
}
```

为了后面安装依赖包顺利完成，运行以下命令设置 npm 淘宝源：
```bash
# 墙内设置 npm 淘宝源，加快网络下载速度，墙外就不要做了
npm config set registry https://registry.npm.taobao.org
```

### **hexo**
前文安装完成 `npm` 包管理器后，就可以安装 `hexo` 预览客户端了，打开前文安装完成的 `Git Bash` 或者系统终端，输入以下命令：
```bash
# 系统全局安装hexo，方便从零开始
# macOS 或 Linux 非 root 用户登录需要 sudo 权限运行
npm install -g hexo-cli
```
安装完成后可使用命令 `hexo version` 验证：
```bash
$ hexo version
INFO  Validating config
hexo: 6.2.0
hexo-cli: 4.3.0
……
```

macOS新版本默认启用的是 `zsh` 终端，`hexo` 安装完成后并未添加到 `zsh` 能识别的系统变量，会出现提示 `zsh: command not found: hexo` 的情况，可添加系统变量解决，具体方法请求助战略合作伙伴 Google和百度，或者就此烂过。

> 也可以 [将系统默认终端改成 `bash`](https://support.apple.com/zh-cn/guide/terminal/trml113/mac)，或者使用后文提到的 VSCODE 集成终端，将 VSCODE 调用默认终端改成 `bash`，然后在 VSCODE 集成终端运行命令即可。

### **packages**
前面的准备工作已完成，剩下就是将仓库文件克隆同步到本地电脑，还是在 `Git Bash` 中，输入这样的命令：
```bash
cd d:\Git   #先切换到要存放Git文件的目录路径
git clone --recurse-submodules 自己的仓库地址 #带子模块一起克隆
```

仓库中只包含网站必须的内容源码文件，一些依赖包文件是忽略提交的，所以本地需要重新安装，在仓库根目录路径下运行以下命令：
```bash
npm install
```

以上命令实际上是下载 `package.json` 中定义好的依赖包，等依赖包下载完成，整个本地预览环境就全部安装完成了，在仓库根目录路径下运行 `hexo s` 即可启动预览服务：
```bash
user@IAY MINGW64 /d/Git/action-hexo (main)
$ hexo s
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```
以上输出信息中，`/d/Git/action-hexo (main)` 就是所谓运行路径，Windows系统表示 `d:\Git\action-hexo` 目录，当前在 `main` 分支。

浏览器中打开 `http://localhost:4000` 就可以预览，按 `Ctrl+C` 组合键停止，一些主题或者网站设置变更需要重启该预览服务才能看到效果。

## 编辑器推荐
工欲善其事必先利其器，一个编辑器可以事半功倍，VSCODE 就是个不错的选择，自行到 [微软官方网站](https://code.visualstudio.com/download) 去下载安装，优点：
1. 全目录管理，一个界面可以管理整个目录下的文件
2. 语法格式显示，也能实时预览
3. 与Git集成，可以界面化操作Git提交同步，比较等
4. 集成命令终端，预览调试方便
 
![VSCODE](https://cdn.jsdelivr.net/gh/828767/static/images/vscode-hexo.png)

其他如 Atom、Sublime Text、Typroa 之类的编辑器，甚至是专业的代码编辑器请自行研究。

作为MarkDown编辑器，建议安装以下插件：
1. Git History
2. GitLens supercharges
3. Markdown All in One
4. Markdown Preview Mermaid Support
5. Markdown Table
6. Markdown Shortcuts

其他有用的插件请自行探索。

## 其他事项
1. 任何增删改都需要提交同步到本仓库，同步后上端会自动处理，等几分钟刷新缓存就能看到效果了
2. 提交前可以本地预览，效果满意了再提交
3. 根目录下的 `_config.yml` 为网址基础配置，主题内容相关请到 `_config.主题名.yml` 中去设置修改， `_config.主题名.yml` 来源于 `themes/主题名/_config.yml` ，如主题有更新请自行同步
4. Git基础用法和MarkDown语法等很多基础知识都可以自行求助战略合作伙伴 Google 或百度，遇问题解决问题
5. 关于怎么用入门教程汇总参考：[从零开始建个小站](https://yiwangmeng.cn/guide-how-to-build-site-0.html)


## Stargazers over time

![Stargazers over time](https://starchart.cc/828767/action-hexo.svg)
