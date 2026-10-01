SGSOL PC 脚本更新

更新源：https://github.com/13835629670/sgsol-pc-updates
手机源：https://github.com/13835629670/sgsol-mobile-updates（独立维护）
源码仓库 sgsol-helper 保持私有。PC 分发包公开，代码可提取；分发包不含账号、口令、邮件记录、运行日志、签名私钥。

使用：点击微端顶部“脚本更新”→“检查更新”→“更新到…”→结束对局并暂停邮件循环→“重启并生效”。检查时下载并校验，点击更新后保存，重启前不替换运行脚本。账号配置与邮件记录保留。

旧微端第一次使用：下载并解压 PC 引导包，退出微端，在 PowerShell 执行 .\Install-PC-Updater.ps1，输入包含 SGSOL.exe 的安装目录。只需安装一次；以后普通脚本更新通过按钮完成。安装失败显示原因并恢复备份，不要求清除账号数据。适用于已核对的 Windows SGSOL 1.0.9 微端结构；其他版本需先验证。官方客户端重装或覆盖更新后可能需要重装引导包。

更新范围：邮件助手和手气卡两个 .user.js 文件；加载器、验签公钥、主进程和官方游戏本体不在普通脚本更新范围。PC 与 Android 使用不同签名密钥，平台和仓库也参与校验，不能混装。

可靠性：签名、文件摘要和 JavaScript 语法检查通过后才保存。下次启动备份两文件，再事务式替换；文件写入失败或上次启动未完成确认时，恢复上一版并拒绝重复安装失败序号。保留备份，不修改邮件库或配置。启动确认仅确认助手入口和同步启动无报错，不代表全部游戏功能验证。启动失败请关闭并重新打开微端以回退。

发布：
1. 验证现役修改后运行 scripts/Sync-FromRuntime.ps1。
2. node --test pc/updater.test.cjs，并完成 Electron 当前版本兼容性检查。
3. node pc/package-update.cjs <工作区外PC专用私钥.pem> <新输出目录> <递增序号> <版本号>。
4. 核对只包含两份现役代码，将 latest.json 发布到 sgsol-pc-updates/main。勿更改手机更新仓库。
5. PC 私钥固定保留在工作区外。首次生成的 electron/pc-update-config.json 只包含公钥，不要随脚本发布修改加载器基线。
6. 引导包包含受控加载器文件、Install-PC-Updater.ps1、install.cjs 和同一签名 latest.json。加载器改动需重新分发引导包。

电脑更新不会自动登录、领取奖励，也不会改代理设置。
