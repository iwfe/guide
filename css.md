# css规范
### 1.关于BEM规范
>块（block）,
>元素（element）,
>修饰符（modifier）
>组件之间的完全解耦，不会造成命名空间的污染，如：.mod-xxx ul li 的写法带来的潜在的嵌套风险
>BEM 命名会使得 Class 类名变长，但经过 gzip 压缩后这个带宽开销可以忽略不计


由以下三种符号表示依赖关系：

```
-   中划线:仅作为连字符使用，表示某个块或者某个子元素的多单词之间的连接记号。
__  双下划线:双下划线用来连接块和块的子元素
_   单下划线:单下划线用来描述一个块或者块的子元素的一种状态

type-block__element_modifier

```

统一风格即可,

```css
/*常规写法*/
.list{}
.list.select{}
.list .item{}
.list .item.active{}

/*推荐写法*/
.list{}
.list_select{}
.list__item{}
.list__item_active{}
```

```html
<ul class="list">
    <li class="list__item">第一项
        <div class="list__name">我是名称</div>
        <a class="list__link">我是link</a>
    <li>
    <li class="list__item_active">第一项
        <div class="list__name">我是名称</div>
        <a class="list__link">我是link</a>
    <li>
</ul>
```

## 2.缩进
>2-4个空格，建议2个;

```css
.list {
    ...
}

.list {
  ...
}

```

## 3.空格
>‘{' 前
>冒号和属性值之间包含一个空格;
>多个属性,句号后跟一个空格;
>选择器 '> + ~’ 前后各保留一个空格;
>注释 /* 后和 */ 前;

```css
.list > .item {
  color: #ccc;
}
```


## 4.注释

```css
/* 颜色 */
/*
 * 颜色
*/

.list {
/* 颜色 */
color: #f00; /* 颜色 */
  ...
}
```

## 5.分号
>通常在大括号结束前的值可以省略分号，但对修改、添加和维护工作带来不必要的失误和麻烦;
>每个属性声明末尾都加分号;

```css
/* bad */
.list {
  color: #ccc;
  font-size: 12px
}

/* good */
.list {
  color: #ccc;
  font-size: 12px;
}
```

## 6.换行
>‘{‘ 后和 ‘}’前;
>每个属性独占一行;
>多个规则的分隔符 ,后;

```css
/* bad */
.list, item {}

/* good */
.list,
.item {
  ...
}

/* bad */
.list {color: #ccc;font-size: 12px;}

/* good */
.list {
  color: #ccc;
  font-size: 12px;
}

```


## 7.空行

>文件最后保留一个空行;
>‘}’ 后最好跟一个空行;
>属性之间也可加适当的空行分割;

```css
/* bad */
.list {
  ...
}
.list {
  color: #ff0;
  .list_item {
    ...
  }

}

/* good */
.list {
  ...
}

.list {
  color: ff0;

  .list_item {
    ...
  }
}
```

## 8.行长度
>每行不要超过120个字符;

```css
.list {
  background-image:
    url(../log.png)
    url(../log.png);
  background:
    transparent url('asdasdasdasdasdasdasd123123123')
    no-repeat;
}
```


## 9.引号
>最外层统一使用单引号；
>url的内容要用引号；
>属性选择器中的属性值需要引号;

```css
.list {
  content: '';
  background-image: url('log.png');
}

.list[data-type='go'] {
  ...
}
```

## 10.色值
>颜色16进制用小写字母,如果一定用了大小，那整个项目保持一致即可;
>颜色16进制尽量用简写;
>不要使用rgba，除非带alpha的颜色值，可以使用rgba;
>不要使用命名色值 如：orange;

```css
/* bad */
.list {
  color: #ff0000;
  background: #CCC;
}

/* good */
.list {
  color: #f00;
  background: #ccc;
}
```

## 11.命名
>scss，less中的变量、函数、混合采用驼峰式命名

```css
/* id */
#myBlog {
  ...
}

/* 变量 */
$colorBlock: #000;

/* 函数 */
@function pxTORem($px) {
  ...
}

@mixin centerBlock {
  ...
}
```

## 12.属性声明顺序
>1.位置属性(position, top, right, z-index, display, float等)
>2.大小(width, height, padding, margin)
>3.文字系列(font, line-height, letter-spacing, color- text-align等)
>4.背景(background, border等)
>5.其他(animation, transition等)

```css
.list {
  display: block;
  float: right;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  width: 100px;
  height: 100px;
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  text-align: center;
  color: #333;
  background-color: #f5f5f5;
  opacity: 1;
}

```

## 13.字体

| 字体  操作系统  | Family Name |
| ----------- | ----------- |
| 宋体 (中易宋体) | Windows SimSun  |
| 黑体 (中易黑体) | Windows SimHei  |
| 微软雅黑  | Windows Microsoft YaHei  |
| 微软正黑  | Windows Microsoft JhengHei  |
| 华文黑体  | Mac/iOS STHeiti  |
| 冬青黑体  | Mac/iOS Hiragino Sans GB  |
| 文泉驿正黑 | Linux WenQuanYi Zen Hei  |
| 文泉驿微米黑  | Linux WenQuanYi Micro Hei  |


「英文字体在前、中文字体在后」、
「效果佳 (质量高/更能满足需求) 的字体在前、效果一般的字体在后」的顺序编写；
最后必须指定一个通用字体族( serif / sans-serif );

```css
body{
  font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
}
```



## 14. 杂项

1.嵌套不要超过3层
2.属性尽量简写
3.不要留空规则
4.属性为0，不用加单位
5.尽量不要用 *
6.尽量不要用 @import
7.z-index掌握在可控范围，也可通过变换书写顺序

