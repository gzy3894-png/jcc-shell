# JCC Shell

金铲铲 `com.tencent.jkchess` 自用壳（**不依赖原 JCC Controller 的 SO**）。

## 做什么

Zygisk 注入游戏进程后：

1. 解析 IL2CPP，调用 `DataBaseManager.SearchACGHero(2)` 扫棋子表  
2. 按当前赛季 `TACG_Hero_Client` 字段读 **id / 名 / 费用 / 头像 key**  
3. 监听 `127.0.0.1:31338`（兼容 `GET:牌库`）  
4. 落盘：
   - `/data/data/com.tencent.jkchess/files/jcc_cardpool.txt`
   - `/data/data/com.tencent.jkchess/files/jcc_shell_status.txt`

## 安装

1. Magisk 安装本模块 zip → 重启  
2. **卸掉** 旧的 Il2CppDumper 模块（避免抢同一进程）  
3. 打开金铲铲 → 进大厅 → 等 1～3 分钟（首次扫表）  
4. 用 MT 看 `jcc_cardpool.txt`，或：

```text
adb shell su -c "cat /data/data/com.tencent.jkchess/files/jcc_shell_status.txt"
adb shell su -c "head -c 500 /data/data/com.tencent.jkchess/files/jcc_cardpool.txt"
```

## 协议（给悬浮窗 / 自己写的 UI）

```text
→ GET:牌库\n
← RSP:id:name:cost:remaining:total[:icon],...\n

→ GET:日志\n  或  GET:STATUS\n
← RSP:<status text>\n

→ DO:RESCAN\n
← RSP:OK ...\n
```

`remaining/total` 第一版静态表为 `0:0`（对局实时库存需后续 hook 商店刷新；名字/费用/ID 先打通）。

## logcat

```text
adb logcat -s JccShell:V
```

## 构建

GitHub Actions → Build → 产物 `jcc-shell-zygisk` artifact（Magisk 模块目录，打 zip 安装）。
