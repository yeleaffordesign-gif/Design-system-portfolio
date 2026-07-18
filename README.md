# Design System · 叶潇蓉个人网站

站点设计令牌的源文件与活文档。令牌不是事前规定的规范，而是从 `assets/style.css` 的实际用值里盘出来、再形式化的系统。

## 文件

| 文件 | 作用 |
| --- | --- |
| `tokens.css` | 令牌源文件（CSS 自定义属性）。向后兼容：现有令牌保持原名原值，其余为在此基础上形式化的隐性系统。 |
| `tokens.json` | 同源令牌的 W3C DTCG 格式，可导入 Style Dictionary / Tokens Studio。 |
| `index.html` | 活文档。每一项令牌用它自己描述的值渲染，可直接访问预览。 |

活文档地址（部署后）：`https://yeleaffordesign-gif.github.io/cherry-portfolio/design-system/`

## 命名逻辑

- **按角色，不按外观**：`text-secondary` 而非 `grey-2`，`accent-surface` 而非 `green-light`。令牌描述用途，换值不换名。
- **字号按层级**：`display / h1…h4 / lead / body / meta / caption`，与内容结构对应，不与像素绑定。
- **节奏成对**：字重（light/regular/medium）、行高（tight→relaxed）、字间距（tight→widest），各自一条连续档位。

## 采纳路径（当前站点无需改动即可运行）

1. 在 `assets/style.css` 顶部加 `@import "../design-system/tokens.css";`
2. 逐步把硬编码值替换为 `var(--token)`——一次一个模块，不必一次性重构。
3. 每次替换后对照活文档确认视觉无偏移。

令牌与 `style.css` 是同源关系：`style.css` 是当前实现，令牌是抽象后的目标。两者对齐是一个渐进过程，不是一次性动作。

## 待对账（审计发现）

盘点实际用值时发现三处不一致，如实记录，供后续统一：

1. **两种绿**：`--accent` 是 `#2d5a3d`（rgb 45,90,61），而着色面 `--accent-surface / line` 基于 `rgb(33,92,51)`。色相接近但不同源。现状值已在令牌中保留以保证视觉一致，建议下次重构时让着色面由 `--accent` 派生（如 `color-mix`）。
2. **灰阶近似值**：`style.css` 中出现 `#8a8a82`、`#7a7a74`、`#555` 等与文字令牌接近、但未落到令牌的散值。建议收归到 `text-secondary / tertiary`。
3. **暖橙单点**：`rgba(168,109,49,.55)` 仅一处使用，未纳入核心系统。若确为独立角色（如某类状态标记），再单独设令牌；否则移除。

## 未落地项（标注为建议，非现状）

- **间距**：`--space-*` 为 8px 节奏的建议基线，`style.css` 尚未消费。当前间距仍为按需的 clamp / px。
- 断点（640 / 720 / 1100px）无法令牌化，仅在 `tokens.css` 注释中记录。

---

© 2026 叶潇蓉 · Cherry Ye
