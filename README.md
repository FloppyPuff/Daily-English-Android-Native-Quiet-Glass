# Daily English Glass（Quiet Glass）

Daily English 的 **Quiet Glass** 版本，独立于稳定版 `native-android`。
功能基线来自原生版 1.0.2；在玻璃视觉之上，把 CET-6 与考研词库/句子合并为综合学习，
统计页保留「全部 / CET-6 / 考研」筛选。

- Application ID：`com.dailyenglish.quietglass`（与稳定版并行安装）
- Kotlin package / namespace：`com.dailyenglish.nativeapp`
- 桌面名：`Daily English Glass`
- 版本：`1.2.0-quietglass`（versionCode 2）
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

- CET-6 与考研词库/句子合并学习；统计保留方向筛选，历史进度共享。
- JVM 52/52 通过；APK 已构建并上传服务器。
- APK：
  `C:\Users\fjh28\Desktop\Daily-English-Glass-1.2.0-quietglass-debug.apk`
  SHA-256 `9c27c4a59cf7b12783cb1397fff32dbcd2be5f9f1b23fbbede4afa490dae7a1c`
- 服务器路径：`/var/www/daily-english/web/Daily-English-Glass-1.2.0-quietglass-debug.apk`
- 真机安装与视觉复核待设备重新连接。
- B 方案仅存档，未实现。
