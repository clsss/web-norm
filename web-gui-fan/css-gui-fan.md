# css规范

###  每个 Vue 组件的最外层容器采用`组件名+comp`的方式命名，如

```
<template>
    <div class="paging-table-comp">
        ...
    </div>
</template>
```

这样做是为了更快速定位一个组件，而不用先通过 vue-devtool 找到组件名，然后再去项目里找。

### css书写规则 <a id="&#x4E66;&#x5199;&#x89C4;&#x5219;"></a>

 每个组件的`<style>`标签都需要添加`scoped`属性：

```
<style scoped>
    ...
</style>
```

选择器之间禁止嵌套，便于代码阅读和后期维护，以及避免权重所带来的影响：

```text
<!-- 好的写法 -->
<style scoped>
    .news-list {}
    .news-item {}
    .news-txt {}
</style>

<!-- 不允许的写法 -->
<style scoped>
    .news-list {}
    .news-list .news-item {}
    .news-item .news-txt {}
</style>
```

css样式书写时按照定位、盒模型、样式、功能的顺序，比如：

```text
<style scoped>
    .news-list {
        /* 定位 */
        position: absolute;
        left: 0;
        z-index: 10;

        /* 盒模型 */
        float: left;
        display: block;
        flex: 1;
        align-items: center;
        width: 0;
        height: 0;
        padding: 0;
        margin: 0;
        border: 0;
        outline: 0;

        /* 样式 */
        background: #fff;
        color: #fff;
        font: italic bold 12px/20px arial,sans-serif;

        /* 功能 */
        transition: all 1s;
        transform: translate(10px, 10px);
        cursor: pointer;
    }
</style>
```

### 命名常用词汇 <a id="&#x547D;&#x540D;&#x5E38;&#x7528;&#x8BCD;&#x6C47;"></a>

#### 常用块（Block） <a id="&#x5E38;&#x7528;&#x5757;&#xFF08;block&#xFF09;"></a>

结构类：header, nav, subnav, menu, submenu, main, aside, footer

内容类：summary, banner, article, login, register, form, news

对于一个简单的组件，优先使用组件名作为 Block，不用把组件名全写出来，选其中一个典型单词就可以，比如：

```text
<div class="morning-news-comp">
    <div class=news-header>
        <p class="news-title">早间新闻</p>
        <a class="news-btn" href="#">更多</a>
    </div>
    <ul class="news-list">
        <li class="news-item">富强明主</li>
    </ul>
</div>
```

#### 常用元素（Element） <a id="&#x5E38;&#x7528;&#x5143;&#x7D20;&#xFF08;element&#xFF09;"></a>

结构类：header, main, content, footer

文本类：txt, link,

表单类：form, input, label

表格类：table, cloumn, row, cell

列表类：list, item, filed

按钮：button

#### 常用修饰符（Modifier） <a id="&#x5E38;&#x7528;&#x4FEE;&#x9970;&#x7B26;&#xFF08;modifier&#xFF09;"></a>

状态类：primary, success, warning, error, active

形状类：large, big, small+

样式类：fl, center, middle, fr

容器类：box, wrap

