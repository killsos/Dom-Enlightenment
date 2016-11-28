# Dom Enlighten reading note
2016年04月17日

## 1 节点概述

### 1.1 文档对象模型 Document Object Model DOM
DOM 是一个由Javascript节点对象组成的层次结构/树

HTML文档被浏览器解析并转换为一个有节点对象组成以体现当前文档结构的树状结构 DOM的目的是使用Javascript操作（添加 删除 替换 修改 创建事件）为当前文档提供一个编程接口。

节点类型 nodeTypoe
1. DOCUMENT_NODE        
document

2. ELEMENT_NODE            
body div a script ...

3. ATTRIBUTE_NODE          
class="funEdges"

4. TEXT_NODE               
换行符与空白符构成的文本字符

5. DOCUMENT_FRAGMENT_NODE        
document.createDocumentFragment()

6. DCUMENT_TYPE_NODE         
<!DOCTYPE html>

而Nodes是上面这些对象的父类对象，并且上面节点类型在Node属性是常量 001.html      
典型DOM树里的每一个节点对象都从Node继承属性和方法。
Node只是一个Javascript构造函数 因此Node与所有Javascript里对象一样,从Object.prototype继承
002.html
* ELEMENT_NODE =1
* ATTRIBUTE_NODE =2
* TEXT_NODE =3
* CDATA_SECTION_NODE =4
* ENTITY_REFERENCE_NODE =5
* ENTITY_NODE =6
* PROCESSING_INSTRUCTION_NODE =7
* COMMENT_NODE =8
* DOCUMENT_NODE =9
* DOCUMENT_TYPE_NODE =10
* DOCUMENT_FRAGMENT_NODE =11
* NOTATION_NODE =12
* DOCUMENT_POSITION_DISCONNECTED =1
* DOCUMENT_POSITION_PRECEDING =2
* DOCUMENT_POSITION_FOLLOWING =4
* DOCUMENT_POSITION_CONTAINS =8
* DOCUMENT_POSITION_CONTAINED_BY =16
* DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC =32


### 最常用属性
1. nodeName
2. nodeType
3. nodeValue 绝大多数节点该属性为null 除了Text Comment 类型的节点

#### 创建Element Text Attbribute Comment 节点方法
1. createElement()

2. createTextNode()

3. createAttribute() //弃用
  * setAttribute()
  * getAttribute()
  * removeAttribute()

4. createComment()


#### 添加元素与文本节点
1. innerHTML  
创建元素或者文件节点并添加到DOM中

2. outerHTML
创建元素或者文本节点并添加到DOM中，同时替换掉元素本身
004.html

3. innerText
替换节点中的文本节点(所有节点都会被替换)
005.html

4. outerText
创建文本节点并将替换自身节点

5. insertAdjacentHTML
  * beforebegin 开标签之前
  * afterbegin  开标签之后
  上面两项仅在该节点有父节点时候有效
  * beforeend   闭标签之前
  * afterend    闭标签之后

6. innerHTML可以将字符串中html元素都转换成DOM节点 textContent只能构造文本节点
textContent的文本包含HTML元素 也是原样输出

7. document.wirte 可以同步创建 添加节点到DOM  write方法会在页面加载 解析时将内容输出到页面
上 wirte方法会堵塞正被加载的HTML文档解析

8. textContent获取所有元素的内容 包括script style 但是innerText不能
innerText能意识到样式 不会返回隐藏的元素  textContent可以返回
innerText 可以显示的自身文本节点 子元素文本节点 和空格
textContent 可以将显示后者隐藏的 自身文本节点 子元素文本节点 和换车 空格
006.html

9. insertAdjacentElement() insertAdjacentText() 在现代浏览器可以使用除去火狐

10. appendChild()  insertBefore(ele,elenext)
如果没有elenext这个参数行为appendChild行为一样

11. removeChild() replaceChild()
parentNode.removeChild(chileNode)
oldNode.parentNode.replaceChild(newNode,oldNode)

12. cloneNode() 复制节点 可以复制该节点或者该节点以及它所有子节点
var cloneele = document.querySelector("ul").cloneNode();
复制的节点同时复制属性和属性值也复制 任何通过addlistener() node.onclick 方式添加事件
不会被复制

13. 节点集合 Nodelist HTMLCollection
  * 类数组
  * 集合可以实时或者静态的
  * 集合中节点以所在树的顺序排序
  * 集合有一个length属性

14. 获取所有直属子节点的列表/集合 chileNodes
    * 不仅包括element 还有Text comment 节点
    * forEach()
    * [].forEach.call(chileNodes,function(item){}) IE11+

15. 遍历节点
  * parentNode
  * firstChild
  * lastChild
  * nextSibling
  * previousSibling
  * 后四个不仅element 还包括Text Comment 节点

  * firstElementChild
  * lastElementChild
  * nextElementChild
  * previousElementChild
  * children  007.html
  * parentElement
  * 这五个只是Element节点

16. 节点包含关系
    * nodeA.contains(nodeB) 节点A是否包含节点b
    * compareDocumentPosition() 返回节点的关系

17. 判断两个节点是否相同
 * 节点类型相同
 * 字符串属性相同
 * attribute NameNodeMaps相等
 * childNodes Nodelists 相等
 * isEqualNode()
 * 如果只想知道节点引用是否指向同一节点 可以用 ===


## 2 文档节点
### 2.1 文档节点简述
HTMLDocument构造函数(从document继承)在DOM中创建DOCUMENT_NODE(如window.document)
* window.document.constructor  == function HTMLDocument(){}
* window.document.nodeType
* document.implementation.createHTMLDocument() 可以在浏览器中当前加载的文档之外创建一个自己的HTML文档 以编程方式给iframe提供HTML文档

* document.DOCTYPE=====doctype
* document.documentElement=====html
* document.head=====head
* document.body=====body

* document.implementation.hasFeature()
* element.isSupported(feature,version)

#### 获取文档中当前聚焦或者激活节点引用
document.activeElement

#### 判断文档中任何节点得到焦点
document.hasFocus()

#### document.defaultView 指向window对象

#### ownerDocument 从某一元素取得文档引用
返回的是 document


## 3元素节点
HTML文档中每个元素都有个唯一的本源 就是一个构造函数
例如 a元素的构造函数 HTMLAnchorElement()

### 常用属性
* createElement()
* tagName
* children
* getAttribute()
* setAttribute()
* hasAttribute()
* removeAttribute()
* classList
* dataSet
* attributes

* classList有add() remove() contains() toggle()
toggle()在某个值缺失时候添加 或者已有则删除

dataset   data-name
dataset.name
delete dataset.name


## 4元素节点选取
document.querySelector()
document.getElementById()

document.querySelectorAll()  静态   008.html
document.getElementByTagName()   实时
document.getElementByClassName() 实时


children属性返回HTMLCollection 由所有直属子节点中的元素节点组成 不包括文本节点 注释节点
如果没有子节点返回一个空的类数组列表

document.all
document.forms
document.images
document.links
document.scripts
document.styleSheets

node.matchesSelector("css选择器字符串")
需要加前缀

## 元素节点几何量、滚动几何量

### CSSOM视图模式(CSSOM View Module)

[CSSOM视图模式草案地址](url](https://www.w3.org/TR/cssom-view-1/)
[张鑫旭的文章地址](http://www.zhangxinxu.com/wordpress/2011/09/cssom%E8%A7%86%E5%9B%BE%E6%A8%A1%E5%BC%8Fcssom-view-module%E7%9B%B8%E5%85%B3%E6%95%B4%E7%90%86%E4%B8%8E%E4%BB%8B%E7%BB%8D/)


#### 获取相对于offsetParent的 offsetTop offsetLeft
* offsetTop offsetLeft 可以获取相对于offsetParent的偏移像素量
* 父级链上的元素没有(reltive absolute fixed) offsetParent是body
* 如果元素本身是fixed定位 无论父级链上的元素没有(reltive absolute fixed)  那么chorme safair offsetparent是null,firefox 是body
* 当容器元素的display 被设置为 "none"时（译注：IE和Opera除外），offsetParent属性返回null



##### fixed的元素 margin依然起作用

#### 获取相对于视图的 getBoundingClientRect()  
可以获取元素外边沿的位置,E、Firefox3+、Opera9.5、Chrome、Safari支持，在IE中，默认坐标从(2,2)开始计算，导致最终距离比其他浏览器多出两个像素，我们需要做个兼容。
left top right bottom width height
width =  width + padding + border


##### getClientRects()
getClientRects 返回一个TextRectangle集合，就是TextRectangleList对象。TextRectangle对象包含了, top left bottom right width height 六个属性

#### 获取元素在视区主中的尺寸（填充+内容）不包含 边框、
clientWidth clientHight

#### 获取视区中某一特定点上最顶层元素 .document.elementFromPoint()

#### 获取滚动元素的尺寸 scrollHeight  scrollwidth
#### 获取滚动元素的距离 scrollLeft  scrollTop
#### 使用scrollIntoView() 滚动元素到视区
scrollIntoView(true) 滚到顶部
scrollIntoview(false) 滚动底部


## 元素节点内联样式
### 样式属性 style
* style属性返回一个cssstyleDeclaration对象  并且仅仅包含内联样式
* style对象中属性使用驼峰命名规则
* background-color   ====   backgroundColor
* setProperty getProperty removeProperty 这三个方法的属性名称是横线的名称
* style对象cssText属性 也可以设置 获取 移除 style的内容
* 使用新字符串替换style属性是批量改动某个元素样式是最快方式
* getComputedStyle 获取元素的已计算样式---即包含任何样式的实际样式  不计算简写属性（margin）而计算具体属性（margin-left）
window.getComputedStyle("#div").color
* 通过setAttribute() removeAttribute和classList.add() classList.remove()

        document.querySelector('#div').setAttribute()...

## 文本节点
#### HTML文档中的文本表现为Text()构造函数的示例即文本节点
#### HTML文档被解析时,在HTML页面中与元素混杂在一起的文本就会被转换为文本节点 016.html
#### DOM中空白符 回车符 文本字符都是文本节点
#### document.createTextNode()
#### Text节点的文本值/数据可以用data或nodeValue获得
#### appendData deleteData insertData replaceData subStringData()
#### 使用textContent移除文本标记并返回所有的子文本节点
* textContent属性可用来后去所有子文本节点,或设置节点内容成某一特定Text节点,当在某个节点上用它获取该节点文本内容时,它将返回一个由调用该方法的的节点内所有文本节点合并而成的字符串
#### 使用normalize()合并兄弟文本节点成单个文本节点
#### 使用spiltText()分割文本节点
#### textContent innerText区别
* 除了火狐都是支持一个与textContent差不多的属性innerTex
* innerTex知道css 如果隐藏文本 innerTex会无视它 而textContent不会
* innerTex关心css 会触发一次重排 而textContent不会
* innerTex无视script  style所含的文本点
* innerTex不像textContent会返回的文本规范化,textContent会完全按照文本所含返回,仅移除标记。该字符串包括字符串 换行符及回车
* innerText是非标准的是特定浏览器 textContent是根据DOM规范实现的

## DocumentFragment节点
* 创建与使用DocumentFragment节点,可在实时DOM树之外提供一个轻量的文档树
* 可以把DocumentFragment看做一个空的文档模板,行为与实时的DOM相仿,但仅在内存中存在,并且的子节点可以简单地内存中操作,而后附加到实时DOM

#### 使用createDocumentFragment()创建

#### 使用createDocumentFragment与createElement()的区别
* 文档片段可以包含任意类型的节点(除了html body这个节点),而元素不行
* 添加文档片段到DOM时,它自身不会添加到.这与附加元素节点相反,元素节点会跟着附加操作一并添加到DOM中
* 当文档片段被附加到DOM中时,它从文档片段传输内容至它被附加的位置,而自身不在存在于创建它时所在的位置,对用来临时包含节点,而后移动到实时DOM树的元素节点来说就不是这情况了

#### 添加DocumentFragment添加到时DOM通过appendChild/insertBefore,文档片段的子节点将被传输成为调用这些方法的DOM节点的子节点

#### 使用文档片段上的innerHTML

#### DOMparser可以解析存在字符串中的HTML成为一个DOM文档
* new DOMParser(),DOMParser.parseFromString()
* IE使用Document.loadXML()

#### 通过复制将片段所含节点保留在内存中
* cloneNode(true)


## css样式与css规则
#### 通过使用HTMLlinkElement引入外部样式
#### 通过使用HTMLStyleElement定义内联样式
#### HTML文档中一旦有样式表添加就会生成CSSStyleSheet对象,样式表里每条CSS规则都表示为一个CSSStyleSheet对象
* 017.html

#### 选取引入样式表的元素(linkstyle)与访问表示样式表自身的实际对象(CSSStyleSheet)是不同的
* 018.html
#### 访问DOM中所有样式表(CSSStyleSheet)
#### document.styleSheets提供一个包含HTML文档中所有样本对象列表的访问方式包含显式链接(link且rel设为stylesheet)和内联样式(style)
#### styleSheets是实时的,length属性
#### styleSheets还可以访问HTML文档中的当个样式表即先选取DOM中的元素style/link再使用,.sheet属性取得CSSStyleSheet对象的访问

            document.querySelector("style/link").sheet
