# 以下内容从现在的角度来看已经非常不合时宜了,因为新的编译器(VScode)等的出现,以及sublime的几乎停止维护,sublime已经基本上可以说是退出历史潮流了.

首先是安装：
按Ctrl+`调出console然后粘贴如下代码：
```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
重启Sublime Text
如果在Perferences->package settings中看到package control这一项，则安装成功。

然后Ctrl+Shift+P后输入install回车
下面是常用插件列表

- emmet html快速编写

- Prefixr CSS前缀

- SublimeLinter 语法高亮

- AllAutocomplete 自动补全

- SublimeCodeIntel 代码提示

- htmlpretty 代码格式化

- SideBarEnhancements 侧边栏增强

- converttoutf8 编码

- OmniMarkupPreviwer markdown 预览
- AutoFileName 文件路径自动补全
下面是一些引用
 >- SublimeLinter = 错误语法
 >- JsMinifier =自动压缩js文件
 >- Sublime CodeIntel =代码自动提示
 >- Bracket Highlighter =代码匹配
 >- CSScomb CSS =属性排序
 >- SublimeTmpl =快速生成文件模板
 >- SideBarEnhancements =设置sublime text2/3支持浏览器预览
 >- ColorPicker =调色盘
 >- Tag = Html格式化
 >- Clipboard History = 剪贴板历史记录
 >- SideBarEnhancements = 侧栏右键功能增强
 >- GBK to UTF8 =GBK转换成UTF8
 >- SFTP =ftp插件
 >- WordPress = WordPress函数
 >- PHPTidy =排版PHP代码
 >- YUI Compressor =压缩JS和CSS文件
 >- Alignment =代码对齐
 >- Emmet =大名鼎鼎呀
 >- Prefixr =css自动添加 -webkit 等私有词缀
 
 ----------------
 删除插件：ctrl+shift+p后remove package
