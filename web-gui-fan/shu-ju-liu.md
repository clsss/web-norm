# 数据流

> 拉取数据
>
> 缓存数据
>
> 格式化数据

```text
export default {
    name: 'process-leave'
    /**
     * 没有其他组件依赖的数据（比如 从服务器拉取的数据）
     * 存放到 data 当中，生命周期与本 Vue 组件相当
     */
    data() {
        // 请假数据
        formData: {
            eduClassId: '',
            recordId: '',
            makeUp: {
                date: '',
                time: ''
            }
        }
        /* 临时数据 ****************************/
        // 班级列表
        eduClassList: [],
        // 排课列表
        schedulingList: []

        /* 处理数据缓存 *************************/
        /* 根据实际场景，判断是否需要缓存数据 *************************/
        // 存储班级的排课信息
        // 班级ID为key的对象
        schedulingInfo: {}
    },
    computed: {
        // 班级选择器的数据源
        classOptions() {
            return this.eduClassList.map(item => {
                return {
                    label: item.name,
                    value: item.eduClassId
                }
            })
        },
        // 排课选择器的数据源
        schedulingOptions() {
            /**
             * 非缓存数据情况
             */
            return this.schedulingList.map(item => {
                return {
                    label: item.courseNo,
                    value: item.recordId
                }
            })

            /**
             * 缓存数据的情况
             */
            const cachedList = this.schedulingInfo[this.formData.eduClassId]
            return cachedList.map(item => {
                return {
                    label: item.courseNo,
                    value: item.recordId
                }
            })
        }
    },
    methods: {
        fetchClassList() {
            // 从服务器拉取数据
            this.eduClassList = ...
        },
        fetchSchedulingList() {
            // 从服务器拉取数据
            /**
             * 不需要缓存的场景
             */
            this.schedulingList = ...

            /**
             * 缓存的场景
             */
            const schedulingList = ...
            this.schedulingInfo[this.formData.eduClassId] = schedulngList
        }
    }
}
```

#### 

## 子组件的数据共享 <a id="&#x5B50;&#x7EC4;&#x4EF6;&#x7684;&#x6570;&#x636E;&#x5171;&#x4EAB;"></a>

**子组件之间数据单向传递**

> 单向的数据流 child1 -&gt; child2
>
> 由父组件调度

* 子组件1维护数据 filters
* 子组件2拉取数据列表（需要filters）

```text
// 我是父组件
<template>
    <child-1 @update:filters="val => filtersByChild1 = val"></child-1>
    <child-2 :filters="filtersByChild1"></child-2>
</template>

export default {
    data() {
        return {
            filtersByChild1: ''
        }
    }
}
```

#### 子组件之间数据双向流动 <a id="&#x5B50;&#x7EC4;&#x4EF6;&#x4E4B;&#x95F4;&#x6570;&#x636E;&#x53CC;&#x5411;&#x6D41;&#x52A8;"></a>

> 双向数据流 child1 -&gt; child2; child2 -&gt; child1
>
> 数据放到vuex

* 子组件1修改list
* 子组件2也会修改list

```text
vuex

index.js
export default {
    state: {
        /**
         * 请注意说明使用场景
         * 说明使用此数据的组件
         */
        scheduleList: []
    }
}

mutations.js
export default {
    // 修改scheduleList
    modifyScheduleList() {
    }
}
```

## 统一数据格式 <a id="&#x7EDF;&#x4E00;&#x6570;&#x636E;&#x683C;&#x5F0F;"></a>

> 从服务器拉取的数据，需要格式化，考虑在 vuex 的 getters 中处理，便于代码复用

```text
getters.js
export default {
    // origin data 由子组件维护的情况
    getFormatData: (context) => (originData) => {

    },
    // origin data 由 vuex 维护的情况
    getFormatData(context) {

    }
}
```

## 减少数据流 <a id="&#x51CF;&#x5C11;&#x6570;&#x636E;&#x6D41;"></a>

> 法则：自己的数据，自己处理

#### 场景 <a id="&#x573A;&#x666F;"></a>

组件：兄弟A、兄弟B

兄弟A接受用户点击事件，然后兄弟B需要导出数据到Excel（或者保存到服务器）

解决方案：

兄弟A使用 `eventBus` 发布事件

兄弟B接收到事件后，自己把数据导出Excel，导出结果使用 `eventBus` 通知相关方

结论：自己处理自己的数据，减少数据流，降低复杂度

提醒：具体情况具体分析，如有疑难，提出讨论



