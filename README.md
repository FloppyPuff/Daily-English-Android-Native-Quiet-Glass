# Daily English Glass（Quiet Glass）

Daily English 的 **Quiet Glass** 视觉原型，独立于稳定版 `native-android`。
功能基线来自原生版 1.0.2；本工程只重构 UI，不改学习、真题、统计、备份与同步逻辑。

- Application ID：`com.dailyenglish.quietglass`（与稳定版并行安装）
- Kotlin package / namespace：`com.dailyenglish.nativeapp`
- 桌面名：`Daily English Glass`
- 版本：`1.1.0-quietglass`（versionCode 1）
- 稳定版：`../native-android`，1.0.2 / `v1.0.2`

## Quiet Glass 设计

- 暖白/墨绿渐变背景，低透明鼠尾草与暖沙光晕。
- 悬浮胶囊底部导航 + 圆形玻璃顶栏按钮。
- 半透明卡片、1dp 高光描边、柔和阴影；阅读页保持高不透明度。
- 认证、专注面板、设置与统计统一玻璃语言。
- 不引入新图形依赖，API 24 起一致；不使用真实背景模糊。

设计说明与任务拆分见 `docs/superpowers/plans/2026-10-19-quiet-glass.md`。

## B 方案存档

真正的 AndroidLiquidGlass（RenderEffect/RuntimeShader 折射）暂不接入，
原因与升级步骤见 `docs/experimental/B-AndroidLiquidGlass.md`。
未来实验分支建议：`experimental/liquid-glass`。

## 构建

```powershell
$env:JAVA_HOME = "D:\Software\Tool\AndroidStudio\jbr"
cd Quiet-Glass-Daily-English
.\gradlew.bat testDebugUnitTest
.\gradlew.bat assembleDebug
```

内容仍由 `syncContent` 从 `../web/data` 同步到 assets。

## 当前状态

- 功能与 1.0.2 一致；JVM 49/49 通过。
- 原型 APK：
  `C:\Users\fjh28\Desktop\Daily-English-Glass-1.1.0-quietglass-debug.apk`
  SHA-256 `3e8637f84009858926801f6d3cf2cd593015f25f11995412ef70f849a34463a0`
- 真机安装与视觉复核待设备重新连接。
- B 方案仅存档，未实现。
