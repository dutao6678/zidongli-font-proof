# 字动力·字体校对 Windows 0.3.92（107）

Windows 首次公开发行。免费使用，应用自身源码保持私有。macOS 版准备中，本次不提供 Mac 下载。

## 功能

- 本地人工字体校对；原字体只读，校对记录保存为 .zproof 工程。
- 搜索清除后保留最近查看字的定位，多选字可批量修改校对状态并整批撤销／重做。
- 文字、箭头、矩形、椭圆、图片批注，描边颜色／线宽／线型及页面信息排版。
- PNG、PDF 和打印预览；Ctrl+W 关闭工程、Ctrl+Q 退出，未保存内容有保存保护。
- “关于”包含品牌、版本、邮箱和两处官方主页、使用条款及第三方许可；帮助菜单可主动检查双渠道签名版本清单。

## 下载与更新

[GitHub 下载 EXE](https://github.com/dutao6678/zidongli-font-proof/releases/download/v0.3.92/ZidongliFontProof-Windows-x64.exe) · [Gitee 下载 EXE](https://gitee.com/postman7729/zidongli-font-proof/releases/download/v0.3.92/%E5%AD%97%E5%8A%A8%E5%8A%9B%E5%AD%97%E4%BD%93%E6%A0%A1%E5%AF%B9.exe)

下载 Windows EXE（GitHub 附件名 `ZidongliFontProof-Windows-x64.exe`，Gitee 附件名 `字动力字体校对.exe`，内容相同），单文件、非安装器，内置 Python／Qt 和必要资源。运行时可解压至系统临时目录，无需安装开发环境或保留旁置依赖目录。

文件大小：48,929,466 字节。

SHA256：`94df6bd0ea69190370484d5fb6ec980ad12d4eb150aafa7da15e67d11c541a05`

更新前请先保存工程并正常退出，浏览器下载后再替换旧 EXE。本期不强制更新，不后台安装或自动替换正在运行的文件。仓库自动生成的 Source code ZIP/tar.gz 仅包含公开资料，不是应用安装包。

## 实际验证范围

已在 Windows 11 26100 x64 上进行定向程序化检查、单文件异地启动及用户交互复测；本轮关于排版获用户确认。先前搜索定位、批量状态、描边、页眉、画布交互和关闭主流程验收保留。94 项本轮定向检查包含五语言、构造浅深调色板和 Qt 有效 DPR 1／1.25／1.5；不冒充逐项物理显示和系统设置实测。

Windows 10 1809 x64 仅为依赖要求下限，最低系统、无开发环境干净机器、完整系统中文输入法及实体打印仍待分别验收。尚无原生 Windows ARM64 包。本 EXE 暂未做 Authenticode 代码签名；Ed25519 保护的是更新清单，两者不同。

## 使用与许可

使用前请阅读仓库 USAGE.md、TERMS.md、THIRD_PARTY.md、LICENSES.txt 与 NATIVE_LICENSES.txt。应用免费使用不等于应用源码开源；第三方组件保留各自许可权利。

作者／品牌：字动力。反馈：outlook5588@gmail.com，或任一官方仓库 Issues。公开反馈请勿上传私人字体、工程、密钥或个人资料。
