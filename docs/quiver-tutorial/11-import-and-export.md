# 导入与导出

Quiver 不会将你的笔记锁住。

Quiver 的笔记本和笔记都保存为普通的 JSON 文本文件。文件格式在此有详细的说明：<https://github.com/HappenApps/Quiver/wiki/Quiver-Data-Format>。

因此你可以放心，你的笔记永远不会无法读取。而且，Quiver 也很容易与你使用的其它工具集成。

Quiver 自带的导出器支持 HTML、 PDF 和 Markdown。你可以导出整个 Quiver 的笔记本为相互链接的 HTML 网页。

导出为 Markdown 时，代码单元格会自动转换为 Markdown 内嵌代码块。这样你可以很方便地将导出的 Markdown 文件上传到 GitHub 或其它使用 Markdown 的平台。

如果你有特殊的导入或导出的需要，你可以很容易地写一个脚本，读取 Quiver 的笔记格式，然后导出成你想要的格式。自定义脚本对于编写编程相关的书籍或教程的用户尤其有用。

几个示例脚本可以在这里找到: <https://github.com/HappenApps/Quiver/wiki/Export-Scripts>。