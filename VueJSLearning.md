# VueJSLearning

## Vue 模版语法
        插值: `{{variable}}`, 置于文本中
        Html: `v-html`, 表明该元素中html内容
        属性: `v-bind`, 用于绑定元素的属性
        表达式: 完全的js表达式
        指令: `v-xxx`, 指令是带有v-前缀的特殊属性
        参数: `v-xxx:xxx`, 指令可以接受一个参数
        修饰符: `v-xxx.xxx`, 修饰符是以半角句号.指明的特殊后缀
        用户输入: `v-model`, 双向数据绑定; v-on, 事件绑定
        过滤器: `{{variable | filter1(arg1, arg2) | filter2 | ...}}`, 用于格式化文本, 前者作为过滤器的输入, 后者为过滤器名称
        缩写: `v-bind:xxx` => `:xxx`, `v-on:xxx` => `@xxx`

## Vue 条件语句
        `v-if`, `v-else`, `v-else-if`, `v-show`

```html
<!-- v-else-if 示例 -->
<div v-if="Math.random() > 0.5">Great</div>
<div v-else-if="Math.random() > 0.2">Good</div>
<div v-else>Bad</div>
<!-- v-show 示例 -->
<div v-show="isShow">Show</div>
```
### v-if vs v-show
        `v-if`是真正的条件渲染，当条件为假时，元素不会被渲染到DOM中；`v-show`只是简单的CSS切换，元素始终会被渲染到DOM中，只是通过CSS的display属性来控制元素的显示与隐藏。
        因此频繁切换使用`v-show`, 切换较少使用`v-if`。

## Vue 循环语句
        `v-for`, `v-for="(value, key, index) in object :key="value"`。其中key属性是为了提高性能，为每个元素提供唯一的key值。

```html
<!-- v-for 示例 -->
<ul>
    <li v-for="(item, index) in items" :key="index">{{item}}</li>
</ul>
<script>
    new Vue({
        el: '#app',
        data: {
            items: ['A', 'B', 'C']
        }
    });
</script>
```
### 过滤或排序后的结果展示
        一般情况下，展示的结果不需要变更原对象，此时可以用计算属性与filter来实现。
        同时使用reverse(), sort() 等方法时注意会改变原对象，请用`[...numbers].reverse()`代替`numbers.reverse()`避免改变原对象。
```html
<!-- 过滤或排序后的结果展示 示例 -->
<ul>
    <li v-for="n in evenNumbers">{{n}}</li>
</ul>
<script>
    new Vue({
        el: '#app',
        data: {
            numbers: [1, 2, 3, 4, 5]
        },
        computed: {
            evenNumbers: function() {
                return this.numbers.filter(function(number) {
                    return number % 2 === 0;
                });
            }
        }
    });
</script>
```

## Vue 计算属性
        `computed`可以用来描述一个值的计算逻辑，当依赖的值发生变化时，`computed`的值会重新计算。
        默认属性只有getter, 但也可以设置setter。

```html
<!-- computed 示例 -->
<div id="app">
    <p>{{message}}</p>
    <p>{{reversedMessage}}</p>
</div>
<script>
    new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue.js!'
        },
        computed: {
            reversedMessage: function() {
                return this.message.split('').reverse().join('');
            }
        }
    });
</script>
```
#### `computed` vs `methods`: 
        `computed`是基于它们的依赖进行缓存的, 只有在相关依赖发生改变时才会重新求值; `methods`是每次调用时都会重新计算；`computed`会在初始化时会先执行一次，`methods`不会。

## Vue 监听属性
        `watch`, 侦听属性的变化并执行相应的回调。

```html
<!-- watch 示例 -->
<div id="app">
    <p> 计数器: {{counter}}</p>
    <button @click="counter++">+1</button>
</div>
<script>
var vm = new Vue({
        el: '#app',
        data: {
            counter: 0
        }
});
vm.$watch('counter', function(newValue, oldValue) {
    console.log('counter: ' + newValue);
});
</script>
```
### 监听的数据源
        `watch`的第一个参数可以是不同数据源，可以是一个ref, 一个getter函数或多个数据源组成的数组。注意，不能直接监听一个对象的属性，必须用`(obj) => obj.prop`的getter函数来监听。
```javascript
// watch 示例
watch(
    [x, () => y.value],
    ([newX, newY], [oldX, oldY]) => {
        /* ... */
    }
)
```
### 侦听的选项
        deep:
        直接给`watch`传入一个响应式对象，可以实现深层侦听。
        但给`watch`传入响应对象的getter函数时，只有返回不同的对象时才会触发回调。此时若需要深层侦听，要在watch中添加`deep: true`选项。
        其它的选项有`immediate`(创建便执行), `once`(只执行一次), `flush:
### 停止侦听
        一般而言，侦听器会在组件销毁时自动停止。但是如果侦听器被异步创建，会导致侦听无法绑定到组件实例上，此时需要手动停止侦听。
        用`watch`的返回值可以手动停止侦听。如`const unwatch = watch(() => count, (count, prevCount) => { /* ... */ }); unwatch();`

## Vue 样式绑定
        `v-bind:class`, `v-bind:style`
        Vue在处理class和sytle时专门做了优化, 可以直接传入对象或数组。

```html
<!-- class 属性绑定示例 -->
    <!-- 动态切换-->
        <div v-bind:class="{ active: isActive }"></div>
    <!-- 绑定对象-->
        <div v-bind:class="classObject"></div> 
    <!-- 绑定数组-->
        <div v-bind:class="[activeClass, errorClass]"></div>
<!-- style 同理，不赘述-->
 ```
 ### 动态和静态
        在Vue中要注意动态和静态。data里的属性会在Vue实例创建时就初始化, 此时里面的属性是静态的, 但是对象表达式，方法表达式，计算属性，watch属性都是动态的。
```html
<script>
var app = new Vue({
    el: '#app',
    data: {
        fontSize: 30,
        objectStyle: {
            color: 'red',
            fontSize: this.fontSize + 'px'
        }
    },
    methods: {
        methodStyle: function() {
            return {
                color: 'blue',
                fontSize: this.fontSize + 'px'
            }
        }
    },
    computed: {
        computedStyle: function() {
            return {
                color: 'green',
                fontSize: this.fontSize + 'px'
            }
        }
    },
    watch: {
        fontSize: function(newValue, oldValue) {
            this.objectStyle.fontSize = newValue + 'px';
        }
    }
});
</script>
<!-- 静态例子 -->
<div v-bind:style = "objectStyle"> Static Style </div>
<!-- 动态例子, 动态对象 -->
<div v-bind:style = "{ color: activeColor, fontSize: fontSize + 'px' }"> Object Style </div>
<!-- 动态例子，methods-->
<div v-bind:style = "methodStyle()"> Method Style </div>
<!-- 动态例子，computed-->
<div v-bind:style = "computedStyle"> Computed Style </div>
<!-- 动态例子，watch-->
<div v-bind:style = "objectStyle"> Watch Style </div>
```
### 组件使用
        对于模版使用class时，会和根元素的class合并。当有多个根元素时，可以使用':class="$attrs.class"'来指定根元素接收外部传入的class。
### 样式多值
        可以对一个样式属性传入一个数组，浏览器仅会渲染浏览器支持的最后一个值，所以据此可以用来实现浏览器兼容。
    
## Vue 事件处理
        `v-on`, 用于绑定事件监听器
        事件修饰符: `.stop`(阻止冒泡), `.prevent`(阻止默认行为), `.capture`(事件捕获), `.self`(只有自己触发), `.once`(只触发一次), `.passive`(默认行为不会被阻止)。事件修饰符可以链式书写，如`.stop.prevent`。
        按键修饰符，监听键盘事件: `.enter`, `.tab`, `.delete`, `.esc`, `.space`, `.up`, `.down`, `.left`, `.right`。

## Vue 表单绑定
        `v-model`, 双向数据绑定, 并且会根据控件类型自动选取正确的方法更新元素
        修饰符: `.lazy`(在change时更新), `.number`(转换为数字), `.trim`(去除首尾空格) 
        `v-model`可以指定绑定的值和事件，用`v-model:prop="value"`可以指定绑定在prop上。
```html
<!-- v-model 示例 -->
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>
```

## Vue 自定义组件
        组件可以扩展HTML元素, 封装可重用的代码。组件系统可以用独立的组件构建大型应用。
        下列options里有的内容包括:template(表示组件中的带有的内容，即模版), data(表示组件的数据), methods(表示组件的方法), props(表示组件的属性), computed(表示组件的计算属性), watch(表示组件的监听属性)
        根元素: 组件模板中的最外层元素。
        注册全局组件: `Vue.component('component-name', {options})`
        注册局部组件: `components: { 'component-name': {options} }`(在Vue实例中)
        调用组件: `<component-name></component-name>`
### Prop
        父组件传递数据给子组件, 子组件通过props选项接收数据。通俗来讲，子组件就相当于定义一个子函数，props就相当于定义一个参数。当调用子组件时，通过定义的props名传递参数，从而让子组件获得父组件的数据。`props: ['propName']`
        如果想让一个对象绑定到一个组件的多个prop上，可以用`v-bind`来传递对象。`<blog-post v-bind="{ title: post.title, content: post.content }"></blog-post>`
        props遵循单项绑定原则，即父组件的变化会传递给子组件，但是子组件的变化不会传递给父组件。此外，prop是只读的，不应该在子组件中修改prop的值。
#### Prop验证
        Prop验证可以为props指定验证要求，如果传入的数据不符合要求，Vue会发出警告。
```javascript
// prop 验证
Vue.component('example', {
    props: {
        // 基础类型检查 (`null` 和 `undefined` 会通过任何类型验证)
        propA: Number,
        // 多种类型
        propB: [String, Number, null],
        // 必填字符串
        propC: {
            type: String,
            required: true
        },
        // 数字，有默认值
        propD: {
            type: Number,
            default: 100
        },
        // 数组/对象的默认值应当由一个工厂函数返回
        propE: {
            type: Object,
            default: function() {
                return { message: 'hello' }
            }
        },
        // 自定义验证函数
        propF: {
            validator: function(value) {
                return value > 10
            }
        }
    }
});
```
### 自定义事件
        子组件可以通过调用内建的$emit方法触发一个父组件上的事件，父组件可以通过v-on监听这个事件。
        `v-on:{eventName}="handler"`与`methosd: {handler: function() {...; this.$emit('eventName', data)}}}`配合使用。`v-on:{eventName}`相当于将函数传递给子组件，子组件通过`$emit`触发父组件的函数。
        其中，component中的data必须是一个函数，且要最好返回一个对象的独立实例，否则会导致多个组件共享一个实例。
```html
<!-- 自定义事件 样例 -->
<div id="app">
    <button-counter v-on:increment="incrementTotal"></button-counter>
    <button-counter v-on:increment="incrementTotal"></button-counter>
    <p>Total clicks: {{ total }}</p>
</div>
<script>
Vue.component('button-counter', {
    template: '<button v-on:click="incrementHandler">{{ counter }}</button>',
    data: function() {
        return {
            counter: 0
        }
    },
    methods: {
        incrementHandler: function() {
            this.counter += 1;
            this.$emit('increment');
        }
    }
});
new Vue({
    el: '#app',
    data: {
        total: 0
    },
    methods: {
        incrementTotal: function() {
            this.total += 1;
        }
    }
});
</script>
```
#### 事件验证
        事件验证可以为自定义事件指定验证要求，如果传入的数据不符合要求，Vue会发出警告。
```javascript
// 事件验证
export default {
    emits: {
        // 无参数
        'click': null,
        // 有参数
        'sumbit': ({email, password}) => {
            if (!email || !password) {
                console.warn('email and password are required');
                return false;
            }
            return true;
        }
    },
    methods: {
        submitForm() {
            this.$emit('submit', { email, password});
        }
    }
}
```
### `v-model`的实现原理
    `v-model`其实是语法糖，相当于`v-bind:value`和`v-on:input`的结合。在自定义组件中，`v-modle`默认利用`value`的prop和`input`的事件。可以通过`model`选项自定义组件的v-model。
```javascript
// 自定义组件的v-model
Vue.component('custom-input', {
    model: {
        prop:'checked',
        event:'change'
    },
    props: {
        checked: Boolean
    },
    template: `
        <input
            type="checkbox"
            v-bind:checked="checked"
            v-on:change="$emit('change', $event.target.checked)"
        >
    `
});
```
### 元素位置限制
        某些HTML元素对于父元素有特殊限制，如`<ul>`只能包含`<li>`，`<table>`只能包含`<tr>`等。此时可以用`is`属性来解决。
```html
<!-- 无效示例 -->
<table>
    <blog-post-row></blog-post-row>
</table>
<!-- 有效示例 -->
<table>
    <tr is="vue:blog-post-row"></tr>
</table>
```
### 插槽 Slots
        插槽是Vue的一项功能，用于分发内容。插槽可以用来分发内容到子组件中，也可以用来分发内容到父组件中。
        相当于是将父组件中的模版内容插入到子组件中的`<slot></slot>`标签中。
        插槽的内容可以是任意类型的，包括文本，HTML，甚至其他组件。
        默认内容: 当在子组件`<slot></slot>`中写入内容时，表示父组件没有提供内容的情况下显示的默认内容。
        具名插槽: 可以用`<slot name="xxx"></slot>`来定义具名插槽，用`<template v-slot:xxx></template>`来使用具名插槽。`v-slot`可以简写成`#`。没有提供具名插槽的内容会被分发到默认插槽，name为`default`。
```html
<!-- 插槽示例 -->
<div id="app">
    <alert-box>
        <template v-slot:title>
            <h1>Alert!</h1>
        </template>
        Only show when true.
    </alert-box>
</div>
<script>
Vue.component('alert-box', {
    template: `
        <div class="demo-alert-box">
            <strong>Error!</strong>
            <slot></slot>
        </div>
    `
});
new Vue({
    el: '#app'
});
</script>
```
#### 插槽的作用域
        插槽的作用域是父子相互隔离。如果要让父组件获取子组件的数据，可以如下操作:
            1. 父组件 `<x-component v-slot="slotProps"> {{ slotProps.data }} </x-component>``
            2. 子组件 `<slot :data="data"></slot>`
        如果同时使用了具名插槽和默认插槽，需要为默认插槽使用显示的`<template>`标签, 直接为组件添加`v-slot`会导致编译错误。
```html
<!-- 插槽作用域示例 -->
 <!-- xComponent template-->
  <div>
    <slot :message="hello"></slot>
    <slot name="footer" />
  </div>
 <!-- wrong usage -->
  <x-component v-slot="{ message }">
    <p>{{ message }}</p>
    <template #footer>
      <p>{{ message }}</p>
    </template>
  </x-component>
<!-- right usage -->
  <x-component>
    <template #default="{ message }">
      <p>{{ message }}</p>
    </template>
    <template #footer>
      <p>not use message</p>
    </template>
  </x-component>
```
### 依赖注入
        依赖注入是一种设计模式，用于向组件提供依赖。Vue提供了一个`provide`和`inject`选项，用于实现依赖注入。
        `provide`, 用于提供数据，可以是一个对象或一个函数，需要在`setup`函数中使用。`provide()`接受两个参数，第一个是注入名，第二个是数据。注入名为了避免命名冲突，推荐使用Symbol, 用变量代替字符串。
        `inject`, 用于接收数据，可以是一个数组或一个对象，需要在`setup`函数中使用。`inject()`接受一个必要参数，即注入名，还有两个可选参数，第一个是默认值，第二个是是否使用工厂函数。
        推荐做法: 尽可能将任何对响应式状态的变更保持在供给方组件内。如下操作。
```html
<!-- 供给方组件内容 -->
<script>
import { provide } from 'vue';
export default {
    setup() {
        const data = ref(0);
        function changeData(newData) {
            data.value = newData;
        }
        provide('data', { data, changeData });
    }
}
</script>
<!-- 接收方组件内容 -->
<script>
import { inject } from 'vue';
export default {
    setup() {
        const { data, changeData } = inject('data');
        return { data, changeData };
    }
}
</script>
<template>
    <div>
        <button @click="changeData(data + 1)">{{ data }}</button>
    </div>
</template>
```
### 异步组件
        异步组件是一种延迟加载组件的方式，可以提高应用的性能。Vue提供了一个`defineAsyncComponent`函数，用于定义异步组件。
        `defineAsyncComponent`接受一个函数作为参数，函数返回一个Promise，Promise的resolve值是一个组件选项对象。`defineAsyncComponent`可以和ES模块动态导入, 即`import()`结合使用。
```html
<!-- 异步组件全局注册 -->
<script>
const AsyncComponent = defineAsyncComponent(() => import('./AsyncComponent.vue'));
Vue.component('async-component', AsyncComponent);
</script>
<!-- 异步组件局部注册 -->
<script>
import { defineAsyncComponent } from 'vue';
export default {
    components: {
        'async-component': defineAsyncComponent(() => import('./AsyncComponent.vue'))
    }
}
</script>
```
## Vue 自定义指令
        Vue 允许注册自定义指令，全局或局部。
        自定义命令: 
            全局:`Vue.directive('directive-name', {options})`, 简写`Vue.directive('directive-name', function(el, binding) {...})`
            局部，在实例里:`directives: { 'directive-name': {options} }`
        钩子函数: 指令定义函数提供了几个钩子函数，用于在指令的生命周期中添加自定义逻辑。即在options里添加。
            `bind`: 只调用一次，指令第一次绑定到元素时调用
            `inserted`: 被绑定元素插入父节点时调用
            `update`: 被绑定元素所在的模板更新时调用
            `componentUpdated`: 被绑定元素所在的模板完成一次更新周期时调用
            `unbind`: 只调用一次，指令与元素解绑时调用
        钩子函数参数:
            `el`: 指令所绑定的元素，可以用来直接操作DOM
            `binding`: 一个对象，包含以下属性, 以`v-example:foo.a.b="1+1" 为例
                `name`: 指令名，不包括v-前缀, 例中为`example`
                `value`: 指令的绑定值, 例中为`2`
                `oldValue`: 指令绑定的前一个值, 仅在update和componentUpdated钩子中可用
                `expression`: 绑定值的字符串形式, 例中为`1+1`
                `arg`: 传给指令的参数, 例中为`foo`
                `modifiers`: 一个包含修饰符的对象, 例中为`{ a: true, b: true }`
            `vnode`: Vue编译生成的虚拟节点
            `oldVnode`: 上一个虚拟节点，仅在update和componentUpdated钩子中可用
```html
<!-- 自定义指令示例 -->
<div id="app">
    <p v-runoob="{ color: 'red', text: 'Hello!' }">Runoob</p>
</div>
<script>
Vue.directive('runoob', {
    bind: function(el, binding, vnode) {
        var s = JSON.stringify;
        el.style.color = binding.value.color;
        el.innerHTML = s(binding.value.text) + '<br>' + s(binding.expression) + '<br>' + s(binding.arg) + '<br>' + s(binding.modifiers);
    }
});
new Vue({
    el: '#app'
});
</script>
```

## Vue 路由
        Vue.js的官方路由库，用于构建单页面应用。一般来说，Vue路由的使用需要引入vue-router库。
        使用 
            0. 模块化编程时，要调用`Vue.use(VueRouter)`
            1. 创建路由组件, `const Foo = { template: '<div>foo</div>' }`
            2. 定义路由, `const routes = [ { path: '/foo', component: Foo } ]`
            3. 创建router实例, `const router = new VueRouter({ routes })`
            4. 挂载到Vue实例, `const app = new Vue({ router }).$mount('#app')`
            5. 使用router-view和router-link
        路由传参(<router-link>相关属性) 
            `to`: 跳转的链接
            `append`: 是否在当前路径后追加
            `tag`: 渲染为指定标签
            `active-class`: 链接激活时使用的CSS类名
            `event`: 触发导航的事件

## Vue 过度 & 动画
        Vue提供了过渡的封装组件，可以轻松的添加过渡效果。
        `transition`组件: 用于包裹要过渡的元素, name属性表示过度的类型，当没有过度类名时，name即为`v-enter`和`v-leave`的前缀。
        过渡类名: 
            `v-enter`: 进入过渡的开始状态，元素被插入时生效
            `v-enter-active`: 进入过渡的结束状态，元素被插入时生效
            `v-enter-to`: 进入过渡的结束状态，元素被插入时生效
            `v-leave`: 离开过渡的开始状态，元素被删除时生效
            `v-leave-active`: 离开过渡的结束状态，元素被删除时生效
            `v-leave-to`: 离开过渡的结束状态，元素被删除时生效
        过渡钩子函数: 
            `before-enter`: 元素被插入时生效
            `enter`: 元素插入完成时生效
            `after-enter`: 元素插入完成时生效
            `enter-cancelled`: 元素插入取消时生效
            `before-leave`: 元素被删除时生效
            `leave`: 元素删除完成时生效
            `after-leave`: 元素删除完成时生效
            `leave-cancelled`: 元素删除取消时生效
        常见的动画名:
            `fade`: 淡入淡出
            `slide`: 滑动
            `bounce`: 弹跳
            `scale`: 缩放
            `rotate`: 旋转

## Vue 混入(mixins)
        Vue 允许在创建组件时混入(mixins)一个或多个对象。混入对象可以包含任意组件选项。
        选择合并: 
            1. 同名函数将会被替换，且实例优先级较高
            2. 同名属性如果是对象，将会被合并；否则将会被替换，且实例优先级较高
            3. 混入对象的钩子将在组件自身钩子之前调用
            4. 混入对象的钩子将按照传入顺序依次调用,优先级从低到高
        全局混入: `Vue.mixin({options})`, 会影响到每个Vue实例，慎用。
```javascript
// 混入示例
var myMixin = {
    created: function() {
        this.hello();
    },
    methods: {
        hello: function() {
            console.log('hello from mixin!');
        }
    }
};
var Component = Vue.extend({
    mixins: [myMixin],
    created: function() {
        console.log('hello from component!');
    }
});
var component = new Component();
```

## Vue 响应接口
        响应式: Vue的响应式系统是基于依赖追踪的，当数据发生变化时，相关的依赖会重新计算，视图会更新。如果用直接赋值的方式修改数据，Vue无法追踪到数据的变化，这样的数据是非响应式的。
        全局Vue: 可以在运行过程中动态添加新的响应式属性，但是只有在初始化时就存在的属性才是响应式的。
        Vue.set: 用于向响应式对象添加属性，确保属性是响应式的。
        Vue.delete: 用于删除对象的属性，确保删除的属性是响应式的。

## Vue3 
        Vue3 与 Vue2 区别，个人认为在于选项式和组合式的区别。Vue3 采用了组合式的API，将原本的选项式API拆分成了多个API，使得代码更加清晰，更加容易维护。同时，Vue3 也提供了更多的功能，比如更好的TypeScript支持，更好的性能，更好的Tree-shaking等等。
### setup组件 
            `setup`是组合式API的入口。`setup`函数在组件创建`createed`之前执行。函数接收两个参数，第一个参数是props，它是响应式的；第二个参数是context，它包含了attrs, slots, emit等属性。
            `setup`中应该避免使用`this`，因为`setup`发生在this被初始化前，找不到组件实例。
            在SFC中，甚至可以用`<script setup>`来初始化组件，不用return。当使用`<script setup>`时，components, props, data, computed, methods, watch等属性都可以直接使用，不用再return。比如`import MyComponent from './MyComponent.vue';`时可以直接使用组件MyComponent,`<my-component></my-component>`。
### ref和reactive函数 
            `ref`函数是Vue3的新特性，它可以接受任何类型的数据，返回一个响应式变量。Vue3中ref可以使任何响应变量在任何地方起作用。
            `reactive`函数和`ref`类似，但是它只能接受对象，创建一个响应式对象。
            `ref`和`reactive`在默认情况下都会解包(不用添加.value访问)，但是当ref作为响应数组或对象的属性时，需要添加.value访问，比如`const books = reactive([ref('I am a book')]);`, 需要`books[0].value`来访问。

            无论是`ref`还是`reactive`，它们创建后返回的是一个深拷贝的响应变量，与原变量无关，不会影响原变量，也不会等于原变量。

### export default 
            Vue3中的组件导出方式，可以直接导出一个对象，而不需要再使用Vue.component。
```javascript
// Vue2 常见
vm = new Vue({
    el: '#app',
    data: {
        count: 0
    },
    methods: {
        increment() {
            this.count++;
        }
    }
});
// 选项式
const vm = Vue.createApp({
    data() {
        return {
            count: 0
        }
    },
    methods: {
        increment() {
            this.count++;
        }
    }
}).mount('#app');
// 组合式
import { ref } from 'vue';
const vm = Vue.createApp({
    setup() {
        const count = ref(0);
        const increment = () => {
            count.value++;
        }
        return {
            count,
            increment
        }
    }
}).mount('#app');
```

### Vue3 组件定义
        Vue3中的组件定义方式有两种，一种是选项式API，一种是组合式API。选项式API一般采用在对象中定义data, methods, computed, watch等属性的方式，组合式API一般采用在setup函数中定义用const定义变量的方式。
```javascript
// 组合式API
import { ref } from 'vue';
const Component = {
    setup() {
        const count = ref(0);
        const increment = () => {
            count.value++;
        }
        return {
            count,
            increment
        }
    }
};
```
### Props
        组合式的单文件Vue里Props的定义方式也有所改变，需要用`defineProps`来定义Props。
        使用参考:`const props = defineProps(['prop1', 'prop2']);`。
        同样的，`$emit`也需要用`defineEmits`来定义。使用参考:`const emit = defineEmits(['event1', 'event2']); emit('event1', data);`。
### 组件注册
        Vue3中的组件注册方式也有所改变，全局注册无大改变，局部注册中如果是使用了`<script setup>`单文件组件时，导入的组件可以直接使用，不用再注册。如果是用了`export default`导出组件时，需要相应的局部注册。
### 组件名格式
        在Vue单文件中，尽量使用`PascalCase`格式来命名组件，这样可以避免与HTML元素冲突。
        在DOM模板中，使用`kebab-case`格式来命名组件，因为HTML不区分大小写。
        Vue支持将`kebab-case`格式的组件名转换为`PascalCase`格式，所以`MyComponent`为名注册的组件可以在模版中用`<my-component>`和`<MyComponent>`两种方式来引用。

### Vue3 生命周期
        生命周期: 生命周期指的是Vue实例从创建到销毁的过程。可以用如下表示Vue3的生命周期。
```
开始
  |
  v
渲染器遇到组件
  |
  +-------------> setup (组合式 API)
  |
  +-------------> beforeCreate
  |
  v
初始化选项式 API
  |
  v
created
  |
  v
是否存在预编译模板--------> 
  |                       |
  |                       v
  |                       即时编译模板
  |                       |
  v                       v
 YES                     NO
  |                       |
  v -----------------------                 
beforeMount               
  |                       
  v                       
初始渲染: 创建和插入 DOM 节点
  |
  v
mounted
  |
  v
挂载
  |
  +-------------> 当数据变化时
  |    ^                   | 
  |    |                   v
  |    |             重新渲染并打补丁
  |    |                   |
  |    |                   v
  |    ---------updated-----
  |
  v
当组件被取消挂载时
  |
  |
  + --------------->beforeUnmount
  |
  v
取消挂载--------------->unmounted
```
        生命周期钩子: 当进入生命周期的某个阶段时，自动触发的函数称为生命周期钩子函数。Vue3中的生命周期钩子与Vue2中的生命周期钩子基本一致，只是名称有所改变。`beforeCreate` => `onBeforeCreate`, `created` => `onCreated`, `beforeMount` => `onBeforeMount`, `mounted` => `onMounted`, `beforeUpdate` => `onBeforeUpdate`, `updated` => `onUpdated`, `beforeDestroy` => `onBeforeUnmount`, `destroyed` => `onUnmounted`, `errorCaptured` => `onErrorCaptured`, `renderTracked` => `onRenderTracked`, `renderTriggered` => `onRenderTriggered`;

### Vue3 模版引用
        Vue3中的模版引用是通过`ref`来实现的。`ref`可以用来获取模版中的DOM元素，也可以用来获取组件实例。
```html
<!-- 模版引用示例 -->
<div id="app">
    <button ref="button">Click me</button>
</div>
<script setup>
import { ref, onMounted } from 'vue';
const button = ref(null);
onMounted(() => {
    button.value.addEventListener('click', () => {
        console.log('clicked');
    });
});
</script>
```
        如果在`v-for`中使用`ref`，可以用`ref`的数组来获取多个元素。`ref`的数组可以用`ref`的`value`属性来访问。

### Vue3与Vue2其他不同:
        全局自定义组件: `app.component('component-name', {options})`;
        局部自定义组件: `const Component = {options}; app.component('component-name', Component)`;
        侦听属性: Vue3中的侦听属性可以替代生命周期钩子，包括`watch`和`watchEffect`。`watch`用于侦听特定的数据变化，`watchEffect`用于侦听任何数据变化。相比于Vue2中的`watch`，Vue3中的`watch`可以侦听多个数据，而且可以侦听嵌套数据。

### Vue3 单文件组件(SFC)
        Vue3的单文件组件(*.vue)可以将模板、样式、脚本都封装在一个文件中，使得代码更加清晰，更加容易维护。
        Vue3的项目进入入口一般为`main.js`，在`main.js`中引入`App.vue`，并且在`main.js`中创建Vue实例。`import ComponentName from './ComponentName.vue';`可以引入`ComponentName.vue`。
#### 组件作用域
        scoped属性: 用于限制样式的作用域，只在当前组件中生效。`<style scoped>...</style>`。全局样式可以和scoped样式共存，即一个组件可以同时包含作用域样式和非作用域样式。
        :deep伪类: 用于穿透scoped组件作用域，使得样式可以作用于子组件。`.a :deep(.b)` 表示样式`.b`可以作用于`.a`的子组件。一般用于穿透第三方库，与`!important`一起使用。
        :slotted伪类: 用于穿透组件的插槽，使得样式可以作用于插槽中的内容。`::slotted(.b)` 表示样式`.b`可以作用于插槽中的内容。
        :global伪类: 用于取消scoped组件作用域，使得样式可以作用于全局。`:global(.b)` 表示样式`.b`可以作用于全局。

### Vue3 常用内置属性
        is : 用于动态组件的切换，可以根据不同的条件加载不同的组件。与`component`标签配合使用。`<component :is="componentName"></component>`; 在js中，用`this.componentName = 'ComponentName';`来切换组件。
        key : 用于优化Vue的性能，当Vue中的组件需要频繁切换时，可以使用`key`来保证组件的唯一性。一般用于for循环中，保证每个组件的唯一性。`<component v-for="item in items" :key="item.key"></component>`;
        ref : 用于获取DOM元素的实例，可以通过`ref`来获取DOM元素的实例，然后调用组件的方法。`<component ref="refName"></component>`; 在js中，用`this.$refs.refName`来获取DOM元素的实例。

### Vue3 逻辑复用
#### 组合式函数
        组合式函数是Vue3中的一个新特性，用于逻辑复用。组合式函数是一个函数，它接收一个参数，返回一个对象。组合式函数可以用于逻辑复用，将逻辑抽离出来，使得代码更加清晰，更加容易维护。
##### 约定和实践
        命名: camelCase, 以use开头
        参数: 尽量对输入参数进行ref或getter处理而非原始值，一般可以用`toValue`函数来处理。如果输入参数为ref或getter情况下创建了响应式effect, 确保使用`watch`进行监视或者`toValue`来获取值。
        返回值: 尽量用多个ref()作为返回值，这样可以更好的控制返回值的响应性。如果想用对象形式获取组合式函数的返回状态，可以使用`reactive()`包装组合式函数。
        使用限制: 组合式函数不能用于模板中，只能用于setup函数中。
#### 插件
        插件是Vue3中的一个新特性，用于逻辑复用。插件是一个函数，它接收一个参数，返回一个对象。插件可以用于逻辑复用，将逻辑抽离出来，使得代码更加清晰，更加容易维护。
        插件一般使用`app.use`来注册，注册后可以在全局使用。一个插件可以拥有`install`方法，用于注册全局组件、指令、过滤器等。
```javascript
// 插件示例
const MyPlugin = {
    install(app) {
        app.component('MyComponent', MyComponent);
        app.directive('my-directive', MyDirective);
        app.config.globalProperties.$myProperty = 'myProperty';
    }
};
app.use(MyPlugin);
```

## 风格指南
        待更新，https://cn.vuejs.org/style-guide/rules-essential.html#avoid-v-if-with-v-for
