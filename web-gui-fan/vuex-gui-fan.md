# vuex规范

**index.js**

```text
// Notice 为定义的数据注释说明
const state = {
    /**
     * 主页标题
     */
    name: ''
}
```



**action.js**

```text
import api from 'api.js'
// Notice 为定义的方法注释说明
// 传递给 api 的参数，封装成对象 params
// 调用action 方法的vue文件，需跳转到API文件查看此方法所需参数
export default {
    // 开始监听后端数据更新
    startSync({commit, params}) {
        return api.doSomething(params)
    },
}
```

**api.js**

```text
import httpRequestor from 'httpRequestor'
// Notice 为定义的方法注释说明
// 传递给后台的 body 数据，封装成对象 params
// 同时有传递给后台的 query 数据，封装成 query
export default {
    // Notice 需要对方法有完整的注释
    /**
     * 方法描述说明
     * @param params {Object}
     * {
     *  schoolName: String? 当前学生所在学校名字
     *  schoolId: String 学校的Id
     * }
     */
    doSomething(params) {
    },

    /**
     * 方法描述说明
     * @param query {Object}
     * {
     *  name: String？ 学生名字
     *  student_id: String 学生id
     * }
     * @param params {Object}
     * {
     *  schoolName: String? 当前学生所在学校名字
     *  schoolId: String 学校的Id
     * }
     */
    doAnotherThing(query, params) {
    }
}
```

