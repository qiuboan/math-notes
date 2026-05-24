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

## Lotus Docs 与 KaTeX 的已知问题

当前使用的 Lotus Docs 模板中，KaTeX 的 `\sqrt` 可能无法正确显示。排查结果是：公式已经被 KaTeX 渲染成 `.katex` DOM，但根号使用的 SVG 被主题的内容区样式覆盖了。

Lotus Docs 的内容区样式会对正文中的 `svg` 设置通用规则：

```css
.docs-content .main-content svg {
  max-width: 100%;
  height: auto;
}
```

KaTeX 的根号、长箭头等符号也会使用 SVG。上面的通用规则会覆盖 KaTeX 自己的 SVG 高度设置，导致 `\sqrt` 的根号显示异常或不可见。

解决方式是在项目中覆盖主题的 KaTeX SCSS 入口文件：

```text
assets/docs/scss/katex.scss
```

内容为：

```scss
@import "custom/plugins/katex/katex";

.docs-content .main-content .katex svg {
  height: inherit;
}
```

这样 Hugo 会优先使用项目内的 `assets/docs/scss/katex.scss`，同时继续引入 Lotus Docs 原本的 KaTeX 样式。该方式不需要修改 Hugo module 缓存或主题源码，部署到 Cloudflare Pages 时也会生效。
