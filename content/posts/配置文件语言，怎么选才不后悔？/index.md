---
title: 配置文件语言，怎么选才不后悔？
date: 2025-01-25 21:21:23
tags: ["标记语言"]
comments: true
---

配置文件这种东西，没人喜欢专门去学它。你打开一个陌生的项目，看到满屏的缩进、引号、中括号，第一反应大概率是——这写的什么天书？

但偏偏每个项目用的语言还不一样。JSON、XML、INI、YAML、TOML……名字一个比一个抽象，语法一个比一个有个性。没办法，还是得认一认。

下面简单聊聊这五种最常见的配置文件语言，帮你下次碰到它们的时候，少上几次百度。

## 1. JSON

JSON 是 Douglas Crockford 基于 JavaScript 的语法整出来的，2000 年就有了第一版标准，2013 年 ECMA 正式给它发了"身份证"。

**它长这样：**

```json
{
  "addr": "127.0.0.1",
  "port": 8080,
  "custom": {
    "args": ["--debug", "--verbose"],
    "timeout": 10
  }
}
```

看着就是一堆花括号、方括号和引号。机器读起来飞快，人读起来嘛——如果你的配置文件超过三层嵌套，眼睛就开始打架了。

**优点：** 几乎所有语言都能解析，生态无敌。

**缺点：** 早期版本连注释都不支持，写配置体验一般。


## 2. XML

XML 是 W3C 在 1998 年正式发布的，本质上是从一个更老的标准 SGML 精简而来。当年 Web 服务盛行的时候，XML 可是绝对的主角。

**它长这样：**

```xml
<app>
  <addr>127.0.0.1</addr>
  <port>8080</port>
  <custom>
    <args>--debug</args>
    <args>--verbose</args>
    <timeout>10</timeout>
  </custom>
</app>
```

如果你会写 HTML，XML 几乎是零门槛，因为它就是同一套标签哲学。但问题也在这：标签太多，文字全淹没在尖括号里了。

**优点：** 语义自描述，基本不需要额外注释。

**缺点：** 啰嗦，体积大，现在被 JSON 抢走了不少饭碗。


## 3. INI

INI 文件是 Windows 系统的原住民，早期几乎所有 Windows 程序的配置都用它。有时候你也看到它叫 `.cfg`、`.conf` 或 `.txt`。

**它长这样：**

```ini
[app]
addr = 127.0.0.1
port = 8080
[custom]
args = --debug --verbose
timeout = 10
```

方括号分节，下面是键值对，简单到不用学就会写。但也因为太简单，稍微复杂点的数据结构（比如列表、嵌套）就搞不定了。

**优点：** 可读性天花板级别的简洁。

**缺点：** 缺乏标准，不同解析器各玩各的，碰到嵌套当场投降。


## 4. YAML

YAML 最早是 2001 年由 Clark Evans 搞出来的，名字经历了从 "Yet Another Markup Language" 到 "YAML Ain't a Markup Language" 的华丽转身，明显是想和 XML 划清界限。

**它长这样：**

```yaml
app:
  addr: 127.0.0.1
  port: 8080
  custom:
    args:
      - --debug
      - --verbose
    timeout: 10
```

YAML 最大的特色就是用缩进表示层级，跟 Python 是同门师兄。看起来干净到像在写提纲，但成也缩进、败也缩进——空格和 Tab 搞混的那一刻，调试起来想砸键盘。

**优点：** 可读性极高，功能全面。

**缺点：** 怕缩进错误，学习曲线不友好。


## 5. TOML

TOML 全称 "Tom's Obvious, Minimal Language"，由 GitHub 联合创始人 Tom Preston-Werner 发起，目标就是做一个比 INI 强、比 YAML 乖、比 JSON 更合适当配置的语言。

**它长这样：**

```toml
[app]
addr = "127.0.0.1"
port = 8080
[custom]
args = ["--debug", "--verbose"]
timeout = 10
```

第一眼像 INI 的升级版，但加了明确的数据类型和嵌套语法。Python 的 `pyproject.toml` 和 Rust 的 `Cargo.toml` 都用它，这算是行业里一张很有分量的推荐信。

**优点：** 语法直觉，类型明确。

**缺点：** 相对年轻，网上资料远不如 JSON 丰富。


## 最后怎么选？

个人经验之谈：

- 超级简单的小项目 → **INI**，不用费脑子。
- 需要复杂数据结构 → **JSON**，哪里都认你。
- 追求人类可读且不怕缩进 → **YAML**，写完自己看着也舒坦。
- 生产项目、团队协作 → **TOML**，站在 INI 肩膀上，少了很多坑。

说到底，无脑用 JSON 也没什么毛病。（毕竟配置写好之后，除了改 bug，谁也不会天天去看它。）
