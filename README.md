突击小分队前端团队开发10大规范
1语言，框架
所有项目一律统一使用ts进行开发，vue使用3.0版本，ui框架使用iview
2项目命名
全部采用小写方式， 以下划线分隔。 例：my_project_name
3文件命名
3.1 views(pages)页面命名
使用连接符(kebab-case)user-info.vue
如果views下的文件件只有一个文件,命名使用index.vue
3.2 HTML文件命名
使用下划线
3.3 CSS, SCSS文件命名
css使用下划线
4id和class和变量的命名原则
id：采用“小驼峰命名法”
class使用连接符(kebab-case)分割
复数类型要以s结尾例如数组类型的列表lists
应反映该元素的功能或使用通用名称，而不要用抽象的晦涩的命名，原则：见名知其义
5id和class命名越精简越好，只要足够表达意思，这样有助于理解，同时也能提高代码效率，严禁使用中文拼音命名
.navigation{} /* 不推荐 */
.login_box_inside_con{} /* 不推荐 */
.nav{} /* 推荐 */
6变量和函数名定义规则全部采用“小驼峰命名法”
例：myStudentCount：变量myStudentCount第一个单词是全部小写，后面的单词首字母大写。
7组件建立规则 components
组件一定是建立在这个文件夹下
系统组件会建立在src下的components，页面组件在目录下建立components文件夹，在components下建立自己的写好的组件

组件名称定义2种规则

--components
----login-form
------index.js
------login-form.vue
或者

--components
----login-form
------index.vue
一般系统组件采用前者，页面小组件采用后者，vue默认可以识别index
8vue使用规范
组件数据
组件的 data 必须是一个函数。

// bad
export default {
  data: {
    foo: 'bar',
  },
};

// good
export default {
  data() {
    return {
      foo: 'bar',
    };
  },
};

单文件组件文件名称
单文件组件的文件名应该要么始终是单词大写开头 (PascalCase)，要么始终是横线连接 (kebab-case)。

// bad
mycomponent.vue
myComponent.vue

// good
my-component.vue
MyComponent.vue

紧密耦合的组件名
和父组件紧密耦合的子组件应该以父组件名作为前缀命名。

// bad
components/
|- TodoList.vue
|- TodoItem.vue
└─ TodoButton.vue

// good
components/
|- TodoList.vue
|- TodoListItem.vue
└─ TodoListItemButton.vue

自闭合组件
在单文件组件中没有内容的组件应该是自闭合的。

<!-- bad -->
<my-component></my-component>

<!-- good -->
<my-component />

Prop 名大小写
在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板中应该始终使用 kebab-case。

// bad
export default {
  props: {
    'greeting-text': String,
  },
};

// good
export default {
  props: {
    greetingText: String,
  },
};

<!-- bad -->
<welcome-message greetingText="hi" />

<!-- good -->
<welcome-message greeting-text="hi" />

指令缩写
指令缩写，用:表示v-bind:，用@表示v-on:

<!-- bad -->
<input v-bind:value="value" v-on:input="onInput" />

<!-- good -->
<input :value="value" @input="onInput" />

Props 顺序
标签的 Props 应该有统一的顺序，依次为指令、属性和事件。

<my-component
  v-if="if"
  v-show="show"
  v-model="value"
  ref="ref"
  :key="key"
  :text="text"
  @input="onInput"
  @change="onChange"
/>

组件选项的顺序
组件选项应该有统一的顺序。

export default {
  name: '',

  mixins: [],

  components: {},

  props: {},

  data() {},

  computed: {},

  watch: {},

  created() {},

  mounted() {},

  destroyed() {},

  methods: {},
};

组件选项中的空行
组件选项较多时，建议在属性之间添加空行。

export default {
  computed: {
    formattedValue() {
      // ...
    },

    styles() {
      // ...
    },
  },

  methods: {
    onInput() {
      // ...
    },

    onChange() {
      // ...
    },
  },
};

单文件组件顶级标签的顺序
单文件组件应该总是让顶级标签的顺序保持一致，且标签之间留有空行。

<template>
  ...
</template>

<script>
  /* ... */
</script>

<style>
  /* ... */
</style>
9接口嵌套使用说明
####接口不允许使用接口套用接口

错误示范
updateSysFun(data).then(ret => {
    isSync(ret.data.id).then(rets => {
             if(rets.data.errcode === 0) {
                    console.log('success')
            }
      })
    })

可以修改如下(接口需要开启await=true)，函数名称前面需要加上async，具体使用参考：接口的定义和调用
let ret = await updateSysFun(data)
let rets = await isSync(ret.data.id)
if(rets.data.errcode === 0) {
    console.log('success')
}

以函数的形式调用

methods: {
    getUserInfo( id ) {
        isSync(id).then(ret=>{
            if(ret.data.errcode === 0) {            
                    console.log('success')
                }
        })
    },
    userData(){
        updateSysFun(data).then(ret=>{
                this.getUserInfo(ret.data.id)
        })
    }
}
10组件选项的顺序
组件选项应该有统一的顺序。

export default {
  name: '',

  mixins: [],

  components: {},

  props: {},

  data () {},

  computed: {},

  watch: {},

  created () {},

  mounted () {},

  destroyed () {},

  methods: {}
}
