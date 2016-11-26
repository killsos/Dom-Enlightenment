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
* getComputedStyle 获取元素的已计算样式---即包含任何样式的实际样式
