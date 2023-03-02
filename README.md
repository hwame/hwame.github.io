## 仓库说明
![Watchers](https://img.shields.io/github/watchers/hwame/hwame.github.io?style=social&label=Watch)
![stars](https://img.shields.io/github/stars/hwame/hwame.github.io?style=social)
![forks](https://img.shields.io/github/forks/hwame/hwame.github.io?style=social&label=Fork)
![contributors](https://img.shields.io/github/contributors/hwame/hwame.github.io)
![commits](https://img.shields.io/github/commit-activity/m/hwame/hwame.github.io)


![Stargazers](https://starchart.cc/hwame/hwame.github.io.svg)


该 Repository 用于个人静态博客的存储，由 [Hexo](https://hexo.io/zh-cn/) 生成、 [Github](https://github.com) 托管。

<a href="https://hwame.top"><img src="https://cdn.jsdelivr.net/gh/hwame/pics@main/avatar.jpg" width="100" height="100" alt="鴻塵"/></a>

以下简要介绍博客搭建的主要流程以及注意事项，详细搭建步骤可以参考如下文章（都是我自己一个一个字写的），点击上方图片直达【[我的博客](https://hwame.top)】

- [Hexo博客搭建(1)——建站及部署](https://hwame.top/20200520/hello-hexo-setup-deploy.html)
- [Hexo博客搭建(2)——主题配置](https://hwame.top/20200520/hello-hexo-configuration.html)
- [Hexo博客搭建(3)——优化评论系统](https://hwame.top/20200520/hello-hexo-optimization.html)
- [Hexo博客搭建(4)——常见问题](https://hwame.top/20200520/hello-hexo-troubleshooting.html)

## 博客搭建
此部分自行参考上面的四篇文章。
### ①准备工作
- 安装`Node.js`、`Git`、`Hexo`；
- 创建Github仓库，名称格式必须为`<username>.github.io`。 **注意：** 若想创建`README.md`，不能在此处新建仓库的时候直接勾选「 ***Initialize this repository with a README*** 」，因为后续部署的时候会覆盖（删除）掉该文件。
- 初始化git：
```bash
git config --global user.name <username>
git config --global user.email <email>

# 可以用以下两条命令检查是否输入正确
git config user.name
git config user.email
```
- 配置SSH密钥：`ssh-keygen -t rsa -C <email>`，配置完成后可通过`ssh -T git@github.com`检查是否成功。
- 博客初始化：
```bash
hexo init <blog_name>
cd <blog_name>
npm install
```
- 到这一步博客就已初具雏形，运行`hexo g && hexo s`预览，如果不报错且浏览器能访问 <http://localhost:4000> 则表示一切正常、喜大普奔。

### ②`hexo`常用操作
当我们写了新的文章后，需要重新部署，就会用到以下命令，常用的一键三连`hexo clean && hexo g && hexo d`。

**注意：** `hexo d`部署之前需要先配置站点的部署信息。
```bash
hexo clean                # 删除缓存和已生成的静态文件
hexo generate             # 生成public静态文件，可简写为hexo g
hexo server               # 本地预览，可简写为hexo s
hexo deploy               # 部署到远程仓库，可简写为hexo d
hexo new [layout] "name"  # 生成新的布局、页面、文章
hexo new "My-new-post"    # 省略layout则为发布文章
```

### ③站点配置
Hexo配置文件有两个，一个是称之为 **「站点配置文件」** 的`./_config.yml`，一个是称之为 **「主题配置文件」** 的`./themes/pure/_config.yml`。

站点配置没有需要特别注意的地方，参考默认配置并结合《[Hexo博客搭建(1)——建站及部署](https://hwame.top/20200520/hello-hexo-setup-deploy.html)》、《[Hexo博客搭建(2)——站点配置](https://hwame.top/20200520/hello-hexo-configuration.html#%E5%9B%9B%E3%80%81%E7%AB%99%E7%82%B9%E9%85%8D%E7%BD%AE)》以及 [官方文档——配置](https://hexo.io/zh-cn/docs/configuration) 等即可。

### ④主题配置
主题配置主要修改 **「主题配置文件」** 即`./themes/pure/_config.yml`，可根据默认配置按需修改，具体参考[Hexo博客搭建(2)——主题配置](https://hwame.top/20200520/hello-hexo-configuration.html)。

此部分在「主题配置文件」中配置了[Valine评论系统的全局设置](https://hwame.top/20200520/hello-hexo-configuration.html#5-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F)，由于[pure主题](https://github.com/cofess/hexo-theme-pure)已集成了`disqus`、`youyan`、`livere`、`gitment`、`gitalk`和`valine`等多种评论系统，但其中有的已经失效，有的不够稳定，有的需要注册才能评论，因此综合比较下选择了[Valine](https://valine.js.org)。

评论配置的细节见[Hexo博客搭建(3)——优化评论系统](https://hwame.top/20200520/hello-hexo-optimization.html)。

### ⑤评论系统
评论系统需要先在「主题配置文件」中启用并做全局设置（见上），然后才能结合[LeanCloud控制台设置](https://console.leancloud.app/apps)使配置生效。

**说明： ①**推荐选择国际版，因为免费提供了一个二级域名，用于评论后台管理、设置自动唤醒；**②**官方文档可参考[帮助信息](https://leancloud.app/help/)和[中文官方文档](https://zh-docs.leancloud.app/)。

- **部署valine-admin。** 首先创建应用、部署项目，然后设置域名白名单和 **环境变量** ，配置完成后重新部署项目，最后将后台评论管理系统初始化即可。
- **防止服务器休眠。** 此处的设置主要是为了解决LeanCloud流控问题制定服务器休眠策略，主要包括两个方面：**①**云引擎定时任务实现邮件漏发检查；**②**云服务器利用`crontab`实现自动唤醒从而防止实例休眠。
- [可选] **评论系统设置必填项。** 此处需要修改源码，实现或解决 *`meta`必填字段* 、 *通过QQ邮箱获取头像* 、 *昵称长度* 等问题。
- [可选] **添加身份标签。** 此处需要修改源码，实现自定义 **`博主`** 、 **`小伙伴`** 和 **`访客`** 的标签。
- [可选] **美化评论区样式。** 此处需要CSS样式文件`./themes/pure/source/css/style.css`，实现 *评论框背景及隐藏* 、 *评论及回复添加边框* 、 *头像悬停旋转* 等功能。

### ⑥修修补补
这部分内容主要对博客做最后的完善，所有的修修补补都可以在[Hexo博客搭建(4)——常见问题](https://hwame.top/20200520/hello-hexo-troubleshooting.html)中找到答案。
主要包括以下三个方面：

+ **①问题修复**
    - [Mathjax支持](https://hwame.top/20200520/hello-hexo-troubleshooting.html#1-%E5%A6%82%E4%BD%95%E4%BD%BF%E5%85%B6%E6%94%AF%E6%8C%81Mathjax)
    - [显示「最近文章」缩略图](https://hwame.top/20200520/hello-hexo-troubleshooting.html#8-%E5%A6%82%E4%BD%95%E6%98%BE%E7%A4%BA%E3%80%8C%E6%9C%80%E8%BF%91%E6%96%87%E7%AB%A0%E3%80%8D%E7%BC%A9%E7%95%A5%E5%9B%BE)
    - [部分地方中文适配](https://hwame.top/20200520/hello-hexo-troubleshooting.html#9-%E9%83%A8%E5%88%86%E5%9C%B0%E6%96%B9%E4%B8%AD%E6%96%87%E9%80%82%E9%85%8D)
    - [免密部署问题](https://hwame.top/20200520/hello-hexo-troubleshooting.html#10-%E5%85%8D%E5%AF%86%E9%83%A8%E7%BD%B2%E9%97%AE%E9%A2%98)
+ **②功能优化**
    - [更改左侧IconFont 图标](https://hwame.top/20200520/hello-hexo-troubleshooting.html#2-%E5%A6%82%E4%BD%95%E6%9B%B4%E6%94%B9%E5%B7%A6%E4%BE%A7IconFont-%E5%9B%BE%E6%A0%87)
    - [取消文章目录的自动编号](https://hwame.top/20200520/hello-hexo-troubleshooting.html#3-%E5%A6%82%E4%BD%95%E5%8F%96%E6%B6%88%E6%96%87%E7%AB%A0%E7%9B%AE%E5%BD%95%E7%9A%84%E8%87%AA%E5%8A%A8%E7%BC%96%E5%8F%B7)
    - [修改代码颜色字体](https://hwame.top/20200520/hello-hexo-troubleshooting.html#4-%E5%A6%82%E4%BD%95%E4%BF%AE%E6%94%B9%E4%BB%A3%E7%A0%81%E5%AD%97%E4%BD%93)
    - [设置文章图片居中](https://hwame.top/20200520/hello-hexo-troubleshooting.html#4-3-%E5%A6%82%E4%BD%95%E4%BD%BF%E6%96%87%E7%AB%A0%E5%9B%BE%E7%89%87%E5%B1%85%E4%B8%AD)
    - [添加文章摘要描述](https://hwame.top/20200520/hello-hexo-troubleshooting.html#5-%E5%A6%82%E4%BD%95%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E6%8F%8F%E8%BF%B0)
    - [调整菜单栏高度](https://hwame.top/20200520/hello-hexo-troubleshooting.html#13-%E8%B0%83%E6%95%B4%E8%8F%9C%E5%8D%95%E6%A0%8F%E9%AB%98%E5%BA%A6)
    - [添加RSS订阅功能](https://hwame.top/20200520/hello-hexo-troubleshooting.html#16-%E6%B7%BB%E5%8A%A0RSS%E8%AE%A2%E9%98%85%E5%8A%9F%E8%83%BD)
+ **③页面魔改**
    - [文章图片点击放大](https://hwame.top/20200520/hello-hexo-troubleshooting.html#6-%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E7%82%B9%E5%87%BB%E5%9B%BE%E7%89%87%E6%94%BE%E5%A4%A7)
    - [添加「相册」页面](https://hwame.top/20200520/hello-hexo-troubleshooting.html#7-%E6%B7%BB%E5%8A%A0%E3%80%8C%E7%9B%B8%E5%86%8C%E3%80%8D%E9%A1%B5%E9%9D%A2)
    - [自定义左下角信息](https://hwame.top/20200520/hello-hexo-troubleshooting.html#11-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B7%A6%E4%B8%8B%E8%A7%92%E4%BF%A1%E6%81%AF)
    - [代码块添加一键复制](https://hwame.top/20200520/hello-hexo-troubleshooting.html#12-%E4%BB%A3%E7%A0%81%E5%9D%97%E6%B7%BB%E5%8A%A0%E4%B8%80%E9%94%AE%E5%A4%8D%E5%88%B6)
    - [隐藏valine版权信息](https://hwame.top/20200520/hello-hexo-troubleshooting.html#14-%E5%A6%82%E4%BD%95%E9%9A%90%E8%97%8Fvaline%E7%89%88%E6%9D%83%E4%BF%A1%E6%81%AF)
    - [添加回到顶部](https://hwame.top/20200520/hello-hexo-troubleshooting.html#15-%E6%B7%BB%E5%8A%A0%E5%9B%9E%E5%88%B0%E9%A1%B6%E9%83%A8)
    - [设置文章置顶](https://hwame.top/20200520/hello-hexo-troubleshooting.html#17-%E8%AE%BE%E7%BD%AE%E6%96%87%E7%AB%A0%E7%BD%AE%E9%A1%B6)
    - [添加文章更新时间](https://hwame.top/20200520/hello-hexo-troubleshooting.html#18-%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E6%9B%B4%E6%96%B0%E6%97%B6%E9%97%B4)
    - [添加搜索引擎收录](https://hwame.top/20200520/hello-hexo-troubleshooting.html#19-%E6%B7%BB%E5%8A%A0%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E%E6%94%B6%E5%BD%95)


## 注意事项
### ①Gitee同步
- 【迁移同步】由于众所周知的原因，不论是Github网页/API还是jsdelivrCDN, 都经常会挂掉导致无法访问，因此在 [Gitee-hwame](https://gitee.com/hwame) 上导入了该项目 [Gitee-hwame/blog](https://gitee.com/hwame/blog) 并且设置了自动同步，后续考虑使用 **GiteePages**
- 【图床修改】Gitee图床仓库不允许设置为「公开」，故未导入 [Github图床hwame/pics](https://github.com/hwame/pics) ，后续会将 【博客图片及资源】迁移到博客目录下，且不再使用 jsdelivrCDN 加速Github静态资源
- 【提交部署】Github与Gitee配置的邮箱不一致，提交代码有可能出问题，采取如下两种措施：
  + **(1)** Gitee自动同步 [Github-hwame/hwame.github.io](https://github.com/hwame/hwame.github.io) 仓库，部署时直接提交到GitHub即可
  + **(2)** Gitee代码提交方式配置svn，自动同步若有延时，可直接通过svn提交
- 【资源加速】若后续使用 GiteePages 而停用 GithubPages，可能会导致图片加载慢的问题，后续再考虑【 **图片压缩** 】、【 **魔改Fancy Box** 】等优化方式进行 **静态资源加速**

### ②添加README

由于Hexo渲染引擎的原因，`README.md`将被解析为`README.html`，将其放在`./source/`目录下（与`CNAME`一致）。同时修改 **站点配置文件** `./_config.yml` ：

```yaml
# Directory
skip_render: README.md
```

### ②添加LICENSE
项目使用 MIT 许可协议，文件添加方式基本与上文 [添加README](#%E6%B7%BB%E5%8A%A0readme) 相同，只需要将 LICENSE 文件放在 `./source/` 目录下（与 `CNAME` 一致）即可，无需修改站点配置文件。

