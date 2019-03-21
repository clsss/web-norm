# 移动端适配

**px**

固定的尺寸使用px

pc端使用px



**ex**

根据屏幕大小变化的尺寸，使用`ex`

原理：**postcss-ex-to-viewport** 插件会将 `ex` 单位计算成 `vw`

设计稿宽为 `750 px`

`1vw = 750 / 100 px = 7.5 px`

`1px = 1/7.5 vw`

有以下设计稿

![](https://xiaojing0.gitbooks.io/web-manual/content/assets/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E9%80%82%E9%85%8D%E6%A0%87%E6%B3%A8%E5%9B%BE1.jpg)

对应以下样式代码

```text
<style>
    /**
     * 需要适配不同屏幕的样式，使用 ex 单位
     */
    .item {
        padding-left: 54ex;
        padding-top: 61ex;
        width: 119ex;
        height: 119ex;
    }
</style>
```

**会被插件转为**

```text
<style>
    .item {
        padding-left: 7.2vw;
        padding-top: 8.13vw;
        width: 15.87vw;
        height: 15.87vw;
    }
</style>
```

