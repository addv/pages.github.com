---
title: Home
layout: wikistyle
---

# 介绍 Pages #

GitHub 的页（Pages）特性允许你，通过简单的推送内容到你的寄宿在 GitHub 的一个仓库，来发布内容到网络。有两种不同的页型可供你创建：用户页和项目页。

## 用户和组织的页面 ##

假设你的 GitHub 用户名是“alice”，如果你创建一个名为`alice.github.com` 的 GitHub 仓库，提交一个名为文件 `index.html` 的文件到 `master` 支，并将它推送到 GitHub，那么这个文件就会自动发布到 <http://alice.github.com/>。

第一次推送时，可能要花上十分钟才能使得内容有效。

对于组织页也是同样的。如果你的组织帐号为“PlanEx”，于公司名下创建的仓库 `planex.github.com` 会发布页面到 <http://planex.github.com/>。

实例：[github.com/defunkt/defunkt.github.com](http://github.com/defunkt/defunkt.github.com/) → <http://defunkt.github.com/>。

## 项目页 ##

假设你的 GitHub 用户名是“bob”并且你有一个现成的仓库名为 `fancypants`。如果你在你的仓库中创建了一个新的根支命名为 `gh-pages`，那么，任何推送到那里的内容都会被发布到 <http://bob.github.com/fancypants/>。

为了创建一个新的根支，第一是确保你的工作目录，通过提交和隐藏变更的过程，是干净的。<span style="color: #a00;">下面的操作会将任何未提交的文件丢弃！你运行这些代码或许应该是在你的仓库的一个新副本里。</span>

	$ cd /path/to/fancypants
	$ git symbolic-ref HEAD refs/heads/gh-pages
	$ rm .git/index
	$ git clean -fdx

运行过这些，你就有了一个空的工作目录（别怛心，你的主仓还存于 `master` 支里）。现在你可以在这个支里创建创建一些内空并将其推送到 GitHub。比如：

	$ echo "My GitHub Page" > index.html
	$ git add .
	$ git commit -a -m "First pages commit"
	$ git push origin gh-pages

第一次推送时，可能要花上十分钟才能看到这些内容。

实例：[github.com/defunkt/ambition@gh-pages](http://github.com/defunkt/ambition/tree/gh-pages) → <http://defunkt.github.com/ambition>。

### 项目页产生器 ###

如果你不想要通过上面的步骤来生成你的分支，或你只想简单地有个一般的页面，你可以使用我们的页面产生器来给你创建你的 gh-pages 分支并置入一张默认页。

首先，导航到你的项目，并点击顶部右边的“Admin”按钮。

> ![Admin button](admin_button.png)

接着点击“GitHub Pages”复选框。

> ![github pages checkbox](ghpages_checkbox.png)

一个弹出框就会出现。点击“Automatic GitHub Page Generator”

> ![github pages popup generator](ghpages_popup.png)

当你的页面产生后，你可以检查你的新分支：

	$ cd Repos/ampere
	$ git fetch origin
	remote: Counting objects: 92, done.
	remote: Compressing objects: 100% (63/63), done.
	remote: Total 68 (delta 41), reused 0 (delta 0)
	Unpacking objects: 100% (68/68), done.
	From git@github.com:tekkub/ampere
	 * [new branch]      gh-pages     -> origin/gh-pages
	$ git checkout -b gh-pages origin/gh-pages
	Branch gh-pages set up to track remote branch refs/remotes/origin/gh-pages.
	Switched to a new branch "gh-pages"

# 为复杂布局使用 Jekyll #

除了支持正规的 HTML 内容，GitHub Pages 还支持 [Jekyll](http://github.com/mojombo/jekyll/)，它是由我们当中的 Tom Preston-Werner 编写的一个简单的、博客化为静态站点的产生器。使用 Jekyll 可以很方便地制作全站点的标题和页脚而不必将它们在一页页间拷贝。它也提供了智能化的博客支持和其他高级模板特性。

当你将内容推送到你的仓库后，每一张 GitHub 页都是通过 Jekyll 来运行。因为一个普通的 HTML 站点也是一个有效的 Jekyll 站点，所以你不必为保证你的标准的 HTML 文件不变而再做什么事。Jekyll 有一个详尽的 [README](http://github.com/mojombo/jekyll/blob/master/README.textile) 用以解说它的特性和用法。

从 2009 年 4 月 7 日起，你可以通过你的 `_config.yml` 来配置绝大部分的 Jekyll 设置。既是绝大部分，你便可以选择你的永久链接样式和选择用 RDiscount 来渲染你的 Markdown 文件 而不用默认的 Maruku。我们不提供的选项只有下面这些：

	safe: true
	source: <your pages repo>
	destination: <the build dir>
	lsi: false
	pygments: true

当你推送到 GitHub 后，如果你的 Jekyll 站点没有正确地转换，最好在本地运行转换器，以便你可以查出任何的解析错误。为了做这个，你应该使用和我们同样的版本。

我们目前使用 <span style="font-weight: bold; color: #0a0;">Jekyll 0.11.0</span> 并且运行它是用类似这样的命令：

	jekyll --pygments --safe

从 2009 年 12 月 27 日起，你可以完全地摆脱 Jekyll 处理，只需要在你的页面仓库的根下创建一个名为 `.nojekyll` 的文件并把它推送到 GitHub。如果你的站点使用以下划线起头的目录，这样做很有必要，因为 Jekyll 将这些当作特殊目录而不会将它们拷到最终目的地。

如果你希望 Jekyll 有某个特性，请随意去 fork 它（从它发出分支），（实现那个特性，）再发送一个 pull request（并支请求）。我们很乐意得到用户的贡献。

实例：[github.com/pages/pages.github.com](http://github.com/pages/pages.github.com/) → <http://pages.github.com/>。

# 定制 Domains #

GitHub Pages 允许在你的页中你指向一个你选择的域名。

假设你有一个域名为 [example.com](http://example.com/)，此外，你的 GitHub 用户名是“charlie”，并且你已经发布了一个用户页在 <http://charlie.github.com/>。现在你想要在你的浏览器中载入 <http://example.com/>，而让它显示的内容来自 <http://charlie.github.com/>。

首先要做的是在你的仓库的根下创建一个名为 `CNAME` 的文件。它应该包含你的域名像这样：

	example.com

推送这个新文件到 GitHub。服务器会将你的页面设置为隶属于 [example.com](http://example.com/)，并创建重定向为从 [www.example.com](http://www.example.com/) 和 [charlie.github.com](http://charlie.github.com/) 至 [example.com](http://example.com/)。

接着，你需要访问你的域名注册商或 DNS 主机，并对你的域名加个记录。对于一个子域像 `www.example.com` 来说，你仅要创建一个 CNAME 记录指向 `charlie.github.com`。如果你正使用一个顶级域像 `example.com`，你必须使用一个 A 记录指向 `207.97.227.245`。**不要对一个顶级域用 CNAME 记录**，它可能会对其他服务如 email 有坏的影响。许多 DNS 服务器会在一个 TLD 上把你设为一个 CNAME，即便你不是。要记得可能会花上一整天才会使 DNS 变化得到扩散，所以要有耐心。

实例：[github.com/mojombo/mojombo.github.com](http://github.com/mojombo/mojombo.github.com/) → <http://tom.preston-werner.com/>。

当然，以上内容对于项目或组织的页也是行得通的。

# 定制 404 页面 #

如果你在你的仓库的根下提供了一个 `404.html`，它会被用来取代默认的 404 页面。注意 Jekyll 生成页不起作用，它<i>必须</i>是一个 html 文件。

实例：<http://github.com/tekkub/tekkub.github.com/blob/master/404.html> → <http://tekkub.net/404.html>。
