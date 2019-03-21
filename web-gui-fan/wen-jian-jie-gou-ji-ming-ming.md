# 文件结构及命名

1. 每个文件夹包含 index.vue
2. 拆分 index 形成的 子文件，与 index 同一级（不放到components中）
3. 与业务无关/不可拆分/共用 的组件，放到 components 中
4. 拆分 index 形成的子文件比较复杂，可再次筛分，使用文件夹管理（不放到components中）

### 文件命名

为了统一，后端以及app，统一使用（\_）下划线作为拼接

```text
比如: 我们现在有一个help文件夹存放一些qa页面/咨询页面/关于我们页面
help/about_us.vue
help/service_center.vue
// 下面的例子为错误命名方式，不够简洁应当劲量干掉下划线，既然我们已经存在help文件夹则，写为：help/index.vue
help/help_center.vue ==> help/index.vue 或 help/center.vue

```

### 目录结构

