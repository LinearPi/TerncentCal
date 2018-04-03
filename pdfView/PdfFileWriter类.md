# PdfFileWriter类

```html
PdfFileWriter类
类PyPDF2.PdfFileWriter
这个类支持写PDF文件，给出其他类（通常PdfFileReader）生成的页面。

addAttachment（fname，fdata ）
在PDF中嵌入文件。

参数：	
fname（str） - 要显示的文件名。
fdata（str） - 文件中的数据。
参考：https : //www.adobe.com/content/dam/Adobe/en/devnet/acrobat/pdfs/PDF32000_2008.pdf第7.11.3节

addBlankPage（width = None，height = None ）
追加一个空白页面到这个PDF文件并且返回它。如果未指定页面大小，请使用最后一页的大小。

参数：	
宽度（浮点数） - 以默认用户空间单位表示的新页面的宽度。
高度（浮点数） - 以默认用户空间单位表示的新页面的高度。
返回：	
新添加的页面

返回类型：	
PageObject

引发PageSizeNotDefinedError：
 	
如果宽度和高度未定义且前一页不存在。

addBookmark（title，pagenum，parent = None，color = None，bold = False，italic = False，fit ='/ Fit'，* args ）
为此PDF文件添加书签。

参数：	
title（str） - 用于此书签的标题。
pagenum（int） - 此书签将指向的页码。
父 - 对创建嵌套书签的父书签的引用。
颜色（元组） - 书签的颜色为从0.0到1.0的红色，绿色和蓝色元组
大胆（布尔） - 书签是大胆的
斜体（布尔） - 书签是斜体
fit（str） - 适合目标页面。详情请参阅 addLink()。
addJS（javascript ）
添加将在打开此PDF时启动的Javascript。

参数：	javascript（str） - 您的Javascript。
>>> 输出。addJS （“this.print（{bUI：true，bSilent：false，bShrinkToFit：true}）;” ）
＃示例：这将在打开PDF时启动打印窗口。
addLink（pagenum，pagedest，rect，border = None，fit ='/ Fit'，* args ）
从矩形区域添加一个内部链接到指定页面。

参数：	
pagenum（int） - 放置链接的页面的索引。
pagedest（int） - 链接应该到的页面的索引。
矩形 - RectangleObject或四个整数数组，指定可点击的矩形区域 ，或表单中的字符串。[xLL, yLL, xUR, yUR]"[ xLL yLL xUR yUR ]"
边框 - 如果提供了一个描述边框图属性的数组。有关详细信息，请参阅PDF规范。如果省略此参数，则不会绘制边框。
fit（str） - 页面拟合或“缩放”选项（请参阅下文）。可能需要提供其他参数。传递None将作为该坐标的空值读取。
有效缩放参数（有关详细信息，请参阅PDF 1.7参考的表8.2）：
/Fit	没有额外的参数
/XYZ	[left] [top] [zoomFactor]
/FitH	[最佳]
/FitV	[剩下]
/FitR	[left] [bottom] [right] [top]
/FitB	没有额外的参数
/FitBH	[最佳]
/FitBV	[剩下]
addMetadata（infos ）
将自定义元数据添加到输出。

参数：	infos（dict） - 一个Python字典，其中每个键都是一个字段，每个值都是您的新元数据。
addPage（页）
添加页面到这个PDF文件。该页面通常从一个PdfFileReader实例中获取 。

参数：	页面（PageObject） - 要添加到文档中的页面。应该是一个实例PageObject
appendPagesFromReader（reader，after_page_append =无）
从阅读器复制页面到作家。包含一个可选的回调参数，在将页面追加到写入器后调用该参数。

参数：	reader - 一个PdfFileReader对象，从该对象将页面注释复制到此writer对象。作者的注释
将会被更新：callback after_page_append（function）：后面调用的回调函数

每个页面都附加到作者。回拨签名：

param writer_pageref（PDF页面参考）：
 	参考附加到作者的页面。
cloneDocumentFromReader（reader，after_page_append =无）
从PDF文件阅读器创建文档的副本（克隆）

参数：	
reader - 应从其创建克隆的PDF文件阅读器实例。

回调after_page_append（功能）：
 	
在每个页面附加到写入器后调用的回调函数。签名包括对附加页面的引用（委托给appendPagesFromReader）。回拨签名：

param writer_pageref（PDF页面参考）：
 	引用刚刚添加到文档中的页面。
cloneReaderDocumentRoot（读者）
将阅读器文档根复制到作者。

参数：	阅读器 - 应复制文档根目录中的PdfFileReader。
：回调after_page_append

encrypt（user_pwd，owner_pwd = None，use_128bit = True ）
使用PDF标准加密处理程序加密此PDF文件。

参数：	
user_pwd（str） - “用户密码”，允许打开和阅读提供的限制的PDF文件。
owner_pwd（str） - “所有者密码”，允许无任何限制地打开PDF文件。默认情况下，所有者密码与用户密码相同。
use_128bit（bool） - 标志是否使用128位加密。当错误时，将使用40位加密。默认情况下，此标志打开。
getNumPages（）
返回：	页数。
返回类型：	INT
getPage（pageNumber ）
通过此PDF文件中的编号检索页面。

参数：	pageNumber（int） - 要检索的页码（页面从零开始）
返回：	由pageNumber给出的索引处的页面
返回类型：	PageObject
getPageLayout（）
获取页面布局。请参阅有关setPageLayout()有效布局的说明。

返回：	目前正在使用的页面布局。
返回类型：	str，如果未指定，则为None
getPageMode（）
获取页面模式。请参阅有关setPageMode()有效模式的说明。

返回：	目前正在使用的页面模式。
返回类型：	str，如果未指定，则为None
insertBlankPage（width = None，height = None，index = 0 ）
将空白页面插入此PDF文件并返回。如果未指定页面大小，请使用最后一页的大小。

参数：	
宽度（浮点数） - 以默认用户空间单位表示的新页面的宽度。
高度（浮点数） - 以默认用户空间单位表示的新页面的高度。
index（int） - 添加页面的位置。
返回：	
新添加的页面

返回类型：	
PageObject

引发PageSizeNotDefinedError：
 	
如果宽度和高度未定义且前一页不存在。

insertPage（page，index = 0 ）
在这个PDF文件中插入一个页面。该页面通常从一个PdfFileReader实例中获取 。

参数：	
页面（PageObject） - 要添加到文档中的页面。这个论点应该是一个实例PageObject。
index（int） - 页面将被插入的位置。
pageLayout
读取和写入访问getPageLayout() 和setPageLayout()方法的属性。

pageMode
读取和写入访问getPageMode() 和setPageMode()方法的属性。

removeImages（ignoreByteStringObject = False ）
从该输出中删除图像。

参数：	ignoreByteStringObject（bool） - 可选参数，用于忽略ByteString对象。
removeLinks（）
从此输出中删除链接和注释。

removeText（ignoreByteStringObject = False ）
从该输出中删除图像。

参数：	ignoreByteStringObject（bool） - 可选参数，用于忽略ByteString对象。
setPageLayout（布局）
设置页面布局

参数：	布局（str） - 要使用的页面布局
有效的布局是：
/NoLayout	显式没有指定布局
/SinglePage	一次显示一页
/OneColumn	一次显示一列
/TwoColumnLeft	以两列显示页面，左边显示奇数页面
/TwoColumnRight
 	以两列显示页面，右侧显示奇数页面
/TwoPageLeft	一次显示两页，左侧显示奇数页
/TwoPageRight	一次显示两页，右侧显示奇数页
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
updatePageFormFieldValues（页面，字段）
更新字段字典中给定页面的表单字段值。将字段文本和值从字段复制到页面。

参数：	
页面 - 来自PDF编写器的页面引用，其中注释和字段数据将被更新。
字段 - 字段名称（/ T）和文本值（/ V）的Python字典
write（流）
将添加到此对象的页面集合写为PDF文件。

参数：	stream - 将文件写入的对象。该对象必须支持写入方法和tell方法，类似于文件对象。
```

