# 字动力·字体校对

**专为字体检查、问题标注和修改意见交接打造的本地校对工具。**

无需掌握专业字体设计软件，也能浏览字库、查找字符、圈出问题，并把修改意见整理交给字体设计师。

支持 **Windows 和 macOS**，免费使用，核心校对功能离线运行。

## 浏览字库，更方便地发现问题

支持打开 TTF、OTF 和 `.glyphs` 文件，通过字格浏览、多字搜索和校对状态筛选检查字形。提供参考字、简繁候选、Unicode 编码（U 码）和拼音等辅助信息，便于辨认和对照。

参考信息受离线数据覆盖范围影响；简繁参考不会改变原始编码。部分 `.glyphs` 特殊结构暂不支持，智能部件尚未正式支持；请以应用提示和发行说明为准。

## 直接在字形上标注修改意见

提供文字、箭头、箭头文字框、矩形、椭圆、直线、弧线和自由画笔等批注工具。支持插入参考图片、调整位置及大小，方便对照笔画、结构和比例。

通过校对状态与问题字总览，集中查看、定位和管理需要修改的字。应用提供人工校对工具，不自动判断字形对错。

## 校对记录独立保存，保留原始字体

应用以只读方式加载源字体，批注、备注及校对状态保存在独立的 **`.zproof` 工程文件**中，支持保存后继续校对，不直接修改原始字体。

**工程默认不嵌入源字体；重新打开或交接工程时，请保留对应的字体文件。** 参考图片随工程嵌入保存。更新前请保存工程并妥善备份；应用回退不等于工程格式回退。

## 导出结果，方便沟通与交接

支持 **PDF、PNG、TXT 导出及打印预览**。

TXT 可集中列出问题字符，便于整批复制到后续处理工具；PDF 和图片可保留直观的批注布局，方便反馈修改意见。问题字符复制和 TXT 导出保留原始字符身份，不以简繁参考字替换。

## 独立运行，无需配置开发环境

- **Windows**：独立 x64 EXE，双击运行，无需安装 Python 或 Qt。运行时会自动解压所需组件至系统临时目录，不是安装器。
- **macOS**：独立应用，提供 DMG 和 ZIP；使用 DMG 时，将应用拖入“应用程序”，推出 DMG 后即可独立运行。

运行库和所需资源随应用提供，不需要在应用旁保留依赖文件夹，首次启动无需联网下载运行组件。字体、工程、批注及输出在本地处理；检查更新需要联网，并由用户主动发起。本期不自动安装或覆盖正在运行的应用。

## 下载与系统要求

请从官方发布页下载对应系统版本：

- [GitHub 官方发布页](https://github.com/dutao6678/zidongli-font-proof/releases)
- [Gitee 官方发布页](https://gitee.com/postman7729/zidongli-font-proof/releases)

| 平台 | 当前正式版本 | GitHub 下载 | Gitee 下载 |
|---|---|---|---|
| Windows x64 | 0.3.92（107） | [独立 EXE](https://github.com/dutao6678/zidongli-font-proof/releases/download/v0.3.92/ZidongliFontProof-Windows-x64.exe) | [独立 EXE](https://gitee.com/postman7729/zidongli-font-proof/releases/download/v0.3.92/%E5%AD%97%E5%8A%A8%E5%8A%9B%E5%AD%97%E4%BD%93%E6%A0%A1%E5%AF%B9.exe) |
| macOS | 0.3.112（127） | [DMG](https://github.com/dutao6678/zidongli-font-proof/releases/download/v0.3.112/ZidongliFontProof-macOS-universal2.dmg) · [ZIP](https://github.com/dutao6678/zidongli-font-proof/releases/download/v0.3.112/ZidongliFontProof-macOS-universal2.zip) | [DMG](https://gitee.com/postman7729/zidongli-font-proof/releases/download/v0.3.112/ZidongliFontProof-macOS-universal2.dmg) · [ZIP](https://gitee.com/postman7729/zidongli-font-proof/releases/download/v0.3.112/ZidongliFontProof-macOS-universal2.zip) |

**Windows**：Windows 10 1809 x64 为依赖下限，已在 Windows 11 26100 x64 验证指定功能；最低系统、无开发环境干净机器及完整系统中文输入法仍待分别验收。尚无 Windows ARM64 原生包，EXE 尚未进行 Authenticode 代码签名。

**macOS**：最低要求 **macOS 15.0**。提供 Universal 2 应用，已检查包内原生依赖的 arm64／x86_64 架构，并在 Apple Silicon／macOS 26.1 完成人工界面验收和发行包完整性核验；具体安装与验证范围见本版发行说明。Intel Mac、macOS 15 实机、多屏及无开发环境干净机器尚未完整验收。

**macOS 版本尚未完成 Developer ID 签名与 Apple 公证；目前仅通过 ad-hoc 签名完整性检查，DMG 也未签名／公证。** 实体打印仍待设备验收，打印预览不能代替实际出纸验证。更完整的兼容范围请查看各版本发行说明。

请勿将仓库自动生成的“Source code ZIP／tar.gz”当作应用安装包；它们只包含本仓库的公开资料。

### 下载校验

两渠道对应附件已完成匿名完整下载核验，文件内容一致：

- **Windows EXE**：48,929,466 字节。GitHub 文件名为 `ZidongliFontProof-Windows-x64.exe`，Gitee 为 `字动力字体校对.exe`。  
  SHA256：`94df6bd0ea69190370484d5fb6ec980ad12d4eb150aafa7da15e67d11c541a05`
- **Mac DMG**：70,653,451 字节。  
  SHA256：`56d869ced9ab0f60c0c7e863b039becf27a8350d727af8d918a88e0886f00365`
- **Mac ZIP**：70,842,584 字节。  
  SHA256：`e22437bbf359d619e43a941f36e78823efbcc1f29ab24627b7ba82a07fd4d154`

应用内“帮助 → 检查更新”读取正式签名清单；Mac 0.3.112 安装包已公开，Mac 更新清单尚待生产签名及发布，当前可从以上官方链接手动下载。清单签名与应用代码签名／Apple 公证是不同事项。

## 使用说明与联系

- [使用说明](USAGE.md) · [反馈方式](FEEDBACK.md) · [使用条款](TERMS.md)
- [第三方许可说明](THIRD_PARTY.md) · [许可资料](LICENSES.txt) · [原生组件许可](NATIVE_LICENSES.txt)
- 联系作者：[**outlook5588@gmail.com**](mailto:outlook5588@gmail.com)，也可在任一官方仓库提交 Issue。

公开反馈时，请勿上传私人字体、工程、密钥或个人资料。

**应用免费发布，应用源码不公开。使用及分发规则请参阅仓库中的使用条款。第三方组件保留各自原有许可权利。**

## 界面示例

![Windows 校对界面](SCREENSHOT.png)

截图使用自绘几何测试字形，不含用户工程或私人字体文件。
