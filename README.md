# pages

按目录区分的静态页面托管。用于放那些需要一个**公开、无端口、HTTPS** 地址的东西
——应用商店审核要的隐私政策、支持页，或者任何需要外链的静态页。

线上地址：<https://3dot141.github.io/pages/>

## 为什么需要这个仓库

App Store Connect 的 URL 字段**不接受带端口的地址**。自建服务常跑在
`example.com:40050` 这类端口上，填进去会判「此栏无效」。把静态页放这里，
就能拿到标准 443 端口下的干净地址。

公共托管的另一个好处是不用为两页 HTML 去维护服务器配置与证书。

## 目录约定

每个用途一个目录，目录名用产品/项目名：

```text
/
├── index.html          入口索引（新增目录时在这里加一张卡片）
├── sapling/
│   ├── privacy.html    → /sapling/privacy.html
│   └── support.html    → /sapling/support.html
└── <next-thing>/
    └── index.html      → /<next-thing>/
```

规则：

- **目录名**用产品名，kebab-case
- 单页类型用语义文件名（`privacy.html` / `support.html`），不要都叫 `index.html`
  ——一个目录下可能有多份文档
- 新增目录后**回到 `index.html` 加一张卡片**，否则入口页会漏

## 新增一份页面的步骤

1. 建目录：`mkdir -p <name>`
2. 写 HTML（可以从同目录其它页面复制 `<style>`，主题变量保持一致）
3. 在根 `index.html` 的对应分组下加 `<a class="card">`
4. 提交推送，GitHub Pages 约 1 分钟生效

## 主题

页面自带明暗两套 CSS 变量，跟随系统偏好，也可由 `localStorage.theme`
覆盖（`light` / `dark` / `auto`）。样式是内联的——不引外部 CSS，
这样单文件复制到别处也能直接用。

配色沿用 Sapling 的设计 token：

| 变量 | 浅色 | 深色 |
|---|---|---|
| `--paper` | `#F7F6F3` | `#191919` |
| `--card` | `#FFFFFF` | `#202020` |
| `--ink` | `#1F2427` | `#F0EEEA` |
| `--brand-deep` | `#346538` | `#8FE3B0` |

## 部署

GitHub Pages，从 `main` 分支根目录发布。推送到 `main` 即自动更新。

首次配置：仓库 Settings → Pages → Source 选 `Deploy from a branch`，
分支 `main`，目录 `/ (root)`。
