## 一.引入：
react本身是一个非常轻量级的视图层框架，因为组件传值太麻烦了。在react基础上配套一个数据层的框架和他一起结合使用，才能做大型项目。用Redux，组件传值变简单，redux要求把数据都放在一个公共的存储区域Store，组件之中尽量少放数据，所有组件的数据都不放在组件自身，都放在公用的存储空间里面store这里。想要改变数据传递给其他组件，一个组件只需要改变store里面对应的数据就行了，接着其他组件会自动感知到store有变化，store只要一有变化，其他组件就会自动的去store里面重新取数据，这样就能非常轻松的在租件之间传值，简化数据的传递。间接的实现在组件之间传递数据的功能。

```

Redux=Reducer+Flux//Flux实际上就是官方推出的最原始的一个辅助react使用的数据层框架，他的公共数据存储区域store这个部分可以由很多的store组成，这样数据存储的时候可能存在数据依赖的问题，不是很好用。于是把Flux升级成Redux， Redux在引用了很多Flux的概念之外又引入了reducer这个概念。

```

## 二. Redux的工作流程（Redux是数据层的框架，把所有数据放在Store之中）


![clipboard.png](https://upload-images.jianshu.io/upload_images/17165819-3f637de013d05b83.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Redux是解决数据传递问题的一个框架，把所有数据放在Store之中进行管理。
- React Components：借书的用户
- Action Creators:你说的想要借什么书这句话
- Store:图书馆的管理员，最重要的一个环节，优先编写这个环节
- Reducers:书放在哪里的记录本
 首先有一个组件，要去**获取**Store中的一些数据，跟Store说我要获取一些数据这句话就是Action Creators，Action Creators创建了一句话之后，告诉了Store，Store接收到你要一些数据之后得去Reducers查一下应该给组件什么数据，Store知道后把对应的数据给到组件就可以了。
**改变**store的数据是一样的：你的组件先跟store说我要改变你的数据（通过Action Creators说），Store知道后，去问Reducers，store的数据应该如何被修改，store数据修改好之后告诉组件说数据修改完了可以重新获取一下数据，组件再来获取数据可以取到最新的数据。![clipboard2.png](https://upload-images.jianshu.io/upload_images/17165819-8a2c239087933ed8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
首先，用户发出 Action。

```
store.dispatch(action);
```
然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action。 Reducer 会返回新的 State 。

```
let nextState = todoApp(previousState, action);
```
State 一旦有变化，Store 就会调用监听函数。


```
// 设置监听函数
store.subscribe(listener);
```
listener可以通过store.getState()得到当前状态。如果使用的是 React，这时可以触发重新渲染 View。

```
function listerner() {
  let newState = store.getState();
  component.setState(newState);   
}
```
## 三、基本概念和 API

### 3.1 Store

Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store。

Redux 提供`createStore`这个函数，用来生成 Store。

> ```
> 
> import { createStore } from 'redux';
> const store = createStore(fn);
> 
> ```

上面代码中，`createStore`函数接受另一个函数作为参数，返回新生成的 Store 对象。

### 3.2 State

`Store`对象包含所有数据。如果想得到某个时点的数据，就要对 Store 生成快照。这种时点的数据集合，就叫做 State。

当前时刻的 State，可以通过`store.getState()`拿到。

> ```
> 
> import { createStore } from 'redux';
> const store = createStore(fn);
> 
> const state = store.getState();
> 
> ```

Redux 规定， 一个 State 对应一个 View。只要 State 相同，View 就相同。你知道 State，就知道 View 是什么样，反之亦然。

### 3.3 Action

State 的变化，会导致 View 的变化。但是，用户接触不到 State，只能接触到 View。所以，State 的变化必须是 View 导致的。Action 就是 View 发出的通知，表示 State 应该要发生变化了。

Action 是一个对象。其中的`type`属性是必须的，表示 Action 的名称。其他属性可以自由设置，社区有一个[规范](https://github.com/acdlite/flux-standard-action)可以参考。

> ```
> 
> const action = {
>   type: 'ADD_TODO',
>   payload: 'Learn Redux'
> };
> 
> ```

上面代码中，Action 的名称是`ADD_TODO`，它携带的信息是字符串`Learn Redux`。

可以这样理解，Action 描述当前发生的事情。改变 State 的唯一办法，就是使用 Action。它会运送数据到 Store。

### 3.4 Action Creator

View 要发送多少种消息，就会有多少种 Action。如果都手写，会很麻烦。可以定义一个函数来生成 Action，这个函数就叫 Action Creator。可以拆分出actionTypes写在actionTypes.js里面

> ```
> 
> const ADD_TODO = '添加 TODO';
> 
> function addTodo(text) {
>   return {
>     type: ADD_TODO,
>     text
>   }
> }
> 
> const action = addTodo('Learn Redux');
> 
> ```

上面代码中，`addTodo`函数就是一个 Action Creator。

### 3.5 store.dispatch()

`store.dispatch()`是 View 发出 Action 的唯一方法。

> ```
> 
> import { createStore } from 'redux';
> const store = createStore(fn);
> 
> store.dispatch({
>   type: 'ADD_TODO',
>   payload: 'Learn Redux'
> });
> 
> ```

上面代码中，`store.dispatch`接受一个 Action 对象作为参数，将它发送出去。

结合 Action Creator，这段代码可以改写如下。

> ```
> 
> store.dispatch(addTodo('Learn Redux'));
> 
> ```

## 3.6 Reducer

Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer。

Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。

> ```
> 
> const reducer = function (state, action) {
>   // ...
>   return new_state;
> };
> 
> ```

整个应用的初始状态，可以作为 State 的默认值。下面是一个实际的例子。

> ```
> 
> const defaultState = 0;
> const reducer = (state = defaultState, action) => {
>   switch (action.type) {
>     case 'ADD':
>       return state + action.payload;
>     default: 
>       return state;
>   }
> };
> 
> const state = reducer(1, {
>   type: 'ADD',
>   payload: 2
> });
> 
> ```

上面代码中，`reducer`函数收到名为`ADD`的 Action 以后，就返回一个新的 State，作为加法的计算结果。其他运算的逻辑（比如减法），也可以根据 Action 的不同来实现。

实际应用中，Reducer 函数不用像上面这样手动调用，`store.dispatch`方法会触发 Reducer 的自动执行。为此，Store 需要知道 Reducer 函数，做法就是在生成 Store 的时候，将 Reducer 传入`createStore`方法。

> ```
> 
> import { createStore } from 'redux';
> const store = createStore(reducer);
> 
> ```

上面代码中，`createStore`接受 Reducer 作为参数，生成一个新的 Store。以后每当`store.dispatch`发送过来一个新的 Action，就会自动调用 Reducer，得到新的 State。

为什么这个函数叫做 Reducer 呢？因为它可以作为数组的`reduce`方法的参数。请看下面的例子，一系列 Action 对象按照顺序作为一个数组。

> ```
> 
> const actions = [
>   { type: 'ADD', payload: 0 },
>   { type: 'ADD', payload: 1 },
>   { type: 'ADD', payload: 2 }
> ];
> 
> const total = actions.reduce(reducer, 0); // 3
> 
> ```

上面代码中，数组`actions`表示依次有三个 Action，分别是加`0`、加`1`和加`2`。数组的`reduce`方法接受 Reducer 函数作为参数，就可以直接得到最终的状态`3`。

### 3.7 纯函数

Reducer 函数最重要的特征是，它是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出。

纯函数是函数式编程的概念，必须遵守以下一些约束。

> *   不得改写参数
> *   不能调用系统 I/O 的API
> *   不能调用`Date.now()`或者`Math.random()`等不纯的方法，因为每次会得到不一样的结果

由于 Reducer 是纯函数，就可以保证同样的State，必定得到同样的 View。但也正因为这一点，Reducer 函数里面不能改变 State，必须返回一个全新的对象，请参考下面的写法。

> ```
> 
> // State 是一个对象
> function reducer(state, action) {
>   return Object.assign({}, state, { thingToChange });
>   // 或者
>   return { ...state, ...newState };
> }
> 
> // State 是一个数组
> function reducer(state, action) {
>   return [...state, newItem];
> }
> 
> ```

最好把 State 对象设成只读。你没法改变它，要得到新的 State，唯一办法就是生成一个新对象。这样的好处是，任何时候，与某个 View 对应的 State 总是一个不变的对象。

### 3.8 store.subscribe()

Store 允许使用`store.subscribe`方法设置监听函数，一旦 State 发生变化，就自动执行这个函数。

> ```
> 
> import { createStore } from 'redux';
> const store = createStore(reducer);
> 
> store.subscribe(listener);
> 
> ```

显然，只要把 View 的更新函数（对于 React 项目，就是组件的`render`方法或`setState`方法）放入`listen`，就会实现 View 的自动渲染。

`store.subscribe`方法返回一个函数，调用这个函数就可以解除监听。

> ```
> 
> let unsubscribe = store.subscribe(() =>
>   console.log(store.getState())
> );
> 
> unsubscribe();
> 
> ```

## 四、Store 的实现

上一节介绍了 Redux 涉及的基本概念，可以发现 Store 提供了三个方法。

> *   store.getState()
> *   store.dispatch()
> *   store.subscribe()

> ```
> 
> import { createStore } from 'redux';
> let { subscribe, dispatch, getState } = createStore(reducer);
> 
> ```

`createStore`方法还可以接受第二个参数，表示 State 的最初状态。这通常是服务器给出的。

> ```
> 
> let store = createStore(todoApp, window.STATE_FROM_SERVER)
> 
> ```

上面代码中，`window.STATE_FROM_SERVER`就是整个应用的状态初始值。注意，如果提供了这个参数，它会覆盖 Reducer 函数的默认初始值。

下面是`createStore`方法的一个简单实现，可以了解一下 Store 是怎么生成的。

> ```
> 
> const createStore = (reducer) => {
>   let state;
>   let listeners = [];
> 
>   const getState = () => state;
> 
>   const dispatch = (action) => {
>     state = reducer(state, action);
>     listeners.forEach(listener => listener());
>   };
> 
>   const subscribe = (listener) => {
>     listeners.push(listener);
>     return () => {
>       listeners = listeners.filter(l => l !== listener);
>     }
>   };
> 
>   dispatch({});
> 
>   return { getState, dispatch, subscribe };
> };
> 
> ```

## 五、Reducer 的拆分

Reducer 函数负责生成 State。由于整个应用只有一个 State 对象，包含所有数据，对于大型应用来说，这个 State 必然十分庞大，导致 Reducer 函数也十分庞大。

请看下面的例子。

> ```
> 
> const chatReducer = (state = defaultState, action = {}) => {
>   const { type, payload } = action;
>   switch (type) {
>     case ADD_CHAT:
>       return Object.assign({}, state, {
>         chatLog: state.chatLog.concat(payload)
>       });
>     case CHANGE_STATUS:
>       return Object.assign({}, state, {
>         statusMessage: payload
>       });
>     case CHANGE_USERNAME:
>       return Object.assign({}, state, {
>         userName: payload
>       });
>     default: return state;
>   }
> };
> 
> ```

上面代码中，三种 Action 分别改变 State 的三个属性。

> *   ADD_CHAT：`chatLog`属性
> *   CHANGE_STATUS：`statusMessage`属性
> *   CHANGE_USERNAME：`userName`属性

这三个属性之间没有联系，这提示我们可以把 Reducer 函数拆分。不同的函数负责处理不同属性，最终把它们合并成一个大的 Reducer 即可。

> ```
> 
> const chatReducer = (state = defaultState, action = {}) => {
>   return {
>     chatLog: chatLog(state.chatLog, action),
>     statusMessage: statusMessage(state.statusMessage, action),
>     userName: userName(state.userName, action)
>   }
> };
> 
> ```

上面代码中，Reducer 函数被拆成了三个小函数，每一个负责生成对应的属性。

这样一拆，Reducer 就易读易写多了。而且，这种拆分与 React 应用的结构相吻合：一个 React 根组件由很多子组件构成。这就是说，子组件与子 Reducer 完全可以对应。

Redux 提供了一个`combineReducers`方法，用于 Reducer 的拆分。你只要定义各个子 Reducer 函数，然后用这个方法，将它们合成一个大的 Reducer。

> ```
> 
> import { combineReducers } from 'redux';
> 
> const chatReducer = combineReducers({
>   chatLog,
>   statusMessage,
>   userName
> })
> 
> export default todoApp;
> 
> ```

上面的代码通过`combineReducers`方法将三个子 Reducer 合并成一个大的函数。

这种写法有一个前提，就是 State 的属性名必须与子 Reducer 同名。如果不同名，就要采用下面的写法。

> ```
> 
> const reducer = combineReducers({
>   a: doSomethingWithA,
>   b: processB,
>   c: c
> })
> 
> // 等同于
> function reducer(state = {}, action) {
>   return {
>     a: doSomethingWithA(state.a, action),
>     b: processB(state.b, action),
>     c: c(state.c, action)
>   }
> }
> 
> ```

总之，`combineReducers()`做的就是产生一个整体的 Reducer 函数。该函数根据 State 的 key 去执行相应的子 Reducer，并将返回结果合并成一个大的 State 对象。

下面是`combineReducer`的简单实现。

> ```
> 
> const combineReducers = reducers => {
>   return (state = {}, action) => {
>     return Object.keys(reducers).reduce(
>       (nextState, key) => {
>         nextState[key] = reducers[key](state[key], action);
>         return nextState;
>       },
>       {} 
>     );
>   };
> };
> 
> ```

你可以把所有子 Reducer 放在一个文件里面，然后统一引入。

> ```
> 
> import { combineReducers } from 'redux'
> import * as reducers from './reducers'
> 
> const reducer = combineReducers(reducers)
> ```
## 六. redux设计和使用的三项原则：
- store是唯一的
- 只有store能够改变自己的内容：不是reducer更新的，而是store拿到reducer返回的数据自己对自己更新
- reducer必须是纯函数：纯函数指给定固定的输入，就一定有固定的输出，而且不会有任何的副作用，一旦函数里有setTimeout或者Ajax请求或者和日期相关的，不再是一个纯函数，reducer里面不能有异步操作和时间相关的操作。对参数的修改就是副作用
##七. redux中核心的api：
- createStore:帮助创建store
- store.dispatch:store里面的方法，帮助我们派发action，这个action会传递给store
- store.getState:帮助我们去获取store里面所有的数据内容
- store.subscribe:可以让我们订阅store的改变，只要store发生改变，store.subscribe这个函数接受到的这个回调函数就会被执行
## 八. react中UI组件与容器组件的拆分：更容易维护
- UI组件（傻瓜组件）：负责页面的渲染，不负责逻辑
- 容器组件（聪明组件）：负责页面的逻辑，不负责UI，只用ui组件而已，负责整个组建的功能实现
## 九.中间件
##### 9.1. 
到底什么是Redux中间件：action和store之间，是dispatch这个方法，中间件是对dispatch的一个封装，或者对dispatch方法的一个升级，比如：使用redux-thunk对dispatch做了一个升级，根据参数不同做不同的事情。当调用dispatch方法，且传递的参数是一个对象的话，dispatch会直接把这个对象传给store。假设传给dispatch的是一个函数，不会把这个函数直接传递给store，它会让你这个函数先执行，执行完需要调用store的时候再去调用store，还有很多中间件
- redux-thunk: 把异步操作放在action中去操作
- redux-logger:可以记录action每一次派发的日志，对dispatch做了升级，在每次传递给store之前（在派发每个action的时候），把action打印出来在控制台
- redux-saga:解决react中异步问题的中间件。单独把异步逻辑拆分出来放到另一个文件里进行管理
##### 9.2.
 使用Redux-thunk中间件进行ajax请求发送：遇到异步请求或者非常复杂的逻辑，移除到其他地方（actionCreators）进行统一管理，做自动化测试的时候会变得简单，比测试生命周期函数简单Redux-thunk这个中间件可以把异步请求或者复杂的逻辑放到action里去处理，把异步操作的代码从组件里移除到action里面去，使用redux-thunk后，action可以不是返回一个对象，==而可以返回函数==，函数里可以做异步操作，还有要去调用这个函数。把异步函数放在组建的生命周期函数里面，这个函数会变得越来越复杂，组件变得越来越大，
```
componentDidMount() {
         const action = getTodoList();
         store.dispatch(action);//当调用store.dispatch，把action发给store时，store发现这不是一个对象，action就会被自动执行，action就是一个函数，这个函数会发一个请求
         //对比
        //  axios.get('/list.json').then((res)=>{
        //    const data = res.data;
        //    const action = initListAction(data);
        //    store.dispatch(action);
        //  })
     }
//actionCreators里面的
export const getTodoList = () => {
   return (dispatch) => {
      axios.get('/list.json').then((res)=>{//当你调用getTodoList生成一个内容是函数的这种action的时候，这个函数能接收到store的dispatch方法
         const data = res.data;
         const action = initListAction(data);//可以直接用这个方法
         dispatch(action);//把action传给store，store判断action这是一个对象，故直接接收这个对象，改变他原始的状态
       }) 
   }
};
```

- 安装：npm install redux-thunk
- 重启：npm run start
- 安装好后使用：创建store的时候使用这个中间件，引入applyMiddleware
- 引入redux-thunk模块
- 创建store的时候，在store的第二个参数里填写一个applyMiddleware(thunk))
```
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
const store = createStore(
    reducer,
    applyMiddleware([thunk, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()])
    );//创建store的时候使用reucer构建初始的数据，然后在创建store的时候store会使用一个中间件thunk。把thunk写成数组的形式，__REDUX_DEVTOOLS_EXTENSION__也是一个redux的中间件
```
- 什么时候用==redux的中间件==：通过redux创建store的时候要使用
- 使用多个中间件，redux-devtools也是中间件，使得store既支持window下的devtools，可以去调试store，又引入了redux-thunk
```
import { createStore, applyMiddleware,  compose } from 'redux';
import reducer from './reducer';
import thunk from 'redux-thunk';
const composeEnhancers =window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose;
const enhancer = composeEnhancers(
    applyMiddleware(thunk),
    // other store enhancers if any
  );
  const store = createStore(reducer, enhancer);
export default store;
```
##### 9.3.
 Redux-saga中间件的使用：[做异步代码拆分的中间件](https://github.com/redux-saga/redux-saga)
- 安装：npm install --save redux-saga
- 使用：先引入方法createSagaMiddleware（帮助创建中间件）  import createSagaMiddleware from 'redux-saga'
- 创建中间件：const sagaMiddleware = createSagaMiddleware()
- 如何用这个中间件：
```
const enhancer = composeEnhancers(
    // applyMiddleware(thunk),
    applyMiddleware(sagaMiddleware),
);
```
- 创建saga文件：在redux-saga里面，会把异步逻辑放在单独的地方（sagas.ja）去管理
- 引入saga：import todoSagas from './sagas';
- 调用sagaMiddleware.run(todoSagas)方法，让saga文件执行起来
- saga里的内容：先只写一个generetor函数，saga这个文件写法必须要求里面的函数是generator函数
```
function* mySaga() {
  }
  
  export default mySaga;
```
- 不只reducer可以接收到action，sagas.js文件里面也可以接收到action
- 在saga这个文件里面引入takeEvery这个方法：import { takeEvery } from 'redux-saga/effects';
- generator函数里面要使用yield这样一个语法yield takeEvery("USER_FETCH_REQUESTED", fetchUser);takeEvery意思是去捕捉每一个，"USER_FETCH_REQUESTED"是action的类型，只要接收到一个某个类型的action的话，就会执行fetchUser这个方法，可以通过takeEvery去捕获到每一次派发出来的action
```
function* mySaga() {
    yield takeEvery(GET_INIT_LIST, getInitList);
  }//在getInitList这个函数里面去发Ajax请求
```
- 代替store.dispatch(action);：put(action);要先引入put方法import { takeEvery, put } from 'redux-saga/effects';
- 在generator里面做异步请求不要使用promise这种形式
```
function* getInitList()  {
    const res = yield axios.get('/list.json');//yield会等待你Ajax数据获取完毕，把结果直接存在res里面（取数据）
    const action = initListAction(res.data);//取完把数据结果再创建一个action派发给store
    yield put(action);}//等action处理完成之后再继续往下执行代码（派发给store）
```


```
 //对Ajax的失败做处理
    try {
        const res = yield axios.get('/list.json');
        const action = initListAction(res.data);
        yield put(action);//把异步代码写在try里面
    }catch(e) {
    console.log('list.json 网络请求失败');
    } 
```
- redux-saga比redux-thunk复杂得多，redux-saga里有非常多的api，call, put, takeEvery, takeLatest ，但是处理大型项目时，单独弄文件来管理复杂的业务逻辑会更好，但是redux-thunk没有什么api,让我们在action里面返回的内容既可以是对象也可以是函数
## 十. React-Redux的使用：
React-Redux是第三方的模块，帮助我们在react中更方便的使用redux，
- 安装：npm add react-redux
- 重启服务器：npm run start
- Provider是react-redux提供的第一个核心api，Provider的意思是：我这个提供器连接了store，那么我这个Provider里面所有的组件都有能力获取到store里面的内容，
```
//index.js里面的内容
import React from 'react';
import ReactDOM from 'react-dom';      
// import App from './App';
import TodoList2 from './TodoList2';
import { Provider } from 'react-redux';//Provider是一个组件
import store from './store1';
const App = (
    <Provider store={store}>
        <TodoList2 />
    </Provider>
)//jsx

ReactDOM.render(App, document.getElementById('root'));//把APP作为组件传给，整个页面要渲染的是app这个组件
```
- connect是react-redux提供的第二个核心api，子组件通过connect获取到store里的数据，connect函数接收三个参数，最后一个参数是组件，代表这个组件要和store做连接，前两个参数是连接的规则。首先要把store里的数据和组件里的数据的关系在mapStateToProps里理清楚，其次把组件里面props如何对store里的数据做修改和store里的dispatch方法做关联，通过mapDispatchToProps这个函数返回的对象来做关联
```
//TodoList.js里面
import React, { Component } from 'react';
// import store from './store1';
import { connect } from 'react-redux';//引入的是react-redux之中的对象的某一部分，要做解构赋值
 class TodoList2 extends Component {

    // constructor(props) {
    //     super(props);
    //     this.state = store.getState();
    // }
     render() {
         return (
             <div>
                <div>
                    <input value={this.props.inputValue} onChange={this.props.changeInputValue}/>
                    <button>提交</button>
                    </div> 
                    <ul>
                        <li>Dell</li>
                    </ul>
                </div>
         )
     }
 }
const mapStateToProps = (state) => {
     return {
       inputValue: state.inputValue
     }
 }//mapStateToProps把store里面的数据映射给这个组件，变成组建的props，state是store里的数据
//在和store做连接的时候要有一定的连接方式。函数固定写法会接受一个state（store里的数据），return出对象。让TodoList和store做连接，连接有一个映射关系，store里面的公用数据会映射到组建的props里面，store里面的inputValue|会映射到组件里面的props的inputValue里面

//第二个参数，函数，接收的是dispatch方法，返回对象.
 //想对store的数据做修改，也可以通过store的props来做修改，Dispatch是发布，指的是store.dispatch，把store.dispatch挂载（映射到）到props上,故可以通过this.props.什么东西去调用store.dispatch方法
 const mapDispatchToProps = (dispatch) => {
    return {
        changeInputValue(e) {
        const action = {
            type: 'change_input_value',
            value: e.target.value
        }    
        dispatch(action);//改变store里的数据就要调用dispatch方法去派发action给store
        }//这个函数能调用store.dispatch方法,参数dispatch就是store.dispatch方法
    }
 }//想派发action的时候，把这样的操作放在mapDispatchToProps里面去，它可以让props里面的方法能够调用dispatch去操作store里的数据
export default connect(null, null)(TodoList);//导出connect方法，把TodoList传给这个方法。让我的TodoList组件和store进行连接，做链接就有规则，规则在mapStateToProps里面
////只需用connect方法就可以==自动==帮助我们把这个组件结合这两个规则和store做连接
//导出connect方法执行的结果
```
- React-Redux的使用：
```
const { inputValue, list, changeInputValue, handleClick } = this.props;  //解构赋值，定义一个inputValue变量，=它的值等于this.props.inputValue
```
```
//导出去的是connect方法执行的结果，导出去的是一个容器组件
export default connect(mapStateToProps, mapDispatchToProps)(TodoList2);//只需用connect方法就可以自动帮助我们把这个组件结合这两个规则和store做连接
```

connect方法把这些映射关系和业务逻辑集成到TodoList这个ui组件之中，TodoList是一个UI组件，当用connect把这个UI组件和一些数据和业务逻辑相结合的时候，返回的内容（connect方法执行生成的内容的结果）实际是一个容器组件，容器组件对UI组件进行包装，去调用这个UI组件，在调用时把数据和方法都准备好了
## 十一. 使用combineReducers完成对数据的拆分管理：
- 搜索GitHub上面的redux-devtools-exten，点击进入redux-devtools-extension插件，compose这个函数在redux这个库里面存在，compose实际是一个包装函数，可以向这个函数里面传递很多方法，传递的方法会依次执行，想用redux去调试就要装redux-devtools-extension插件。这个工具有时光穿梭机的功能，之前的操作可以帮助你复现，
- 不能让reducer变得太大，redux提供一个新方法，把一个手册拆分成很多小手册进行管理，按分类去拆分。
- store下的reducer要整合小的reducer，把他聚合成一个大的笔记本
- redux提供的函数combineReducers,它可以把一些小的reducer合并成大的reducer，调用这个方法合并。combineReducers会把小的reducer做一个整合然后生成一个最终的reducer出来。
- 把跟header相关的数据和操作放到了headerReducer里面去，在header下创建一个store文件夹，再建一个reducer.js存放的是header相关的默认数据和对数据的操作，然后拿到headerRedux对他做一个整合，整合出一个大的reducer，
- store下面的index.js是header的store部分的一个出口文件，可以通过引用store下面的index.js来间接引入reducer,
```
import { combineReducers } from 'redux';
import headerReducer from '../common/header/store/reducer';

export default combineReducers({
  header: headerReducer
})



//其他写法
import { combineReducers } from 'redux';
import headerReducer from '../common/header/store/reducer';



// import headerReducer from '../common/header/store/reducer';
//会自动到store下面找index.js，index.js恰好道出了reducer，可以直接引入reducer，减少目录结构
//reducer as headerReducer起别名,as是压缩的语法
import { reducer as headerReducer } from '../common/header/store';



// export default combineReducers({
//   header: headerReducer
// })
const reducer =  combineReducers({
  header: headerReducer
});
//导出整合后的大的reducer
export default reducer;
```
