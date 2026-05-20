# 打卡 App — 安卓 APK 打包指南

## 准备工作（只需一次）

1. 安装 Node.js：https://nodejs.org（选 LTS 版本）
2. 安装 Android Studio：https://developer.android.com/studio
3. 在 Android Studio 里安装 Android SDK（默认会提示安装）

---

## 打包步骤

### 第一步：安装依赖

打开终端，进入项目文件夹：

```bash
cd punchcard-app
npm install @capacitor/core @capacitor/cli @capacitor/android
```

### 第二步：添加安卓平台

```bash
npx cap add android
```

### 第三步：同步代码

```bash
npx cap sync android
```

### 第四步：生成 APK

**方式 A（推荐）：用 Android Studio 打开**
```bash
npx cap open android
```
在 Android Studio 里：
- 菜单 → Build → Build Bundle(s) / APK(s) → Build APK(s)
- APK 文件在 `android/app/build/outputs/apk/debug/app-debug.apk`

**方式 B：命令行直接构建（需配置好 Java）**
```bash
cd android
./gradlew assembleDebug
```
APK 在 `android/app/build/outputs/apk/debug/app-debug.apk`

---

## 安装到手机

```bash
# 手机开启「USB调试」后连接电脑
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

或者直接把 APK 文件传到手机，点击安装（需要开启「允许未知来源」）。

---

## 如果嫌麻烦：用在线服务

把 www/index.html 上传到：
- **PWABuilder**（https://www.pwabuilder.com）→ 可直接生成 APK
- **PhoneGap Build**（已停止）→ 用 Cordova 替代

---

## 文件说明

```
punchcard-app/
├── www/
│   └── index.html     ← 完整的 App 代码（改这个文件）
├── capacitor.config.json  ← App ID 和配置
├── package.json
└── BUILD_GUIDE.md     ← 本文件
```

## 修改 App 图标和名称

- 名称：修改 capacitor.config.json 里的 "appName"
- 图标：运行 `npx @capacitor/assets generate` 生成各尺寸图标
- App ID：修改 "appId"（格式：com.你的名字.app）
