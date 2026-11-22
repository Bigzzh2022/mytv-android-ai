# 我的电视（mytv-android）Code Wiki

> 面向 Android TV 的原生直播播放应用，使用 Kotlin + Jetpack Compose（TV）+ Media3 ExoPlayer 实现。
> 本 Wiki 基于仓库 `v1.4.4` 源码静态分析整理，用于快速理解项目结构、核心实现与二次开发方式。

## 项目速览

| 项目 | 内容 |
| --- | --- |
| 应用名称 | 我的电视 / My TV |
| 包名 / namespace | `top.yogiczy.mytv` |
| 版本 | `versionCode 1`、`versionName 1.4.4` |
| 最低 / 目标 SDK | minSdk 21（Android 5.0）/ targetSdk 34 |
| 语言 | Kotlin 2.0.0 |
| UI | Jetpack Compose + AndroidX TV Material 3 |
| 播放内核 | AndroidX Media3 ExoPlayer 1.3.1（HLS / RTSP / Progressive，可扩展 FFmpeg 解码 AAR） |
| 网络 | OkHttp 4.12.0、AndroidAsync（内置 HTTP 配置服务） |
| 序列化 | kotlinx.serialization 1.7.0 |
| 构建 | Gradle 8.7 + AGP 8.5.0，JDK 17 |
| 主要入口 | [LeanbackActivity](../app/src/main/java/top/yogiczy/mytv/activities/LeanbackActivity.kt) |

## 文档地图

| 编号 | 文档 | 内容 |
| --- | --- | --- |
| 01 | [项目概览](01-项目概览.md) | 项目定位、功能清单、技术栈、目录结构、运行时组件 |
| 02 | [架构总览](02-架构总览.md) | 分层架构、模块职责、启动时序、核心数据流、设计模式 |
| 03 | [数据层](03-数据层.md) | 实体模型、IPTV/EPG/Git 仓库、解析器、文件缓存机制 |
| 04 | [播放与选台](04-播放与选台.md) | 播放器抽象与 Media3 实现、播放状态、选台/多线路/超时重连 |
| 05 | [界面层](05-界面层.md) | Compose 界面树、选台面板、经典面板、快捷面板、设置、Toast、更新、FPS |
| 06 | [配置与网络服务](06-配置与网络服务.md) | SP 配置项全集、内置 HTTP 配置服务 API、设置页与网页联动 |
| 07 | [构建与运行](07-构建与运行.md) | 环境要求、编译、签名、CI 发布、安装运行与排障 |
| 08 | [依赖与调用关系](08-依赖与调用关系.md) | Gradle 依赖清单、模块依赖图、关键调用链、源码文件索引 |

## 建议阅读路径

- **第一次接触项目**：01 → 02 → 07，先建立整体认知并跑通应用。
- **改业务功能（源/节目单/收藏）**：02 → 03 → 05 → 06。
- **改播放行为（多线路、超时、解码）**：02 → 04 → 03。
- **排查构建或发布问题**：07 → 08。

## 核心设计一句话总结

应用采用「Activity → Compose Screen / StateHolder → Repository → Parser/Fetcher → 本地文件缓存」的分层结构：
- `MainViewModel` 负责启动时拉取直播源与节目单；
- `IptvParser` / `EpgFetcher` / `GitReleaseParser` 通过接口 + 实例列表实现可插拔的格式策略；
- `LeanbackMainContentState` 驱动频道与线路切换，`LeanbackVideoPlayerState` 封装播放器回调；
- `SP` 统一管理全部持久化配置，`HttpServer` 在 `10481` 端口提供网页配置与 APK 上传能力。

## 文档约定

- 源码链接均为相对仓库根目录的路径，可直接在 GitHub / 本地 Markdown 预览中跳转。
- “关键类/函数”表格中，函数名后括号内为简要签名说明。
- 图表使用 Mermaid 语法，支持 GitHub、Typora、VS Code 预览。
- 文档描述以源码实际行为为准；源码中标注 `TODO` 或尚未启用的能力会单独注明。

## 相关链接

- 仓库：[yaoxieyoulei/mytv-android](https://github.com/yaoxieyoulei/mytv-android)
- 更新日志：[CHANGELOG.md](../CHANGELOG.md)
- 原始说明：[README.md](../README.md)
