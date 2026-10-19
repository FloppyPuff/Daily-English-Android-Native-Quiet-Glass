# Quiet Glass 进度

更新时间：2026-10-19 01:58（CST）
状态：**Quiet Glass 1.2.0 已实现并构建；词库/句子合并完成；真机复核待设备重新连接。**

## 仓库

- 目录：`Quiet-Glass-Daily-English/`
- 分支：`quiet-glass`
- 基线：`native-android` 1.0.2（`v1.0.2`）
- Application ID：`com.dailyenglish.quietglass`
- 版本：`1.2.0-quietglass`（versionCode 2）

## 已完成

- 独立工程与 B 方案存档。
- 渐变背景、半透明表面、玻璃描边与阴影组件 `theme/Glass.kt`。
- 玻璃顶栏（返回/专注/设置圆形按钮）。
- 悬浮胶囊底部导航；宽屏玻璃 NavigationRail。
- 今日计划、练习卡、统计卡、笔记卡、设置卡、认证卡、词卡、句子卡、真题卡、
  专注面板统一半透明/描边语言。
- CET-6 与考研词库/句子合并为综合学习；统计页保留「全部 / CET-6 / 考研」筛选，
  历史进度与事件按内容归属聚合。
- JVM 52/52 通过，APK 构建成功。
- APK：`C:\Users\fjh28\Desktop\Daily-English-Glass-1.2.0-quietglass-debug.apk`
  SHA-256 `9c27c4a59cf7b12783cb1397fff32dbcd2be5f9f1b23fbbede4afa490dae7a1c`
- 服务器路径：`/var/www/daily-english/web/Daily-English-Glass-1.2.0-quietglass-debug.apk`

## 待做

1. 连接 PMW110，安装 `com.dailyenglish.quietglass`，复核：
   - 今日/练习/记录/笔记/设置；
   - 认证页、词卡、句子、真题、专注面板；
   - 深色、横屏 NavigationRail、字体缩放；
   - 卡片对比度与玻璃层视觉。
2. 根据真机截图微调背景光晕、表面透明度和导航尺寸。
3. 真机通过后 tag `v1.2.0-quietglass`。

## 设计边界

- 本工程是**半透明毛玻璃近似**，不是 AndroidLiquidGlass 的真实折射。
- 不修改业务、状态协议、后端契约。
- 真实液态玻璃实验见 `docs/experimental/B-AndroidLiquidGlass.md`。
