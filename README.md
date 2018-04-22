# bilibili-zhuanlan-markdown-tool

[![Build Status](https://travis-ci.org/zihengCat/bilibili-zhuanlan-markdown-tool.svg?branch=master)](https://travis-ci.org/zihengCat/bilibili-zhuanlan-markdown-tool)

![bilixmd][bilixmd]

这是一款可以让你使用`Markdown`撰写哔哩哔哩（bilibili.com）专栏文章的外部辅助工具。

# Usage（使用说明）

1. 本机安装`Node.js`环境，获取项目源码，使用`npm install`安装项目依赖。

2. 取得`cookies`，写入配置文件。

3. 使用`Markdown`格式写作。

4. 运行`node new.js && node upload [md_file]`创建并提交`Markdown`文章。

# Example（实例讲解）

通过一个实例，来具体讲解应如何使用此工具。

## 步骤1 - 安装环境与获取源码

此工具使用`Node.js`写成，要想使用它，你需要先在本机上安装好`Node.js`环境。
获取GitHub上的项目源码，可以使用`git`，也可以直接下载`zip`压缩包。对于`Node.js`项目，我们一般使用`npm install`来安装项目依赖。

## 步骤2 - 获取关键参数写配置文件

这是至关重要的一步。我们需要**手动**取得关键参数：`cookies`，再写出配置文件。
`cookies`是用户个人身份认证信息。工具依赖该参数与B站专栏服务器正常通信。
使用**浏览器开发者工具**可以获得该参数。

![step2][step2]

> 图: 获取`cookies`参数

我们将取得的关键参数写入到`./config/config.json`配置文件。

## 步骤3 - Markdown 写作

至此，准备工作已完成。我们可以告别B站专栏富文本编辑器，转而使用`Markdown`撰写文章了。**拿起你最钟爱的一支`Markdown`编辑器，愉快地写文章吧！**

![step3][step3]

> 图: `Markdown`文章

## 步骤4 - 命令提交

最后，我们来将这篇`Markdown`格式的文章**变身**成为B站专栏文章。此工具正是帮助你完成这项任务的。我们通过运行命令来提交`Markdown`文章，请将你的文章与配置文件一并输入，注意先后顺序。如果命令没有报错，那说明提交成功。
```
$ node src/new.js
$ node src/upload.js './test/Markdown来到了B站专栏.md'
```
我们回到专栏草稿箱看一看，我们会发现，这篇`Markdown`格式的文章已经变身成为B站专栏文章了，排版、样式丝毫不差，静静地躺在专栏草稿箱之中，专栏文章的标题正是`Markdown`文件名。

![step4][step4]

> 图: 由`Markdown`变身的专栏文章（网页端预览）

预览文章，添加头图，选择分类，写专栏推荐语，这些都是文章发布前的准备工作。手动完成后就可以提请发布文章了。当然，B站是要审核的。

# Attentions（注意事项）

有一些注意事项你一定要知悉。

## 不支持的Markdown语法

目前，B站专栏所能提供的功能选项还非常有限，甚至连`Markdown`基本语法标准都无法达到完全支持。对于下列`Markdown`功能选项（甚至是常用选项），B站专栏目前还无法提供支持。对于扩展`Markdown`功能，更是没有可能。

- 六级标题
- 斜体文本
- 超链接
- 外链图片
- 代码块
- 表格
- 内联HTML

所以，如果你考虑将`Markdown`文章发布到B站专栏上，请**谨慎使用**上述语法格式，并考虑替代方案（如: 使用图片替换表格，代码块）。

## 专有功能

另外，B站也针对自家的专栏文章添加了一些**专有**功能选项，这些选项大多含有B站专栏特色。

- 字号
- 对齐
- 颜色
- 图片分割线
- 站内选项卡

这些选项大多没有合适的`Markdown`语法与之对应，只能通过**内联HTML**实现。

如果你分析过B站专栏的文章结构，就会发现，这些专有功能都是通过`class样式 + 行内css样式`实现的，并不具备可移植性，也不符合**结构与样式分离**的原则。

所以，**此工具并不对这些专有功能提供支持**。

当然，如果你想为你的`Markdown`文章添加B站专有功能，完全可以在使用此工具提交后回到B站专栏富文本编辑器中手动修改。

# Configure（配置选项）

此工具的`json`配置文件非常简单，就像这样:

```
{
  "cookies": ""
}
```

更加详细的说明：

```
cookies ->  以下四枚 Cookie 必需, 有效期大概1个月（过期重取）
            "DedeUserID"
            "DedeUserID__ckMd5"
            "SESSDATA"
            "bili_jct"
```

# Develop（开发相关）

利用该工具的代码实例:

```
/*
 * API 说明
 * 参数: Markdown 文档路径, 配置选项
 * 处理流程: 取得 MD 文档与配置选项 -> Markdown 转换 HTML ->
 *           上传本地图片取得B站外链 -> 替换本地图片地址为B站外链地址 ->
 *           合成表单发送更新
 */
biliZhuanlanMarkdown.startProcess (
    "path",
    {
      "aid":     "",
      "cookies": "",
      "csrf":    ""
    }
);
```

# License（许可协议）

[MIT](./LICENSE)

[bilixmd]: ./docs/bilixmd.png
[step2]:   ./docs/step2.png
[step3]:   ./docs/step3.png
[step4]:   ./docs/step4.png

