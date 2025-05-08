# WorkRecord

## StoryBook, historie

这种类似的文档开发工具可以独立于项目的形式实现组件独立可视化，并且还可以给 prop,slot 等添加自定义显示。

```js
export default {
    title: '工具名称',
    component: 组件名称,
    tags: [], // 可以包括'autodocs'(自动文档)等
    argTypes: {
        // props
        prop1: {
            control: { // 表示该属性的控制方式
                type: '', // 表示该属性的类型，常见的有'select'(下拉框), 'text'(文本框)等
            },
            options: [], // 该属性的选项，只有type为'select'时才有效
        },
        ...
    },
    args: {
        // emit
        emit1: fn(), // 表示该属性的回调函数
    }
```

## CI/CD

## 大模型的前端构建

打字机、组件组装、流式 API
### 打字机
打字机指的是大模型输出的文字在前端展示时，需要一个打字机效果，即逐字显示，而不是一次性显示所有内容。这种效果可以给用户一种沉浸式的体验，让他们感觉自己正在与大模型进行对话。

### 流式 API
流式API指的是大模型API的流式响应，即返回的数据是分块返回的，而不是一次性返回的。这种API在处理大模型时非常有用，因为它可以避免一次性加载所有数据而导致的性能问题。
```js
/* fetch 发起请求 */
const fetchStreamData = async (prompt) => {
    const response = await fetch("https://api.openai.com/v1/completions", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer YOUR_API_KEY`,
        },
        body: JSON.stringify({
            model: "gpt-4",
            prompt: prompt,
            stream: true, // 启用流式响应
        }),
    });

    // 检查响应状态
    if (!response.ok) {
        throw new Error("Network response was not ok");
    }

    // 获取响应的可读流并处理流数据
    const reader = response.body.getReader();
    const decoder = new TextDecoder("utf-8");
    let done = false;

    while (!done) {
        // 读取流中的下一个数据块
        const { value, done: readerDone } = await reader.read();
        done = readerDone;

        // 将数据块解码为字符串
        const chunk = decoder.decode(value, {
            stream: true,
        });
        // ***** 这需要注意，各个大模型的分块数据结构可能不一样，甚至会有可能出现部分数据的情况，要单独兼容和处理哦
        // 以及有些模型内容的路径不一样，一次性响应在content，但是流式在delta字段下
    }
};

/* 逐步更新 */
const chatBox = document.getElementById("chat-box");
const updateChat = (text) => {
    // 将新数据块追加到界面上
    chatBox.innerHTML += `<p>${text}</p>`;
};
// 在逐块接收时更新
while (!done) {
    const { value, done: readerDone } = await reader.read();
    const chunk = decoder.decode(value, {
        stream: true,
    });
    updateChat(chunk); // 实时更新聊天框
}
```

## 逆向函数获取元素位置信息

通过逆向函数获取元素位置信息的方法是通过 JavaScript 的 DOM 操作来获取元素的位置信息，逆向位置获取函数，通过点击事件获取元素的位置信息。

## v-if, v-for 和 ref([]) 使用时出现的问题