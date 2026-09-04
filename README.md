# Roam Research 深度优化套件 (roam)

这是一个面向 Roam Research 的主题与交互增强组合，当前由两部分组成：

- `roam.css`：完整视觉系统（配色、字体、组件主题覆盖、日夜模式一致性）
- `Roam.js`：系统日夜自动同步（无顶栏按钮）、Excalidraw 主题同步、`￥￥ → $$$$` 数学输入快捷键

目标是提供统一、沉浸、可读性高且可长期维护的使用体验。

## ✨ 主要特性

### 🎨 视觉系统 (roam.css)

- **语义化主题变量**：使用 `--m-*` 及映射变量统一管理日间/夜间配色与组件色彩。
- **分角色字体体系**：为 `title / heading / body / quote / tag / code / ui` 分别配置字栈与回退链。
- **模块化样式结构**：按章节组织（Variables、Typography、Code Blocks、Tags、Settings、Dark Mode、References 等），便于维护与扩展。
- **全局组件一致性覆盖**：对 Blueprint UI、命令面板、设置页、引用区、弹层等统一主题语义，减少原生内联样式带来的视觉割裂。
- **日夜统一体验**：夜间模式采用与日间对应的语义变量与交互色，尽量保持信息层级一致。

`roam.css` 当前章节：

1. CSS Variables (Light)  
2. Global Overrides  
3. Base Layout  
4. Typography  
5. Code Blocks  
6. Embed & Query  
7. 左侧边栏  
8. Block References & Blockquote  
10. Kanban  
11. Tags & Labels  
12. Highlights  
13. Settings & Plugins  
15. Dark Mode  
17. Gap-Filling & Global Resets  
18. References - Borderless Immersion

> 注：章节编号保留历史演进痕迹（如 9/14/16 预留），不影响功能。

### 🔌 交互增强 (Roam.js)

- **系统日夜同步**：始终根据 `prefers-color-scheme` 为 `body` / `documentElement` 切换 `rm-dark-theme`，不注入顶栏按钮，也不再移除旧版 `#roam-theme-toggle-btn`（若旧按钮仍存在会保留原样）。
- **系统主题监听**：`matchMedia("(prefers-color-scheme: dark)")` 的 `change`（及旧版 `addListener`）触发时重新应用主题。
- **Excalidraw 主题同步**：同步 `.excalidraw` 根节点 `theme--dark / theme--light`，并处理：
  - Roam 主题 class 变化
  - Excalidraw 节点新增
  - 全屏切换
- **数学输入快捷键**：
  - `￥￥` → `$$$$`：在 block 中输入两个全角 `￥￥` 时，自动替换为 `$$$$` 并把光标停在中间（两对 `$$` 之间），可直接键入公式；单个 `￥` 保持原样。
  - **回车跳出 `$$...$$`**：当光标位于一对未闭合的 `$$...$$` 内部时，按回车不再换行/新建块，而是把光标挪到闭合 `$$` 之后，便于直接续写正文。
  - 仅作用于 Roam block 文本域（`#block-input-*` / `.rm-block__input`）
  - 通过 `execCommand("insertText")` 走浏览器原生输入通路，等价于 Roam 自带 `【【 → [[]]` 的实现，自动同步 React `value tracker` 与 undo 历史
  - 同时监听 `input` / `compositionend` / `keydown`，覆盖英文键盘与中文 IME 两条输入通路

## 🚀 安装与部署

### 1) 部署 CSS

1. 在 Roam 中创建页面 `roam/css`。
2. 新建代码块（`/code`，语言选 `CSS`）。
3. 粘贴 [roam.css](roam.css) 全部内容。

### 2) 部署 JavaScript

1. 在 Roam 中创建页面 `roam/js`。
2. 首次执行脚本时，在 Roam 提示中点击 *"Yes, I know what I'm doing"* 授权。
3. 新建代码块（`/code`，语言选 `JavaScript`）。
4. 粘贴 [Roam.js](Roam.js) 全部内容并刷新页面。

## 📝 维护说明

- 主题相关逻辑优先集中在 `roam.css` 变量层，减少散点硬编码。
- `Roam.js` 当前包含系统主题同步、Excalidraw 同步与数学输入快捷键三块独立逻辑，每块以独立 IIFE 组织，便于单独维护与裁剪。

## 📄 开源协议

本项目采用 [MIT License](LICENSE)。
