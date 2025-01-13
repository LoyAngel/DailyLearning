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
2. 组件自动引入: easycom 正则导入
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

# 轮播图
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
