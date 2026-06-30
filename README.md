# ziya-updates

字芽 APP 自动更新元数据。

## 文件结构

- `latest.json` — 当前最新版本信息（APP 启动时拉取）

## 工作机制

字芽 APP 通过以下 URL 检查更新：

  https://cdn.jsdelivr.net/gh/gzzhenxiang-cpu/ziya-updates@main/latest.json

APP 内嵌此地址。每次启动异步拉取该 JSON，跟当前 versionCode 比较，
新版可用就提示用户下载。

APK 文件托管在 [字芽主仓库的 Releases](https://github.com/gzzhenxiang-cpu/ziya/releases)。

## 发版流程

1. `flutter build apk --release` 生成新 APK
2. 在主仓库的 Releases 上传 APK 文件
3. 修改本仓库的 `latest.json` 指向新 release 的 download URL
4. `git push` → jsDelivr CDN 自动同步（通常 5-10 分钟）
5. 用户下次打开 APP 就能看到更新提示
