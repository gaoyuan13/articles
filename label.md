在游戏开发中，文字起了非常重要的作用。游戏介绍、游戏中的提示以及对话等都需要用到文字，Cocos2d-x中给文字渲染提供了灵活的机制，既可以用系统文字，也可以使用自定义渲染字体。另外，文本标签还可用来初始化菜单。

在开发中，我们最常用的4种文本标签是：Label, LabelAtlas, LabelTTF和LabelBMFont，其中lua尤其提倡使用Lable代替LabelTTF和LabelBMFont，因为Label在渲染速度上较其快。以下我们详细讲解下它们的使用方法。

# 新文本标签类Label #

lua中你可以使用Label类创建LabelTTF和LabelBMFont中任意一种标签，与他们2种不同的是，新标签类继承于SpriteBatchNode类，这样一来大大提高了渲染速度。以下代码列举几种创建Label的方法：

```
local label1 = cc.LabelTTF:create("New Label", "Arial", 64)
```
```
local layer = cc.Layer:create()  
    local label2 = cc.LabelBMFont:create("New Label", "bitmapFontTest.fnt")     
    label:setPosition(cc.p(display.cx / 2,
	display.cy / 2 -100 ))
```
```
local label2 =dispaly.newTTFLabel 
({text = "New Label", font = "Paint Boy.ttf",size = 30})
        :align(display.CENTER, display.cx, display.cy/2+100)
        :addTo(self)
```

![](http://www.tairan.com/usr/uploads/2014/04/newlabel.png)

上面的例子中，我们使用新标签类创建了一个LabelTTF标签和LabelBMFont标签：



默认创建一个LabelTTF标签，参数也和创建LabelTTF标签一样

创建一个LabelBMFont标签，第一个参数为显示内容，第二个参数为文件名

TTF方法使用.ttf文件来创建一个LabelTTF标签，需要注意的是要设置字体大小必须先配置好TTFConfig

#其他文本标签#

以上介绍了新标签类后，我们来看下以前的标签类。尽管3.0使用了新标签类，但是为了向下兼容，一些以前的标签类仍然可以使用。

## 图片文字LabelAtlas ##

LabelAtlas类是使用图片作为文字，该类直接使用图片初始化文字对象。此类支持两种文件类型来初始化：


- PNG文件
- plist文件

以下代码使用两种不同文件初始化一个文字对象：

```
local layer = cc.Layer:create()  
    local label = cc.LabelAtlas:_create("PNG Test",   
                        "tuffy_bold_italic-charmap.png", 48, 64, string.byte(" "))                
    label:setPosition(cc.p(size.width/2,  
   size.height/2))  
	:addTo(self)
```
```
local layer = cc.Layer:create()  
    local label = cc.LabelAtlas:_create("Plist Test",   
                        "tuffy_bold_italic-charmap.plist")                
    label:setPosition(cc.p(size.width/2,  
   size.height/2-100))  
	:addTo(self)
```
![](http://www.tairan.com/usr/uploads/2014/04/labelatlas.png)

下面解释一下其中的几个参数：

- 第一个参数：标签要显示的内容
- 第二个参数：图片资源的名称
- 第三个参数：每个字符的高度
- 第四个参数：每个字符的宽度
- 第五个参数：开始字符

## 系统字体LabelTTF ##

LabelTTF类使用系统中自带的字体，如果创建LabelTTF对象时未给出字体名字或者给出的名字系统中不存在，则使用引擎默认字体初始化对象。

引擎提供两种方式创建LableTTF:

- 用LabelTTF类的create方法创建
- 用Label类的方法创建，但是Label类是通过.ttf文件来创建的

以下代码分别使用LabelTTF和Label来创建Label:

```
local label1 = cc.LabelTTF:create("Create with Label", "Arial", 64)
:align(display.CENTER, display.cx, display.cy)
:addTo(self)
```

```
local label2 =dispaly.newTTFLabel 
({text = "Create with Label", font = "Paint Boy.ttf",size = 30})
        :align(display.CENTER, display.cx, display.cy/2 - 100)
        :addTo(self)
```
![](http://www.tairan.com/usr/uploads/2014/04/labelttf.png)

## 字体图集LabelBMFont ##

LabelBMFont类是一个基于位图的字体图集，是一个包含所有你需要于坐标数据一起显示在屏幕上的字符的图像，它允许字符从主图中剪切出来。

以下代码用来创建LabelBMFont对象：

```
local label = display.newBMFontLabel({
	text = "BMFont TEST",
	font = "bitmapFontTest.fnt"})
	:align(display.center, display.cx, display.cy)
	:addTo(self)
```
![](http://www.tairan.com/usr/uploads/2014/04/labelbmfont.png)

## 字体制作工具使用介绍 ##

Cocos2d-x支持许多使用fnt文件格式的位图字体，下面介绍下如何使用Glyph Designer一款Mac下的字体设计器来创建字体图集（Windows下可使用BMFont）：

- 步骤一：启动Glyph Designer,选择File->New，在左上的搜索框中键入需要的字体集名（这里使用"Helvetica"）
- 步骤二：设置字体尺寸为32，默认情况下Glyph Designer自动调整字体图集尺寸为最小可能值以适配所有可能的图像。
- 步骤三：在右边Glyph Fill里面选择颜色
- 步骤四：在Included Glyph里面点击NEHE按钮。在此区域键入你所需要用到的字符
- 步骤五：点击Export导出文件
- 步骤六：选择导出文件类型

下图展示了整个步骤

![](http://www.tairan.com/usr/uploads/2014/04/Glyph-Designer1.png)

![](http://www.tairan.com/usr/uploads/2014/04/Glyph-Designer2.png)

![](http://www.tairan.com/usr/uploads/2014/04/Glyph-Designer3.png)


