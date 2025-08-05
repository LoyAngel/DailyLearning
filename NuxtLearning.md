# NuxtLearning

## 零、前提概念

### 什么是服务器端渲染（SSR）？

对于传统的 Vue.js 应用，我们通常构建的是单页面应用（SPA）。SPA 的特点是：
1. **客户端渲染 (CSR)**：浏览器首先下载一个空的 HTML 页面和大量的 JavaScript 文件。
2. **数据请求与渲染**：JavaScript 负责获取数据、创建 Vue 实例、挂载组件，并动态生成 DOM 元素，最终才展示给用户。

这种模式的缺点是：
- **首屏加载慢**：用户需要等待所有 JavaScript 下载、解析和执行完成后才能看到内容，导致白屏时间较长。
- **SEO 不友好**：搜索引擎爬虫在抓取页面时，可能无法获取完整的页面内容，因为内容是 JavaScript 动态生成的。

而**服务器端渲染（SSR）**则是一种不同的渲染方式。简单来说，SSR 就是在服务器上将 Vue 组件预渲染成 HTML 字符串，然后将这些 HTML 直接发送给浏览器。

SSR 的工作流程：
1. **服务器预渲染**：当用户请求页面时，服务器上的 Nuxt.js 会运行 Vue 应用，并将组件渲染成完整的 HTML 字符串。
2. **发送 HTML**：这个包含完整内容的 HTML 字符串被发送到浏览器。
3. **快速首屏**：浏览器接收到 HTML 后，可以直接解析并显示页面内容，用户可以立即看到页面，无需等待 JavaScript 下载和执行，大大提升了首屏加载速度。
4. **SEO 友好**：搜索引擎爬虫可以轻松抓取到完整的 HTML 内容，从而更好地进行索引和排名。

### 什么是水合（Hydration）？

虽然 SSR 解决了首屏加载和 SEO 问题，但仅仅发送静态 HTML 是不够的。用户仍然需要一个完整的、可交互的 Vue 应用。这时就需要“水合”（Hydration）这个过程。

**水合**是指在客户端（浏览器）上，Vue.js 接管由服务器端渲染生成的静态 HTML 页面，并使其“活”起来的过程。具体来说：
1. **匹配 DOM 结构**：客户端的 Vue 应用会尝试匹配服务器端生成的 DOM 结构。
2. **绑定事件**：将 Vue 组件的交互逻辑（如点击事件、数据绑定等）附加到已有的 HTML 元素上。
3. **激活组件**：将静态 HTML 转换为一个完全交互式的 Vue 单页面应用。

简单来说，水合就像是给一个“骨架”（SSR 生成的 HTML）注入“灵魂”（客户端 Vue 应用的交互逻辑），让页面从静态变为动态。

如果没有正确的水合过程，用户虽然能看到页面，但无法进行任何交互，直到客户端的 Vue 应用完全重新渲染。Nuxt.js 框架会自动化这个水合过程，确保服务器端渲染和客户端激活之间的无缝衔接。

**为什么水合很重要？**
- **无缝用户体验**：用户在看到首屏内容后，可以立即进行交互，而无需等待页面完全重新渲染。
- **性能优化**：避免了客户端重新生成所有 DOM 的开销，直接复用服务器端生成的 DOM，减少了不必要的性能损耗。

### Nuxt.js 在 SSR 和水合中的角色

Nuxt.js 是一个基于 Vue.js 的通用（Universal）框架，它旨在简化 Vue 应用的 SSR 开发。Nuxt.js 在内部自动化了大量的配置和流程，让开发者能够专注于编写 Vue 组件，而无需过多关注复杂的 SSR 和水合细节。

Nuxt.js 提供了：
- **约定式路由**：基于文件系统的路由，简化了路由配置。
- **数据获取策略**：`useFetch`、`useAsyncData` 等 API，内置了对 SSR 数据预取和水合的支持。
- **自动导入**：自动导入 Vue 和 Nuxt 的核心 API、组件、组合式函数等，减少了手动导入的繁琐。
- **构建优化**：针对 SSR 进行了性能优化，包括代码分割、静态资源处理等。

通过 Nuxt.js，开发者可以更轻松地构建高性能、SEO 友好的 Vue 应用，充分利用 SSR 带来的优势，并确保客户端的无缝交互体验。

### 什么是通用应用 (Universal Application)？

在前端开发中，"通用应用"（Universal Application），有时也称为“同构应用”（Isomorphic Application），指的是一套代码既可以在服务器端（Node.js 环境）运行，也可以在客户端（浏览器环境）运行的应用。Nuxt.js 的核心理念就是帮助开发者构建这样的通用应用。

**为什么需要通用应用？**

通用应用结合了客户端渲染（CSR）和服务器端渲染（SSR）的优点：

1.  **首次加载速度快**：在服务器端预渲染页面，用户可以更快地看到内容。
2.  **SEO 友好**：搜索引擎可以直接抓取到完整的 HTML 内容。
3.  **交互性好**：在客户端进行水合后，页面具备完整的 Vue 应用交互能力。
4.  **开发体验统一**：开发者可以使用一套 Vue.js 代码来处理前后端的渲染逻辑，避免了传统多页面应用中前端模板和后端模板分离带来的开发复杂度。

Nuxt.js 通过其架构和内置功能，自动化了在服务器和客户端之间共享代码和状态的复杂性，让开发者可以更高效地构建具备上述优势的应用。

### 约定优于配置 (Convention over Configuration)

Nuxt.js 遵循“约定优于配置”的原则，这意味着它通过预设的、智能的默认行为和目录结构来简化开发流程，减少了开发者需要手动配置的工作量。你只需要按照特定的约定来组织文件，Nuxt.js 就会自动处理很多事情。

**主要体现：**
1.  **文件系统路由**：你无需手动定义路由配置。只要在 `pages/` 目录下创建 Vue 文件，Nuxt.js 就会自动生成对应的路由。例如，`pages/about.vue` 会自动映射到 `/about` 路径。
2.  **自动导入**：Nuxt.js 会自动导入 Vue 核心 API (如 `ref`, `reactive`)、Nuxt 特有 Composable (如 `useFetch`, `useState`)，以及 `components/`, `composables/`, `utils/` 目录下的组件和函数。你无需手动 `import` 它们，可以直接在代码中使用。
3.  **目录结构约定**：特定的目录（如 `assets/`, `layouts/`, `middleware/`, `plugins/`, `server/` 等）都有其预定义的用途，遵循这些约定可以帮助 Nuxt.js 自动处理相关逻辑。

这种模式的好处是：
-   **降低学习成本**：开发者可以更快上手，因为很多配置都是约定好的。
-   **提高开发效率**：减少了重复的配置工作，让开发者更专注于业务逻辑。
-   **代码规范性**：强制遵循一定的结构，使得团队协作更加顺畅，代码维护更加容易。

理解这一原则对于快速掌握 Nuxt.js 至关重要，它让你能够充分利用框架的自动化能力。

### SSR 下的开发注意事项

在构建通用（SSR）应用时，由于代码需要在服务器和客户端两个不同的环境中运行，因此需要特别注意一些开发细节，以避免潜在的问题。

#### 1. 组件生命周期钩子

在 SSR 环境中，Vue 组件的生命周期钩子执行方式与纯客户端渲染有所不同。你需要了解哪些钩子会在服务器端执行，哪些只在客户端执行：

-   **服务器端和客户端都执行的钩子**：`beforeCreate` 和 `created`。这意味着你可以在这两个钩子中进行数据预取（如果不需要访问浏览器特定的 API）。
-   **只在客户端执行的钩子**：`beforeMount`, `mounted`, `beforeUpdate`, `updated`, `beforeUnmount`, `unmounted`。

**重要提示：**
-   避免在 `beforeCreate` 和 `created` 中执行依赖浏览器 `window` 或 `document` 等全局对象的代码，因为这些对象在 Node.js 环境中是不存在的。如果必须使用，应在 `mounted` 或使用 `process.client` / `process.server` 进行环境判断。
-   任何需要进行 DOM 操作、订阅事件或使用 `setInterval` 等产生副作用的代码，都应该放在 `mounted` 钩子中，以确保它们只在客户端执行并能正确清理。

#### 2. 跨请求状态污染 (Cross-Request State Pollution)

在传统的 Vue SPA 中，当你刷新页面时，整个应用实例会重新初始化。但在 SSR 环境中，服务器是一个长期运行的进程，应用实例可能会被多个用户请求共享。

如果你的应用中存在可变的全局共享状态（例如，一个定义在模块顶层的 `let` 变量），那么不同用户之间的请求可能会相互影响这个状态，导致数据混乱，这就是“跨请求状态污染”。

**错误示例（可能导致状态污染）：**

```js
// store/counter.js
let count = 0; // 全局变量，会被所有请求共享
export const increment = () => count++;
export const getCount = () => count;
```

当一个用户修改 `count` 后，另一个用户的请求可能会看到被修改后的 `count` 值。

**解决方案：**

为了避免状态污染，你必须确保每个服务器请求都能获得一个“独立”的应用实例和状态。Nuxt.js 通过 `useState` 或使用专门的状态管理库（如 Pinia，Nuxt 3 推荐）来解决这个问题。

-   **`useState`**: Nuxt.js 提供的 `useState` 组合式函数能够创建一个在服务器端和客户端都能正确初始化和同步的响应式状态，并且为每个请求隔离状态，防止污染。
-   **状态管理库**：Pinia（Vue 3 的官方推荐状态管理库）是专门为通用应用设计的，它确保每个请求都有独立的 store 实例，从而避免状态污染。

始终确保你的全局状态是“请求隔离”的，这是构建健壮的 SSR 应用的关键。

### Nuxt.js 的其他渲染模式

除了服务器端渲染（SSR），Nuxt.js 还提供了多种灵活的渲染模式，以适应不同的项目需求和部署场景。理解这些模式能帮助你根据网站的特点选择最优的性能和开发策略。

#### 1. 客户端渲染 (Client-Side Rendering, CSR)

虽然 Nuxt.js 默认是通用应用框架，但你也可以将其配置为纯客户端渲染应用（类似于传统的 Vue SPA）。在这种模式下：

-   **特点**：浏览器下载 JavaScript 后在客户端渲染所有内容。服务器只提供一个空的 HTML 文件。
-   **优点**：部署简单（可以部署到任何静态文件服务器），开发复杂度相对较低。
-   **缺点**：首屏加载慢（白屏时间），SEO 不友好。
-   **适用场景**：对 SEO 和首屏性能要求不高的管理后台、内部工具等。

#### 2. 静态站点生成 (Static Site Generation, SSG)

SSG 是一种在**构建时**生成所有 HTML 页面的渲染模式。这意味着在部署之前，Nuxt.js 会预先渲染好所有页面，并将它们保存为静态 HTML、CSS 和 JavaScript 文件。

-   **特点**：在构建阶段生成完全静态的 HTML 文件。每个页面都提前生成好。
-   **优点**：极快的首屏加载速度，优秀的 SEO，部署简单（只需静态文件服务器），CDN 友好，成本低廉。
-   **缺点**：不适合内容频繁变动或需要实时用户交互的页面（除非结合客户端数据获取），每次内容更新都需要重新构建和部署。
-   **适用场景**：博客、文档站、营销网站、企业官网等内容相对固定且对性能和 SEO 要求极高的场景。

#### 3. 混合渲染 (Hybrid Rendering)

混合渲染允许你在同一个 Nuxt.js 应用中，为不同的路由（页面）配置不同的渲染模式（SSR, SSG 或 CSR）。这提供了极大的灵活性，让你能够根据每个页面的具体需求来优化性能。

-   **特点**：通过 `routeRules` 在 `nuxt.config.ts` 中为特定路由定义渲染策略。
-   **优点**：结合了 SSR 和 SSG 的优点，可以实现按需渲染，最大限度地优化性能和部署效率。
-   **适用场景**：大部分现代网站的理想选择，例如，博客文章页面可以使用 SSG 提高性能，而用户个人中心页面则可以使用 SSR 保证实时性。

#### 4. 边缘渲染 (Edge-Side Rendering, ESR)

边缘渲染是 Nuxt 3 引入的一种高级渲染模式，它利用内容分发网络（CDN）的边缘节点来渲染页面。这意味着页面渲染发生在全球各地离用户最近的服务器上，而不是回源到你的主服务器。

-   **特点**：页面在 CDN 边缘节点渲染，而非你的源服务器。
-   **优点**：显著降低延迟，提高全球用户的访问速度，减轻源服务器压力。
-   **缺点**：依赖于支持边缘计算的 CDN 服务，配置可能更复杂。
-   **适用场景**：全球性应用、对性能和用户体验有极高要求的场景。

了解这些渲染模式将帮助你根据项目需求做出明智的决策，从而构建出更高效、更具扩展性的 Nuxt.js 应用。

## 一、基础知识

### 自动导入

Nuxt 会自动导入以下内容，无需手动 import 即可直接使用：

1. Vue 核心 API：
   - 响应式 API：ref, reactive, computed, watch
   - 生命周期钩子：onMounted, onUpdated, onUnmounted 等
   - 工具函数：toRef, toRefs, isRef 等
2. Nuxt 特有 Composable：
   - 数据获取：useFetch, useAsyncData
   - 状态管理：useState
   - 路由相关：useRouter, useRoute
3. 项目目录中的内容：
   - components/目录下的 Vue 组件
   - composables/目录下的自定义组合函数
   - utils/目录下的工具函数

示例代码：

```vue
<script setup>
// 无需import，直接使用
const count = ref(0);
const state = useState("counter", () => 0);
const { data } = await useFetch("/api/items");
</script>
```

### 文件系统路由

Nuxt 采用约定优于配置的原则，根据文件系统自动生成路由：

1. 入口文件配置：
   
   - 当项目根目录存在`app.vue`时，将其作为应用入口
   - 当存在`pages/`目录时，以`pages/index.vue`作为主页

2. 基本路由规则：
   
   - `pages/index.vue` → `/`
   - `pages/about.vue` → `/about`
   - `pages/users/[id].vue` → `/users/:id` (动态路由)
   - `pages/users/index.vue` → `/users`

3. 路由配置扩展：
   可以通过`definePageMeta`宏来扩展路由配置，`definePageMeta`可以定义一些路由的元信息，如布局、中间件等，一般实现页面级的权限校验、SEO 优化等。
   
   - 权限校验示例
     
     ```ts
     // auth.ts
     export default defineNuxtRouteMiddleware((to, from) => {
         // 模拟检查用户是否已登录
         const userIsLoggedIn = false; // 这里应替换为实际的登录状态检查逻辑
     
         if (!userIsLoggedIn && to.meta.middleware === "auth") {
             // 用户未登录且该路由需要认证，重定向到登录页面
             return navigateTo("/login");
         }
     });
     ```
     
     ```vue
     <!-- protected.vue -->
     
     <template>
         <div>
             <h1>受保护的页面</h1>
             <p>只有登录用户才能访问此页面。</p>
         </div>
     </template>
     
     <script setup>
     // 权限校验示例
     definePageMeta({
         middleware: "auth",
     });
     </script>
     ```
     
     ```vue
     <!-- login.vue -->
     <template>
         <div>
             <h1>登录页面</h1>
             <button @click="login">登录</button>
         </div>
     </template>
     
     <script setup>
     const login = () => {
         // 模拟登录成功
         // 这里应替换为实际的登录逻辑
         // 登录成功后跳转到之前尝试访问的页面或首页
         navigateTo("/");
     };
     </script>
     ```

### 组合式函数与 useState

#### 组合式函数

组合式函数（Composable Functions）是 Vue 3 引入的一个重要概念，Nuxt 也鼓励开发者使用 Composition API 来组织代码。在 Nuxt 项目中，`composables/` 目录专门用于存放可复用的组合式函数，这些函数可以封装有状态的逻辑，并在多个组件之间共享。

**概念**：组合式函数本质上是一个普通的 JavaScript 函数，它可以使用 Vue 的响应式 API 来封装逻辑。通过将相关的逻辑封装到组合式函数中，可以提高代码的复用性和可维护性。

**使用场景**：

1. **状态管理**：当多个组件需要共享相同的状态逻辑时，可以将状态管理逻辑封装到组合式函数中。
2. **数据获取**：将数据获取的逻辑封装到组合式函数中，方便在不同组件中复用。
3. **副作用处理**：如定时器、事件监听等副作用逻辑，可以封装到组合式函数中进行统一管理。

**示例代码**：

```js
// composables/useCounter.js
export function useCounter() {
    const count = ref(0);

    const increment = () => {
        count.value++;
    };

    const decrement = () => {
        count.value--;
    };

    return {
        count,
        increment,
        decrement,
    };
}
```

```vue
<!-- components/Counter.vue -->
<template>
    <div>
        <p>Count: {{ count }}</p>
        <button @click="increment">+</button>
        <button @click="decrement">-</button>
    </div>
</template>

<script setup>
import { useCounter } from "~/composables/useCounter";

const { count, increment, decrement } = useCounter();
</script>
```

#### useState

`useState` 是 Nuxt 特有的一个组合式函数，用于创建响应式状态，并且这个状态是 SSR (Server-Side Rendering) 友好的。

**概念**：`useState` 可以创建一个全局响应式状态，该状态在服务器端和客户端都能正确初始化和同步。在服务器端渲染时，`useState` 会将初始状态注入到客户端，避免客户端水合时的闪烁或状态不一致问题。

**使用场景**：

1. **全局状态管理**：对于需要在多个组件之间共享的全局状态，如用户信息、主题设置等，可以使用 `useState` 进行管理。
2. **SSR 应用**：在服务器端渲染的应用中，使用 `useState` 可以确保状态在服务器端和客户端的一致性。

**示例代码**：

```vue
<script setup>
const counter = useState("counter", () => 0);

const increment = () => {
    counter.value++;
};

const decrement = () => {
    counter.value--;
};
</script>

<template>
    <div>
        <p>Counter: {{ counter }}</p>
        <button @click="increment">+</button>
        <button @click="decrement">-</button>
    </div>
</template>
```

**注意事项**：

1. **命名唯一性**：`useState` 的第一个参数是状态的名称，需要确保在整个应用中唯一，避免状态冲突。
2. **初始化函数**：`useState` 的第二个参数是一个初始化函数，用于设置状态的初始值。该函数只会在状态首次创建时执行。
3. **SSR 同步**：在服务器端渲染时，`useState` 会自动将状态同步到客户端，但需要确保在服务器端和客户端使用相同的状态名称和初始化逻辑。

#### 不使用 useState 易出现的错误

- 服务端状态污染
  在 Node.js 环境下，服务器是长生命周期的进程。如果你不小心创建了可变且全局共享的状态（例如，一个模块级别的变量），那么不同用户请求之间可能会互相影响这个状态，导致数据混乱。

错误示例

```ts
// utils/globalCounter.ts
let counter = 0; // 这是一个模块级别的变量，全局共享

export const increment = () => {
    counter++;
    return counter;
};

export const getCounter = () => counter;
```

```vue
<!--component.vue-->
<template>
    <p>计数器: {{ getCounter() }}</p>
    <button @click="increment()">增加</button>
</template>

<script setup>
import { increment, getCounter } from "~/utils/globalCounter.ts";
</script>
```

正确示例

```ts
// composables/useMyCounter.ts
export const useMyCounter = () => {
    // 'my-global-counter' 是一个唯一的键，Nuxt 会为每个请求隔离这个状态
    const counter = useState<number>("my-global-counter", () => 0);

    const increment = () => {
        counter.value++;
    };

    const decrement = () => {
        counter.value--;
    };

    return {
        counter: readonly(counter), // 返回只读的，防止直接修改
        increment,
        decrement
    };
};
```

```vue
<!--component.vue-->
<template>
    <p>计数器: {{ counter }}</p>
    <button @click="increment()">增加</button>
    <button @click="decrement()">减少</button>
</template>

<script setup>
import { useMyCounter } from "~/composables/useMyCounter";

const { counter, increment, decrement } = useMyCounter();
</script>
```

- 客户端状态不同步
  在服务器端渲染（SSR）应用中，若不使用 `useState`，服务器端和客户端的状态可能无法正确同步，导致客户端水合时出现闪烁或状态不一致的问题。
  示例同上。

- 数据更新异常
  当多个组件共享非 `useState` 管理的状态时，可能会出现数据更新不同步的问题，导致部分组件显示旧数据。

错误示例

```js
// utils/sharedState.js
let sharedState = 0;

const updateState = (newValue) => {
    sharedState = newValue;
};

const getState = () => sharedState;

module.exports = {
    updateState,
    getState
};
```

```vue
<!-- ComponentA.vue -->
<template>
    <div>
        <p>State: {{ state }}</p>
        <button @click="update">Update</button>
    </div>
</template>

<script setup>
import { getState, updateState } from "~/utils/sharedState.js";

const state = getState();

const update = () => {
    updateState(state + 1);
};
</script>
```

```vue
<!-- ComponentB.vue -->
<template>
    <div>
        <p>State: {{ state }}</p>
    </div>
</template>

<script setup>
import { getState } from "~/utils/sharedState.js";

const state = getState();
</script>
```

正确示例

```vue
<script setup>
const sharedState = useState("sharedState", () => 0);

const update = () => {
    sharedState.value++;
};
</script>

<template>
    <div>
        <p>State: {{ sharedState }}</p>
        <button @click="update">Update</button>
    </div>
</template>
```

### $fetch, useFetch 和 useAsyncData

        Nuxt 3 提供了三个主要的数据获取方式：`$fetch`、`useFetch` 和 `useAsyncData`。它们各自有不同的设计目的和适用场景，但彼此之间存在紧密联系。`$fetch` 是一个通用的 HTTP 客户端，`useAsyncData` 是一个通用的异步数据获取组合式函数，而 `useFetch` 则是 `useAsyncData` 的一个便捷封装，专门用于处理 HTTP 请求，并内部使用了 `$fetch`。理解它们之间的异同，有助于开发者根据具体需求选择最合适的数据获取策略。

#### $fetch

`$fetch` 是 Nuxt 3 中用于发起 HTTP 请求的函数，它可以在客户端和服务器端使用。
特点：

- **全局可用性**：一个全局可用的 HTTP 客户端，基于 `ofetch` 库。既可以在客户端代码中使用，也可以在服务器端（例如 `server/api` 路由处理器、plugins、`defineNuxtRouteMiddleware` 等）中使用。
- **非绑定生命周期**：不绑定 Vue 组件生命周期，可以随时随地调用。
- **自动处理**：自动处理 JSON 解析、错误抛出、`baseURL` 推断（特别是对于 Nuxt Server API）。
- **无内置状态**：不提供内置的加载状态 (`pending`) 或错误状态 (`error`) 响应式数据，你需要自己管理这些状态（通常结合 `ref` 和 `try...catch`）。
- **无 SSR 水合**：它只是一个通用的请求发送器，不会自动将数据序列化到 HTML 中用于水合。

使用场景：

- **事件处理器中触发的 API 调用**：例如用户点击按钮后发送请求。
- **轮询 (`setInterval`) 中的 API 调用**：轮询查询某个任务状态。
- **Nuxt Server API 内部调用**：在服务器端 API 路由中调用其他外部 API。
- **非组件上下文**：在自定义插件 (`plugins`) 或 中间件 (`middleware`) 中进行数据获取。
- 当你的数据获取逻辑不直接与组件的生命周期（特别是在页面首次加载时）绑定，或者你需要在非组件上下文中进行请求时。

优势：

- **简洁、灵活**：API 简洁，可以用于任何需要发送 HTTP 请求的地方。
- **前后端通用**：同一套 API 可以在整个 Nuxt 应用中无缝使用。
- **性能**：对于简单、直接的请求，避免了 `useFetch` / `useAsyncData` 带来的额外开销。

#### useAsyncData

`useAsyncData` 是 Nuxt 3 提供的一个通用组合式函数，用于处理**任何**异步数据获取操作，并确保其在服务器端渲染 (SSR) 和客户端水合 (hydration) 过程中的无缝衔接。
特点：

- **通用异步数据获取**：它不限于 HTTP 请求，可以用于数据库查询、文件读取或任何返回 Promise 的异步操作。
- **SSR 友好**：这是它的核心优势。它会在服务器端执行数据获取逻辑，并将获取到的数据序列化并嵌入到生成的 HTML 中。在客户端水合时，它会从 HTML 中提取数据，而不是重新执行异步操作，从而避免二次请求和水合不匹配问题。
- **内置响应式状态**：返回 `data`、`pending`（加载状态）、`error`（错误信息）等响应式 `ref`，方便在模板中处理加载状态和错误。
- **数据缓存**：你可以为 `useAsyncData` 提供一个唯一的键 (`key`)，Nuxt 会缓存相同键的数据，避免重复请求。
- **组件上下文**：通常在 Vue 组件的 `setup()` 或 `<script setup>` 中使用。

使用场景：

- **复杂异步逻辑**：当你的数据源不是简单的 HTTP API 调用（例如：直接与数据库交互、读取本地文件、执行耗时计算）时。
- **SSR 应用中的数据预取**：需要在页面或组件渲染前获取数据，以优化首屏加载性能和用户体验。
- **需要自动管理加载/错误状态**：当你需要 Nuxt 自动为你提供数据获取过程中的加载和错误状态时。
- **需要数据水合**：确保服务器端渲染的内容与客户端数据一致，消除闪烁。

优势：

- **高度灵活**：可以封装任何异步操作，不仅仅是 HTTP 请求。
- **完美水合**：确保服务器端渲染的内容与客户端数据一致，消除闪烁。
- **自动化状态管理**：自动提供 `pending`, `error`, `data` 状态，简化 UI 逻辑。
- **内置缓存和优化**：通过 `key` 机制优化重复数据获取。

#### useFetch

`useFetch` 是 Nuxt 3 提供的一个组合式函数，它是 `useAsyncData` 的一个便捷封装，专门用于发起 HTTP 请求。它内部默认就使用了 `$fetch` 作为其数据获取的驱动。
特点：

- **HTTP 请求专用**：专门用于发送 HTTP 请求，内部封装了 `$fetch`。
- **继承 `useAsyncData` 优点**：继承了 `useAsyncData` 的所有优点：SSR 友好、内置加载/错误/数据状态、可缓存。
- **API 简洁**：API 更简洁，特别适合直接请求 API 接口。
- **组件上下文**：通常在 Vue 组件的 `setup()` 或 `<script setup>` 中使用。

使用场景：

- **组件内 API 数据获取**：当你的组件需要在页面加载时，或者当组件的依赖（如路由参数、组件 `props`）发生变化时，从 API 获取数据并希望 Nuxt 自动处理 SSR 和水合。
- **最常用选择**：它是 Nuxt 中最常用的数据获取组合式函数，因为它将 `useAsyncData` 的强大功能和 `$fetch` 的简洁性结合在一起，用于处理绝大多数的 API 调用场景。

优势：

- **最佳实践**：对于大多数组件内 API 数据获取，`useFetch` 是 Nuxt 推荐和优化的方式。
- **开箱即用**：无需手动管理请求、加载状态、错误捕获和数据水合。
- **完美水合**：确保服务器端渲染的内容与客户端数据一致。

#### 三者之间的关系与选择

##### 核心关系对比

| 特性    | $fetch      | useFetch                      | useAsyncData                  |
| ----- | ----------- | ----------------------------- | ----------------------------- |
| 本质    | 通用 HTTP 客户端 | `useAsyncData` 的 HTTP 封装      | 通用异步数据获取组合式函数                 |
| 底层依赖  | `ofetch`    | `$fetch` + `useAsyncData`     | 无 (可自定义异步源)                   |
| 适用上下文 | 全局可用        | 组件 `setup` 中                  | 组件 `setup` 中                  |
| SSR支持 | 基础支持        | 完美支持                          | 完美支持                          |
| 状态管理  | 需手动实现       | 内置 (`pending`/`error`/`data`) | 内置 (`pending`/`error`/`data`) |
| 数据缓存  | 无           | 基于 `key` 缓存                   | 基于 `key` 缓存                   |
| 自动水合  | 无           | 有                             | 有                             |

##### 决策指南

1. **使用场景决策树**
   
   - 是否在组件 `setup` 中使用并需要 SSR 水合和状态管理？
     - 否 → 使用 `$fetch` (用于事件处理、非组件上下文或无需 SSR 水合的场景)
     - 是 → 你的异步操作是 HTTP 请求吗？
       - 是 → 使用 `useFetch` (推荐用于大部分 API 请求)
       - 否 → 使用 `useAsyncData` (用于数据库查询、文件读取等非 HTTP 异步操作)

2. **典型应用场景**
   
   - **`$fetch`**: 事件处理器中触发的 API 调用、定时器轮询、服务器 API 内部调用其他外部 API、自定义插件或中间件中进行数据获取。
   - **`useFetch`**: 页面初始数据加载、基于路由参数或组件 `props` 变化的 API 数据获取、需要自动状态管理的 HTTP 请求。
   - **`useAsyncData`**: 复杂异步逻辑封装（如：直接与数据库交互、读取本地文件、执行耗时计算），不限于 HTTP 请求的通用异步数据获取。

3. **代码示例对比**
   
   **`$fetch` 使用示例**：
   
   ```vue
   <template>
     <button @click="loadData">加载数据</button>
     <div v-if="data">{{ data }}</div>
     <div v-if="error">错误: {{ error }}</div>
   </template>
   
   <script setup>
   const data = ref(null)
   const error = ref(null)
   
   const loadData = async () => {
     try {
       data.value = await $fetch('/api/data')
     } catch (err) {
       error.value = err.message
     }
   }
   </script>
   ```
   
   **`useFetch` 使用示例**：
   
   ```vue
   <template>
     <div v-if="pending">加载中...</div>
     <div v-else-if="error">错误: {{ error.message }}</div>
     <div v-else>{{ data }}</div>
   </template>
   
   <script setup>
   import { useFetch, useRoute } from '#app';
   const route = useRoute();
   
   const { data, pending, error } = useFetch('/api/data', {
     watch: [route.params.id] // 路由参数变化时重新请求
   })
   </script>
   ```
   
   **`useAsyncData` 使用示例**：
   
   ```vue
   <template>
     <div v-if="pending">加载中...</div>
     <div v-else-if="error">错误: {{ error.message }}</div>
     <div v-else>{{ data }}</div>
   </template>
   
   <script setup>
   const { data, pending, error } = useAsyncData('user-data', async () => {
     // 模拟数据库查询或文件读取等非 HTTP 异步操作
     const res = await new Promise(resolve => setTimeout(() => resolve({ rows: 'Some data from DB/file' }), 1000));
     return res.rows
   })
   </script>
   ```

### 后端部分

