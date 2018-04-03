# PageObject类

```	html
PageObject类
class PyPDF2.pdf.PageObject（pdf = None，indirectRef = None ）
此类表示PDF文件中的单个页面。通常，这个对象将通过访问该类的getPage()方法 来创建 PdfFileReader，但也可以使用createBlankPage()静态方法创建一个空页面 。

参数：	
pdf - 页面所属的PDF文件。
indirectRef - 将源对象的原始间接引用存储在其源PDF中
addTransformation（ctm ）
将转换矩阵应用于页面。

参数：	ctm（tuple） - 包含变换矩阵的操作数的6元素元组。
artBox
A RectangleObject，以默认用户空间单位表示，用于定义页面创建者所期望的页面有意义内容的范围。

bleedBox
A RectangleObject，以默认的用户空间单位表示，定义在生产环境中输出时应将页面内容剪切到的区域。

compressContentStreams（）
通过连接所有内容流并应用FlateDecode过滤器来压缩此页面的大小。

但是，如果内容流压缩由于某种原因变为“自动”，则此功能可能不执行任何操作。

static createBlankPage（pdf = None，width = None，height = None ）
返回一个新的空白页面。如果width或者height是None，尝试从最后一页得到的页面大小的PDF。

参数：	
pdf - 页面所属的PDF文件
宽度（浮点数） - 以默认用户空间单位表示的新页面的宽度。
高度（浮点数） - 以默认用户空间单位表示的新页面的高度。
返回：	
新的空白页面：

返回类型：	
PageObject

引发PageSizeNotDefinedError：
 	
如果pdf是None或不包含页面

cropBox
A RectangleObject，以默认用户空间单位表示，定义默认用户空间的可见区域。当页面被显示或打印时，其内容将被裁剪（裁剪）到该矩形，然后以某种实现定义的方式强加在输出媒体上。默认值：与mediaBox。

extractText（）
按照它们在内容流中提供的顺序查找所有文本绘图命令，并提取文本。这适用于某些PDF文件，但对其他文件很不好，具体取决于所使用的发生器。这将在未来得到改进。不要依赖这个函数产生的文本的顺序，因为如果这个函数变得更复杂，它将会改变。

返回：	一个unicode字符串对象。
getContents（）
访问页面内容。

返回：	该/Contents对象，或者None它不存在。 /Contents是可选的，如PDF参考7.7.3.3中所述
mediaBox
A RectangleObject，以默认用户空间单位表示，定义打算在其上显示或打印页面的物理介质的边界。

mergePage（第2页）
将两个页面的内容流合并为一个。资源引用（即字体）由两个页面维护。此页面的mediabox / cropbox / etc不会更改。参数页面的内容流将被添加到此页面的内容流的末尾，这意味着它将在本页面的后面或之后绘制。

参数：	page2（PageObject） - 要合并到此页的页面。应该是一个实例PageObject。
mergeRotatedPage（page2，rotation，expand = False ）
这与mergePage类似，但要合并的流通过应用转换矩阵进行旋转。

参数：	
page2（PageObject） - 要合并到这个页面中的页面。应该是一个实例PageObject。
旋转（浮动） - 旋转的角度，以度为单位
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeRotatedScaledPage（page2，rotation，scale，expand = False ）
这与mergePage类似，但要合并的流通过应用转换矩阵进行旋转和缩放。

参数：	
page2（PageObject） - 要合并到这个页面中的页面。应该是一个实例PageObject。
旋转（浮动） - 旋转的角度，以度为单位
比例（浮点数） - 比例因子
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeRotatedScaledTranslatedPage（page2，rotation，scale，tx，ty，expand = False ）
这与mergePage类似，但要合并的流通过应用转换矩阵进行转换，旋转和缩放。

参数：	
page2（PageObject） - 要合并到这个页面中的页面。应该是一个实例PageObject。
tx（float） - 在X轴上的平移
ty（float） - Y轴上的平移
旋转（浮动） - 旋转的角度，以度为单位
比例（浮点数） - 比例因子
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeRotatedTranslatedPage（page2，rotation，tx，ty，expand = False ）
这与mergePage类似，但要合并的流通过应用转换矩阵进行旋转和翻译。

参数：	
page2（PageObject） - 要合并到这个页面中的页面。应该是一个实例PageObject。
tx（float） - 在X轴上的平移
ty（float） - Y轴上的平移
旋转（浮动） - 旋转的角度，以度为单位
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeScaledPage（page2，scale，expand = False ）
这与mergePage类似，但要合并的流通过应用转换矩阵进行缩放。

参数：	
page2（PageObject） - 要合并到此页的页面。应该是一个实例PageObject。
比例（浮点数） - 比例因子
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeScaledTranslatedPage（page2，scale，tx，ty，expand = False ）
这与mergePage类似，但要合并的流将通过应用转换矩阵进行转换和缩放。

参数：	
page2（PageObject） - 要合并到这个页面中的页面。应该是一个实例PageObject。
比例（浮点数） - 比例因子
tx（float） - 在X轴上的平移
ty（float） - Y轴上的平移
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeTransformedPage（page2，ctm，expand = False ）
这与mergePage类似，但转换矩阵应用于合并流。

参数：	
page2（PageObject） - 要合并到此页的页面。应该是一个实例PageObject。
ctm（元组） - 一个包含变换矩阵操作数的6元素元组
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
mergeTranslatedPage（page2，tx，ty，expand = False ）
这与mergePage类似，但要合并的流通过应用转换矩阵进行转换。

参数：	
page2（PageObject） - 要合并到这个页面中的页面。应该是一个实例PageObject。
tx（float） - 在X轴上的平移
ty（float） - Y轴上的平移
展开（布尔） - 页面是否应该展开以适应要合并页面的尺寸。
rotateClockwise（角度）
顺时针以90度为增量旋转页面。

参数：	angle（int） - 旋转页面的角度。必须是90度的增量。
rotateCounterClockwise（角度）
逆时针以90度为增量旋转页面。

参数：	angle（int） - 旋转页面的角度。必须是90度的增量。
scale（sx，sy ）
通过向其内容应用转换矩阵并更新页面大小，按给定因子缩放页面。

参数：	
sx（float） - 水平轴上的缩放因子。
sy（float） - 垂直轴上的缩放因子。
scaleBy（因素）
通过向其内容应用转换矩阵并更新页面大小，按给定因子缩放页面。

参数：	factor（float） - 缩放因子（对于X和Y轴）。
scaleTo（宽度，高度）
通过向其内容应用转换矩阵并更新页面大小，将页面缩放到指定的维度。

参数：	
宽度（浮点数） - 新的宽度。
高度（浮动） - 新的高度。
trimBox
A RectangleObject，用默认的用户空间单位表示，在修剪后定义完成页面的预期尺寸。
```

