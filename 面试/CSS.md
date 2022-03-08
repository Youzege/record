## CSS 基础复习



#### @规则

CSS 里包含了以下 @规则：

- [@namespace](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2F%40namespace) 告诉 CSS 引擎必须考虑XML命名空间。
- [@media](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2F%40media), 如果满足媒体查询的条件则条件规则组里的规则生效。
- [@page](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2F%40page), 描述打印文档时布局的变化.
- [@font-face](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2F%40font-face), 描述将下载的外部的字体。
- [@keyframes](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2F%40keyframes), 描述 CSS 动画的关键帧。
- [@document](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2F%40document), 如果文档样式表满足给定条件则条件规则组里的规则生效。

```css
@font-face {
  font-family: "Open Sans";
  src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2"),
       url("/fonts/OpenSans-Regular-webfont.woff") format("woff");
}
```



#### @charset

用于定义样式表的字符集，它必须是样式表中的第一个元素，如有多个@charset，只生效第一个。

注意：值必须是双引号包裹

```css
@charset"UTF-8"
```



#### @import

用于告诉 CSS 引擎引入一个外部样式表。

与link的区别

- link 是 HTML 标签，除了能导入 CSS 外，还能导入别的资源，比如图片、脚本和字体等；而 @import 是 CSS 的语法，只能用来导入 CSS
- link 导入的样式会在页面加载时同时加载，@import 导入的样式需等页面加载完成后再加载
- link 没有兼容性问题，@import 不兼容 ie5 以下
- link 可以通过 JS 操作 DOM 动态引入样式表改变样式，而@import不可以



### 层叠性

层叠样式表，有许多的 CSS 声明都能作用到的时候，那最后谁应该起作用

针对不同源的样式，将按照如下的顺序进行层叠，越往下优先级越高

- 用户代理样式表中的声明(例如，浏览器的默认样式，在没有设置其他样式时使用)
- 作者样式表中的常规声明(这些是我们 Web 开发人员设置的样式)
- 作者样式表中的 !important 声明

需要结合 CSS 选择器的优先级以及继承性来理解。比如针对同一个选择器，定义在后面的声明会覆盖前面的；作者定义的样式会比默认继承的样式优先级更高



### 选择器

#### 基础选择器

- 标签选择器：`h1 div p`
- 类选择器：`.checked .container`  
- ID 选择器：`#picker #map`
- 通配选择器：`*`

**属性选择器**

- `[attr]`：指定属性的元素；
- `[attr=val]`：属性等于指定值的元素；
- `[attr*=val]`：属性包含指定值的元素；
- `[attr^=val]` ：属性以指定值开头的元素；
- `[attr$=val]`：属性以指定值结尾的元素；



#### 组合选择器

- 相邻兄弟选择器：`A + B`
- 普通兄弟选择器：`A ~ B`
- 子选择器：`A > B`
- 后代选择器：`A B`



#### 伪类

**条件伪类**

- `:lang()`：基于元素语言来匹配页面元素；
- `:dir()`：匹配特定文字书写方向的元素；
- `:has()`：匹配包含指定元素的元素；
- `:is()`：匹配指定选择器列表里的元素；
- `:not()`：用来匹配不符合一组选择器的元素；

**行为伪类**

- `:active`：鼠标激活的元素；
- `:hover`： 鼠标悬浮的元素；
- `::selection`：鼠标选中的元素；

**状态伪类**

- `:target`：当前锚点的元素；
- `:link`：未访问的链接元素；
- `:visited`：已访问的链接元素；
- `:focus`：输入聚焦的表单元素；
- `:required`：输入必填的表单元素；
- `:valid`：输入合法的表单元素；
- `:invalid`：输入非法的表单元素；
- `:in-range`：输入范围以内的表单元素；
- `:out-of-range`：输入范围以外的表单元素；
- `:checked`：选项选中的表单元素；
- `:optional`：选项可选的表单元素；
- `:enabled`：事件启用的表单元素；
- `:disabled`：事件禁用的表单元素；
- `:read-only`：只读的表单元素；
- `:read-write`：可读可写的表单元素；
- `:blank`：输入为空的表单元素；
- `:current()`：浏览中的元素；
- `:past()`：已浏览的元素；
- `:future()`：未浏览的元素；



**结构伪类**

- `:root`：文档的根元素；
- `:empty`：无子元素的元素；
- `:first-letter`：元素的首字母；
- `:first-line`：元素的首行；
- `:nth-child(n)`：元素中指定顺序索引的元素；
- `:nth-last-child(n)`：元素中指定逆序索引的元素；；
- `:first-child	`：元素中为首的元素；
- `:last-child`	：元素中为尾的元素；
- `:only-child`：父元素仅有该元素的元素；
- `:nth-of-type(n)	`：标签中指定顺序索引的标签；
- `:nth-last-of-type(n)`：标签中指定逆序索引的标签；
- `:first-of-type`	：标签中为首的标签；
- `:last-of-type`：标签中为尾标签；
- `:only-of-type`：父元素仅有该标签的标签；



#### 伪元素

- `::before`：在元素前插入内容；
- `::after`：在元素后插入内容；



### 优先级

优先级就是分配给指定的 CSS 声明的一个权重，它由匹配的选择器中的每一种选择器类型的数值决定。为了记忆，可以把权重分成如下几个等级，数值越大的权重越高

- 10000：!important；
- 01000：内联样式；
- 00100：ID 选择器；
- 00010：类选择器、伪类选择器、属性选择器；
- 00001：元素选择器、伪元素选择器；
- 00000：通配选择器、后代选择器、兄弟选择器；