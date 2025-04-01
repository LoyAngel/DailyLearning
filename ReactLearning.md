# ReactLearning

## React 前置思想

### 浏览器 html 展示机理

### 纯函数

-   纯函数是指满足以下条件的函数：
    1. 相同的输入始终产生相同的输出。
    2. 自包含(函数内部不依赖外部变量)。
    3. 无副作用(不修改外部变量，不修改和程序状态)。
-   纯函数的优点：利于重构；可并行；可缓存。

### 函数式编程

-   函数式编程是一种编程范式，它是一种编程风格，不是一种编程语言。
-   函数式编程的思想是：只关注做什么，而不关注怎么做。
-   函数式编程的特点：函数是一等公民（可传递）；函数是纯函数。

### 声明式 UI

声明式 UI 的特点：只关注 UI 的状态，不关注 UI 的变化。

### 科里化

- 科里化是指将接受多个参数的函数转换为接受一个参数的函数，并返回接受余下参数的函数的技术。
```javascript
// 科里化前
function add(x, y) {
    return x + y;
}
// 科里化后
function add(x) {
    return function (y) {
        return x + y;
    };
}
```
- 科里化的优点：提高函数的复用性；提高函数的灵活性。

### 副作用

-   副作用包括特定情况下不得不发生的变动，它们是“额外”发生的事情，与渲染无关。
-   副作用的场景：数据请求；DOM 操作；定时器；本地存储；全局变量；异常处理。

### Hook

-   Hook 是 React 16 中增加的新特性，任何以 use 开头的函数都是 Hook。
-   Hook 示特殊的函数，只在 React 渲染时有效。

## React JSX

React 使用 JSX 来替代常规的 JavaScript。JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。  
JSX 有以下优点：

-   JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
-   它是类型安全的，在编译过程中就能发现错误。
-   使用 JSX 编写模板更加简单快速。

### JSX 语法

1. 可以在变量中插入 HTML 标签
2. JSX 也是一个表达式, 类型为 `ReactElement`，可以作为参数传递

```jsx
const element = (
    <h1>
        Hello, {user}
        {user ? "!" : "."}
    </h1>
);
```

1. 可以使用大括号 `{}` 在 JSX 中嵌入表达式

```jsx
const element = <h1>{getGreeting(user)}</h1>;
```

1. JXS 可以使用内联样式，样式名使用驼峰命名

```jsx
var myStyle = {
    fontSize: 100,
    color: "#FF0000",
};
const root = React.createRoot(document.getElementById("root"));
root.render(<h1 style={myStyle}>Hello World!</h1>);
```

-   副作用包括特定情况下不得不发生的变动，它们是“额外”发生的事情，与渲染无关。
-   副作用的场景：数据请求；DOM 操作；定时器；本地存储；全局变量；异常处理。

## React 组件

React 组件是构建 React 应用的基本单位。
组件可以是函数组件或者类组件。

### 函数组件

函数组件是一个接受 props 对象并返回 React 元素的函数，是最新的 React 特性，用来代替以往的类组件。

```jsx
import React from "react";
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
```

### 类组件

类组件是一个类，类中必须包含一个 render() 方法，render() 方法返回一个 React 元素。

```jsx
import React from "react";
class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>;
    }
}
```

### 复合组件

组件可以在其输出中引用其他组件。这可以让我们用相同组件抽象出任意层次的细节。

```jsx
import React from "react";
function Name(props) {
    return <h1>{props.name}</h1>;
}
function Url(props) {
    return <h1>{props.url}</h1>;
}
function App() {
    return (
        <div>
            <Name name="React" />
            <Url url="https://reactjs.org/" />
        </div>
    );
}

const root = React.createRoot(document.getElementById("root"));
root.render(<App />);
```

### 组件生命周期

#### 生命周期

React 组件有三个生命周期阶段：

1. 挂载阶段：组件被创建并插入到 DOM 中。
2. 更新阶段：组件被重新渲染。
3. 卸载阶段：组件被从 DOM 中移除。

#### 生命周期方法

React 组件的不同生命周期阶段有不同的生命周期方法，用于在组件的生命周期中执行一些操作。

1. 挂载阶段
    - constructor()：构造函数，初始化 state。
    - componentDidMount()：组件挂载后调用。
    - static getDerivedStateFromProps()：在调用 render 方法之前调用，用于更新 state。
2. 更新阶段
    - shouldComponentUpdate()：返回一个布尔值，用于判断是否需要重新渲染组件。
    - render()：渲染组件的 UI。
    - getSnapshotBeforeUpdate()：在更新前获取 DOM 信息。
    - componentDidUpdate()：更新后调用。
3. 卸载阶段
    - componentWillUnmount()：组件卸载后调用。

## React Props

Props 是 React 组件的输入，是一个对象，包含组件的一些数据。Props 通过父组件传递给子组件，是只读的，不能修改。  
Props 可以传输任何类型的数据，包括函数。

```jsx
import React from "react";
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
const element = <Welcome name="React" />;
```

Props 和 State 主要区别在于 Props 是不可变的，而 State 可以根据与用户交互来改变。

-   默认 Props: `Component.defaultProps = {}`
-   多个 Props

```jsx
function Welcome(props) {
    return (
        <div>
            <h1>Hello, {props.name}</h1>
            <h2>{props.url}</h2>
        </div>
    );
}
const element = (
    <Welcome
        name="React"
        url="https://reactjs.org/"
    />
);
```

-   propTypes 验证: 通过引入 prop-types 库，可以对 props 进行类型验证

```jsx
import PropTypes from "prop-types";
Welcome.propTypes = {
    name: PropTypes.string,
    url: PropTypes.string,
};
```

-   传递函数作为 props

```jsx
function Welcome(props) {
    return <button onClick={props.clickMethod}>Click Me</button>; // clickMethod为父组件传给子组件的方法名,通过`props.methodName`调用
}
function App() {
    function handleClick() {
        alert("Clicked");
    }
    return <Welcome clickMethod={handleClick} />; // handleClick为父组件的方法, 通过`methodName={}`调用
}
```

-   解构 props

```jsx
function Welcome({ name, url }) {
    return (
        <div>
            <h1>Hello, {name}</h1>
            <h2>{url}</h2>
        </div>
    );
}
const App = () => {
    return (
        <Welcome
            name="React"
            url="https://reactjs.org/"
        />
    );
};
```

## React Context

Context 提供了一种在组件之间共享值的方式，而不必通过组件树的逐层传递 props。

-   Context 可以将父组件的参数传递给 child 组件。
-   Context 常见方法：
    -   createContext(defaultValue): 创建一个 Context 对象，defaultValue 为默认值。
    -   useContext(context): 使用 Context 对象，返回当前的 Context 值。
    -   <Context.Provider value={value}>: 用于提供 Context 值。

## React States

-   组件的状态是一个对象，包含组件的一些数据。组件的状态可以通过 `this.state` 访问。 状态是可变的，但是不能直接修改状态，必须使用 `this.setState()` 方法，此时状态更新可能是异步的。

```jsx
// 类组件的状态
import React from "react";
class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = { date: new Date() };
    }
    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
        );
    }
}
// 函数组件的状态
import React, { useState } from "react";
function Clock() {
    const [date, setDate] = useState(new Date());
    return (
        <div>
            <h1>Hello, world!</h1>
            <h2>It is {date.toLocaleTimeString()}.</h2>
        </div>
    );
}
```

-   React 中使用 state 处于两种原因：局部变量无法在多次渲染之间保持；更改局部变量不会触发重新渲染。
-   一些注意点:
    -   state 与其他模块顶部的普通变量不同，它不依赖于特定函数调用，而是属于组件的私有数据。
    -   state 更新一般在渲染之后，正常情况多次调用 setState() 会合并更新，只会触发一次重新渲染。(要想更新多次可以传入更新函数)
        -   可以将 setState(n) 拆解为 setState(() => n), 而 React 会遍历 state 更新队列，从前往后执行。
    -   state 不用担心异步函数中对 state 引用会造成数据不一致，state 默认以快照的形式保存，不会引用最新的值，而是保留之前的值。
    -   state 中所有存放的对象应该被视为只读的(就算存放的是可变对象)。
        -   state 在正常情况下更新嵌套对象需要使用展开运算符，但是可以安装 Immer 库，使用`useImmer`来更新嵌套对象。
        -   state 更新数组替换：`push`,`unshift`->`concat`,`[...arr]`; `pop`,`shift`,`splice`->`filter`,`slice`; `splice`,`arr[i]=...`->`map`;`sort`,`reverse`->复制后进行。
    -   state 要想在组件间共享状态，可以将状态提升到共同的父组件中，然后通过 props 传递给子组件，并将 setState 方法传递给子组件。
    -   state 的保留与重置与渲染树的位置有关，相同位置相同组件会保留，相同位置不同组件会重置。用 key 属性可以保证组件的状态可以区分。

## React Reducer

Reducer 是处理状态的另一种方式，相当于将同一类的操作封装到一个函数中，通过 dispatch 一个 action 来触发这个函数，从而更新状态。

-   可以通过三个步骤将 useState 迁移到 useReducer:
    1. 将设置状态的逻辑修改为 dispatch 一个 action。
    2. 编写一个 reducer 函数，接收 state 和 action，返回新的 state。
    3. 使用 useReducer 代替 useState。
-   Reducer 的常见方法
    -   dispatch({type: 'xxx', ...other}), type 为必须的属性，用于区分不同的操作，其他属性可以根据需要添加。
    -   function reducer(state, action) { switch(action.type) { case 'xxx': return {...state, ...action}; default: return state; } }, reducer 函数接收两个参数，state 和 action，返回新的 state。
    -   useReducer(reducer, initialState), useReducer 接收两个参数，reducer 函数和初始状态，返回一个数组，第一个元素为当前状态，第二个元素为 dispatch 函数。
-   Reducer 同样可以用 Immer 库来更新嵌套对象，使用`useImmerReducer`方法可实现效果。

## React 事件处理

React 事件处理和 DOM 事件处理类似，但有一些语法上的区别。

1. React 事件的命名采用驼峰命名法，而不是小写。
2. 如果要阻止事件冒泡，不能使用 `return false`，而是调用 `event.stopPropagation()` 或 `event.preventDefault()`。
3. 添加监听器时不需要使用 `addEventListener`，而是直接在 JSX 中添加。
4. 使用类组件时，事件处理器会成为类的一个方法，需要绑定 this。
5. 注意传递事件参数应该直接传递，而非调用。

```jsx
import React from "react";
class Toggle extends React.Component {
    constructor(props) {
        super(props);
        this.state = { isToggleOn: true };
        this.handleClick = this.handleClick.bind(this); // 必须绑定才能在方法中使用this
    }
    handleClick() {
        this.setState((state) => ({
            isToggleOn: !state.isToggleOn,
        }));
    }
    render() {
        return (
            <button onClick={this.handleClick}>
                {this.state.isToggleOn ? "ON" : "OFF"}
            </button>
        );
    }
}
```

若不想绑定 this，可以使用属性初始化器语法或者箭头函数

```jsx
// 属性初始化器语法
class Toggle extends React.Component {
    handleClick = () => {
        console.log("this is:", this);
    };
    render() {
        return <button onClick={this.handleClick}>Click me</button>;
    }
}
// 箭头函数
class Toggle extends React.Component {
    handleClick() {
        console.log("this is:", this);
    }
    render() {
        return <button onClick={(e) => this.handleClick(e)}>Click me</button>;
    }
}
```

使用函数组件时，事件处理函数可以避免绑定 this。

```jsx
import React, { useState } from "react";
function Toggle() {
    const [isToggleOn, setIsToggleOn] = useState(true);
    const handleClick = () => {
        setIsToggleOn(!isToggleOn);
    };
    return <button onClick={handleClick}>{isToggleOn ? "ON" : "OFF"}</button>;
}
```

5. 传递参数
   事件处理函数可以接收参数，有两种方式:

```jsx
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

当第一种方式使用时，事件对象 e 必须显式传递，而第二种方式不需要传递事件对象。
函数 e 接收参数时，事件对象 e 必须放在参数的最后。

## 条件渲染和列表渲染

### 条件渲染

React 的条件渲染和 JavaScript 中的条件语句类似，可以使用 if 语句或者三元运算符。

```jsx
import React from "react";
// if语句
function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;
    if (isLoggedIn) {
        return <h1>Welcome back!</h1>;
    }
    return <h1>Please sign up.</h1>;
}
// 三元运算符
function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;
    return (
        <div>
            {isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign up.</h1>}
        </div>
    );
}
```

### 列表渲染

React 中使用 js 的循环语句，比如 for,map 等来渲染列表。循环时需要给每个元素添加一个 key 属性，且 key 属性值必须是唯一的。

```jsx
import React from "react";
function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) => (
        <li key={number.toString()}>{number}</li>
    ));
    return <ul>{listItems}</ul>;
}
const numbers = [1, 2, 3, 4, 5];
const element = <NumberList numbers={numbers} />;
```

## React AJAX

React 可以通过 AJAX 来获取远程数据，通常使用第三方库如 Axios 或 Fetch。

### 使用 fetch

1. 引入 fetch
2. 使用 useEffect 处理副作用
3. 发起请求
4. 处理响应
5. 错误处理
6. 更新状态

```jsx
import React, { useState, useEffect } from "react";
function App() {
    const [data, setData] = useState([]);
    useEffect(async () => {
        fetch("https://api.example.com/data")
            .then((response) => response.json())
            .then((data) => setData(data));
    }, []);
    return (
        <ul>
            {data.map((item) => (
                <li key={item.id}>{item.name}</li>
            ))}
        </ul>
    );
}
```

### 使用 Axios

1. 安装 axios
2. 引入 axios
3. 使用 useEffect 处理副作用
4. 发起请求
5. 处理响应
6. 错误处理
7. 更新状态

```jsx
import React, { useState, useEffect } from "react";
import axios from "axios";
function App() {
    const [data, setData] = useState([]);
    useEffect(async () => {
        axios
            .get("https://api.example.com/data")
            .then((response) => setData(response.data));
    }, []);
    return (
        <ul>
            {data.map((item) => (
                <li key={item.id}>{item.name}</li>
            ))}
        </ul>
    );
}
```

## React 表单

React 表单元素与 HTML 表单元素类似，但有一些区别。  
HTML 表单，像`<input>`、`<textarea>`、`<select>`等元素通常维护自己的状态，并根据用户输入进行更新。但在 React 中，可变状态通常保存在组件的 state 属性中，并且只能通过 setState()方法来更新。

```jsx
class Content extends React.Component {
    render() {
        return (
            <div>
                <input
                    type="text"
                    value={this.props.myDataProp}
                    onChange={this.props.updateStateProp}
                />
            </div>
        );
    }
}

class HelloMessage extends React.Component {
    constructor(props) {
        super(props);
        this.state = { value: "Hello!" };
        this.handleChange = this.handleChange.bind(this);
    }
    handleChange(e) {
        this.setState({ value: e.target.value });
    }
    render() {
        return (
            <div>
                <Content
                    myDataProp={this.state.value}
                    updateStateProp={this.handleChange}
                />
                <h4>{this.state.value}</h4>
            </div>
        );
    }
}
```

## React Refs

Refs 是 React 提供给我们的一种方式，用于访问在 render 方法中创建的 DOM 元素或者类组件实例。  
使用`useRef()`会创建一个可变的 ref 对象，其`current`属性被初始化为传入的参数（可以是任何值）。

### Ref 与 State 的区别

-   useRef 返回`{current: null}`，而 useState 返回`{[value, setValue]}`。
-   ref 更改不会触发组件重新渲染，而 state 更改会触发组件重新渲染。
-   ref 在渲染之外可以修改与更新，state 只能通过 setState 更新。
-   ref 无法在渲染期间读写。（即不要在 render 中使用 ref）

### 使用 Ref 操作 DOM

React 中没有内置的方法管理 DOM 元素，比如节点获得焦点、选择文本、或者媒体播放，但是这些可以使用 ref 来操作 DOM。

```jsx
// 文本框获取焦点
import React, { useRef } from "react";
function App() {
    const inputRef = useRef(null);
    function handleClick() {
        inputRef.current.focus();
    }
    return (
        <div>
            <input
                ref={inputRef}
                type="text"
            />
            <button onClick={handleClick}>Focus</button>
        </div>
    );
}
```

## React Effect

Effect 指的是在 React 组件渲染后执行的副作用操作，用来避免渲染期间对 DOM 的直接操作导致的错误。

1. useEffect 包裹副作用，会把它们分离到渲染周期之外。

```jsx
// video播放与暂停
import { useState, useRef, useEffect } from "react";

function VideoPlayer({ src, isPlaying }) {
    const ref = useRef(null);

    useEffect(() => {
        // 如果不用useEffect将会报错
        if (isPlaying) {
            ref.current.play();
        } else {
            ref.current.pause();
        }
    });

    return (
        <video
            ref={ref}
            src={src}
            loop
            playsInline
        />
    );
}

export default function App() {
    const [isPlaying, setIsPlaying] = useState(false);
    return (
        <>
            <button onClick={() => setIsPlaying(!isPlaying)}>
                {isPlaying ? "暂停" : "播放"}
            </button>
            <VideoPlayer
                isPlaying={isPlaying}
                src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4"
            />
        </>
    );
}
```

2. 在默认情况下, Effect 会在每次渲染后执行，因此需要设置第二个参数，即依赖项数组，只有数组中的值发生变化时，Effect 才会执行。当传入空数组时，Effect 只会在组件挂载时执行。依赖项不需要传入 ref。

```jsx
useEffect(() => {
    // Effect
}, [value]);
```

P.S.: React 为了让开发者注意到挂载问题，在开发环境中，会在组件首次挂载时立即重新挂载一次。  
3. Effect 会返回一个清理函数，用于清理 Effect。

```jsx
useEffect(() => {
    // Effect
    return () => {
        // Cleanup
    };
}, [value]);
```

4. 不需要使用 Effect 的场景

-   一个值可以通过现有的 props 或 state 计算得出，那么直接`const value = ... `即可。当计算的方法需要耗时过长，可以使用 useMemo 的 HOOK 来实现缓存。useMemo 仅是适用于纯函数场景。
-   当 props 变化时重置所有 state，可以新建一个组件，将 state 放置在组件内部，并在原组件将变化的 props 传入给新组件的 key 属性，这样当 props 变化时，新组件会重新渲染并重置 state。
-
