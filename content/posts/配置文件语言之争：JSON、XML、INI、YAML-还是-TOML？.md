---
title: 配置文件语言之争：JSON、XML、INI、YAML 还是 TOML？
date: 2025-01-25 21:21:23
tags: [语言, 后端]
---

常见的配置文件语言有 JSON、XML、INI、YAML 和 TOML 等。配置文件的格式并没有规范可言，不同规模和种类的配置文件使用不同的语言很合常理。但五花八门的语言极大地增加了普通人修改配置文件的学习成本，遇到不熟悉的语言，往往需要费很大工夫查阅资料，才能搞清楚配置文件的结构和语法。下面我们来简单地了解一下这 5 种配置文件语言。

## 1. JSON (JavaScript Object Notation)

JSON 是由 Douglas Crockford 根据 JavaScript 的规范发明推广的，被设计为 JavaScript 的子集。最早的 JSON 标准于 2000 年发布，2013 年，ECMA 国际发布了 ECMA-404 标准，正式定义了 JSON 的数据交换格式，详细描述了 JSON 的语法和结构。

*以上内容参考了百度百科，[JSON](https://baike.baidu.com/item/JSON/2462549)*

### 语法格式

JSON 是一种简洁的数据交换格式，这种设计有利于机器读写，但有时可读性较差。其基本语法包括对象（键值对集合，相当于 Python 中的 dict）和数组。

```json
// 这是 JSON 中的注释
{
  "addr": "127.0.0.1",
  "port": 8080,
  "custom": {
    "args": ["--debug", "--verbose"]
    "timeout": 10
  }
}
```

### 优点

- 简洁明了，易于编写
- 广泛支持，几乎所有编程语言都有 JSON 解析库

### 缺点

- 早期版本不支持注释
- 复杂的数据结构不易读

## 2. XML (eXtensible Markup Language)

1996 年 7 月 W3C 在 Jon Bosak（SUN公司的网络技术专家）的建议下成立了 XML 规范制订小组，其目的是为了将标准通用标记语言 SGML（Standard Generic Markup Language）方便地应用于网络，参加规范制订的是一大批著名公司、学术机构代表和 SGML 专家。在他们的共同努力下，XML 1.0 建议书于 1998 年 2 月 10 日正式公布于众。

*以上内容参考了百度百科，[可扩展标记语言](https://baike.baidu.com/item/%E5%8F%AF%E6%89%A9%E5%B1%95%E6%A0%87%E8%AE%B0%E8%AF%AD%E8%A8%80/2885849)*

### 语法格式

XML 是 HTML 的子集，其语法包括标签（tag）、属性（attribute）和文本内容。

```xml
<!-- 这是 XML 中的注释 -->
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

### 优点

- 支持复杂数据结构
- 学习成本几乎没有，HTML 基础即可
- 自描述性强，基本不用写注释

### 缺点

- 语法冗杂，不易编写
- 文件体积较大
- 使用频率较低，逐渐被 JSON 取代

## 3. INI (Initialization File)

INI 在 Windows 系统中广泛使用，用于存储配置信息。有时候，INI文件也会以不同的扩展名，如 “.CFG”、“.CONF”、或是 “.TXT” 代替。

*以上内容参考了维基百科，[INI文件](https://zh.wikipedia.org/zh-cn/INI%E6%96%87%E4%BB%B6)*

### 语法格式

INI 文件由节（section）和键值对（key-value pair）组成。

```ini
; 这是 INI 文件中的注释
[app]
addr = 127.0.0.1
port = 8080
[custom]
args = --debug --verbose
timeout = 10
```

### 优点

- 语法简单，结构清晰易于读写
- 历史悠久，广泛使用
- Windows 原生支持

### 缺点

- 语法过于简单，不支持复杂数据结构，如嵌套、数组等
- 缺乏标准化，不同解析器的实现可能有所不同

## 4. YAML (YAML Ain't a Markup Language)

YAML 是 "YAML Ain't a Markup Language"（YAML不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种标记语言），但为了强调这种语言以数据做为中心，而不是以标记语言为重点，而用反向缩略语重命名。

Clark Evans 在 2001 年首次发表了这种语言，另外 Ingy döt Net 与 Oren Ben-Kiki 也是这语言的共同设计者。YAML 参考了其他多种语言，包括： C 语言、Python、Perl，并从 XML、电子邮件的数据格式（RFC 2822）中获得灵感。

*以上内容参考了百度百科，[YAML](https://baike.baidu.com/item/YAML/1067697)*

### 语法格式

YAML 的语法包括键值对、列表和嵌套结构。

```yaml
# 这是 YAML 文件中的注释
app:
  addr: 127.0.0.1
  port: 8080
  custom:
    args:
      - --debug
      - --verbose
    timeout: 10
```

### 优点

- 语法和 Python 一样利用了缩进，易于阅读
- 后起之秀，借鉴了百家之长，功能强大

### 缺点

- 语法较为复杂，学习成本较高
- 厌恶强制缩进的人可能会觉得很难看

## 5. TOML (Tom's Obvious, Minimal Language)

TOML 是一种旨在成为一个小规模、易于使用的语义化的配置文件格式，它被设计为可以无二义性的转换为一个哈希表。由 Tom Preston-Werner、Pradyun Gedam 等创建

*以上内容参考了维基百科，[TOML](https://zh.wikipedia.org/wiki/TOML) 和 (toml.io)[https://toml.io/cn/v1.0.0]*

### 语法格式

TOML 的语法包括键值对、列表和嵌套结构。

```toml
# 这是 TOML 文件中的注释
[app]
addr = "127.0.0.1"
port = 8080
[custom]
args = ["--debug", "--verbose"]
timeout = 10
```

### 优点

- 语法类似 INI，但更强大
- 发明时间较晚，但使用十分广泛
- 支持丰富的数据类型
- TOML 在 Python 和 Rust 中使用广泛（pyproject.toml、Cargo.toml）（这一点是出于偏爱）

### 缺点

- 语法较为复杂，学习成本较高
- 发明时间较晚，社区支持较弱（查资料时明显能感受到）

## 结论

综合考虑，我的选择是：

- 非常简单的情况下，使用 JSON 或 INI
- 需要复杂数据结构时，使用 JSON 或 TOML

总之无脑用 JSON 就对了（doge），牺牲一点可读性而已。
