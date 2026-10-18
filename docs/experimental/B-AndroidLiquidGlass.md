# B 方案存档：AndroidLiquidGlass 实验分支

状态：**暂缓，未实现。** 当前主线先做 Quiet Glass（半透明毛玻璃壳层，不升级工具链）。  
未来分支名建议：`experimental/liquid-glass`。

## 目标

用 [Kyant0/AndroidLiquidGlass](https://github.com/Kyant0/AndroidLiquidGlass) 的
`io.github.kyant0:backdrop:2.0.1`，为底部导航、专注面板或今日主卡提供真实的
RenderEffect / RuntimeShader 玻璃折射，而不是半透明近似。

## 已确认的阻塞（2026-10-19）

| 项目 | 当前主线 | backdrop 2.0.1 |
|---|---|---|
| compileSdk | 36 | **37（AAR minCompileSdk=37）** |
| Kotlin 元数据 | 2.3.20 | **2.4.0**（Kotlin 2.4.10） |
| Compose | 1.10.6 | **1.12.0** |
| AGP | 9.0.1 | 仓库使用 9.3.2 |
| 本机平台 | android-36 / 36.1 | 需要安装 android-37 |

`backdrop:2.0.0` 的 Kotlin 元数据是 2.3.0、Compose 1.11.0，仍要求
`minCompileSdk=37`，因此也不是零成本替代。

## 运行时边界

- 模糊/链式效果：Android 12（API 31）起。
- RuntimeShader / 镜头折射：Android 13（API 33）起。
- 应用 minSdk 24；API 24–30 必须提供不透明降级，否则效果静默消失。
- 库没有现成 Material 组件，需要自己实现 `LiquidBottomBar`、`LiquidCard`，
  并补齐无障碍语义、对比度与触摸反馈。
- 许可 Apache-2.0；发布时保留 NOTICE/许可文本。

## 升级步骤（未来）

1. 安装 Android SDK Platform 37。
2. 升级 Kotlin 2.4.10、KSP 对应版本、Compose Compiler、Compose BOM（1.12 对齐）、
   AGP 9.3.2，`compileSdk = 37`。
3. 回归 Hilt 2.60.1、Room 2.8.5、Navigation 3、WorkManager、Room schema。
4. 添加 `implementation("io.github.kyant0:backdrop:2.0.1")`。
5. 新建 `ui/glass/`：
   - `LiquidBottomBar`：只替换紧凑屏底部导航；宽屏继续 NavigationRail。
   - `LiquidPanel`：用于专注面板/今日主卡。
6. API 31/33 检查失败时退回 Quiet Glass 的半透明表面。
7. 增加“减少透明效果”开关；验证深色、横屏、字体缩放。
8. 仅小面积使用（导航/面板），不在长列表卡片上铺满模糊。

## 验收门槛

- PMW110 上滚动 60fps，无明显掉帧；连续滑动 2 分钟温度可接受。
- 浅色/深色文字对比度达到 WCAG AA。
- API 24 模拟/低版本真机不出现空白或不可读。
- 返回栈、NavigationRail、专注计时、TTS 等功能不回归。
- 与 Quiet Glass 主线视觉可一键切换，不破坏稳定版。

## 不在本阶段

- 不替换 `com.dailyenglish.quietglass` 的稳定主线。
- 不为玻璃效果改动业务/同步协议。
- 不把高成本模糊应用到词库、句子、真题全文等阅读页面。
