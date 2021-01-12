---
sidebar: auto
---

# D2 Advance

D2 Advance 是受 [D2 Admin](https://github.com/d2-projects/d2-admin/) 交互设计影响启发的新项目。保留 D2 Admin 经典设计的同时，**整理出清晰的架构、提升代码质量和规范开发流程**，探索中后台及其以外的更多应用场景。

使用须知：

- 和 D2 Admin 1x 版本的代码完全不一样，**你需要重新学习，先看懂再用**，避免风险
- 代码里没有注释，**好的代码不需要注释**，如果有，要么是标注的文档地址，要么是有坑
- 基于 vue-cli@4，请一定要熟悉 [vue-cli](https://cli.vuejs.org/) 的文档，它能解决你遇到的大部分问题
- 更规范的代码提交、版本演进和自动化发布，**需要开发者做好每一次提交**
- **请不要关闭 lint 和测试等提示，这是代码质量的基本保障**，如果不能接受，请勿使用该项目

## 仓库

| 位置 | 链接 |
| --- | --- |
| GitHub | [https://github.com/d2-projects/d2-advance](https://github.com/d2-projects/d2-advance) |
| 码云 | [https://gitee.com/d2-projects/d2-advance](https://gitee.com/d2-projects/d2-advance) |

## 环境要求

### NodeJS

NodeJS 版本要求受 `devDependencies` 影响，以下是主要的依赖清单。尽管有的依赖的新版本在该项目还未采用，但为了之后的升级，这里以新版本为准。

推荐 `node@12`

- 打包使用的 [brotli](https://github.com/webpack-contrib/compression-webpack-plugin#using-brotli) 压缩算法需要 `>= node@11.7.0`

最低 `node@10`

- `webpack@5` 需要 `>= node@10.13.0`
- `prettier@2` 需要 `>= node@10`

**该项目使用 yarn 作为包管理器**，如果没有全局安装，请运行 `npm i -g yarn` 安装。

## 快速开始

该项目可以直接作为项目模版，进行二次开发，以下几种推荐几种初始化方式，任选其一：

- 适合私有项目二次开发：点击仓库上方工具栏的下载 zip 按钮，直接下在纯源码。在本地解压后，自行初始化为 git 仓库或其他类型的仓库。
- 适合开源项目二次开发：使用 github 的模版初始化功能，创建一个只带一次文件初始化提交的 github 仓库，并 `git clone` 到本地。
- 适合该项目贡献者：直接 `git clone` 到本地。

本地项目文件夹准备完毕后，将命令行切换到项目根目录，并按以下命令操作：

``` bash
# 安装依赖
yarn

# 启动开发服务
yarn serve
```

启动完成后，浏览器访问 [http://localhost:8080](http://localhost:8080) 即可预览。

## 开发规范

### 小步提交

在使用 git 管理代码时，提倡**小步提交**，即产生一个功能最小化，且能运行的代码，就 commit 到本地。在几次 commit 形成一个小功能后，就 push 到远程仓库。

``` bash
# 👎
git commit -m "feat: 添加登陆页面，修复若干问题，添加打包命令"
git push

# 👍
git commit -m "feat: 添加登陆页面"
git commit -m "fix: 登陆失败缺少错误提示"
git commit -m "chore(npm): 添加预览版本的打包命令"
git push
```

好处：
- 在多人协作的情况下，能及时同步代码，产生冲突能提前发现
- 提高对代码的归纳总结能力，类似于语文中的划分段落，并归纳中心思想 :)

### 预定式提交

在小步提交的提出上，进一步书写**格式统一、描述准确**的 commit message，而不是随意书写：

``` bash
# 👎
git commit -m "登陆"
git commit -m "登陆失败显示错误提示"
git commit -m "打包"

# 👍
git commit -m "feat: 添加登陆页面"
git commit -m "fix: 登陆失败缺少错误提示"
git commit -m "chore(npm): 添加预览版本的打包命令"
```

好处：
- 统一格式，方便查阅
- 便于自动生产变更日志和版本号

该项目采用常见的 [angular 提交准则](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit)，具体可参考：https://www.conventionalcommits.org/zh-hans

为避免手写失误，该项目已经使用 [commitizen](https://github.com/commitizen/cz-cli) 工具进行初始化，可以直接在命令行中体验交互式提交，通过选择+填空的方式生成规范的 commit message：

``` bash
# 方法 1
# 要先运行 `npm i -g commitizen` 全局安装 commitizen
git cz

# 方法 2
yarn commit # 或 npm run commit
```

### 分支管理

**私有项目和开源项目的侧重点不同，在分支管理上会有区别。**

#### 开源项目

该仓库使用的简单的 master + dev 模式：

- `master`：默认分支，包含了所有的版本 tag，最后一次提交永远是最近一次版本发布，保证同个版本下载的代码都是一致的，同时也和部署到预览的代码一致
- `dev`：开发分支，里面是上一次版本发布后，待发布的提交，当需要发布时直接合并到 `master`
- `gh-pages`：部署 Github Pages 时生产的分支，请忽略

开发流程如下：

``` bash
# ...在 dev 完成多次 commit 后
(dev) git push
(dev) git checkout master
(master) git merge dev # 把即将发布的代码合并到 master
(master) git push
# ...等待发布完成
(master) git pull # 发布的过程中可能会自动产生一些提交
(master) git checkout dev
(dev) git merge master
(dev) git push # 让 dev 与 master 保持一致
# ... 继续在 dev 开发
```

#### 私有项目

私有项目一般会有开发环境和测试、生产环境，在开发过程中更多关注开发环境与最新代码，所以多为 master + release 的方式。
如果你是以该项目为模版的私有项目，直接在 master 开发，在必要的时候切 release 分支即可。

### 代码风格

``` bash
# 检查代码风格，并自动修复
yarn lint

# 严格检查，不会自动修复
yarn lint:strict
```

#### 配置

代码风格设置主要以 eslint 为主，搭配 [prettier](https://prettier.io/docs/en/options.html) 和 [vue](https://github.com/vuejs/eslint-plugin-vue/blob/master/docs/rules/README.md) 的 lint 规则：

``` js
// .eslintrc

module.exports = {
  // ...
  extends: [
    'plugin:vue/recommended',
    'eslint:recommended',
    '@vue/prettier'
  ],
  // ...
}
```

可以将 `'plugin:vue/recommended'` 换成 `'plugin:vue/essential'` 以使用更简单的 vue 规则。

如何覆盖 prettier 的规则：

``` js
// .eslintrc

module.exports = {
  // ...
  rules: {
    'prettier/prettier': [
      'warn',
      {
        singleQuote: true,
        semi: false,
        trailingComma: 'none',
        quoteProps: 'preserve',
        arrowParens: 'always'
      }
    ]
  },
  // ...
}
```

## 文件结构

TODO

## 代码架构

TODO

## 测试

TODO

## 打包

TODO

## 部署

TODO

## CI/CD

TODO