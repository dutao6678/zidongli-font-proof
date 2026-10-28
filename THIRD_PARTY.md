# 第三方许可与对应源码

应用自身源码私有。各第三方组件按其原有许可提供，完整许可文本见 [LICENSES.txt](LICENSES.txt)。这些许可不表示应用自身采用同样的开源授权。

运行组件包括 CPython、PySide6／Qt／Shiboken、fontTools、glyphsLib、openstep-plist、ufoLib2、attrs、cattrs、packaging、cryptography、cffi；打包使用 PyInstaller 及其例外条款。拼音、Unicode 和简繁转换资料的原有许可亦一并保留。资源目录中的 Cocoa 说明仅适用于以后独立验收的 Mac 包，不是 Windows 替换机制说明。

Qt／PySide6 6.10.3 使用 LGPL-3.0，未修改其源码。对应版本源码：

- https://download.qt.io/official_releases/qt/6.10/6.10.3/submodules/
- https://code.qt.io/cgit/pyside/pyside-setup.git/tag/?h=v6.10.3
- https://github.com/qt/qtbase/tree/v6.10.3

## Windows 动态库替换（可选，普通使用不需要）

包内Qt/PySide6/Shiboken动态库未加反修改校验。下列MIT许可的辅助脚本只重封装库，保留应用对象代码，不需要私有源码。它不是应用自身源码，也不改变应用源码的授权。你可以为修改 LGPL 库和调试这些修改进行必要的逆向工程。

在可选开发环境中准备 Python 3，取得ABI兼容的 x64 Qt/PySide6/Shiboken修改库。将下面代码保存为replace_qt_library.py，执行：

`python replace_qt_library.py original.exe modified.exe PySide6/Qt6Core.dll modified-Qt6Core.dll`

需要同时替换多个兼容组件时，将上一步新EXE作为下一步输入，并选择另一个新输出名。正常运行应用仍只需要最终单EXE，不要求旁置库。示例不包含任何私有字体、工程或应用源码。不得覆盖正在运行的EXE。修改包的SHA256和原官方包不同；请勿冒充官方包。未来有代码签名时，本工具会拒绝不认识的布局，需另行核对格式，不能默默移除签名。

许可：Copyright (c) 2026 字动力。Permission is hereby granted, free of charge, to any person obtaining a copy of this helper software to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies, subject to retaining this copyright and permission notice. THE HELPER IS PROVIDED AS IS, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY ARISING FROM USE OF THE HELPER.


```python
"""Optional LGPL library replacement for this unsigned Windows onefile format.
This helper is provided under MIT; it contains no application source or keys.
Normal users do not need Python or this helper.
"""
import sys,struct,zlib
from pathlib import Path
COOKIE='!8sIIII64s';ENTRY='!IIIIBc';MAGIC=b'MEI\014\013\012\013\016'
def replace(source,target,member,replacement):
 source=Path(source);target=Path(target);replacement=Path(replacement)
 if source.resolve()==target.resolve() or target.exists():raise ValueError('Use a new output path')
 member=member.replace('\\','/')
 if not member.startswith(('PySide6/','shiboken6/')) or not member.endswith(('.dll','.pyd')):raise ValueError('Only Qt/PySide6/Shiboken libraries may be replaced')
 raw=source.read_bytes();at=raw.rfind(MAGIC);size=struct.calcsize(COOKIE)
 if at<0 or at+size!=len(raw):raise ValueError('Unsupported or signed archive; do not remove signatures automatically')
 magic,total,toc_at,toc_len,pyver,pylib=struct.unpack(COOKIE,raw[at:]);start=at+size-total;toc=raw[start+toc_at:start+toc_at+toc_len];pos=0;entries=[];data=bytearray();found=False
 while pos<len(toc):
  n,offset,compressed,expanded,flag,kind=struct.unpack_from(ENTRY,toc,pos);name=toc[pos+struct.calcsize(ENTRY):pos+n].rstrip(b'\0');pos+=n
  content=raw[start+offset:start+offset+compressed]
  if name.decode('utf8').replace('\\','/')==member:
   if kind!=b'b':raise ValueError('Entry is not a native library')
   original=zlib.decompress(content) if flag else content;value=replacement.read_bytes()
   if original[:2]!=b'MZ' or value[:2]!=b'MZ':raise ValueError('Expected Windows PE library')
   found=True;expanded=len(value);content=zlib.compress(value,9) if flag else value
  entries.append((len(data),len(content),expanded,flag,kind,name));data.extend(content)
 if not found:raise ValueError('Library was not found')
 new_toc=bytearray()
 for offset,compressed,expanded,flag,kind,name in entries:
  n=(struct.calcsize(ENTRY)+len(name)+1+15)//16*16
  new_toc.extend(struct.pack(ENTRY,n,offset,compressed,expanded,flag,kind)+name+b'\0'*(n-struct.calcsize(ENTRY)-len(name)))
 cookie=struct.pack(COOKIE,magic,len(data)+len(new_toc)+size,len(data),len(new_toc),pyver,pylib)
 with target.open('xb') as f:f.write(raw[:start]);f.write(data);f.write(new_toc);f.write(cookie)
if __name__=='__main__':
 if len(sys.argv)!=5:raise SystemExit('Usage: python replace_qt_library.py original.exe new.exe PySide6/Qt6Core.dll modified-Qt6Core.dll')
 replace(*sys.argv[1:])

```
