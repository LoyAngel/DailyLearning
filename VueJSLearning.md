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
    <li
        v-for="(item, index) in items"
        :key="index"
    >
        {{item}}
    </li>
</ul>
<script>
    new Vue({
        el: "#app",
        data: {
            items: ["A", "B", "C"],
        },
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
        el: "#app",
        data: {
            numbers: [1, 2, 3, 4, 5],
        },
        computed: {
            evenNumbers: function () {
                return this.numbers.filter(function (number) {
                    return number % 2 === 0;
                });
            },
        },
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
        el: "#app",
        data: {
            message: "Hello Vue.js!",
        },
        computed: {
            reversedMessage: function () {
                return this.message.split("").reverse().join("");
            },
        },
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
    <p>计数器: {{counter}}</p>
    <button @click="counter++">+1</button>
</div>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            counter: 0,
        },
    });
    vm.$watch("counter", function (newValue, oldValue) {
        console.log("counter: " + newValue);
    });
</script>
```

### 监听的数据源

        `watch`的第一个参数可以是不同数据源，可以是一个ref, 一个getter函数或多个数据源组成的数组。注意，不能直接监听一个对象的属性，必须用`(obj) => obj.prop`的getter函数来监听。

```javascript
// watch 示例
watch([x, () => y.value], ([newX, newY], [oldX, oldY]) => {
    /* ... */
});
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
        el: "#app",
        data: {
            fontSize: 30,
            objectStyle: {
                color: "red",
                fontSize: this.fontSize + "px",
            },
        },
        methods: {
            methodStyle: function () {
                return {
                    color: "blue",
                    fontSize: this.fontSize + "px",
                };
            },
        },
        computed: {
            computedStyle: function () {
                return {
                    color: "green",
                    fontSize: this.fontSize + "px",
                };
            },
        },
        watch: {
            fontSize: function (newValue, oldValue) {
                this.objectStyle.fontSize = newValue + "px";
            },
        },
    });
</script>
<template>
    <!-- 静态例子 -->
    <div v-bind:style="objectStyle">Static Style</div>
    <!-- 动态例子, 动态对象 -->
    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">
        Object Style
    </div>
    <!-- 动态例子，methods-->
    <div v-bind:style="methodStyle()">Method Style</div>
    <!-- 动态例子，computed-->
    <div v-bind:style="computedStyle">Computed Style</div>
    <!-- 动态例子，watch-->
    <div v-bind:style="objectStyle">Watch Style</div>
</template>
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
<input
    v-model="message"
    placeholder="edit me"
/>
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

#### Prop 验证

        Prop验证可以为props指定验证要求，如果传入的数据不符合要求，Vue会发出警告。

```javascript
// prop 验证
Vue.component("example", {
    props: {
        // 基础类型检查 (`null` 和 `undefined` 会通过任何类型验证)
        propA: Number,
        // 多种类型
        propB: [String, Number, null],
        // 必填字符串
        propC: {
            type: String,
            required: true,
        },
        // 数字，有默认值
        propD: {
            type: Number,
            default: 100,
        },
        // 数组/对象的默认值应当由一个工厂函数返回
        propE: {
            type: Object,
            default: function () {
                return { message: "hello" };
            },
        },
        // 自定义验证函数
        propF: {
            validator: function (value) {
                return value > 10;
            },
        },
    },
});
```

### 自定义事件

        子组件可以通过调用内建的$emit方法触发一个父组件上的事件，父组件可以通过v-on监听这个事件。
        `v-on:{eventName}="handler"`与`methods: {handler: function() {...; this.$emit('eventName', data)}}`配合使用。其中，`eventName`是子组件自定义的事件名，`handler`是父组件的函数，在子组件的`methods`中调用`this.$emit('eventName', data)`触发父组件传递来的函数。
        其中，component中的data必须是一个函数，且要最好返回一个对象的独立实例，否则会导致多个组件共享一个实例。

```html
<!-- 自定义事件 样例 -->
<!-- 父组件 -->
<template>
    <div>
        <button-counter @increment="incrementTotal"></button-counter>
        <p>Total clicks: {{ total }}</p>
    </div>
</template>
<script>
    import ButtonCounter from "./ButtonCounter.vue";
    export default {
        components: {
            ButtonCounter,
        },
        data() {
            return {
                total: 0,
            };
        },
        methods: {
            incrementTotal() {
                this.total++;
            },
        },
    };
</script>
<!-- 子组件 ButtonCounter.vue -->
<template>
    <button @click="increment">{{ count }}</button>
</template>
<script>
    export default {
        data() {
            return {
                count: 0,
            };
        },
        emits: ["increment"],
        methods: {
            increment() {
                this.count++;
                this.$emit("increment");
            },
        },
    };
</script>
```

#### 事件验证

        事件验证可以为自定义事件指定验证要求，如果传入的数据不符合要求，Vue会发出警告。

```javascript
// 事件验证
export default {
    emits: {
        // 无参数
        click: null,
        // 有参数
        sumbit: ({ email, password }) => {
            if (!email || !password) {
                console.warn("email and password are required");
                return false;
            }
            return true;
        },
    },
    methods: {
        submitForm() {
            this.$emit("submit", { email, password });
        },
    },
};
```

### `v-model`的实现原理

    `v-model`其实是语法糖，相当于`v-bind:value`和`v-on:input`的结合。在自定义组件中，`v-modle`默认利用`value`的prop和`input`的事件。可以通过`model`选项自定义组件的v-model。

```javascript
// 自定义组件的v-model的等效实现
Vue.component("custom-input", {
    model: {
        prop: "checked",
        event: "change",
    },
    props: {
        checked: Boolean,
    },
    template: `
        <input
            type="checkbox"
            v-bind:checked="checked"
            v-on:change="$emit('change', $event.target.checked)"
        >
    `,
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
        <h3>Something went wrong!</h3>
        <template #footer>
            <button @click="show = false">Close</button>
        </template>
    </alert-box>
</div>
<script>
    Vue.component("alert-box", {
        template: `
        <div class="demo-alert-box">
            <strong>Error!</strong>
            <slot></slot>
            <slot name="footer"></slot>
        </div>
    `,
    });
    new Vue({
        el: "#app",
    });
</script>
```

#### 插槽的作用域

        插槽的作用域是父子相互隔离。如果要让父组件获取子组件的数据，可以使用`scope`来获取子组件的数据。
        用法：
        子组件，`<slot :data="data"></slot>`传递数据给插槽；
        父组件，`<template v-slot:slotName="slotProps"></template>`获取插槽数据，可以简写为`<template #slotName="slotProps"></template>`。

```html
<!-- 子组件 -->
<template>
    <div>
        <slot :student="stus"></slot>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                stus: ["A Student", "B Student", "C Student"],
            };
        },
    };
</script>
<!-- 父组件 -->
<template>
    <div>
        <student-list>
            <template #="stus">
                <ul>
                    <li v-for="stu in stus.student">{{ stu }}</li>
                </ul>
            </template>
        </student-list>
    </div>
</template>
```

### 依赖注入

        依赖注入是一种设计模式，用于向组件提供依赖。Vue提供了一个`provide`和`inject`选项，用于实现依赖注入。
        `provide`, 用于提供数据，可以是一个对象或一个函数，需要在`setup`函数中使用。`provide()`接受两个参数，第一个是注入名，第二个是数据。注入名为了避免命名冲突，推荐使用Symbol, 用变量代替字符串。
        `inject`, 用于接收数据，可以是一个数组或一个对象，需要在`setup`函数中使用。`inject()`接受一个必要参数，即注入名，还有两个可选参数，第一个是默认值，第二个是是否使用工厂函数。
        推荐做法: 尽可能将任何对响应式状态的变更保持在供给方组件内。如下操作。

```html
<!-- 供给方组件内容 -->
<script>
    import { provide } from "vue";
    export default {
        setup() {
            const data = ref(0);
            function changeData(newData) {
                data.value = newData;
            }
            provide("data", { data, changeData });
        },
    };
</script>
<!-- 接收方组件内容 -->
<script>
    import { inject } from "vue";
    export default {
        setup() {
            const { data, changeData } = inject("data");
            return { data, changeData };
        },
    };
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
    const AsyncComponent = defineAsyncComponent(() =>
        import("./AsyncComponent.vue")
    );
    Vue.component("async-component", AsyncComponent);
</script>
<!-- 异步组件局部注册 -->
<script>
    import { defineAsyncComponent } from "vue";
    export default {
        components: {
            "async-component": defineAsyncComponent(() =>
                import("./AsyncComponent.vue")
            ),
        },
    };
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
    Vue.directive("runoob", {
        bind: function (el, binding, vnode) {
            var s = JSON.stringify;
            el.style.color = binding.value.color;
            el.innerHTML =
                s(binding.value.text) +
                "<br>" +
                s(binding.expression) +
                "<br>" +
                s(binding.arg) +
                "<br>" +
                s(binding.modifiers);
        },
    });
    new Vue({
        el: "#app",
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
    created: function () {
        this.hello();
    },
    methods: {
        hello: function () {
            console.log("hello from mixin!");
        },
    },
};
var Component = Vue.extend({
    mixins: [myMixin],
    created: function () {
        console.log("hello from component!");
    },
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

### setup 组件

            `setup`是组合式API的入口。`setup`函数在组件创建`createed`之前执行。函数接收两个参数，第一个参数是props，它是响应式的；第二个参数是context，它包含了attrs, slots, emit等属性。
            `setup`中应该避免使用`this`，因为`setup`发生在this被初始化前，找不到组件实例。
            在SFC中，甚至可以用`<script setup>`来初始化组件，不用return。当使用`<script setup>`时，components, props, data, computed, methods, watch等属性都可以直接使用，不用再return。比如`import MyComponent from './MyComponent.vue';`时可以直接使用组件MyComponent,`<my-component></my-component>`。

### ref 和 reactive 函数

            `ref`函数是Vue3的新特性，它可以接受任何类型的数据，返回一个响应式变量。Vue3中ref可以使任何响应变量在任何地方起作用。
            `reactive`函数和`ref`类似，但是它只能接受对象，创建一个响应式对象。
            `ref`和`reactive`在默认情况下都会解包(不用添加.value访问)，但是当ref作为响应数组或对象的属性时，需要添加.value访问，比如`const books = reactive([ref('I am a book')]);`, 需要`books[0].value`来访问。

            无论是`ref`还是`reactive`，它们创建后返回的是一个深拷贝的响应变量，与原变量无关，不会影响原变量，也不会等于原变量。

### export default

            Vue3中的组件导出方式，可以直接导出一个对象，而不需要再使用Vue.component。

```javascript
// Vue2 常见
vm = new Vue({
    el: "#app",
    data: {
        count: 0,
    },
    methods: {
        increment() {
            this.count++;
        },
    },
});
// 选项式
const vm = Vue.createApp({
    data() {
        return {
            count: 0,
        };
    },
    methods: {
        increment() {
            this.count++;
        },
    },
}).mount("#app");
// 组合式
import { ref } from "vue";
const vm = Vue.createApp({
    setup() {
        const count = ref(0);
        const increment = () => {
            count.value++;
        };
        return {
            count,
            increment,
        };
    },
}).mount("#app");
```

### Vue3 组件定义

        Vue3中的组件定义方式有两种，一种是选项式API，一种是组合式API。选项式API一般采用在对象中定义data, methods, computed, watch等属性的方式，组合式API一般采用在setup函数中定义用const定义变量的方式。

```javascript
// 组合式API
import { ref } from "vue";
const Component = {
    setup() {
        const count = ref(0);
        const increment = () => {
            count.value++;
        };
        return {
            count,
            increment,
        };
    },
};
```

### Props

        组合式的单文件Vue里Props的定义方式也有所改变，需要用`defineProps`来定义Props。
        使用参考:`const props = defineProps(['prop1', 'prop2']);`。

### Emit

        `emit`也需要用`defineEmits`来定义。使用参考:`const emit = defineEmits(['event1', 'event2']); emit('event1', data);`。
        Vue3中`emit`还加了双向绑定的语法糖，即`update:propName`。示例如下：

```vue
<!-- 双向绑定示例 -->
<!-- 父组件 -->
<template>
    <child-component v-model:count="count" />
</template>
<script setup>
import { ref } from "vue";
const count = ref(0);
</script>
<!-- 子组件 -->
<template>
    <input
        type="text"
        v-model="countComputed"
    />
    <view>{{ countComputed }}</view>
</template>
<script setup>
import { computed } from "vue";
import { defineProps, defineEmits } from "vue";
const props = defineProps(["count"]);
const emit = defineEmits(["update:count"]);
const countComputed = computed({
    get: () => props.count,
    set: (value) => emit("update:count", value),
});
</script>
```

### 组件注册

        Vue3中的组件注册方式也有所改变，全局注册无大改变，局部注册中如果是使用了`<script setup>`单文件组件时，导入的组件可以直接使用，不用再注册。如果是用了`export default`导出组件时，需要相应的局部注册。

### 组件名格式

        在Vue单文件中，尽量使用`PascalCase`格式来命名组件，这样可以避免与HTML元素冲突。
        在DOM模板中，使用`kebab-case`格式来命名组件，因为HTML不区分大小写。
        Vue支持将`kebab-case`格式的组件名转换为`PascalCase`格式，所以`MyComponent`为名注册的组件可以在模版中用`<my-component>`和`<MyComponent>`两种方式来引用。

### Vue3 生命周期

-   生命周期: 生命周期指的是 Vue 实例从创建到销毁的过程。可以用如下表示 Vue3 的生命周期。

-   生命周期图示:
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
-   生命周期所做的事情:

    -   beforeCreate：实例初始化之后，数据观测和事件配置之前。此时组件实例刚被创建，properties、methods、data 和 computed 等选项都不可用。
    -   created：实例创建完成后立即调用。此时已完成数据观测、属性和方法的运算，watch/event 事件回调，但还未挂载 DOM，$el 属性不可见。可以在此阶段进行 API 调用或数据初始化。
    -   beforeMount：DOM 挂载开始之前被调用。render 函数首次被调用，DOM 初步挂载，数据双向绑定还未完成。此时可以访问到 DOM 元素，但是不能修改 DOM 元素。
    -   mounted：实例被挂载后调用，此时 el 被新创建的 vm.$el 替换，并挂载到实例上。可以在此阶段操作 DOM 元素，进行第三方库初始化等。
    -   beforeUpdate：数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。此阶段可以进一步更改数据，不会触发附加的重渲染过程。
    -   updated：由于数据更改导致的虚拟 DOM 重新渲染和打补丁后调用。组件 DOM 已更新，可执行依赖 DOM 的操作。应避免在此阶段更改状态，可能导致无限更新循环。
    -   beforeDestroy：实例销毁之前调用。此时实例仍然完全可用，可以执行清理工作，如清除定时器、取消网络请求等。
    -   destroyed：实例销毁后调用。调用后，所有的事件监听器被移除，所有的子实例也被销毁。

-   生命周期钩子: 当进入生命周期的某个阶段时，自动触发的函数称为生命周期钩子函数。Vue3 中的生命周期钩子与 Vue2 中的生命周期钩子基本一致，只是名称有所改变。`beforeCreate` => `onBeforeCreate`, `created` => `onCreated`, `beforeMount` => `onBeforeMount`, `mounted` => `onMounted`, `beforeUpdate` => `onBeforeUpdate`, `updated` => `onUpdated`, `beforeDestroy` => `onBeforeUnmount`, `destroyed` => `onUnmounted`, `errorCaptured` => `onErrorCaptured`, `renderTracked` => `onRenderTracked`, `renderTriggered` => `onRenderTriggered`;

-   父子组件执行顺序：
    -   加载渲染过程
        -   父组件 `beforeCreate`
        -   父组件 `created`
        -   父组件 `beforeMount`
        -   子组件 `beforeCreate`
        -   子组件 `created`
        -   子组件 `beforeMount`
        -   子组件 `mounted`
        -   父组件 `mounted`
    -   更新渲染过程
        -   父组件 `beforeUpdate`
        -   子组件 `beforeUpdate`
        -   子组件 `updated`
        -   父组件 `updated`
    -   销毁渲染过程
        -   父组件 `beforeDestroy`
        -   子组件 `beforeDestroy`
        -   子组件 `destroyed`
        -   父组件 `destroyed`

### Vue3 模版引用

        Vue3中的模版引用是通过`ref`来实现的。`ref`可以用来获取模版中的DOM元素，也可以用来获取组件实例。

```html
<!-- 模版引用示例 -->
<div id="app">
    <button ref="button">Click me</button>
</div>
<script setup>
    import { ref, onMounted } from "vue";
    const button = ref(null);
    onMounted(() => {
        button.value.addEventListener("click", () => {
            console.log("clicked");
        });
    });
</script>
```

        如果在`v-for`中使用`ref`，可以用`ref`的数组来获取多个元素。`ref`的数组可以用`ref`的`value`属性来访问。

### Vue3 与 Vue2 其他不同:

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
        app.component("MyComponent", MyComponent);
        app.directive("my-directive", MyDirective);
        app.config.globalProperties.$myProperty = "myProperty";
    },
};
app.use(MyPlugin);
```

## 风格指南

        待更新，https://cn.vuejs.org/style-guide/rules-essential.html#avoid-v-if-with-v-for

## 八股补充知识

### Vue 基础

-   Vue 的底层原理
    Vue2 在实例创建时，会遍历 data 中的属性，利用 Object.defineProperty()将属性转换为 getter/setter，在内部追踪依赖，数据变化时通知视图更新。每个组件都有一个 watcher 实例，在组件渲染过程中把属性记录为依赖，当属性变化时，watcher 会重新渲染组件。  
    Vue3 使用 Proxy 来实现响应式，提供了更强大的拦截机制，比起 Object.defineProperty()，它的优点在于：更完整的拦截能力，可以拦截数组和对象的所有操作；更好的性能，前者需要深度遍历对象的每个属性，后者只需要在对象层面拦截，只有访问属性才会执行拦截；惰性观察，只有访问嵌套对象才会观察。
-   双向绑定的原理
    Vue 是采用数据劫持与发布-订阅模式结合的方式实现双向绑定的。Vue 在初始化时会遍历 data 中的属性，利用 Object.defineProperty()将属性转换为 getter/setter，在数据变动时发消息给订阅者，触发相应监听回调，主要分为以下步骤：
    1. 对需要监听的数据进行劫持，使用 Object.defineProperty() 将数据转换为 getter/setter，当数据被访问或修改时，触发相应的回调函数。
    2. 使用 compile 解析模板指令，将模板中的变量替换为数据，生成对应的 DOM 节点，并初始化页面视图，将每个指令绑定到相应的 watcher 上。
    3. Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁，主要做的事情是: 在自身实例化时往属性订阅器添加自己；自身拥有个 update 方法，主要是更新视图；在属性值变化时，调用自身的 update 方法，通知 Compile 更新视图。
    4. MVVM 作为数据绑定的入口，整合 Observer、Compile 和 Watcher 三者，通过 Observer 来监听自己的 model 数据变化，通过 Compile 来解析编译模板指令，最终利用 Watcher 搭起 Observer 和 Compile 之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据 model 变更的双向绑定效果。
-   Computed, Watcher 的底层原理
    -   理解 effect
        在 Vue 的响应式系统中，effect（副作用函数）是整个响应式系统的核心。从本质上讲，effect 是一个会在数据变化时重新执行的函数。它连接了"数据变化"和"更新操作"这两个环节。  
        Vue 中的 effect 主要实现两个核心机制：依赖收集，访问数据时会将当前的 effect 记录到依赖列表中；触发更新，当数据变化时，会遍历依赖列表，调用所有的 effect 函数。
    -   Computed
        computed 是一个基于依赖收集的懒计算属性，它会在依赖的数据变化时重新计算值。computed 的实现原理是：计算属性创建了一个特殊的 effect; 使用 dirty 标志控制是否需要重新计算; 只有访问值时才会计算，且只在 dirty 为 true 时重新计算; 当依赖项变化时，只是将 dirty 标记为 true，并不立即重新计算在访问 computed 属性时，会将当前的 effect 添加到依赖列表中；当依赖的数据变化时，会触发更新，重新计算 computed 的值。
    -   Watcher
        watcher 是一个基于依赖收集的观察者，它会在依赖的数据变化时执行回调函数。watcher 的实现原理是： Watch 创建了一个 effect，但自定义 scheduler;对于对象类型的侦听源，会递归访问所有属性来收集依赖;通过 scheduler 控制回调的执行时机;支持 immediate、deep 等高级选项。
        watcher 的特点时可以访问旧值和新值，可以深度监听对象的变化，支持立即执行和延迟执行等选项，支持异步更新和批量更新等特性。
-   v-if, v-show 底层原理
    -   v-if 调用 addTransitionClass()方法添加过渡类名，调用 removeTransitionClass()方法移除过渡类名。v-if 还会在 DOM 中添加一个注释节点，用于标记 v-if 的位置。
    -   v-show 会生成 vnode, render 时也会渲染成真实 DOM, 但是不会添加注释节点。v-show 只会添加一个 display:none 的样式类名，而不会移除 DOM 节点。
-   $nextTick 的底层原理
    Vue 的 $nextTick 是一个异步函数，它会在 数据更新与DOM 更新后执行回调函数。$nextTick 的实现原理是：使用 Promise、MutationObserver 或 setTimeout 来实现异步更新；在 DOM 更新后，将所有的回调函数放入一个队列中；使用微任务或宏任务来执行队列中的回调函数。
    -   Vue2 中使用了 setTimeout 来实现异步更新；Vue3 中使用了 Promise 来实现异步更新。Vue3 中的 $nextTick 会在 DOM 更新后立即执行回调函数，而不是等到下一个事件循环。
    -   $nextTick 常见的使用场景一般在于要在数据更新后立即操作 DOM 元素，比如在数据更新后立即获取 DOM 元素的高度、宽度等信息，或者在数据更新后立即执行某个函数等。
-   Vue 如何收集依赖
    在初始化 Vue 组件时，会对 data 初始化，将普通对象变为响应式对象，在这个过程中执行依赖收集相关的逻辑。
    1. Dep 部分。Dep 是一个用于收集依赖的类，它会在数据变化时通知所有的订阅者。Dep 中有一个 subs 数组，用于存储所有的订阅者。同时，Dep 还有一个静态属性 target，用于存储当前的订阅者，保证同一时间只有一个订阅者被计算。
    2. Watcher 部分。Watcher 是一个用于观察数据变化的类，它会在数据变化时执行回调函数。
    3. 过程：初始化 initState，普通对象通过 defineReactive 将对象转换为响应式对象；在访问属性时，触发 getter 方法，Dep.target = watcher; mountComponent 时，实例化 Watcher；在数据变化时，触发 setter 方法，Dep.notify()方法通知所有的订阅者。
-   Vue 模版解析原理
    Vue 中的模板 template 无法被浏览器解析并渲染，因为这不属于浏览器的标准，不是正确的 HTML 语法，所有需要将 template 转化成一个 JavaScript 函数，这样浏览器就可以执行这一个函数并渲染出对应的 HTML 元素，就可以让视图跑起来了，这一个转化的过程，就成为模板编译。模板编译又分三个阶段，解析 parse，优化 optimize，生成 generate，最终生成可执行函数 render。
    1. 解析阶段：使用正则表达式将模板字符串解析成 AST 语法树，AST 语法树是一个描述模板结构的对象，包含了所有的节点信息。
    2. 优化阶段：对 AST 语法树进行静态标记，标记出哪些节点是静态的，哪些节点是动态的。静态节点不会被重新渲染，动态节点会被重新渲染。
    3. 生成阶段：将 AST 语法树转换成可执行的 JavaScript 函数，函数中包含了所有的节点信息和渲染逻辑。最终生成的函数会被挂载到 Vue 实例上，作为 render 函数使用。
-   Vue 传参
    1. 父子传参：子组件 props 接受父组件数据，emit 向父组件传递数据; ref 属性设置子组件名, $refs 获取子组件实例, $parents 获取父组件实例; provide/inject 实现跨级传参。
    2. 兄弟传参：使用 EventBus 实现兄弟组件之间的通信; $parents/$refs 进行通信; Vuex 实现全局状态管理。
-   虚拟DOM
    -   虚拟 DOM 是 Vue 中的一个重要概念，它是对真实 DOM 的一种抽象表示。虚拟 DOM 本质是一个 JavaScript 对象，它描述了真实 DOM 的结构和属性。Vue 在渲染组件时，会先生成一个虚拟 DOM 树，然后将虚拟 DOM 树转换为真实 DOM 树，最后将真实 DOM 树渲染到页面上。
    -   虚拟 DOM 的优点是：
        1. 性能高：虚拟 DOM 是一个 JavaScript 对象，操作速度比真实 DOM 快很多。
        2. 跨平台：虚拟 DOM 可以在不同的平台上运行，比如浏览器、服务器等。
        3. 可测试：虚拟 DOM 可以方便地进行单元测试和集成测试。
    -   虚拟 DOM 的缺点是：
        1. 内存占用大：虚拟 DOM 是一个 JavaScript 对象，内存占用比真实 DOM 大。
        2. 学习成本高：虚拟 DOM 是一个新的概念，需要学习和理解。
-   Diff 算法
    -   Vue 中的 Diff 算法是一个高效的算法，用于比较新旧虚拟 DOM 树的差异，并更新真实 DOM。Diff 算法的核心思想是：
        1. 通过对比新旧虚拟 DOM 树，找出差异的部分，并将差异的部分更新到真实 DOM 中。
        2. Diff 算法的时间复杂度是 O(n)，空间复杂度是 O(n)，性能较高。
    -   Vue 中的 Diff 算法主要分为以下几个步骤：
        1. 比较新旧虚拟 DOM 树的根节点，如果根节点不同，则直接替换整个树。
        2. 如果根节点相同，则比较子节点，使用深度优先遍历的方式，递归比较新旧虚拟 DOM 树的子节点。
        3. 对于同级节点，使用算法进行比对，对于不同的节点进行增删或移动的操作。
        4. 对于新增或删除的节点，使用 patch 方法进行处理。
    -   Vue2 跟 Vue3 的 Diff 算法的区别：
        1. 核心策略：Vue2 使用的是双端比较算法，遍历所有新旧节点，逐层比较；Vue3 引入动态规划思想，使用最长递增子序列算法，减少最小的插入和删除操作。
        2. 静态内容处理：Vue2 无静态内容优化，每次更新需全量比较；Vue3 通过静态提升和 PatchFlag 优化静态内容，避免不必要的比较。

### Vue Router

        Vue Router 是 Vue.js 的官方路由管理器，支持嵌套路由、动态路由、路由懒加载等功能。Vue Router 通过 Vue.extend() 创建路由组件，并使用 Vue.use() 安装路由插件。

-   SPA(Single Page Application) 和 MPA(Multi Page Application) 的区别
    -   SPA 是单页面应用，所有的页面都在一个 HTML 页面中加载，使用 JavaScript 动态加载数据和渲染视图。SPA 的优点是用户体验好，页面切换快，缺点是 SEO 不友好，首次加载时间长。
    -   MPA 是多页面应用，每个页面都是一个独立的 HTML 页面，使用服务器渲染。MPA 的优点是 SEO 好，首次加载时间短，缺点是用户体验差，页面切换慢。
    -   Vue Router 可以实现 SPA 的路由管理，支持嵌套路由、动态路由、路由懒加载等功能。

-   Vue Router常见导航钩子
    -   全局守卫
        -   beforeEach：在路由跳转之前调用，可以用于权限验证、数据预处理等操作。
        -   beforeResolve：在路由解析完成后调用，可以用于权限验证、数据预处理等操作。
        -   afterEach：在路由跳转完成后调用，可以用于数据清理、日志记录等操作。
    -   路由独享守卫
        -   beforeEnter：在路由进入之前调用，可以用于权限验证、数据预处理等操作。
    -   组件内守卫
        -   beforeRouteEnter：在路由进入之前调用，可以用于权限验证、数据预处理等操作。
        -   beforeRouteUpdate：在路由更新之前调用，一般用于重用组件时更新数据。
        -   beforeRouteLeave：在路由离开之前调用，可以用于权限验证、数据预处理等操作。

-   路由模式
    1. hash 模式：使用 URL 的 hash 部分来实现路由，hash 部分不会被发送到服务器，适合单页面应用。hash 模式的路由地址以 # 开头。
    2. history 模式：使用 HTML5 的 history API 来实现路由，history 模式的路由地址不带 #，可以实现更好的 SEO 和用户体验。history 模式需要服务器支持，服务器需要配置路由重定向，将所有请求都指向 index.html。
    3. abstract 模式：使用 Node.js 的内置模块来实现路由，适合服务端渲染的应用。abstract 模式的路由地址不带 #，也不带 /，适合服务端渲染的应用。
    -   hash 模型切换到 history 模型需要: 添加`base`属性; 将所有相对路径改为绝对路径; 在服务器端配置路由重定向，将所有请求都指向 index.html。

-   Vue Router完整的导航流程
    1. 导航触发: 用户点击链接或调用 router.push() 方法，触发路由导航。
    2. 组件失活: 如果当前路由和目标路由的组件不同，则需要先失活当前路由的组件，调用 beforeRouteLeave 钩子函数。
    3. 全局守卫: 调用全局的 beforeEach 钩子函数，进行权限验证、数据预处理等操作。
    4. 重用检测: 检测是否可重用，可重用则调用 beforeRouteUpdate 钩子函数。
    5. 路由解析: 解析目标路由的信息，获取路由的组件、参数、查询字符串等信息，解析路由前调用 beforeEnter 钩子函数。
    6. 组件激活: 激活目标路由的组件，调用 beforeRouteEnter 钩子函数。
    7. 全局解析: 调用全局的 beforeResolve 钩子函数，进行权限验证、数据预处理等操作。
    8. 路由确认: 确认路由的变化，调用 afterEach 钩子函数。
    9. 组件渲染: 渲染目标路由的组件，更新DOM。
    10. 导航完成: 导航完成，用创建好的实例传给 beforeRouteEnter 钩子函数，调用 next() 方法，完成路由导航。

-   常见的辨析
    -   route 与 router
        -   route 包含了当前路由的信息， 如 path、params、query、meta 等。可以通过 route 获取到当前路由的信息, 比如 route.path 获取当前路由的路径。
        -   router 包含了路由的配置信息， 如 routes、mode、base、linkActiveClass 等。通过 router.push() 可以实现当前路由的跳转。
    -   params 与 query
        -   params 和 query 都是路由传参时使用的参数。
        -   params 是路由参数。params传参时name不能带路径。params 刷新页面时会丢失，并且参数不会显示在 URL 中。相较于query，params 适合传递复杂的对象，且安全性更高。
        -   query 是查询参数。query传参时name可以带路径。query 刷新页面时不会丢失，并且参数会显示在 URL 中。相较于params，query 适合传递简单的参数，做为 URL 的查询字符串。
-   路由懒加载
    路由懒加载是指在路由切换时，才加载对应的组件，而不是在应用启动时就加载所有的组件。路由懒加载可以提高应用的性能，减少首屏加载时间。路由懒加载的实现原理是：使用 webpack 的代码分割功能，将路由组件分割成多个文件，在路由切换时，动态加载对应的组件。  
    Vue Router 使用路由懒加载有以下方式:
    1. 使用 import() 函数动态加载组件。
    2. 使用 webpack 的 require.ensure() 函数动态加载组件。
    3. 使用 Vue Router 的异步组件功能，使用 Vue.component() 函数动态加载组件。
    
### Vuex 和 Pinia
#### Vuex
Vuex 是 Vue.js 的官方状态管理库，使用单向数据流的方式来管理状态。Vuex 的核心概念是 Store，Store 是一个容器，用于存储应用的状态。Vuex 的核心 API 包括：
-   Vuex 核心概念
    -   State：状态，存储应用的状态。
    -   Getter：计算属性，从 State 中派生出一些状态。
    -   Mutation：变更函数，用于修改 State 的状态。
    -   Action：异步操作，用于处理异步请求。
    -   Module：模块化，将 Store 分割成多个模块。

-   Vuex 常用 API
    -   mapState：将 State 映射到组件的计算属性中。
    -   mapGetters：将 Getter 映射到组件的计算属性中。
    -   mapMutations：将 Mutation 映射到组件的方法中。
    -   mapActions：将 Action 映射到组件的方法中。
    -   createStore：创建 Store 实例。
