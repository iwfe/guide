## css规范
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