# PdfFileMerger类

```html
PdfFileMerger类
class PyPDF2.PdfFileMerger（strict = True ）
初始化一个PdfFileMerger对象。PdfFileMerger将多个PDF合并为一个PDF。它可以连接，切片，插入或上述的任意组合。

查看功能merge()（或append()）和write()使用信息。

参数：	严格（bool） - 确定是否应该警告用户所有问题，并且导致一些可纠正的问题是致命的。默认为True。
addBookmark（title，pagenum，parent = None ）
为此PDF文件添加书签。

参数：	
title（str） - 用于此书签的标题。
pagenum（int） - 此书签将指向的页码。
父 - 对创建嵌套书签的父书签的引用。
addMetadata（infos ）
将自定义元数据添加到输出。

参数：	infos（dict） - 一个Python字典，其中每个键都是一个字段，每个值都是您的新元数据。例：{u'/Title': u'My title'}
addNamedDestination（title，pagenum ）
将输出目标添加到输出中。

参数：	
标题（str） - 要使用的标题
pagenum（int） - 此目的地指向的页码。
append（fileobj，bookmark = None，pages = None，import_bookmarks = True ）
与merge()方法相同，但假定您要将所有页面连接到文件的末尾而不是指定位置。

参数：	
fileobj - 文件对象或支持与文件对象类似的标准读取和查找方法的对象。也可以是表示PDF文件路径的字符串。
书签（str） - 您可以选择通过提供书签文本来指定要在包含文件的开头应用的书签。
页面 - 可以是页面范围或元组，以将源文档中指定范围的页面合并到输出文档中。(start, stop[, step])
import_bookmarks（bool） - 您可以通过指定为，来防止源文档的书签被导入False。
close（）
关闭所有文件描述符（输入和输出）并清除所有内存使用情况。

merge（position，fileobj，bookmark = None，pages = None，import_bookmarks = True ）
将给定文件中的页面合并到指定页码的输出文件中。

参数：	
position（int） - 插入此文件的页码。文件将在给定的数字后插入。
fileobj - 文件对象或支持与文件对象类似的标准读取和查找方法的对象。也可以是表示PDF文件路径的字符串。
书签（str） - 您可以选择通过提供书签文本来指定要在包含文件的开头应用的书签。
pages – can be a Page Range or a (start, stop[, step]) tuple to merge only the specified range of pages from the source document into the output document.
import_bookmarks (bool) – You may prevent the source document’s bookmarks from being imported by specifying this as False.
setPageLayout(layout)
Set the page layout

Parameters:	layout (str) – The page layout to be used
Valid layouts are:
/NoLayout	Layout explicitly not specified
/SinglePage	Show one page at a time
/OneColumn	Show one column at a time
/TwoColumnLeft	Show pages in two columns, odd-numbered pages on the left
/TwoColumnRight
 	Show pages in two columns, odd-numbered pages on the right
/TwoPageLeft	Show two pages at a time, odd-numbered pages on the left
/TwoPageRight	Show two pages at a time, odd-numbered pages on the right
setPageMode（模式）
设置页面模式。

参数：	模式（str） - 要使用的页面模式。
有效的模式是：
/UseNone	不要显示轮廓或缩略图面板
/UseOutlines	显示轮廓（又名书签）面板
/UseThumbs	显示页面缩略图面板
/FullScreen	全屏视图
/UseOC	显示可选内容组（OCG）面板
/UseAttachments
 	显示附件面板
write（fileobj ）
将已合并的所有数据写入给定的输出文件。

参数：	fileobj - 输出文件。可以是文件名或任何类型的文件类对象。
```

