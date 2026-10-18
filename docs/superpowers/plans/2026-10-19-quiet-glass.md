# Quiet Glass 视觉重构 Implementation Plan

**Goal:** 在不升级 Kotlin/Compose/AGP 的前提下，把 Daily English 重构为轻量毛玻璃风格的现代 UI，并保留全部学习、真题、笔记、统计与同步能力。

**Architecture:** 以半透明表面、柔和渐变背景、悬浮胶囊导航和圆形玻璃按钮构成 `Quiet Glass` 设计语言；真实液体折射留到 B 方案实验分支。业务层、Room、同步协议不动。

**Spec:** `docs/experimental/B-AndroidLiquidGlass.md`（B 方案边界）；当前工程基线为 native-android 1.0.2。

**Tech:** 现有 Jetpack Compose、Material 3、Navigation 3；新增 `theme/Glass.kt`、`ui/glass/GlassSurface.kt`。

## Global Constraints

- applicationId `com.dailyenglish.quietglass`，版本 `1.1.0-quietglass`（versionCode 1）。
- 不修改 `AppState`、后端契约与同步协议。
- 不引入 AndroidLiquidGlass 或任何新图形依赖；保持 Compose 1.10.6 / Kotlin 2.3.20。
- 阅读型页面（词库、句子、真题全文）保持高不透明度；玻璃只用于导航、顶栏、主卡与专注面板。
- API 24 起可用；API < 31 只是没有模糊，不出现空白。
- 深色、横屏 NavigationRail、字体缩放、48dp 触控目标不回归。

## Tasks

### Task 1: 工程身份与基线

- [x] 新目录 `Quiet-Glass-Daily-English/`，独立 git 分支 `quiet-glass`。
- [x] applicationId `com.dailyenglish.quietglass`，名称 `Daily English Glass`。
- [x] 归档 B 方案文档。

### Task 2: 主题与玻璃基础

- `theme/Theme.kt`：更新 light/dark 色板：暖白背景、鼠尾草玻璃、暖琥珀强调色；卡片 20–24dp 圆角。
- 新增 `theme/Glass.kt`：
  - `QuietBackground()`：暖白/墨绿底 + 两团低透明径向光晕。
  - `GlassSurface`：半透明白/绿表面、1dp 高光描边、柔和阴影。
  - `GlassCircleButton`：圆形玻璃按钮。
  - `glassPillColors()` / `GlassTokens`。
- 单测/构建验证。

### Task 3: 悬浮导航与顶栏

- `MainScaffold.kt`：
  - 顶部透明 TopAppBar，专注/设置/返回变圆形玻璃按钮。
  - 底部 NavigationBar 替换为悬浮胶囊玻璃导航（4 项），内容底部留 96dp。
  - 宽屏保持玻璃质感 NavigationRail。
- `NavDisplay` 的滚动内容与导航之间保留安全留白。

### Task 4: 主页面重绘

- Today：日期 + 玻璃主计划卡 + 玻璃统计条；减少纯色大块。
- Practice：四个玻璃卡片，图标/标题/说明层级保留。
- Stats：玻璃统计卡、周图与热力图容器；保持数据可读。
- Notebook：玻璃分段控件与搜索框；单词/句子卡片高不透明。
- Settings：玻璃设置组、账号与备份卡片。

### Task 5: 次级页面

- Auth：渐变背景 + 玻璃登录卡 + 玻璃次按钮。
- Words / Sentences / Papers：保留阅读卡不透明；模式切换、顶栏操作玻璃化。
- FocusSheet：玻璃内容面板 + 大号计时。
- 深色模式与横屏检查。

### Task 6: 验证与交付

- `testDebugUnitTest` 全绿。
- 安装 PMW110，检查：今日/练习/记录/笔记/设置、认证、词卡、句子、真题、专注、横屏。
- 截图复核深浅色与对比度。
- 打包 APK，复制桌面，算 SHA-256；更新 README/PROGRESS。
- 提交并 tag `v1.1.0-quietglass`。
