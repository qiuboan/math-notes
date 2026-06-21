# 阿果的数学笔记

这是一个用 Hugo 构建的数学笔记网站，内容主要放在 `content/docs/` 下。

站点使用 [Lotus Docs](https://github.com/colinwilson/lotusdocs) 作为文档主题，并通过 Hugo Modules 引入主题和 Bootstrap SCSS 模块。主题相关配置在 `hugo.toml` 中。

## 本地运行

```bash
hugo server -D
```

默认访问地址：

```text
http://localhost:1313/
```

## 新建文章

在 `content/docs/` 下新建文章：

```bash
hugo new content/docs/分类/文章标题.md
```

例如：

```bash
hugo new content/docs/等差数列/等差中项.md
```

新文件会使用 `archetypes/default.md` 中的默认 front matter。发布前把文件头部的 `draft` 改为 `false`。

## 提交与推送

提交修改：

```bash
git add .
git commit -m "更新数学笔记"
```

推送到远程仓库：

```bash
git push
```
