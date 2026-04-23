---
title: 白嫖服务器 + .link 顶级域名
date: 2023-07-19 13:33:10
tags: 前端
---
*观前提示：Vercel 和 GitHub 在国内被墙了，没有梯子就歇菜吧*

# 注册域名

首先来到白嫖域名的网站：[https://www.dynadot.com/register-your-free-link-domain](https://www.dynadot.com/register-your-free-link-domain)

![检查域名可用性](images/白嫖服务器-link-顶级域名/1.png)

在搜索框里填上你想要注册的域名，如果可以注册就会是图中的样式，点 Next

会提示你注册账号，按着提示填就行。实测一个账号只能注册一个免费域名，所以这一步是必须的。

![注册账号](images/白嫖服务器-link-顶级域名/2.png)

这里有一个要注意的地方就是在页面最下方 Create Account 上面有三个勾选框，第一个取消掉，第二第三个勾上。

填完以后点 Create Account 就行了。

下一步是验证账号，打开邮箱，它会一次性给你发很多个邮件，找到验证那一封，大概长这样：

![验证邮件](images/白嫖服务器-link-顶级域名/3.png)

点击验证链接，会跳转到浏览器，然后显示网站的登录页面，我们用刚刚创建的账号登录。

登录完成后跳转到账号的 dashboard，在页面的右侧会有个设置安全问题，照着提示填就行。

打开域名管理界面：

![域名管理](images/白嫖服务器-link-顶级域名/4.png)

刚刚注册的链接会显示在这，点进去：

![点进域名](images/白嫖服务器-link-顶级域名/5.png)

往下划，找到 DNS Settings：

![DNS-Settings](images/白嫖服务器-link-顶级域名/6.png)

点进去，在展开的选项中选第一个 Name Servers：

![Name-Servers](images/白嫖服务器-link-顶级域名/7.png)

我们先把这个网页搁置，去搞 CloudFlare。

# CloudFlare 设置

打开 [CloudFlare 仪表板](https://dash.cloudflare.com/)（如果你还没有账号，点进去页面上的注册链接，两分钟就注册好了）

![主页](images/白嫖服务器-link-顶级域名/8.png)

（接下来开始实机演示就进行不下去了，所以没有配图了）

点击右边的蓝色按钮“添加站点”，跳转到添加站点页面，输入刚刚注册的域名，点击按钮。

跳转到选择方案界面，往下划选择 Free 方案，点击继续。

等待扫描一会，划到下方一堆 DNS 记录（一条一条末尾有个蓝色删除链接的）

把它们全删除（是的，全部删除，最下面的两个点击编辑就会展开，里面也有删除链接，也都删除）

点击继续，准备下一阶段。

# 回到域名注册的网站

点击继续后会跳转到下一个页面，往下划找到 Name Servers，它们前面有一个 CloudFlare 的图标（橙色的云）

还记得之前离开域名注册的最后一个步骤吗？选中了 Name Servers 然后搁置，现在将 CloudFlare 提供的两个 Name Servers 填上去，填完后点击保存按钮。

接下来是一个等待的步骤，一般几分钟就好了。在注册 CloudFlare 的邮箱收到提示后（或者在主页显示这个域名已经可用后），回到 CloudFlare 仪表板的主页（即之前第一次打开仪表板的链接）。回顾一下之前的图片：

![主页](images/白嫖服务器-link-顶级域名/8.png)

像这样的就是可用了。点进去你的域名，进到 DNS 记录页面：

![DNS记录](images/白嫖服务器-link-顶级域名/9.png)

这是我已经设置好的样子，你的应该是空的，点击图中右上方的添加记录按钮，你需要添加两个，一个需要在左侧的选项中选则“A”，一个是“CNAME”：

![A](images/白嫖服务器-link-顶级域名/10.png)
![CNAME](images/白嫖服务器-link-顶级域名/11.png)

这个页面就可以搁置了，接下来进行 GitHub 部分。

# GitHub 设置

（首先你要有一个 GitHub 账号，如果没有就去注册一个）

你需要在 GitHub 上新建一个仓库，然后在本地用 git 连接，这将作为你的网站根目录（不用 git 只用 GitHub 网页版理论上也是可行的，如果你实在用不来 git 的话）

最好再新建一个名为“index.html”的文件，内容是“Hello World”或者其他什么的，这能更好的表示你的网站成功运行。

*如果你打算使用框架（包括我的博客框架 Hexo）之类的，最好在下一步 vercel 设置之前就在 GitHub 弄好仓库，这样在 vercel 新建项目的时候可以自动识别，或者在新建项目的时候手动选择框架。*

所有 GitHub 设置到此为止（不考虑后续网站开发），接下来是 vercel 部分。

# Vercel 设置

进入 [vercel 的 dashboard 页面](https://vercel.com/dashboard)（如果你没有 Vercel 账号，用 GitHub 账号注册一个，然后再回来继续）

点击 Add New，选择 Project：

![vercel](images/白嫖服务器-link-顶级域名/12.png)

然后选中刚刚创建的 GitHub 仓库，点击 import：

![GitHub-repo](images/白嫖服务器-link-顶级域名/13.png)

按照提示完成项目的创建，进入到项目页面，点击上方横向菜单最后一个 Settings，然后点击左侧竖向菜单的 Domains：

![Settings-Domains](images/白嫖服务器-link-顶级域名/14.png)

在输入框中输入新注册的域名，点击 Add：

![Add](images/白嫖服务器-link-顶级域名/15.png)

三个选项自己选择，如果不懂就选第一个。选好以后会跳出来两个配置未确认页面：

![config-A](images/白嫖服务器-link-顶级域名/16.png)
![config-CNAME](images/白嫖服务器-link-顶级域名/17.png)

（因为域名是瞎填的，所以会报错）

接下来进行最后一步，回到 CloudFlare 页面。

# 回到 CloudFlare

回顾一下 CloudFlare 最后的步骤：

![A](images/白嫖服务器-link-顶级域名/10.png)
![CNAME](images/白嫖服务器-link-顶级域名/11.png)

对照 vercel 的两个未确认配置，填上去，保存，就行了。

打开你的 .link 域名，如果你在这个地方：

![Add](images/白嫖服务器-link-顶级域名/15.png)

没有选第三个的话，www.你的域名.link 和 你的域名.link 都是可以打开的，如果选了第三个就只有后者能打开。

如果不出意外，这时候访问你的网站，就能展示出你 GitHub 仓库（即网站根目录）的内容了。

注：这个博客网站也是这么创建的，用了 Hexo 作为后端，以及 next 主题。如果你也想这样配置你的网站，自己上网查或者联系我获得帮助都可以，这方面网上资料很多的。