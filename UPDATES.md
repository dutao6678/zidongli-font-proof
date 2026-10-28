# 双渠道更新协议

首期只由用户主动检查，通过浏览器下载；不会自动安装或替换正在运行的程序。

## 同一份签名版本清单

两仓库计划在 updates/stable.json 提供相同字节的清单。GitHub 使用 main 分支，Gitee 使用 master 分支。正式文件须在作者确认、两个真实附件均上传并下载核验后发布，本文件不是正式清单。

清单外层为 schema=1、key_id、base64 payload、base64 Ed25519 signature。签名覆盖 payload 解码后的原始UTF-8字节，避免不同JSON排版影响核验。软件内置公钥；私钥不随应用或仓库分发。

payload 的 schema=2，product=zidongli-font-proof，channel=stable，包含单调递增revision、UTC issued_at/expires_at，以及独立windows/macos记录。未发行平台仅有status=unpublished；已发行记录包含status=released、三段数字version、整数build、notes及artifacts。每个artifact记录architecture、minimum_os、filename、bytes、sha256和github/gitee两个独立实际下载URL。

## 故障及不同步

两个HTTPS请求异步进行，各有8秒总时限、体积上限和受限重定向；关闭对话框取消请求。一个失效时仍可使用另一个有效签名源。两有效源以数字三段版本比较，其次比较构建号；相同版本构建内容冲突或高revision回退时拒绝推荐。已见revision和平台版本保存到应用偏好，旧清单不能使软件降级。

两个首次访问均为404才显示暂无发行；已有历史清单后均404不认作正常无发行。网络/超时与无效签名分别报检查失败/无效清单，不误报最新版。macOS未发行不会得到Windows安装包。

签名只验证发行资料来源，不是EXE的Authenticode代码签名，也不是完整TUF体系；有效期需维护，公钥更换需另行设计可信升级。无自动下载和安装，因此软件展示SHA256供用户对下载文件核对。
