# 梧桐兼雨 · 博客园个性化主题

这是为个人博客 [潇湘梧主](https://www.cnblogs.com/followbylyj/) 定制的博客园主题。

项目以 CNblogs Theme Sakura 为基础，保留了首页头图、随笔卡片、文章目录、评论区美化等功能，并对顶栏、品牌标识、社交入口、favicon 与移动端布局进行了重新设计。

## 主题特色

- “梧桐兼雨”紫金羽毛品牌标识
- 淡紫色毛玻璃固定顶栏
- 无外链依赖的 SVG 顶栏图标与 favicon
- 首页随机头图、座右铭和社交链接
- 首页随笔卡片化展示
- 随笔页头图、文章目录和代码复制按钮
- 评论区、赞赏区和返回顶部按钮美化
- 桌面端与移动端响应式导航
- B 站、GitHub、微博、X、知乎和邮件入口

## 文件结构

```text
.
├── cnblogs-theme.css     # 博客园“页面定制 CSS”
├── cnblogs-theme.js      # 主题核心逻辑
├── cnblogs-sidebar.html  # 侧栏公告配置与主题脚本入口
├── cnblogs-footer.html   # 页脚脚本与可选装饰效果
├── README.md             # 项目说明和部署文档
├── CHANGELOG.md          # 版本变更记录
└── .gitignore            # Git 忽略规则
```

GitHub 约定文件 `README.md`、`CHANGELOG.md` 和 `.gitignore` 保留标准名称；博客园部署文件统一使用 `cnblogs-` 前缀，避免与其他项目文件混淆。

## 使用前提

1. 拥有博客园账号和个人博客。
2. 已申请并开通博客园 JavaScript 权限。
3. 博客皮肤应与当前主题所依赖的博客园 DOM 结构兼容。
4. 建议先在本地或测试博客验证，再覆盖线上配置。

## 部署方法

### 1. 上传核心脚本

在博客园文件管理中上传 `cnblogs-theme.js`，记录上传后的实际 URL。

如果博客园自动修改了文件名，需要同步修改 `cnblogs-sidebar.html` 顶部的脚本地址：

```html
<script src="https://blog-static.cnblogs.com/files/你的目录/cnblogs-theme.js?v=版本号"></script>
```

修改脚本后应同步递增查询参数，避免 CDN 和浏览器继续使用旧缓存：

```text
?v=20260809-1
```

### 2. 配置 CSS

将 `cnblogs-theme.css` 的完整内容复制到博客园后台的“页面定制 CSS”中并保存。

### 3. 配置侧栏

将 `cnblogs-sidebar.html` 的内容复制到博客园后台对应的侧栏公告或自定义 HTML 配置区域。

主要配置项：

```js
profile.avatar       // 头像
profile.notice       // 首页公告
topImg.homeTopImg    // 首页头图
topImg.notHomeTopImg // 随笔页头图
topInfo.title        // 首页主标题
topInfo.text         // 首页座右铭
topInfo.github       // GitHub
topInfo.weibo        // 微博
topInfo.bilibili     // B 站个人主页
topInfo.twitter      // X 主页
topInfo.zhihu        // 知乎
topInfo.mail         // 邮件或联系页面
```

### 4. 配置页脚

将 `cnblogs-footer.html` 的内容复制到博客园后台的页脚 HTML 配置区域。

页脚中的 Live2D、雪花、鼠标点击、图片缩放和 NProgress 均属于可选功能。第三方 CDN 不稳定时，可以直接删除对应模块。

### 5. 刷新缓存

保存后关闭旧标签页，重新打开博客并使用 `Ctrl + F5` 强制刷新。favicon 的缓存可能需要清除站点缓存后才会更新。

## 上传到 GitHub

建议将 GitHub 仓库命名为 `cnblogs-theme-wutong`，仓库说明可填写：

> 为“梧桐兼雨”博客定制的博客园 Sakura 主题。

在 GitHub 创建一个空仓库时，不要额外生成 README、`.gitignore` 或许可证，以免与本地文件冲突。随后在 `Blogcode` 目录运行：

```bash
git init
git add .
git commit -m "Initial release of Wutong CNBlogs theme"
git branch -M main
git remote add origin https://github.com/你的用户名/cnblogs-theme-wutong.git
git push -u origin main
```

GitHub 只用于保存和展示源码，不会自动更新博客园。每次发布仍需：

1. 将 `cnblogs-theme.js` 上传到博客园文件管理。
2. 确认 `cnblogs-sidebar.html` 使用新的脚本 URL 和缓存版本。
3. 将 CSS、侧栏和页脚内容分别复制到博客园后台。

首次公开仓库前，建议再次检查 `cnblogs-sidebar.html` 中的头像、社交主页、邮箱和其他个人链接是否适合公开。当前项目暂不附加许可证，原因见文末“许可证说明”。

## 顶栏实现

顶栏保留博客园原始导航 ID，以维持首页、联系、订阅和管理功能；Logo、友链、赞赏、关于及各栏目图标由 `cnblogs-theme.js` 动态生成。

新版顶栏不再依赖 Font Awesome 图标：

- Logo 使用内嵌 SVG 月牙羽毛图案。
- 导航栏目使用统一线性 SVG。
- favicon 使用内嵌 SVG Data URL。
- 滚动行为仅切换 `is-scrolled` 状态类。
- CSS 使用 Flex 布局，不再通过固定 `margin-left` 推算 Logo 空间。

## 外部资源与稳定性

新版顶栏本身不依赖图标 CDN，但主题其他模块仍使用一些外部资源：

- 博客园静态资源 CDN
- 阿里 Iconfont 与 Font Awesome（旧文章卡片和头图图标）
- 随机头图 API
- Live2D、图片缩放、鼠标点击和雪花脚本
- 头像及赞赏二维码图床

如果页面再次出现加载缓慢，建议优先停用 `cnblogs-footer.html` 中的 Live2D 和装饰性脚本，并避免重复加载旧版 jQuery。

## 开发与维护建议

- 正式脚本统一使用 `cnblogs-theme.js`，不要继续创建 `blog2.js`、`blog3.js` 等临时版本。
- 每次修改前提交一次 Git，使用提交历史代替文件复制备份。
- 所有源码保存为 UTF-8，避免中文被错误转换为 GBK/ANSI。
- 修改后使用 `node --check cnblogs-theme.js` 检查 JavaScript 语法。
- 不要删除博客园原始导航 ID，否则管理、订阅等功能可能失效。
- 发布公开仓库前检查头像、二维码和个人链接是否适合公开。

## 致谢与来源

本项目基于以下公开主题继续定制：

- [Zou-Wang/CNblogs-Theme-Sakura](https://github.com/Zou-Wang/CNblogs-Theme-Sakura)
- 博客园及原主题所使用的 Silence/Sakura 相关样式与脚本

新版紫金顶栏、SVG 品牌标识、导航图标、favicon、兼容性修复及个人配置是在原主题基础上的二次开发。

## 许可证说明

上游仓库页面未显示明确的许可证文件，因此本仓库暂不附加新的开源许可证。源码可以用于个人备份和学习；如需公开分发、授权他人复用或用于商业项目，请先确认上游代码与第三方素材的许可范围，并保留原作者署名。
