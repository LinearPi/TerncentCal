# PdfFileReader

```thml
PdfFileReader类
class PyPDF2.PdfFileReader（stream，strict = True，warndest = None，overwriteWarnings = True ）
初始化一个PdfFileReader对象。由于PDF流的交叉引用表被读入内存，此操作可能需要一些时间。

参数：	
stream - File对象或支持与File对象类似的标准读取和查找方法的对象。也可以是表示PDF文件路径的字符串。
严格（bool） - 确定是否应该警告用户所有问题，并且导致一些可纠正的问题是致命的。默认为True。
warndest - 记录警告的目的地（默认为 sys.stderr）。
overwriteWarnings（bool） - 确定是否warnings.py用自定义实现覆盖Python的 模块（默认为 True）。
decrypt（密码）
当使用带有PDF标准加密处理程序的加密/安全PDF文件时，此功能将允许对文件进行解密。它会根据文档的用户密码和所有者密码检查给定的密码，然后在密码正确的情况下存储解密密钥。

密码是否匹配并不重要。这两个密码都提供了正确的解密密钥，可以使文档与该库一起使用。

参数：	密码（str） - 要匹配的密码。
返回：	0如果密码失败，1密码与用户密码匹配，并且2密码与所有者密码匹配。
返回类型：	INT
引发NotImplementedError：
 	如果文档使用不受支持的加密方法。
documentInfo
访问该getDocumentInfo()函数的只读属性。

getDestinationPageNumber（目的地）
检索给定目标对象的页码

参数：	目的地（目的地） - 获取页码的目的地。应该是一个实例 Destination
返回：	页码或-1如果找不到页面
返回类型：	INT
getDocumentInfo（）
检索PDF文件的文档信息字典（如果存在）。请注意，某些PDF文件使用元数据流而不是docinfo字典，并且这些元数据流将不会被此功能访问。

返回：	该PDF文件的文件信息
返回类型：	DocumentInformation或者None如果不存在。
getFields（tree = None，retval = None，fileobj = None ）
如果此PDF包含交互式表单字段，则提取字段数据。该树和retval的参数是递归使用。

参数：	fileobj - 一个文件对象（通常是一个文本文件），用于在所有找到的交互式表单域上编写报告。
返回：	一个字典，其中每个键是一个字段名称，每个值都是一个Field对象。默认情况下，映射名称用于密钥。
返回类型：	字典，或者None表单数据无法找到。
getFormTextFields（）
从文档中检索带有文本数据的表单域（输入，下拉列表）

getNamedDestinations（tree = None，retval = None ）
检索文档中存在的指定目标。

返回：	一个将名字映射到的字典 Destinations。
返回类型：	字典
getNumPages（）
计算此PDF文件中的页面数。

返回：	页数
返回类型：	INT
引发PdfReadError：
 	如果文件被加密并且限制阻止了此操作。
getOutlines（节点=无，轮廓=无）
检索文档中出现的文档大纲。

返回：	一个嵌套列表Destinations。
getPage（pageNumber ）
通过此PDF文件中的编号检索页面。

参数：	pageNumber（int） - 要检索的页码（页面从零开始）
返回：	一个PageObject实例。
返回类型：	PageObject
getPageLayout（）
获取页面布局。请参阅有关setPageLayout() 有效布局的说明。

返回：	目前正在使用的页面布局。
返回类型：	str，None如果没有指定
getPageMode（）
获取页面模式。请参阅有关setPageMode() 有效模式的说明。

返回：	目前正在使用的页面模式。
返回类型：	str，None如果没有指定
getPageNumber（页）
检索给定PageObject的页码

参数：	页面（PageObject） - 获取页码的页面。应该是一个实例PageObject
返回：	页码或-1如果找不到页面
返回类型：	INT
getXmpMetadata（）
从PDF文档根目录中检索XMP（可扩展元数据平台）数据。

返回：	一个XmpInformation 可用于从文档访问XMP元数据的实例。
返回类型：	XmpInformation或者 None如果在文档根目录中找不到元数据。
isEncrypted
显示此PDF文件是否加密的只读布尔属性。请注意，如果该属性为true，则即使在decrypt()调用该方法后该属性也将保持为真 。

namedDestinations
访问该getNamedDestinations()函数的只读属性 。

numPages
访问该getNumPages()函数的只读属性 。

outlines
访问的只读属性
getOutlines() 功能。
pageLayout
访问该getPageLayout()方法的只读属性 。

pageMode
访问该getPageMode()方法的只读属性 。

pages
基于getNumPages()和 getPage()方法模拟列表的只读属性 。

xmpMetadata
访问该getXmpMetadata()函数的只读属性 。
```



