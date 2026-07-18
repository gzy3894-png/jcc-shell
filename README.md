# JCC Shell 2.5.1

金铲铲（`com.tencent.jkchess`）**当前赛季数据版**。

## 一句话

2.5.0 不能用，多半是**游戏数据旧了**。  
2.5.1 = **同一套用法 + 真机扫出来的新字段**，先恢复**牌库表可读**。

## 数据从哪来

- 真机 `jcc-scan` 扫描成功（2026-07-18）
- 关键偏移写在 `module/src/main/cpp/season_offsets.h`

| 字段 | 偏移 |
|------|------|
| 英雄 id | 0x10 |
| 名字 | 0x18 |
| 费用 | 0x60 |
| 小图标 | 0xf8 |
| 套数 | 0x114 |

## 两种用法

### A. Zygisk 模块（本仓库）

Magisk 安装 Actions 产物 zip，重启，打开金铲铲进大厅。  
看：`/data/user/0/com.tencent.jkchess/files/jcc_cardpool.txt`  
或本机 `127.0.0.1:31338` → `GET:牌库`

### B. 普通 APK 注入

见姊妹仓：**[jcc-shell-apk](https://github.com/gzy3894-png/jcc-shell-apk)** 的 **v2.5.1**  
Root 点启动即可（不必装 Zygisk 模块）。

## 版本说明

| 版本 | 含义 |
|------|------|
| 2.5.0 | 旧数据（会失效） |
| **2.5.1** | **当前赛季数据（本版）** |

尚未完整复刻 2.5.0 全部开关（剩余量/对局叠层等），牌库静态表已按新数据接好。

## 构建

Push `master` → GitHub Actions → Artifact `jcc-shell-zygisk`
