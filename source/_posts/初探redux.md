---
title: 初探redux
date: 2016-07-14 11:34:52
categroies: 归纳整理
tags: [redux]
---

#### 初探redux

1. 三大原则

   - 单一数据源

     整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中。

     来自服务端的 state 可以无需编写更多代码的情况下被序列化并注入客户端中。

   - State 是只读的

     唯一改变 state 的方法就是触发 action ，action 是一个用于描述已发生事件的普通对象。

     所有的修改都被集中化处理，且按照一个接一个的顺序执行，不用担心 race condition 的出现。

     Action 就是普通对象，可以被 console 打印、序列化、储存、后期调试。

   - 使用纯函数来执行修改

   - 为了描述 action 如何改变 state tree，需要编写 reducers

   - Reducer 只是一些纯函数，它接收先前的 state 和 action，并返回新的 state。

   - 因为 reducer 只是函数，你可以控制它们被调用的顺序，传入附加数据，甚至编写可复用的 reducer 来处理一些通用任务，如分页器。

2. 先前技术

   - Redux 的灵感来源于 Flux 的几个重要特性。和 Flux 一样，Redux 规定，将模型的更新逻辑全部集中于一个特定的层（Flux 里的 store，Redux 里的 reducer）。Flux 和 Redux 都不允许程序直接修改数据，而是用一个叫作 “action” 的普通对象来对更改进行描述。

   - **Redux 并没有 dispatcher 的概念**。原因是它依赖纯函数来替代事件处理器。纯函数构建简单，也不需额外的实体来管理它们。你可以将这点看作这两个框架的差异或细节实现，取决于你怎么看 Flux。Flux 常常[被表述为 `(state, action) => state`](https://speakerdeck.com/jmorrell/jsconf-uy-flux-those-who-forget-the-past-dot-dot-dot)。从这个意义上说，Redux 无疑是 Flux 架构的实现，且得益于纯函数而更为简单。

   - 应该在 reducer 中返回一个新对象来更新 state 。

     ```javascript
     const counter = (state = 0, action) => {
       switch (action.type) {
         case 'INCREMENT':
           return state + 1;
         case 'DECREMENT':
           return state - 1;
         default:
           return state;
       }
     }

     const { createStore } = Redux;
     const store = createStore(counter);
     const render = () => {
       document.body.innerText = store.getState();
     }

     console.log(store.getState());
     // 0 

     store.dispatch({ type: 'INCREMENT' });
     console.log(store.getState());
     // 1

     store.subscribe(render);
     render();

     document.addEventListener('click', ()=> {
       store.dispatch({ type: 'INCREMENT' });
     })

     expect(
     	counter(0, { type: 'INCREMENT' })
     ).toEqual(1);

     expect(
     	counter(1, { type: 'INCREMENT' })
     ).toEqual(2);

     expect(
     	counter(2, { type: 'DECREMENT' })
     ).toEqual(1);

     expect(
     	counter(1, { type: 'DECREMENT' })
     ).toEqual(0);
     ```

     subscribe , getState() , render

3. 基础知识

   ![](http://f8-app.liaohuqiu.net/static/images/redux_flowchart.png)

   - **Action**

   - **Action** 是把数据从应用（译者注：这里之所以不叫 view 是因为这些数据有可能是服务器响应，用户输入或其它非 view 的数据 ）传到 store 的有效载荷。它是 store 数据的**唯一**来源。一般来说你会通过[`store.dispatch()`](http://cn.redux.js.org/docs/api/Store.html#dispatch) 将 action 传到 store。

   - ```
     const ADD_TODO = (text) => {
       return {
      	type: 'ADD_TODO',
         id: nextTodoId++,
         text
      }
     }
     ```

   - Action 本质上是 JavaScript 普通对象。我们约定，action 内必须使用一个字符串类型的 `type` 字段来表示将要执行的动作。多数情况下，`type` 会被定义成字符串常量。当应用规模越来越大时，建议使用单独的模块或文件来存放 action。

   - ```javascript
     import { ADD_TODO, REMOVE_TODO } from './actionType'
     ```

   - 我们应当尽量减少在 action 中传递数据。

   - Action 创建函数

   - ```
     function addTodo(text) {
       return {
         type: ADD_TODO,
         text
       }
     }
     ```

   - **Reducer**

   - ##### 处理 Reducer 关系时的注意事项

     >  开发复杂的应用时，不可避免会有一些数据相互引用。建议你尽可能地把 state 范式化，不存在嵌套。把所有数据放到一个对象里，每个数据以 ID 为主键，不同实体或列表间通过 ID 相互引用数据。把应用的 state 想像成数据库。这种方法在 [normalizr](https://github.com/gaearon/normalizr) 文档里有详细阐述。例如，实际开发中，在 state 里同时存放 `todosById: {只要传入参数相同，返回计算得到的下一个 state 就一定相同。没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算。 id -> todo }` 和 `todos: array` 是比较好的方式，本文中为了保持示例简单没有这样处理。

   - Action 处理

   - 确定 state 对象结构之后，就可以开始开发 reducer。reducer 就是一个纯函数，接收旧的 state 和 action，返回新的 state。

   - ```javascript
     (previousState, action) => newState
     ```

   - 之所以称作 reducer 是因为它将被传递给 [`Array.prototype.reduce(reducer, ?initialValue)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 方法。保持 reducer 纯净非常重要。**永远不要**在 reducer 里做这些操作：

     - 修改传入参数；
     - 执行有副作用的操作，如 API 请求和路由跳转；
     - 调用非纯函数，如 `Date.now()` 或 `Math.random()`。

   - **只要传入参数相同，返回计算得到的下一个 state 就一定相同。没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算。**

   - Redux 首次执行时，state 为 undefined ，此时可以借机设置并返回应用的初始 state。

   - ```javascript
     import { VisibilityFilters } from './actions'

     const initialState = {
       visibilityFilter: VisibilityFilters.SHOW_ALL,
       todos: []
     };

     function todoApp(state, action) {
       if (typeof state === 'undefined') {
         return initialState
       }

       // 这里暂不处理任何 action，
       // 仅返回传入的 state。
       return state
     }
     ```
     ​
