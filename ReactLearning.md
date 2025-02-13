# ReactLearning

## React JSX
React使用JSX来替代常规的JavaScript。JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。  
JSX有以下优点：
- JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
- 它是类型安全的，在编译过程中就能发现错误。
- 使用 JSX 编写模板更加简单快速。
### JSX 语法
1. 可以在变量中插入HTML标签
2. JSX 也是一个表达式, 类型为 `ReactElement`，可以作为参数传递
```jsx
const element
    = <h1>
        Hello, {user}
        {user ? '!' : '.'}
        </h1>;
```
4. 可以使用大括号 `{}` 在 JSX 中嵌入表达式
```jsx
const element = <h1>{getGreeting(user)}</h1>;
```
5. JXS可以使用内联样式，样式名使用驼峰命名
```jsx
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
const root = React.createRoot(document.getElementById('root'));
root.render(
    <h1 style={myStyle}>Hello World!</h1>
);
```


## React 组件
React 组件是构建 React 应用的基本单位。
组件可以是函数组件或者类组件。
### 函数组件
函数组件是一个接受 props 对象并返回 React 元素的函数。
```jsx
import React from 'react';
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
```
### 类组件
类组件是一个类，类中必须包含一个 render() 方法，render() 方法返回一个 React 元素。
```jsx
import React from 'react';
class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>;
    }
}
```
### 复合组件
组件可以在其输出中引用其他组件。这可以让我们用相同组件抽象出任意层次的细节。
```jsx
import React from 'react';
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

const root = React.createRoot(document.getElementById('root'));
root.render(<App />);
```
### 组件生命周期
#### 生命周期
React 组件有三个生命周期阶段：
1. 挂载阶段：组件被创建并插入到 DOM 中。
2. 更新阶段：组件被重新渲染。
3. 卸载阶段：组件被从 DOM 中移除。
#### 钩子函数
React 组件有一些钩子函数，用于在组件的生命周期中执行一些操作，这些也是React.Component中可以重写的方法。
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

### 组件的状态
组件的状态是一个对象，包含组件的一些数据。组件的状态可以通过 `this.state` 访问。
```jsx
// 类组件的状态
import React from 'react';
class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = {date: new Date()};
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
import React, { useState } from 'react';
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
### Props
Props 是 React 组件的输入，是一个对象，包含组件的一些数据。Props 通过父组件传递给子组件，是只读的，不能修改。
```jsx
import React from 'react';
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
const element = <Welcome name="React" />;
```
Props 和 State 主要区别在于 Props 是不可变的，而 State 可以根据与用户交互来改变。
- 默认Props: `Component.defaultProps = {}`
- 多个Props
```jsx
function Welcome(props) {
    return (
        <div>
            <h1>Hello, {props.name}</h1>
            <h2>{props.url}</h2>
        </div>
    )
}
const element = <Welcome name="React" url="https://reactjs.org/" />;
```
- propTypes验证: 通过引入prop-types库，可以对props进行类型验证
```jsx
import PropTypes from 'prop-types';
Welcome.propTypes = {
    name: PropTypes.string,
    url: PropTypes.string
};
```
- 传递函数作为props
```jsx
function Welcome(props) {
    return <button onClick={props.clickMethod}>Click Me</button>;// clickMethod为父组件传给子组件的方法名,通过`props.methodName`调用
}
function App() {
    function handleClick() {
        alert('Clicked');
    }
    return <Welcome clickMethod={handleClick} />;// handleClick为父组件的方法, 通过`methodName={}`调用
}
```
- 解构props
```jsx
function Welcome({name, url}) {
    return (
        <div>
            <h1>Hello, {name}</h1>
            <h2>{url}</h2>
        </div>
    )
}
const App= () => {
    return <Welcome name="React" url="https://reactjs.org/" />;
}
```

## 事件处理
React 事件处理和 DOM 事件处理类似，但有一些语法上的区别。
1. React 事件的命名采用驼峰命名法，而不是小写。
2. 如果要阻止事件冒泡，不能使用 `return false`，而是调用 `event.stopPropagation()` 或 `event.preventDefault()`。
3. 添加监听器时不需要使用 `addEventListener`，而是直接在 JSX 中添加。
4. 使用类组件时，事件处理器会成为类的一个方法，需要绑定this。
```jsx
import React from 'react';
class Toggle extends React.Component {
    constructor(props) {
        super(props);
        this.state = {isToggleOn: true};
        this.handleClick = this.handleClick.bind(this); // 必须绑定才能在方法中使用this
    }
    handleClick() {
        this.setState(state => ({
            isToggleOn: !state.isToggleOn
        }));
    }
    render() {
        return (
            <button onClick={this.handleClick}>
                {this.state.isToggleOn ? 'ON' : 'OFF'}
            </button>
        );
    }
}
```
若不想绑定this，可以使用属性初始化器语法或者箭头函数
```jsx
// 属性初始化器语法
class Toggle extends React.Component {
    handleClick = () => {
        console.log('this is:', this);
    }
    render() {
        return (
            <button onClick={this.handleClick}>
                Click me
            </button>
        );
    }
}
// 箭头函数
class Toggle extends React.Component {
    handleClick() {
        console.log('this is:', this);
    }
    render() {
        return (
            <button onClick={(e) => this.handleClick(e)}>
                Click me
            </button>
        );
    }
}
```
5. 传递参数
事件处理函数可以接收参数，有两种方式:
```jsx
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```
当第一种方式使用时，事件对象e必须显式传递，而第二种方式不需要传递事件对象。
函数e接收参数时，事件对象e必须放在参数的最后。

## 条件渲染和列表渲染
### 条件渲染
React的条件渲染和JavaScript中的条件语句类似，可以使用if语句或者三元运算符。
```jsx
import React from 'react';
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
            {isLoggedIn ? (
                <h1>Welcome back!</h1>
            ) : (
                <h1>Please sign up.</h1>
            )}
        </div>
    );
}
```
### 列表渲染
React中使用js的循环语句，比如for,map等来渲染列表。循环时需要给每个元素添加一个key属性，且key属性值必须是唯一的。
```jsx
import React from 'react';
function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
        <li key={number.toString()}>{number}</li>
    );
    return <ul>{listItems}</ul>;
}
const numbers = [1, 2, 3, 4, 5];
const element = <NumberList numbers={numbers} />;
```


