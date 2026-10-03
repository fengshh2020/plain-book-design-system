# 书籍设计系统 — 素卷 · 锦册

本仓收录两套并列的程序书籍前端设计系统，以兄弟目录共处。它们共享同一副阅读解剖——单栏正文居中、720px 文字列嵌于组件版心、抽屉目录 + 本页大纲轨、五档提示框、中文排印——与同一套图内语义（白底全彩描边 + 连线七则 + dg 分型，正典在素卷，锦册再令牌化）；技术立场各异：素卷零依赖单文件，锦册以全内置的框架组件为第一性。两套均为 v1.0。

[English](README.md)

## 体系分工

| | 素卷 · Plain Book | 锦册 · Brocade Book |
|---|---|---|
| 路径 | `plain/index.html` | `brocade/index.html` |
| 技术立场 | 零依赖，单文件自足 | daisyUI 5 + Tailwind 4 + Alpine 3 + highlight.js 11 + Lucide，全 vendored 固定版本 |
| 定位 | 书籍生产体系——书页直接消费其 `<style>` 主块 | 组件化体系——组件原生形态与多主题体验优先 |
| 主题 | 纸面 / 墨版（PB-31） | 六款 OKLCH 手调传统色调色板 |
| 规则 | 32 条（PB-1 … PB-32）+ 三条总原则 | 28 条（JC-1 … JC-28），12 节 |
| JavaScript | 完全无 JS 也可通读 | JS 只做增强（复选框抽屉、`details`、原生 `dialog`、原生 diff 拖拽） |

上表图内可视化语义的正典源在素卷；锦册持有的是改挂 daisyUI 主题变量的再令牌化副本（图随主题翻转）——演进时先改素卷。

## 素卷 · Plain Book v1.0 — `plain/`

面向程序 / 算法类书籍的单文件、令牌驱动的前端设计规范——把书页当**文档站**设计：单栏正文居中独占屏幕；全书目录收进顶部按钮唤出的抽屉，宽屏另设右侧「本页」大纲细轨滚动跟随；近单色墨系 + 静墨蓝强调，白底细框代码（GitHub-light 语义色），提示框为软色卡片，插图为白底全彩描边的语义配色。纸面 / 墨版双主题（PB-31）：墨版整页翻转——深灰纸面 + 米白墨字 + 提亮静墨蓝 + GitHub-dark 代码，绝不浅深混排；默认跟随系统，手动切换即记忆。页面本身既是规范，也是规范的参照实现；书籍按「使用」一节消费其 `<style>` 主块。

### 截图

| 令牌速查 | 组件样张 |
|:---:|:---:|
| ![令牌速查](docs/plain-cheatsheet.png) | ![组件样张](docs/plain-components.png) |

| 书籍封面 | 图内语义配色 |
|:---:|:---:|
| ![书籍封面](docs/plain-cover.png) | ![图内语义配色](docs/plain-diagram.png) |

### 特点

- **单文件自足。** 规范、样式与参照实现同在一个 `plain/index.html`（约 63 KB）：无需构建、无需服务器、零依赖。
- **全令牌驱动。** 裸值只声明在 `:root`（墨版整组重声明）；组件一律 `var(--token)` 引用。
- **9 章 32 条编号规则（PB-1 … PB-32）+ 三条总原则。** 条文按「可校验」措辞书写，阈值显式（「强调色 ≤5% 版面」「间距只用 12/14/24/64 四档」）。
- **三条总原则：** 零装饰（层次只来自字阶、间距、发丝线）；单栏独占、导航按需（全书导航在抽屉、宽屏右设「本页」大纲轨）；代码属于纸面（纸面主题浅底细框、墨版与页面同底——永远与页面同面，不做浮版）。
- **中文排印内建（PB-7）：** 正文两端对齐 + `line-break: strict` 避头尾、`text-autospace` 中西文间距、标题 `text-wrap: balance` / 正文 `pretty`、字重一律 600 并配 `font-synthesis: none` 防合成粗体、中文标题字距不为负。
- **图内语义配色（PB-30）：** 白底全彩描边——正红 = 失效 / 悬垂 / 危险，亮绿 = 新分配 / 新增，紫 = 外部系统；只染边框不染底色，图内文字永远墨色，中性状态用灰虚线表达、不冒充危险色。

### 使用

直接用浏览器打开 `plain/index.html` 离线阅读；生成书页时把其中的 `<style>` 主块（书籍 CSS）原样作为 `assets/style.css`，页面骨架按 §3 的 `topbar / drawer / pagerail / main / prose` 五层装配。

## 锦册 · Brocade Book v1.0 — `brocade/`

`brocade/index.html` 是组件化的设计系统。它保留书籍的阅读解剖（单栏正文、720px 文字列嵌于 880px 组件版心、抽屉目录 + 本页大纲轨、五档提示框、中文排印规则），但以框架为第一性：组件的原生形态与各库的最佳阅读体验优先；从素卷整组搬来的只有可视化语义，并改由主题令牌着色、随主题翻转。章头承载全套体系唯一的装饰母题：由主色令牌派生的 1px 交叉织锦细纹，向下淡出——锦册之名，织纹为记。

- **daisyUI 5.7.47**：组件主干——navbar（glass）、drawer + menu、dropdown 主题菜单、breadcrumbs、tabs、diff、alert（+soft/outline/dash 变体）、table-zebra、collapse、steps、timeline、join、hero、card、stats + radial-progress、toast、tooltip、kbd、modal（插图放大）、mockup-window、status、skeleton、loading、divider；主题菜单提供六款 OKLCH 手调调色板，各以一味传统色定气质——素 / 缥 / 皓（日间）与 玄 / 檀 / 宵（夜间），页内覆盖出厂主题变量（data-theme 键沿用 light / corporate / nord / dark / dim / night，兼容深链与本地记忆）。
- **Tailwind CSS 4.3.3**（browser 版）：版式、间距与排印原子类，令牌渐变、悬停过渡、min-[1400px] 大纲轨断点。
- **Alpine.js 3.17.4**（+ Intersect）：tab 切换、复制 → toast 反馈、Esc 关抽屉、大纲轨滚动跟随。
- **highlight.js 11.12.0**：github / github-dark 双主题按各主题的 `color-scheme` 自动跟随（cpp / bash / json 样张）。
- **Lucide 0.577.0**：全套描边图标（菜单、色板书、日/月、五档提示图形、时间线标记）。

全部库（含 `themes.css`）以固定版本内置在 `brocade/assets/`——无 CDN、无构建，断网双击即完整打开。规范为 12 节 28 条编号规则（JC-1 … JC-28）：组件优先 + 白名单制、令牌驱动零裸色值、多主题同构、JS 只做增强。直接用浏览器打开 `brocade/index.html`。

| 日间主题 | 夜间主题 |
|:---:|:---:|
| ![锦册日间](docs/brocade-light.png) | ![锦册夜间](docs/brocade-dark.png) |
