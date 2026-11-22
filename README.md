<div align="center">

# 我的电视

**面向 Android TV 与低端电视盒子的原生直播播放器**

[![Release](https://img.shields.io/github/v/release/Bigzzh2022/mytv-android-ai?sort=semver&label=release)](https://github.com/Bigzzh2022/mytv-android-ai/releases)
[![Downloads](https://img.shields.io/github/downloads/Bigzzh2022/mytv-android-ai/total)](https://github.com/Bigzzh2022/mytv-android-ai/releases)
[![Stars](https://img.shields.io/github/stars/Bigzzh2022/mytv-android-ai)](https://github.com/Bigzzh2022/mytv-android-ai/stargazers)
[![License](https://img.shields.io/github/license/Bigzzh2022/mytv-android-ai)](./LICENSE)

![Android](https://img.shields.io/badge/Android-5.0%2B-3DDC84?logo=android&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-2.0-7F52FF?logo=kotlin&logoColor=white)
![Compose](https://img.shields.io/badge/Jetpack%20Compose-TV-4285F4?logo=jetpackcompose&logoColor=white)

[下载](#下载与安装) · [快速开始](#快速开始) · [功能特性](#功能特性) · [配置直播源](#配置直播源) · [操作方式](#操作方式) · [从源码编译](#从源码编译) · [常见问题](#常见问题)

</div>

<p align="center">
  <img src="./screenshots/Screenshot_panel.png" width="32%" alt="频道列表" />
  <img src="./screenshots/Screenshot_temp_panel.png" width="32%" alt="快捷面板" />
  <img src="./screenshots/Screenshot_settings.png" width="32%" alt="设置界面" />
</p>

## 简介

「我的电视」是一款使用 Android 原生技术开发的电视直播播放器，基于 Kotlin、Jetpack Compose 与 Media3 ExoPlayer 构建。项目针对低端电视与电视盒子优化，界面与交互围绕遥控器设计，同时兼容触摸屏手势。

应用**不内置直播源**，首次使用需自行配置 M3U 或 TVBox 订阅源。支持 HLS / RTSP 播放、多线路切换、节目单、频道收藏、局域网网页配置等能力。

## 功能特性

| 分类 | 能力 |
| --- | --- |
| 播放 | HLS / RTSP、超时换源、断线重连、全局画面比例、后台画中画 |
| 频道 | 数字选台、换台反转、频道收藏、直播源精简（仅央视 / 卫视） |
| 线路 | 同频道多线路、手动切换、播放失败自动切换、可播放域名记忆 |
| 节目单 | XML / XML.GZ、多节目单、当天节目单 |
| 直播源 | M3U / TVBox 格式、多订阅源历史、缓存时间可调 |
| 配置 | 局域网网页配置（`10481`）、自定义 UA、运行日志、网页上传 APK |
| 系统 | 开机自启、自动更新、遥控器与触摸手势 |

## 下载与安装

前往 [Releases](https://github.com/Bigzzh2022/mytv-android-ai/releases) 下载最新 APK：

- 最新版本：`v1.4.5`
- 安装包：`mytv-android-1.4.5.apk`
- 系统要求：Android 5.0（API 21）及以上，推荐 Android TV / 电视盒子

安装提示：

- 需要在系统中允许“安装未知来源应用”。
- 若设备已安装其他签名的同包名版本，请先卸载再安装，否则会提示签名冲突。
- 首次启动会提示“尚未配置直播源”，按下一节完成配置即可。

## 快速开始

1. 将电视与手机 / 电脑连接到同一局域网。
2. 在电视上启动应用，并确认设备 IP 地址。
3. 在浏览器打开 `http://<设备IP>:10481`。
4. 在“直播源”中填入可用的 M3U 或 TVBox 地址，点击保存。
5. 重启电视端应用，即可加载频道列表。

> 也可以在电视端进入 `设置 → 直播源 → 自定义直播源` 完成配置。

## 配置直播源

### 支持的格式

| 类型 | 格式 | 说明 |
| --- | --- | --- |
| 直播源 | M3U / M3U8 | 标准 `#EXTM3U` 播放列表 |
| 直播源 | TVBox | `#genre#` 分组格式 |
| 节目单 | XML / XML.GZ | 标准 EPG，按频道名匹配 |

### 网页配置项

| 配置项 | 必填 | 说明 |
| --- | --- | --- |
| 直播源 | 是 | M3U 或 TVBox 地址 |
| 节目单 | 否 | EPG 地址，留空使用默认节目单 |
| 播放器 UA | 否 | 部分直播源需要自定义 User-Agent |
| 安装 APK | 否 | 通过网页上传新版本 APK 并拉起系统安装器 |

网页端同时提供配置状态提示、地址校验、保存撤销与运行日志查看。页面所需的静态资源随应用本地打包，局域网内无需访问外部 CDN。

### 多订阅源

- 成功加载过的订阅源会写入历史列表，可在电视端 `设置 → 直播源 → 自定义直播源` 中快速切换。
- 历史列表短按切换、长按删除；切换后需重启应用生效。

### 多线路

- 同一频道存在多个播放地址时，频道名称后会显示线路标识。
- 使用左右方向键或屏幕左右滑动切换线路。
- 当前线路播放失败后会自动尝试下一条线路，并记忆可用的播放域名。

## 操作方式

| 操作 | 遥控器 | 触摸 |
| --- | --- | --- |
| 换台 | 上 / 下方向键、数字键 | 上下滑动 |
| 选台 | OK 键 | 单击 |
| 打开设置 | 菜单 / 帮助键、长按 OK | 双击、长按屏幕 |
| 切换线路 | 左 / 右方向键 | 左右滑动 |
| 收藏 / 取消收藏 | 选台界面长按 OK | 长按频道 |
| 显示收藏列表 | 频道列表顶部再按上 | 长按频道信息 |
| 查看当天节目单 | 选中频道后按菜单 / 帮助键 | 双击 |
| 退出应用 | 返回键按两次 | 返回手势两次 |

## 从源码编译

### 环境要求

| 项目 | 版本 |
| --- | --- |
| IDE | Android Studio（Ladybug 或更新） |
| JDK | 17 |
| Android SDK | compileSdk 34 |
| Gradle | 8.7（使用仓库自带 wrapper） |
| 最低系统 | Android 5.0（API 21） |

### 编译 Debug

```bash
git clone https://github.com/Bigzzh2022/mytv-android-ai.git
cd mytv-android-ai
./gradlew assembleDebug
```

产物位于 `app/build/outputs/apk/debug/`。

### 编译 Release

先在项目根目录创建 `key.properties`（已被 `.gitignore` 忽略）：

```properties
storeFile=keystore.jks
storePassword=your_store_password
keyAlias=your_key_alias
keyPassword=your_key_password
```

将签名文件放到 `app/keystore.jks`，然后执行：

```bash
./gradlew assembleRelease
```

也支持通过环境变量 `KEYSTORE`、`KEYSTORE_PASSWORD`、`KEY_ALIAS`、`KEY_PASSWORD` 提供签名信息。

### 自动发布

推送 `v*.*.*` 格式的标签会触发 GitHub Actions 构建并发布 Release：

```bash
git tag v1.4.5
git push origin v1.4.5
```

## 项目结构

```text
app/src/main/
├── java/top/yogiczy/mytv/
│   ├── activities/        # 启动入口
│   ├── data/              # 实体、数据仓库、直播源与节目单解析
│   ├── ui/                # Compose 界面、主题、HTTP 服务
│   └── utils/             # 通用工具
└── res/raw/               # 内置网页配置页
```

更完整的架构说明、模块职责与调用关系见 [开发文档](./docs/README.md)。

## 常见问题

| 问题 | 处理方式 |
| --- | --- |
| 首次启动提示“尚未配置直播源” | 应用不内置源，请通过网页或电视端设置添加订阅源后重启 |
| 网页配置页打不开 | 确认设备在同一局域网、`10481` 端口未被占用，并核对电视 IP |
| 频道列表为空 | 确认源为 M3U 或 TVBox 格式，且地址可直接访问 |
| 有频道但没有节目单 | 检查 EPG 地址、频道名与 `tvg-name` 是否匹配；节目单默认凌晨刷新 |
| 播放黑屏或卡顿 | 源可能失效或编码不支持，尝试切换线路或更换直播源 |
| IPv6 源无法播放 | 需要网络环境支持 IPv6 |
| 覆盖安装失败 | 新旧 APK 签名不一致，请先卸载旧版本再安装 |
| 自动更新失败 | 网络无法访问 GitHub 时，手动从 Releases 下载安装 |

## 技术栈

- Kotlin 2.0 + Android Gradle Plugin 8.5
- Jetpack Compose for TV + TV Material 3
- Media3 ExoPlayer（HLS / RTSP）
- OkHttp + kotlinx.serialization
- 内置 HTTP 服务（配置页与 APK 上传）
- 网页配置页使用 Vue 3 + Vant，资源本地打包

## 许可证

本项目基于 [yaoxieyoulei/mytv-android](https://github.com/yaoxieyoulei/mytv-android) 二次开发，遵循 [MIT License](./LICENSE)。

Copyright (c) 2020-PRESENT yaoxieyoulei
