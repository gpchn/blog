---
title: 使用 oh-my-posh 美化 CMD 和 PowerShell
date: 2025-02-09 15:04:12
tags: [终端, 美化]
---

我个人的使用习惯，在 Linux 上使用 zsh，在 Windows 上 CMD 和 PowerShell 混用。Linux 终端的美化非常好办，安装 oh-my-zsh 插件，搭配 powerlevel10k 主题，可以说是一键美化。

![Linux 美化效果](images/使用-oh-my-posh-美化-CMD-和-PowerShell/1.png)

但 Windows 终端，愿意折腾的人不多，顶多从 Microsoft Store 下载一个 Windows Terminal。如何真正强化 CMD 和 PowerShell，使其拥有比拟 zsh 的体验呢？[oh-my-posh](https://ohmyposh.dev/) 就是答案。

接下来我将介绍如何使用 oh-my-posh 美化 CMD 和 PowerShell。

## 0. 安装 Nerd Font

请务必下载安装至少一种 Nerd Font 字体，以保证终端美化体验。

Nerd Font 是一类特殊的字体，比普通字体包含了更多特殊符号和图标，在终端上显示各种图标都靠它了。

Nerd Font 字体下载地址：[https://www.nerdfonts.com/](https://www.nerdfonts.com/)

拿我使用的 FiraCode Nerd Font 举例，从官网进入 GitHub Release 页面，下载压缩包后解压，里面有 ttf 等各种格式的文件夹，全选 ttf 文件夹里所有字体文件，右键安装即可。

## 1. 安装 oh-my-posh

官网提供了三种安装方式，但现在已经可以用 Microsoft Store 安装了，但考虑到路径问题，我选择手动安装。

官网文档中详细介绍了安装方法：[https://ohmyposh.dev/docs/installation/windows](https://ohmyposh.dev/docs/installation/windows)

截至 2025 年 2 月 9 日，oh-my-posh 最新版本为 24.19.0。我在这里贴一段翻译后的官网原文，以便读者一站解决。

### 使用 winget 安装

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

### 手动安装

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ohmyposh.dev/install.ps1'))
```

### 使用 chocolatey 安装

官网注：这个包管理器由社区维护，可能不提供最新版本。

```powershell
choco install oh-my-posh
```

我原先就安装了 winget，因此使用 winget 安装。安装完成后，新开一个 PowerShell 终端，输入 `oh-my-posh --version`，如果显示版本号，则表示安装成功。

## 2. PowerShell 配置 oh-my-posh

我选择的是 [powerlevel10k_rainbow](https://ohmyposh.dev/docs/themes/powerlevel10k_rainbow) 主题，和 oh-my-zsh 的 powerlevel10k 很像，只是不能自定义，只有四种 powerlevel10k 主题供选择，详见官网。安装方法如下：

### 找到配置文件

首先查看 PowerShell 配置文件的路径，在 PowerShell 中输入以下命令：

```powershell
$PROFILE
```

此时会显示配置文件的路径，例如：

`C:\Users\gpchn\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`

但这个配置文件不一定存在，如果不存在，需要手动创建。

### 写入配置

打开配置文件，写入以下内容：

```powershell
# 以下四条命令：导入 PowerShell 的插件，有些需要下载，可自行上网搜索
#Import-Module posh-git
#Import-Module Terminal-Icons
#Import-Module PSReadLine
#Import-Module ZLocation

# 这条必须要有，可以只有这一条
# 其中 -c C:\Users\...\powerlevel10k_rainbow.omp.json 是指定终端主题，可自行修改或删除
oh-my-posh init pwsh -c C:\Users\gpchn\AppData\Local\Programs\oh-my-posh\themes\powerlevel10k_rainbow.omp.json | Invoke-Expression

# 设置 Tab 自动补全，这个命令是可选的
Set-PSReadLineKeyHandler -Key Tab -Function MenuComplete
```

保存并关闭文件，重新打开 PowerShell 终端，即可看到美化效果。

**注：首次启动会消耗较长时间，PowerShell 启动速度慢的缺点向来饱受诟病，我这即使缓存后也需要 3 秒多……**

美化效果（powerlevel10k_rainbow 主题下）：

![PowerShell 美化效果](images/使用-oh-my-posh-美化-CMD-和-PowerShell/2.png)

### 选择主题 & 安装插件

大体弄好了以后就可以细心雕琢配置了，如上所述，如果想要自定义主题，可以在官网查看所有主题：[https://ohmyposh.dev/docs/themes](https://ohmyposh.dev/docs/themes)，也可以在 PowerShell 中运行 `Get-PoshThemes` 命令，输出所有的主题。如果没有喜欢的，你甚至可以自己写一个主题配置文件。

可以安装一些 PowerShell 插件来增强功能，但代价是启动时间。

## 3. CMD 配置 oh-my-posh

### 安装 clink

大体上和 PowerShell 差不多，只是 CMD 没有什么配置文件，因此我们需要安装 `clink` 来增强 CMD 的功能，在 [官网](https://chrisant996.github.io/clink/) 右上方下载最新版本。（注：下载用 GitHub Release 托管，需科学上网）

安装完成后打开一个 CMD 终端，输一些命令试试有没有自动补全功能，有的话就说明安装成功。

### 配置 clink

在 clink 的安装目录下新建一个 `oh-my-posh.lua`，这是 clink 的配置文件，写入以下内容：

```lua
-- 其中 -c C:\Users\...\powerlevel10k_rainbow.omp.json 是可选命令，用于指定终端主题，可自行修改或删除
-- 要改命令就在这个模板上改
-- load(io.popen('oh-my-posh init cmd [这里面添参数]'):read("*a"))()
load(io.popen('oh-my-posh init cmd -c C:\\Users\\gpchn\\AppData\\Local\\Programs\\oh-my-posh\\themes\\powerlevel10k_rainbow.omp.json'):read("*a"))()
```

保存并关闭文件，重新打开 CMD 终端，即可看到美化效果。

美化效果：

![CMD 美化效果](images/使用-oh-my-posh-美化-CMD-和-PowerShell/3.png)

clink 是个很强大的工具，可使用右箭头补全命令，还有更多功能可自行探索。

### 巧用 doskey 命令

在 CMD 中，`doskey` 命令可以用来设置别名，类似于 Linux 中的 alias。例如 `doskey ls=dir`，这样在 CMD 中输入 `ls` 就相当于输入 `dir`。

在你的用户的 `AppData\Local\clink` 路径下新建一个 `clink_start.cmd`，写入以下内容：

```batch
@echo off
doskey ls=dir
doskey rm=del
doskey cp=copy
doskey mv=move
doskey clear=cls
doskey pwd=chdir
doskey cat=type
doskey less=type
```

这是一些常用 Linux 命令对应的 CMD 命令，你可以根据需要自行修改。保存并关闭文件，重新打开 CMD 终端，即可使用这些别名。

![展示别名](images/使用-oh-my-posh-美化-CMD-和-PowerShell/4.png)

## 4. 拓展：GitBash 美化

在 GitBash 中，oh-my-posh 的美化效果和 PowerShell 差不多，只是主题选择较少，因为 GitBash 不能在 Windows Terminal 中打开（也可能是我没找到方法，懒得折腾），它用的是自己的终端模拟器。我在它模拟器的设置里找不到换 Nerd Font 的方法，因此不能使用带图标的主题（只能用名字带 .minimal 后缀的主题）。

### 转移主题文件

将你看中的主题文件（xxx.omp.json）复制到 GitBash 的目录下面，随便找个地方，例如我放在了 `/etc/oh-my-posh/xxx.nmp.json`

### 登录时初始化 oh-my-posh

在 `~/.profile` 中输入以下命令（如果文件不存在就新建一个）：

```bash
# 将路径替换为你存放主题文件的路径
eval "$(oh-my-posh init bash -c /path/to/xxx.omp.json)"
```

## 5. 局限性

需要指出，oh-my-posh 的美化很依赖终端模拟器，例如在 VSCode 中美化有时会直接失效，目前我找不到方法解决这个问题，应该是 VSCode 自带终端不好使。

## 6. 总结

使用 oh-my-posh 美化 CMD 和 PowerShell 的效果还是很明显的，但代价是启动时间。CMD 不怎么明显，美化前后都是不用等的延迟。PowerShell 每次启动往往要等待 3 秒以上，清理 C 盘删缓存后，延迟一度达到 7 秒，这个缺点是不可避免的。

PowerShell 语法又丑，启动又慢，体积又庞大，但有时候就得用它……内置 C# 了不起啊！
