

## 初始
* jQuery=javaScript query=js的查询 write less do more DOM 和 BOMde api太low了

jQuery实际就是js的插件 （但一般不这样说） **链式调用 读写合一**

* **两把利器： jQuery核心函数  jQuery对象 jQuery**

`(function( window, undefined ) {
​	jQuery = function( selector, context ) {
​		return new jQuery.fn.init( selector, context, rootjQuery );
​	}
​    window.jQuery = window.$ = jQuery;
}(window)`

* 我认为dom元素对象和jQuery元素对象的最大区别就是是否绑定了事件函数

##  jQuery作为函数

​	**jQuery既可以作为函数调用也可以作为方法调用**

​	作为函数调用 可以传 **回调函数**，**DOM元素**封装成jQuery对象，**选择器字符串**得到jQuery对象，也可以传递一个**标签字符串**，创建标签对象并封装成jQuery对象。

​	**参数为选择器字符**：查找到所有匹配的标签，并**将它们封装成jQuery对象 该jQuery对象中包含DOM元素对象**事件回调函数的this是触发该事件的DOM元素对象 而不是jQuery对象

### 基本选择器

* id，属性，并集，交集，任意选择器

### 层次选择器：

* 后代元素  空格  
* 子元素  >  
* 兄弟选择器 （所有兄弟~  紧接着的兄弟+)

### 过滤选择器：

* :lt(index) 过滤小于index的元素 :gt(index)过滤大于index的元素
* :first :last
* :not()
* :contains("...")选择内容为...的元素
* [attribute="..."]选择属性为...的元素

### 表单专属选择器：

* :input
* :text
* :password
* :radio
* :checkbox
* :submit 
* :image
* :reset
* button
* :file
* :hidden(可以匹配type=hidden或者所有的不可见元素 )

### 表单特有属性选择器：

* :enabled 
* :disabled
* :checked
* :selected 

## jQuery作为对象

​	**jQuery对象是一个包含所有匹配的任意多个dom元素的伪数组对象 （还包含context和selector等对象）**

### 伪数组对象基本行为  

> 不就是把js数组的方法给了伪数组对象

- size()/length: 包含的DOM元素个数
- [index]/get(index): 得到对应位置的DOM元素
- each(): 遍历包含的所有DOM元素
- index(): 得到在所在兄弟元素中的下标

### 工具方法

>  不就是把js一些对象的一些方法给了jQuery对象

* $.each(): 遍历数组或对象中的数据
* $.trim(): 去除字符串两边的空格
* $.type(obj): 得到数据的类型
* $.isArray(obj): 判断是否是数组
* $.isFunction(obj): 判断是否是函数
* $.parseJSON(json) : 解析json字符串转换为js对象/数组

### 属性相关

* 操作任意属性

  1. attr()

  2. removeAttr()

  3. prop()

* 操作HTML代码/文本/值

  1. val()

  2. html()

* 操作class属性

  1. addClass()

  2. removeClass()

### 样式相关

* css

  1. css()

* 位置
  1. offset(): 相对浏览器左上角的坐标 offset().left  offset().top  原生的offset是相对于定位父元素 区别相对于视口和相对于屏幕
  2. position(): 相对于父元素左上角的坐标
  3. scrollTop()
  4. scrollLeft()

* 元素尺寸

  1. height(): height  width(): width

  2. innerHeight(): height+padding  innerWidth(): width+padding

  3. outerHeight(false/true): height+padding+border  如果是true, 加上margin

     outerWidth(false/true): width+padding+border 如果是true, 加上margin

### 元素过滤

- 在jQuery对象中的元素对象**数组**中过滤出一部分元素来
  1. first()
  2. last()
  3. eq(index|-index)
  4. filter(selector)
  5. not(selector)
  6. has(selector)
- 在已经匹配出的元素**集合**中根据选择器查找孩子/父母/兄弟标签
  1. children(selector): 子标签中找
  2. find(selector) : 后代标签中找
  3. parent(selector) : 父标签
  4. prevAll(selector) : 前面所有的兄弟标签
  5. nextAll(selector) : 后面所有的兄弟标签
  6. siblings(selector) : 前后所有的兄弟标签

### 文档的增删改

- 添加/替换元素

1. append(content)向当前匹配的所有元素**内部的最后**插入指定内容
2. prepend(content)向当前匹配的所有元素**内部的最前面**插入指定内容
3. before(content)将指定内容插入到当前所有匹配元素的**前面**
4. after(content)将指定内容插入到当前所有匹配元素的**后面**
5. replaceWith(content)用指定内容**替换**所有匹配的标签

- 删除元素
  1. empty()删除所有匹配元素的**子元素**
  2. remove()删除所有匹配的**元素**
  3. 事件相关

### 事件的绑定与解绑

- 事件绑定 
  1. eventName(function(){}) 绑定对应事件名的监听, 例如：$('#div').click(function(){})
  2. on(eventName, funcion(){}) 通用的绑定事件监听, 例如：$('#div').on('click', function(){})
- 优缺点
  1. eventName: 编码方便, 但只能加一个监听, 且有的事件监听不支持
  2. on: 编码不方便, 可以添加多个监听, 且更通用
- 事件解绑
  1. off(eventName)

- 事件的坐标
  - event.clientX, event.clientY  相对于视口的左上角
  - event.pageX, event.pageY  相对于页面的左上角
  - event.offsetX, event.offsetY 相对于事件元素左上角
- 事件相关处理
  - 停止事件冒泡 : event.stopPropagation()  对于IE event.cancelBubble=true
  - 阻止事件默认行为 : event.preventDefault() 对于IE event.returnValue=false

### 内置动画相关

- 淡入淡出: 不断改变元素的透明度来实现的
  * fadeIn(): 带动画的显示
  * fadeOut(): 带动画隐藏
  * fadeToggle(): 带动画切换显示/隐藏

- 滑动
  * slideDown(): 带动画的展开
  * slideUp(): 带动画的收缩
  * slideToggle(): 带动画的切换展开/收缩
- 显示隐藏
  * show(): (不)带动画的显示
  * hide(): (不)带动画的隐藏
  * toggle(): (不)带动画的切换显示/隐藏
- 最可怕的动画
  * animate(属性，时间): 自定义动画效果的动画
  * stop(): 只停止当前动画
  * stop(true):停止所有动画

## 自定义插件 

* 给 $ 添加4个工具方法
* jQuery.extend(object)
  * min(a, b) : 返回较小的值
  * max(c, d) : 返回较大的值
  * leftTrim() : 去掉字符串左边的空格
  * rightTrim() : 去掉字符串右边的空格
* 给jQuery对象 添加3个功能方法
* jQueryjQuery.fn.extend(object)
  * checkAll() : 全选
  * unCheckAll() : 全不选
  * reverseCheck() : 全反选

* 区别: window.onload与 $(document).ready()

  * window.onload 包括页面的图片加载完后才会回调(晚) 只能有一个监听回调

  * $(document).ready() 等同于: $(function(){}) 页面加载完就回调(早) 可以有多个监听回调

## 多库共存

​	如果有2个库都有$, 就存在冲突

解决 : jQuery库可以释放$的使用权, 让另一个库可以正常使用, 此时jQuery库只能使用jQuery了

API : jQuery.noConflict()

##  官方扩展插件

* jquery.validate.js 声明式表单验证 只需要声明各种验证规则，可以自定义错误验证信息。
* jquery.UI.js 手风琴，自动搜索，选项卡等效果展示。
* laydate 非jQuery扩展插件，但是是十分好用的时间插件。



