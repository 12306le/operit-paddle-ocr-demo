# Paddle OCR Android Demo — GitHub Actions 自动构建版

基于 [onlyloveyd/Android-PaddleOCR](https://github.com/onlyloveyd/Android-PaddleOCR) 的最小改造,补上现代化的 GitHub Actions 自动构建流水线,让不会本地编译的人也能拿到 APK 体验 PaddleOCR 的效果。

## 🎯 和 ML Kit 版的区别

| | [operit-ocr-demo](https://github.com/12306le/operit-ocr-demo) (ML Kit) | 本项目 (Paddle) |
|---|---|---|
| OCR 引擎 | Google ML Kit | PaddleOCR (Paddle-Lite 推理) |
| UI | Jetpack Compose + 圈选 | 原版 View + 整图识别 |
| 中文精度 | ★★★ | ★★★★ |
| 竖排/方向校正 | ❌ | ✅ |
| APK 大小 | ~25 MB | ~40 MB |
| 源码体量 | 小 (纯 Kotlin) | 大 (含 JNI + C++) |

## 📦 如何获取 APK

### 方式 A: GitHub Actions 下载 (推荐)
1. 进入 [Actions 页面](../../actions)
2. 点击最新一次 `Build Debug APK (Paddle)` 运行
3. 最底部 Artifacts 区域下载 `paddle-ocr-debug-apk`

### 方式 B: 本地构建
需要 Android Studio 4.0+、JDK 11、NDK 20、CMake 3.10.2:
```bash
./gradlew assembleDebug
```
Gradle 会自动从百度 CDN 下载 Paddle-Lite (~100MB)、OpenCV (~300MB) 和 OCR 模型 (~9MB),首次构建约需 5-10 分钟。

## 🔧 相对原版的改动

- ✅ 根 `build.gradle` 中 `jcenter()` 替换为 `mavenCentral()` (jcenter 已停服)
- ✅ 补充 `.github/workflows/build.yml` 自动构建流水线
- ✅ 补充 `LICENSE` (Apache 2.0)
- ✅ `.gitignore` 排除自动下载的 400MB 二进制依赖,使仓库保持精简

## 🙏 致谢

- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) — 文字检测 + 识别模型
- [Paddle-Lite](https://github.com/PaddlePaddle/Paddle-Lite) — 移动端推理引擎
- [OpenCV](https://opencv.org/) — 图像预处理
- [onlyloveyd/Android-PaddleOCR](https://github.com/onlyloveyd/Android-PaddleOCR) — Android 集成原型

---

## 原版 README (保留供参考)

### 1. 安装最新版本的 Android Studio
可以从 https://developer.android.com/studio 下载。本 Demo 使用的是 4.0 版本 Android Studio 编写。

### 2. 安装 NDK 20 以上版本
Demo 测试时使用的是 NDK 20b 版本,20 版本以上均可支持编译成功。

### 3. 导入项目
点击 `File -> New -> Import Project...`,然后跟着 Android Studio 的引导导入。
