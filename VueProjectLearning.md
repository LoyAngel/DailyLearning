# admin-test

## 1. nvm 与 nrm 安装

## 2. 项目启动与路由搭建

- 别名的配置
  - 在 vue.config.ts 配置 resolve.alias
  - 在 tsconfig.json 配置 CompilerOptions.baseUrl 和 paths
  - 在 vite-env.d.ts 声明 '\*.vue' 模块
- 路由的搭建
  - 路由通过 vue-router 来实现
  - vue-router 通过 定义 routes 和 router 来实现， 定义了之后在 main.ts 中引入 router 并挂载到 app 上。
  - vue-router 提供 `router-view` 插件，可以将其看作一个容器，用来放置路由匹配到的组件。
  - 路由配置方法:
    1. 在 src/router/index.ts 中配置路由
    2. 在 src/views 中创建页面
    3. 在 src/components 中创建组件
  - 嵌套路由: 嵌套路由指的是在一个路由下有多个子路由， 子路由的配置方法是在父路由的 children 中配置。然后再在父路由的组件中使用 `router-view` 来放置子路由。
- route 与 router
  - route 包含了当前路由的信息， 如 path、params、query、meta 等。可以通过 route 获取到当前路由的信息, 比如 route.path 获取当前路由的路径。
  - router 包含了路由的配置信息， 如 routes、mode、base、linkActiveClass 等。通过 router.push() 可以实现当前路由的跳转。

## 3. element-plus 的使用

- [element-plus 的文档地址](https://element-plus.org/#/zh-CN)
- element-plus 的三种引入方式
  - 全局引入， 直接在 main.ts 中引入 ElementPlus 和 element-plus/dist/index.css
  - 自动引入， 安装 unplugin-vue-components 和 unplugin-auto-import 两款插件， 并在 vite.config.ts 中配置 AutoImport 和 Components。
  - 手动引入， 安装 unplugin-element-plus 插件， 并在 vite.config.ts 中配置 plugins 里添加 ElementPlus。
- @elment-plus/icons-vue 是 element-plus 的图标库， 可以在 element-plus 的文档中查看图标的使用方式。引用后在任意 ts 中通过 icon 名与 component 搭配即可使用。

## 4. 搭建项目视图

- 项目视图可以根据文档中的样式图与实际项目需求进行调整。
- 用样式控制布局大小， 用组件控制布局结构。
- element-ui 提供了很多常用的组件， 可以根据项目需求来选择使用。
  - element-container 实现了容器的功能，与 el-header、el-main、el-footer、el-aside 等组件搭配使用可以快速实现页面布局。
  - element-menu 实现了菜单栏的功能， 可以通过配置 router 来实现菜单栏的动态生成。
  - elment-row 和 element-col 实现了栅格布局的功能， 可以通过配置 span 来实现不同的布局效果。
  - element-card 实现了卡片的功能， 可以实现博客卡片展示等效果。
  - element-table 实现了表格的功能， 可以实现数据的展示。

## 5. pinia 的使用

- pinia 是一个状态管理库， 可以用 store 来管理全局状态。
- 在 src/store/index.ts 中配置 store， 并在 main.ts 中引入 store。
- 在 store 的组合式 index.ts 中， ref 相当于 state 属性，computed 相当于 getters， function 相当于 actions；在引用时，可以通过定义的函数名直接调用。
- 运用 pinia 可以跨组件实现状态共享。
- pinia的应用：tab的实现，通过 store 来管理 Tab 的状态，通过 computed 来获取 Tab 的状态，通过 function 来实现 Tab 的操作。
- pinia 可以和 缓存配合使用，通过 localStorage 来实现数据的持久化。

## 6. axios 与 mockjs 的使用

- axios 是一个基于 promise 的 HTTP 库， 可以用来发送请求。
- axios 是异步实现的，需要通过 then 或 async/await 来获取数据。(async/await 不能在 setup 时作为匿名函数使用，应该定义函数后放入 onMounted 中调用)
- axios 可以用来发送 get、post、put、delete 等请求。
- 将 axios 的请求拦截器与响应拦截器封装成一个插件，可以在 main.ts 中引入并使用。
- mockjs 是一个模拟数据的库， 可以用来模拟后端数据。
- mockjs 可以通过 mock.mock() 来模拟数据， 并通过 mock.setup() 来配置拦截请求, 返回模拟数据。mock.mock() 可以使用正则表达式来匹配请求路径, 如`/api\/user/1/`。
- mockjs 还可以通过 mock.Random 来生成随机数据， 如 mock.Random.cname() 可以生成中文名字。
- mockjs 中获取参数一般用自定义的 param2Obj 函数，将 url 中的参数转化为对象，方便后续使用。

## 7. 开发环境与生产环境的配置

- 开发环境与生产环境的配置可以在 config/index.ts 中配置。
- env 可以通过 import.meta.env.MODE 来获取当前环境, 可以取值为 development, test, production。
- 在 index.ts 中，配置 EnvConfig 接口，一般创建 dev, test, prod 三个环境。每个环境包含 baseURL 和 mockURL 两个属性, 作为测试的区分。最后通过 export default 导出。
- 一般在 request.ts 中使用该配置功能，实现根据环境的不同，请求不同的 url。
- 用 app.config.globalProperties.$properties_name 可以创建全局变量，之后在任意组件中可以用{proxy} = useProperties()来获取实例后，通过proxy.$properties_name 来获取全局变量。

# 8. echarts 的使用与监听的实现

- [echarts 的文档地址](https://echarts.apache.org/zh/get-started.html)
- echarts 是一个数据可视化的库，可以用来展示数据，常见的有折线图、柱状图、饼图等。
- 监听可以通过 Observer 来实现，通过监听数据的变化，来实现数据的实时更新。比如 ResizeObserver 可以监听元素的大小变化，MutationObserver 可以监听元素的子元素变化等。

# 9. 表格的数据展示与编辑

- 表格的数据展示可以通过 element-ui 的 table 组件来实现，可以通过配置 columns 来实现表头的展示，通过配置 data 来实现数据的展示。其中表格的数据在获得后，可以通过.map 函数来进行数据的处理（比如 gender 数字转文字的处理）。
- 分页的实现在 mock 中用 page 和 limit 来实现，通过计算总页数，来实现分页的功能。
- 通过:?表达式可以实现数据动态调整，比如宽度可以通过:width="item.width ? item.width : '100px'"来实现。
- 注意: 渲染的速度是很慢的，可能比代码执行的速度还要慢。在通过 el-dialog 进行编辑时，如果传递速度过快，会导致传递进去的数据变为默认值，使之后打开每次的值成为最初打开数据的值。解决的方法是通过 tiktok 来延迟传递数据，避免渲染速度过慢。除此之外，响应式对象无法用常规方法（赋值空或者 Object.assign 空值）来清空，需要通过 delete 来删除对象的属性或者 Object.assign 带有空值键值对的对象覆盖来实现；响应式数组同理，需要通过 length=0 或者 splice(0, length)来清空。
  p.s: 在 html 中可以通过`:`绑定的方式实现数字类型。

# 10. 账号的登录和路由守卫

- 账号的登录可以通过 mockjs 来模拟数据，通过 axios 来发送请求，通过 localStorage 来存储数据。
- 账号的权限通过动态路由来实现，通过登录后获取的权限来动态生成路由。动态路由指的是在登录后获取到权限后，通过 router.addRoute() 来动态添加路由，实现权限的控制。
- 路由守卫可以通过 router.beforeEach() 来实现，对于访问不存在的页面，可以通过 return {name: 'pageName'} 来实现跳转到指定页面。