# 前期准备
## pages.json 和 manifest.json
下面两者需要在 vscode 文件关联设置为 jsonc 格式
1. `pages.json`  
   pages: 配置小程序的页面路径  
   globalStyle: 配置小程序的全局样式  
   tabBar: 配置小程序的底部导航
2. `manifest.json`  
   配置小程序的全局配置, 包括 appid、app 名称等
## uni-app 和 原生小程序 区别
1. 属性绑定, `src={{url}}` 替换成 `:src="url"`
2. 事件绑定, `bindclick="handleClick"` 替换成 `@click="handleClick"`，并支持传参
3. 支持 Vue 常用的语法糖, 如: v-if、v-for、v-model 等

    P.S. 调用接口时，尽量将前缀`wx`替换成`uni`，支持多端开发
## 创建 uni-app 项目
1. HBuilderX 创建
2. 命令行创建
    - npx degit dcloudio/uni-app-template my-project 拉取模板
    - manifest 添加小程序 appid
    - pnpm install 安装依赖
    - pnpm run dev:mp-weixin 编译 Vue 文件到小程序
    - 导入到微信开发者工具进行热更新调试
## VsCode 配置
1. 安装插件: uni-helper, uni-create-view, uniapp 小程序扩展
2. ts 类型校验:
    - 安装类型声明文件
    - 配置tsconfig.json: 配置 types 与 vueCompilerOptions 选项，并在`compilerOptions` 中添加 `"ignoreDeprecations": "5.0"`

# 基础架构
## uni组件库
1. 安装uni-ui
2. 组件全局自动引入: easycom 正则导入（记得重启微信小程序）
3. 配置uni类型: @uni-helper/uni-ui-types
## pinia持久化
1. 安装pinia
2. 安装vuex-persistedstate
3. 在defineStore的options中添加带有getItem和setItem的storage选项
## 请求和上传文件拦截器
1. 拦截器
    设置基础地址、超时时间、请求头标识、添加token
2. 请求函数
    - 成功: 提取数据，添加类型
    - 失败: 不同状态码的处理
    - uni.request 和 axios区分: uni.request 的success是表示服务器请求成功，不处理状态码；axios的resolve只有在状态码为2xx时才会执行，表示数据获取成功。

# 首页
## 轮播图
1. 全局组件自动导入: easycom 正则导入（注意正则导入无法将驼峰和短横线组件名统一）
2. 全局组件类型声明: 
```ts
declare module 'vue'{
  export interface GlobalComponents{
    'my-component': typeof import('path of my-component')
  }
}
```
3. 小程序生命周期: onLoad -> onShow -> onReady -> onHide -> onUnload
4. 自定义组件可以有自定义属性，通过props传递，组件内部通过defineProps接收
## 前台分类
1. 通过flex: 1可以实现自适应高度，使得组件占据剩余空间
2. 组件挂载完毕调用api可以避免重复写业务代码
## 骨架屏
1. 骨架屏指的是在数据加载过程中，先展示一个大致的页面结构，等数据加载完毕后再展示真实数据。如果没有骨架屏，可能会导致渲染层出错等问题。
2. 骨架屏在微信小程序中可以自动生成，生成完后将html和css复制到uni-app进行修改。
3. 在需要加载的页面中，通过v-if控制骨架屏的显示与隐藏。v-if与标记变量配合，标记变量则通过`onLoad`里对于数据的请求来改变，在Promise.all请求前为true，等待请求完成后为false。

# 子页面
1. 通过`defineProps`定义子页面的props，父页面可以通过url里传参，子页面通过props接收
2. 可以通过`&`符号对类型进行交叉，比如`Object A`和`{name: string}`两者的交叉
3. 表格展开时再用v-if渲染，能够减少页面加载时间
4. fixed定位的元素会脱离文档流，不会影响其他元素的位置，可以通过z-index来调整层级；同时之后的元素可以用margin-top/...等属性来调整位置

# sku模块
1. eslint可以通过注释进行关闭，如`// eslint-disable-next-line`，`/* eslint-disable */`
2. uni-app插件市场可以下载到一些常用的插件，如`uni-popup`等

# 项目打包
1. 打包时可以通过`pnpm run build:mp-weixin`来打包微信小程序
2. 可以通过条件编译来区分不同的打包环境，如`#ifdef H5`、`#endif`等

# 跨端兼容
1. 小程序端不支持*选择器，直接用`view`和`text`等标签代替
2. 页面视口差异，h5的视口包括了tabbar和导航栏，小程序端则不包括。此时可以设置page的style为`height: 100%`来适配
3. uni-app提供了css语法，包括`--window-bottom`,`--window-top`等，避免了不同端的差异