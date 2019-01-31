# 1 CSS 选择器

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

> 无论何种选择，最后选中的都是 DOM 中的元素，也就是**标签**。

# 2 选择器分类

1. 简单选择器 (Simple Selectors)
2. 属性选择器 (Attribute Selectors)
3. 伪类选择器 (Pseudo-Class)
4. 伪元素选择器 (Pseudo-Element)
5. 组合器 (Combinators)
6. 多重选择器 (Multiple Selectors)

---

## 2.1 简单选择器

1. 元素选择器 (Element Selectors)  
   <kbd>元素名</kbd>
2. 类选择器  
   <kbd>.类名</kbd>
3. id 选择器  
   <kbd>#id</kbd>
4. 通用选择器  
   <kbd>\*</kbd>
5. 组合器与多重选择器 (Combinators and Multiple Selectors)
   - **后代选择器**  
     `A B` 表示 A 的任意**后代** B 元素
   - **子选择器**  
     `A > B` 表示 A 的任意**子代** B 元素
   - **相邻兄弟选择器**  
     `A + B` 表示 A  之后任意相邻的 B 兄弟元素 (一个)
   - **通用兄弟选择器**  
     `A ~ B` 表示 A 之后的任意 B\* 兄弟元素 (多个)
   - **多重选择器**  
     `A , B` 表示 A 和 B 同时选择

## 2.2 属性选择器

1. 存在和值 (Presence and Value) 属性选择器

- `[attr]`: 选择包含 attr 属性的所有元素, 不考虑 attr 的值
- `[attr=val]`: 选择包含 attr 属性的, 值为 val 的所有元素
- `[attr~=val]`: 选择包含 attr 属性的, 值 **包含** val 的所有元素 (例如 `attr="aaa bbb **val** eee"`)

2. 子串值 (Substring Value) 属性选择器

- `[attr|=val]`: 选择包含 attr 属性的, 值以 val 或者 val- 开头的所有元素
- `[attr^=val]`: 选择包含 attr 属性的, 值以 val 开头的所有元素
- `[attr$=val]`: 选择包含 attr 属性的, 值以 val 结尾的所有元素
- `[attr*=val]`: 选择包含 attr 属性的, 值中 **包含** val 所有元素

## 2.3 伪类和伪元素

1. 伪类 (Pseudo-Class)

- :active
- :any
- :checked
- :default
- :dir()
- :disabled
- :empty
- :enabled
- :first
- :first-child
- :first-of-type
- :fullscreen
- :focus
- :hover
- :indeterminate
- :in-range
- :invalid
- :lang()
- :last-child
- :last-of-type
- :left
- :link
- :not()
- :nth-child()
- :nth-last-child()
- :nth-last-of-type()
- :nth-of-type()
- :only-child
- :only-of-type
- :optional
- :out-of-range
- :read-only
- :read-write
- :required
- :right
- :root
- :scope
- :target
- :valid
- :visited

2. 伪元素 (Pseudo-Element)

所谓伪元素, 就是在元素边界内隐藏的子虚拟元素位置, 添加伪元素就相当于添加虚拟的子元素; 天生自带 content 属性

- ::after
- ::before
- ::first-letter
- ::first-line
- ::selection
- ::backdrop

## 2.4 伪类分类

1. 与链接相关

- `E:active`  鼠标按下到鼠标弹起结束前的元素
- `E:focus`  当前拥有键盘输入焦点的元素
- `E:hover` 鼠标划过的元素
- `E:link` 未访问的链接
- `E:visited` 已点击的链接

2. 与用户界面相关

- `E:enabled` 匹配表单中激活的元素
- `E:disabled` 匹配表单中禁用的元素
- `E:checked` 匹配表单中被选中的 radio（单选框）或 checkbox（复选框）元素
- `E::selection` 匹配用户当前选中的元素

3. 结构性

- `E:root` 匹配文档的根元素，对于 HTML 文档，就是 HTML 元素
- `E:nth-child(an+b)`
- `E:nth-last-child(an+b)`
- `E:nth-of-type(an+b)` 与:nth-child()作用类似，但是仅匹配 E **同种标签**的元素
- `E:nth-last-of-type(an+b)` 与:nth-last-child() 作用类似，但是仅匹配 E **同种标签**的元素
- `E:first-child` 匹配父元素的第一个子元素，等同于:nth-child(1)
- `E:last-child` 匹配父元素的最后一个子元素，等同于:nth-last-child(1)
- `E:first-of-type` 匹配父元素下 E **同种标签**的第一个子元素，等同于:nth-of-type(1)
- `E:last-of-type` 匹配父元素下 E **同种标签**的最后一个子元素，等同于:nth-last-of-type(1)
- `E:only-child` 匹配父元素下仅有的一个子元素，等同于:first-child:last-child 或 :nth-child(1):nth-last-child(1)
- `E:only-of-type` 匹配父元素下使用同种标签的唯一一个子元素，等同于:first-of-type:last-of-type 或 :nth-of-type(1):nth-last-of-type(1)
- `E:empty` 匹配一个不包含任何子元素的元素，注意，文本节点也被看作子元素

4. 反选

- `E:not(.foo)` 类名不是 .foo 的所有 E 元素

5. 目标

- `E:target` 文档中的 ID 元素被访问时, 被选中

```html
<a href="#section2">Test</a>
<section id="section2">Example</section>
```

```css
section:target {
  border: 2px solid black;
}
```

---

# 3 CSS 权重

## 3.1 权重规则总结:

1. !important 优先级最高，但也会被权重高的 important 所覆盖
2. 行内样式总会覆盖外部样式表的任何样式(除了!important)
3. 单独使用一个选择器的时候，不能跨等级使 css 规则生效
4. 如果两个权重不同的选择器作用在同一元素上，权重值高的 css 规则生效
5. 如果两个相同权重的选择器作用在同一元素上：以后面出现的选择器为最后规则.
6. 权重相同时，与元素距离近的选择器生效

## 3.2 权重的五个等级

1. !important: infinite!
2. 行内样式: infinite-
3. ID 选择器: 100
4. 类选择器, 伪类选择器和属性选择器: 10
5. 元素选择器和伪元素选择器: 1

## 3.3 等级关系

!important > 行内样式 > ID 选择器 > 类选择器 / 伪类选择器 / 属性选择器 > 元素选择器 / 伪元素选择器

## 3.4 详解权重

1. 不推荐使用 !important
   其没有结构与上下文可言，并且很多时候权重的问题，就是因为不知道在哪里定义了一个
2. 行内样式总会覆盖外部样式表的任何样式, 会被 !important 覆盖
3. 单独使用一种选择器的时候，不能跨等级使 css 规则生效  
   无论多少个 class 组成的选择器，都没有一个 ID 选择器权重高。类似的，无论多少个元素组成的选择器，都没有一个 class 选择器权重高, 无论多少个 ID 组成的选择器，都没有行内样式权重高
4. 如果两个权重不同的选择器作用在同一元素上，权重值高的 css 规则生效
5. 如果两个相同权重的选择器作用在同一元素上, 以后面出现的选择器为准
6. 权重相同时, 与元素距离近的选择器生效  
   比如同样的两组选择器, 权重一致, 但是一个在文件内是内联表, 另一个是文件外时是引入表, 则内联表为准

**慎用 id 选择器**

> 权重过高, 极有可能出现严重的选择器权重失衡
> id 选择器具有唯一性, 这样的东西该留给 JavaScript, 算是另一种意义上的解耦合...
