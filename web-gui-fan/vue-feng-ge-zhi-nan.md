---
description: >-
  这里是官方的 Vue 特有代码的风格指南。如果在工程中使用
  Vue，为了回避错误、小纠结和反模式，该指南是份不错的参考。不过我们也不确信风格指南的所有内容对于所有的团队或工程都是理想的。所以根据过去的经验、周围的技术栈、个人价值观做出有意义的偏差是可取的。https://cn.vuejs.org/v2/style-guide/
---

# vue 风格指南

### 排放顺序有 eslint 作为约束，做简单解释

html:

```bash
<template>
    <div>
        # Notice: 组件换行格式
        <custom-component
            position="top"
            :class="customClass"
            :list="list">
            <div class="avatar"></div>
        </custom-component>
        # 属性顺序
        <div
            # 指令放到最前面，if for show 放到最前面
            v-if=""
            v-for=""
            v-show=""
            v-model=""
            v-clickoutside
            #  属性放到中间，属性之间的顺序随意
            #  事件放到后面
            class=""
            id=""
            src=""
            plain
            :class=""
            :propValue=""
            @click="">
        </div>
        # 复杂的数据转化，提取到 methods 中，创建 getXXX 方法
        <div v-for="item in timeRange">{{getRangeTips(item)}}</div>
    </div>
</template>
```

js：

```bash
import Vue from 'vue'
import {mapGetters, mapState} from 'vuex'
// Notice: 引入的组件实例，使用大驼峰命名法
import CustomComponent from './custom_component.vue'
// Notice: 注意元素的位置顺序
export default {
    name:'', // Notice: 写组件的时候需要给一个名字
    directives: {},
    components: {
        CustomComponent
    },
    mixins: [],
    data() {
        return {
            timeRange: [], // Notice: 给data里面的变量留下说明文字
        }
    },
    props: {
        /**
         * Notice: 写下props数据的描述、用途
         * 学生的年龄，筛选的时候会用到
         */
        age: { // Notice: props 里面的定义，使用此结构，type、default
            type: Number,
            default: 0
        },
        thisObj: {
            type: Object,
            default: () => ({}) // Notice：返回默认对象，需要加括号（）
        }
    },
    computed: {
        /*
         Notice: 写下computed数据的描述
         */
        ...mapGetters({
            vxgStudentList: 'student/studentList' // Notice: mapGetters 里面的变量，加 vxg 前缀
        }),
        ...mapState({
            vxStudentCount: state => state.student.count // Notice: mapState, mapActions, mapMutations 里面的变量，加 vx 前缀
        }),
        address() {
            return ''
        }
    },
    filters: {},
    methods: {
        /*
         Notice: 复杂的方法，写下说明
         */
        sayHello() {
        },
        handleDataChange() {
            /*
            Notice:
                 使用 prop async 机制同步数据，不需要深拷贝
                 其他情况下本组件同步数据出去，注意使用深拷贝（同步的数据是对象、数组）
            */
            const deepCloneData = /* 深拷贝数据 */
            this.$emit('change', deepCloneData)
        },
        // 复杂的数据转化，提取到 methods 中，创建 getXXX 方法
        getRangeTips(item) {
            return item.helloWorld
        }
    },
    watch: {
        /*
         Notice: 写下说明
         */
        isLaughing() {
        }
    },
    beforeCreate() {},
    created() {},
    beforeMount() {},
    mounted() {},
    beforeUpdate() {},
    updated() {},
    activated() {},
    deactivated() {},
    beforeDestroy() {},
    destroyed() {},
    errorCaptured() {}
}
```

## Mixin 文件规范 <a id="vue-&#x6587;&#x4EF6;&#x76F8;&#x5173;&#x89C4;&#x8303;"></a>

**mixin 文件的变量、方法都使用 mx 前缀**

```bash
export default {
    data() {
        return {
            mxHello: ''
        }
    },
    computed() {
        mxGetStudentName() {
            return 'nate'
        }
    },
    methods: {
        mxPrintSchoolName() {
            console.log('nate-log')
        },
    }
}
```

**慎用 mixin**

mixin 很方便很好用，但是会降低代码易读性+

1. 基础组件可以考虑使用 mixin
2. 业务组件尽量不用 mixin，如果要使用，请抛出来大家一起具体情况具体分析

## 方法命名 <a id="vue-&#x6587;&#x4EF6;&#x76F8;&#x5173;&#x89C4;&#x8303;"></a>

**handleXXX**

> 事件处理方法

处理各种事件，`click` `mouseover` `change` `input` 等事件的处理方法，皆使用 `handleXXX`

example:

- handleProfileUpdate
- handleFilterChange
- handleMouseover
- handleAvatarMouseover
- handleNameClick

**处理数据的方法**

**requestXXX 拉取数据的方法**

> api 或 vuex/actions 层使用 fetchXXX
>
> vue 业务代码里面使用 requestXXX

**createXXX 创建数据的方法**

**updateXXX 更新数据的方法**

**removeXXX 删除数据的方法**

**formatXXX 格式化数据的方法**

**refXXX**

暴露方法给父组件调用
