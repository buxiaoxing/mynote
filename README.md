### 	React

#### React概念

- 是什么

  `React` 是一个将数据渲染为 `HTML` 视图的开源的 `JS` 库

- 为什么用

  1. 原生 JS 操作 DOM 繁琐、效率低（DOM-API 操作 UI）
  2. 使用 JS 直接操作 DOM ，浏览器会进行大量的重绘重排
  3. 原生 JS 没有组件化编码方案，代码复用率低

- 特点

  1. 采用组件化模式、声明式编程，提高开发效率及组件复用率
     - 声明式编程与命令式编程
  2. 在 React Native 中可以使用 React 语法进行移动端开发
  3. 使用虚拟 DOM + 优秀的 Diffing 算法，尽量减少与真实的 DOM 的交互



#### React 涉及到的核心概念

- 模块化

  代码角度，可复用代码抽离为单个模块，便于项目维护和开发

- 组件化

  UI 角度，可复用的 UI 元素，抽离为单个模块

- `DOM`

  浏览器中的概念，用 JS 对象表示元素，并提供了操作元素的 API

- 虚拟 `DOM`

  框架中的概念，程序员用 JS 对象模拟页面上的 DOM 和 DOM 嵌套，来是实现页面 DOM 元素的高效更新

- DOM 树

  1. 浏览器请求服务器获取 HTML 代码
  2. 浏览器先在内存中解析 DOM 结构，并在浏览器内存中渲染一个 DOM 树
  3. 浏览器将 DOM 树呈现到页面

- JS 对象模拟 DOM 树

  手动模拟两颗新旧 DOM 树，就是虚拟 DOM 的概念

  虚拟 DOM 是以 JS 对象形式存在的

  通过对比新旧 DOM 树的不同

  从而实现页面元素的高效更新（按需更新）

- Diff 算法

  - tree diff

    逐层对比

  - component diff

    组件级别的对比

  - element diff

    组件类型相同则进行元素级别的对比
  
- 高阶组件

  参数是组件，返回值是新的组件

#### React 入门

- 官网

  [中文官网](https://react.docschina.org/)

  [英文官网](https://react.org/)

- 创建虚拟DOM的两种方式

  - js

    ```js
    const element = React.createElement('h1', null, 'Hello React')
    ```

    当有元素嵌套时，写法复杂

  - JSX

    ```jsx
    const element = (
        <h1>Hello, React!</h1>
    );
    ```

    html 的形式，写法简洁

    需要通过babel翻译成第一种形式

- 虚拟DOM

  - 本质是 Object 类型的对象
  - 虚拟DOM比较"轻"，真实DOM比较重，因为虚拟DOM是React内部在用，无需真实DOM上那么多属性
  - 虚拟DOM最终会被React转化为真实DOM，渲染到页面上

- JSX基本语法

  - 当我们需要在 `JSX` 控制区域内写 JS 表达式了，则需要把 JS 代码写到 `{}` 中，类似于要在 vue 的结构区写 js 代码，需要写在 `{{}}` 中

    ```jsx
    let a = 1
    let str = "hello world"
    const mydiv =
    <div>
        {a}
        <hr />
        {str}
        <hr />
        这是一个div
        <h1>这是H1</h1>
    </div>
    ```

    - 注意区分js语句和js表达式

      - 表达式

        一个表达式会产生一个值，可以放在任何一个需要值的地方

        ```js
        a
        a+b
        demo(1)
        arr.map()
        function test(){}
        ```

        只要拿一个变量放在左边接受，能够接受到值，那就是表达式

      - 语句（代码）

        ```js
        if(){}
        for(){}
        switch(){case:}
        ```

        

  - JSX 的注释

    `{/*注释内容*/}`

    

  - class 和 for

    JSX 中需要使用 className 代替 class 属性

    使用 htmlfor 代替 label 标签的 for 属性

    因为这两个属性名会与 Js 产生歧义

  - React 中需要把 key 添加给被循环直接控制的元素上

  - 内联样式

    ```jsx
    <span style={{color: 'white', fontSize: ''}}>hello react</span>
    ```

  - 只有一个根标签

  - 标签必须闭合

  - 标签首字母

    - 若小写字母开头，则将该标签转为html同名标签，若Html中无该标签的同名元素，则报错
    - 若大写字母开头，react就去渲染对应组件，若组件没有定义，则报错

- 开发者工具

  `React Developer Tools`

  在谷歌应用商店里下载

#### react生命周期

![image-20210706100359793](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210706100359793.png)



**只有类组件才具有生命周期方法，函数组件是没有生命周期方法的，因此永远不要在函数组件中使用生命周期方法。**

相关文章

1. 初始化阶段

   1. `constructor`

      构造函数，接受父类传过来的 `props` 属性对象，必须在这个方法中调用 `super(props)` ，通常用于初始化组件的 `state` 以及绑定事件处理方法，通常可以省略

   2. `componentWillMount`

      组件被挂在到 `dom` 前调用，只调用一次，很少调用，一般该方法中执行的工作都可以提前到 constructor 中。

   3. `render`（**常用**）

      定义组件唯一必要的方法(组件的其他生命周期方法都可省略)。在这个方法中，根据组件的 `props` 和 `state` 返回一个 `React` 元素，用于描述组件真正的 `UI` ，通常 `React` 元素使用 `JSX` 语法定义。`render` 并不负责组件的实际渲染工作，只是返回一个`UI` 描述，真正渲染出页面的 `DOM` 的工作由 `React` 自身负责。 `render` 是一个纯函数，在里面不能执行任何有副作用的操作，所以不能在 `render` 里面调用 `this.setState` ，这会改变组件的状态。

   4. `componentDidMount`（**常用**）

      类似于 `vue` 的 `mounted` 在组件被挂载到 DOM 后调用，只调用一次。这是可以获取到 `DOM` 结构，依赖`DOM`节点的操作可以放在这个方法中，这个方法还经常用于向服务器端请求数据。

    该钩子是执行组件和服务器通信的最佳地方，原因有两个：

       1. 在 `componentDidMount` 中执行服务器执行可以保证获取到数据时，组件已经处于挂载状态，这时即使要直接操作 `DOM` 也是安全的，而 `componentWillMount` 无法保证这一点。

     2. 当组件在服务器渲染时，`componentWillMount` 会被调用两次，一次在服务端，一次在浏览器端，另一次是在浏览器端，而 `componentDidMount` 能保证在任何情况下只会被调用一次，从而不会发送多余的数据请求。

2. 更新阶段

   1. `componentWillReceiveProps`

      props 引起组件更新过程中，才会被调用

   2. `shouldComponentUpdate`

      

   3. `componentWillUpdate`

      

   4. `componentDidUpdate`

3. 卸载阶段

   1. `componentWillUnmount` （**常用**）

      这个方法在组件被卸载前调用，可以在这里执行一些清理工作，比如清楚组件中使用的定时器，清除 `componentDidMount` 中手动创建的 `DOM` 元素等，以避免引起内存泄漏

- 生命周期写在组件的最开始

  ```
  class component{
      生命周期
      函数
      render()
  }
  ```

  

#### React 脚手架

> 快速创建一个模板项目

- 脚手架的作用

1. 包含了所有需要的配置(语法检查、jsx编译、devServer)
2. 下载了所有相关依赖
3. 可以直接运行得到一个简单的效果

`react` 提供了一个用于创建 `react` 项目的脚手架库：`create-react-app`

`npx create-react-app project`

项目整体架构为：`react` + `webpack` + `es6` + `eslint`

脚手架项目特点：模块化，组件化，工程化

- 脚手架目录结构分析

  `node_modeles` ：依赖包

  `public` ：静态资源

  	- `favicon.ico`  ： 图标
  	- `index.html` ： 单页面（常用）
  	- `manifest.json` ： 应用加壳
  	- `robots.txt` ： 爬虫规则文件

  `src` ： 源代码

  - `App.css` ： `App.js` 的样式文件
  - `App.js` ： 应用的最外层组件，其他组件都放在该组件内部（常用）
  - `App.test.js` ： 专门测试 `App.js` 的测试文件
  - `index.css` ： 全局样式
  - `index.js` ： 入口文件（常用）
  - `reportWebVitals.js` ： 记录页面性能
  - `setupTests.js` ： 全局测试

  综上整个项目最基础的文件就是：`index.html` `App.js` `index.js` 这3个文件。

- react 默认将所有配置项都隐藏了，修改配置可以使用命令

  `npm run eject` 将所有配置项显示出来（不可逆）



#### React 组件

- 状态提升

  > react 应用中，任何可变数据应当只有一个相对应的唯一“数据源”。通常, state 都是首先添加到需要渲染数据的组件中去。然后，如果其他组件也需要这个 state ，那么你可以将它提升至这些组件的最近共同的父组件中。依靠 **至上而下的数据流**，而不是尝试在不同组件间同步 state 

- 函数式组件

  ```jsx
  // 创建函数式组件
      function Demo(){
          return(
             <h2>我是函数定义的组件【适用于简单组件的定义】</h2> 
          )
      }
      // 渲染虚拟DOM到页面
      ReactDOM.render(<Demo/>, document.getElementById('example'));
      /*
          执行了 ReactDOM.reder(<Demo/>......之后发生了什么？)
          1. React解析组件标签，找到了Demo组件。
          2. 发现组件式使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM，随后呈现到页面上
      */
  ```

- 类式组件

  ```jsx
   // 创建类式组件(必须继承,必须写render,render必须有返回值)
      class MyComponent extends React.Component{
          // render放在类的原型上，供实例使用
          // render中的this指向MyComponent的实例对象（组件实例对象）
          render(){
              console.log(this)
              return(
                  <h2>我是类定义的组件（适用于【复杂组件】的定义）</h2>
              )
          }
      }
      // 渲染虚拟DOM到页面
      ReactDOM.render(<MyComponent />, document.getElementById('example'));
      /*
          执行了 ReactDOM.reder(<Demo/>......之后发生了什么？)
          1. React解析组件标签，找到了Demo组件。
          2. 发现组件式使用类定义的，随后new出来该类的实例，并通过该实例调用原型上的render方法
          3. 将render返回的虚拟DOM转为真实DOM，随后呈现到页面上
      */
  ```

  类的基本知识

  ```js
   /*
              总结：
              1. 类中的实例不是必须写的，要对实例进行一些初始化操作，如添加指定属性才写
              2. 如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须调用的
              3. 类中所定义的方法，都是放在了类的原型上，供类的实例使用
          */
          class Person{
              //构造器方法(定义属性)
              constructor(name, age){
                  //构造器中的this指向类的实例对象
                  this.name = name
                  this.age = age
              }
              //一般方法(行为)
              speak(){
                  //方法放在了类的原型对象上了,供实例使用，通过Person实例调用方法时，this指向实例对象
                  console.log(`我叫${this.name},我${this.age}岁`)
              }
          }
  
          // const p1 = new Person('tom', 18)
          // p1.speak()
          // console.log(p1)
  
          //创建一个Student，继承自Person
          class Student extends Person{
              constructor(name, age, grade){
                  //super 必须放在最前面
                  super(name, age)
                  this.grade = grade
                  this.school = "清华"    //所有创建的实例都是清华大学的学生
              }
  
              //重写父类方法
              speak(){
                  console.log(`我叫${this.name}，我${this.age}岁，我读${this.grade}年纪`)
              }
          }
          
          const s1 = new Student('bob', 15, '高一')
          console.log(s1)
          s1.speak()
  ```

- 组件实例的三大属性：`state`，组件的状态

  函数定义的组件没有三大属性，有没有状态是简单组件和复杂组件的区分

  - `state` 是组件对象最重要的属性，值是对象（可以包括多个 `k-v` 组合）

  - 组件被称为"状态机"，通过更新组件的 `state` 来更新对应的页面显示（重新渲染组件）

  - `state` 与自定义方法修改 `state` 的标准使用

    ```jsx
    //1.创建组件
        class Weather extends React.Component{
            //初始化状态
            state = {
                isHot: false,
                wind: "微风"
            }
    
            render(){
                return(
                    <h1 onClick={this.changeWeather}>今天天气很{this.state.isHot ? "炎热" : "凉爽"}，{this.state.wind}</h1>
                )
            }
    
    
            //自定义方法——要用赋值语句+箭头函数
            //复制语句放在了自身实例对象上，没有放在原型上
            changeWeather = () => {
                //箭头函数本身没有this，会找外一层的this
                console.log(this)
                const isHot = this.state.isHot
                this.setState({isHot: !isHot})
            }
        }
    ```

    1. 状态 `state` 不可以直接修改，要通过内置的 API `setState()` 去修改，里面的参数必须是对象，这里的修改会和原来的 `state` 对象进行合并
    2. 自定义方法一定要使用 赋值语句+箭头函数的方式来实现。
    3. `render()` 函数调用 1+ n 次，1 是页面初始化那次，n 是状态更新的次数

- 组件实例的三大属性：`props`

  > 用于外界向组件内部传值

  - 基本使用

    ```jsx
    class Person extends React.Component{
            render(){
                console.log(this)
                //对象的解析赋值
                const {name, age, sex} = this.props
                return(
                    <ul>
                        <li>姓名: {name}</li>
                        <li>年龄: {age}</li>
                        <li>性别: {sex}</li>    
                    </ul>
                )
            }
        }
        
    
        //渲染组件，单个传值
        // ReactDOM.render(<Person name = "tom" age="18" sex = "女"/>, document.getElementById("app"))
    
    
        const p = {
            name: 'jack',
            age: 20,
            sex: "女"
        }
        //只有标签属性可以使用展开运算符展开对象
        ReactDOM.render(<Person {...p}/>, document.getElementById("app"))
    ```

  - 对传入的值进行约束和默认值设定

    1. 需要一个新的外部依赖 `prop-types`

       ```html
       <!-- 对 props 进行限制 -->
       <script src="https://unpkg.com/prop-types@15.6/prop-types.js"></script>
       ```

    2. 在类的自身上添加属性

       ```jsx
       //标签属性类型，必要性限制
       Person.propTypes = {
           //这个PropTypes对象就是引入 prop-types 中的
       
           //name属性是必传的，而且必须是字符串
           name: PropTypes.string.isRequired,
           sex: PropTypes.string,
           age: PropTypes.number,
       }
       
       //指定标签默认值
       Person.defaultProps = {
           sex: '男',
           age: 18
       }
       ```

       最好将约束条件写道类的内部去(在类的内部添加类自身属性)，需要使用要 `static` 关键字

       ```jsx
       //标签属性类型，必要性限制
       static propTypes = {
           //这个PropTypes对象就是引入 prop-types 中的
       
           //name属性是必传的，而且必须是字符串
           name: PropTypes.string.isRequired,
           sex: PropTypes.string,
           age: PropTypes.number,
       }
       
       //指定标签默认值
       static defaultProps = {
           sex: '男',
           age: 18
       }
       ```

  - 函数组件中也可以使用 `props` 属性，可以通过函数的参数接收

    ```jsx
    function Home(props){
        return(
        	<h1>{props.name}</h1>
        )
    }
    ```

    

- 构造器

  - 构造器的作用

    1. 通过给 `this.state` 赋值对象来初始化内部 `state`
    2. 为事件处理函数绑定实例

    但是，这两种功能完全可以不通过构造器实现

    1. 初始化 `state` 可以之间在类里面赋值实现

       ```js
       //初始化状态
       state = {
           isHot: false,
           wind: "微风"
       }
       ```

    2. 为事件处理函数绑定实例也可以使用 赋值语句+箭头函数 的方式实现

       ```jsx
       changeWeather = () => {
           //箭头函数本身没有this，会找外一层的this
           console.log(this)
           const isHot = this.state.isHot
           this.setState({isHot: !isHot})
       }
       ```

    所以构造器完全是可以不用写的，但是一旦写了构造器，就需要在里面使用 `super(props)`

- `refs`

  > 可以拿到`dom`元素，操作`dom`元素

  - 字符串形式的 `refs`

    可以在每个元素上添加 `ref` 属性，唯一表示这个元素，并通过 `this.refs` 拿到这个元素的真实 `DOM`

    ```jsx
    alertData = () => {
        //这里拿到的是 真实 DOM
        const {input1} = this.refs
        alert(input1.value)
    }
    
    alertData2 = () => {
        const {input2} = this.refs
        alert(input2.value)
    }
    
    render(){
        return(
            <div>
                <input ref = "input1" type="text" />
                <button onClick = {this.alertData}>点击弹出左侧输入</button>    
                <input ref = "input2" onBlur = {this.alertData2} type="text" />
            </div>
        )
    }
    ```

    ![image-20210705135449241](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210705135449241.png)

  - `createRef()` 形式的 `refs`

    > `React.createRef()` 调用后可以直接返回一个容器，该容器可以存储被 ref 所标识的节点，该容器只能存一个元素

    ```jsx
    //创建 ref
    constructor(props){
        super(props)
        this.input1 = React.createRef()
    }
    
    //放在元素身上
    <input ref = {this.input1} type="text" />
    
    //获取元素
    alertData = () => {
        const input1 = this.input1.current
        console.log(input1)
        alert(input1.value)
    }
    ```

  - 回调函数形式的 `refs`

    ```jsx
    class Demo extends React.Component{
            state = {isHot: false}
    
            showInfo = ()=>{
                const {input1} = this
                alert(input1.value)
            }
    
            changeWeather = ()=>{
                const {isHot} = this.state
                this.setState({isHot: !isHot})
            }
    
            saveInput = (currentNode) => {
                this.input1 = currentNode;
                console.log('@', currentNode)
            }
    
            render(){
                const {isHot} = this.state
                return(
                    <div>
                        <h2>今天天气很{isHot ? '炎热' : '凉爽'}</h2>    
                        {/* 内联方式定义回调函数：更新的时候会调用两次该回调，第一次传入空，第二次传入DOM，但无关紧要 */}
                        {/*<input ref={(currentNode) => {this.input1 = currentNode; console.log('@', currentNode)}} type="text" />*/}
    
                        {/* 定义为 class 绑定函数，这种方式不会多那两次调用，但写法复杂点 */}
                        <input ref={this.saveInput} type="text" />
                        <button onClick = {this.showInfo}>点我提示输入的数据</button>
                        <button onClick = {this.changeWeather}>点我切换天气</button>
                    </div>
                )
            }
        }
    ```

    

  - 使用的情况

    1. 管理焦点，文本选择和媒体播放
    2. 触发强制动画
    3. 集成第三方 `DOM` 库

- 事件处理

  1. 通过 `onXxx` 属性指定事件处理函数，之一大小写
     1. `React` 使用的时自定义（合成）事件，而不是使用原生的 `DOM` 事件——为了更好的兼容性
     2. `React` 中的事件是通过事件委托方式处理的（委托给组件最外层的元素）——为了高效
  2. 通过 `event.target` 得到发生事件的 `DOM` 元素——不要过度使用 `ref`

  

  

- 高阶函数

  > 如果一个函数符合下面两个规范中的任何一个，那该函数就是高阶函数

  1. 接受的参数是一个函数
  2. 返回值为一个函数

  - 常见高阶函数：`Promise setTimeOut arr.map()...`

- 函数柯里化

  > 通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式

  

- 收集表单数据

  - 非受控组件

    输入的数据没有存在状态里，每次通过 ref 取出来，由 dom 管理表单数据

  - 受控组件

    将输入框绑定到状态里，状态里实时更新值，类似与 `vue` 的双向绑定的实现，由 react 管理表单数据
  
- `<Fragments>`

  > 代码片段，当一个组件需要返回几个子组件时，可以使用 `<Fragments>` 包裹(因为组件需要唯一的根节点)，渲染时，仍然会渲染为几个组件。

  使用

  ```jsx
  import {Fragment} from 'react'
  
  <Fragment></Fragment>	//可以写 key 属性
  <></>	//不能使用任何属性
  ```




#### 组件通信的多种方式

- `props`

  > 常用于【父子组件】通信

- `context`

  > 常用于【祖组件】和【后代组件】间通信

  使用步骤

  ```jsx
  const MyContext = React.createContext() //1. 创建 context 对象
  
  //2. 祖组件中，使用 Provider 包裹后代组件且传值
  <MyContext.Provider value={{ username, age }}>
      <B username={this.state.username} />
  </MyContext.Provider>
  
  //3. 要使用的后代组件中声明接受 context
  static contextType = MyContext; //3. 声明接受context
  
  //4. 使用
  <h4>我从A收到的用户名是 {this.context.username}，{this.context.age}岁</h4>
  ```

  函数使用 `context`

  ```jsx
  // 前两步都一样，因为函数中没有 this，所以需要一个新的标签 Consumer
  function C() {
    return (
      <div className="grand">
        <h3>我的C组件</h3>
        <h4>我从A收到的用户名是
          <MyContext.Consumer>
            {
              value => {
                return `${value.username}，年龄是${value.age}`
              }
            }
          </MyContext.Consumer>
        </h4>
      </div>
    )
  }
  ```

- `refs`

- `store`

- 发布-订阅

#### 组件优化

> component 存在两个问题
>
> 1. 只要执行`setState()`,即使不改变状态数据，像`setState({})`, 组件也会重新`render()` ==> 效率低
> 2. 只当前组件重新 `render()`, 就会自动重新 `render()` 子组件，纵使子组件没有用到父组件的任何数据 ==> 效率低

- 原因

  > `Component` 中的 `shouldComponentUpdate()` 总是返回 `true`，总是调用 `render()`

- 解决

  1. 重写 `shouldComponentUpdate()` 方法

     > 通过判断状态是否有改变来决定返回值
     >
     > 参数1，目标 props
     >
     > 参数2，目标 state

     ```js
     shouldComponentUpdate(nextProps, nextState) {
         console.log(this.state, this.props)  // 目前的state, 目前的 props
         console.log(nextState, nextProps)    // 目标 state,  目标 props
         return this.state.carName !== nextState.carName
     }
     ```

  2. 组件继承 `PureComponent`

     该父类已经帮我们重写了 `shouldComponentUpdate()` ，只有 `state` 或 `props` 数据有变化时才返回 `true`

     **注意**：

     如果 `setState(obj)` 中的 对象，和 `state` 指向同一内存地址，则直接返回 `false`，不调用 `render()`

- 组件的错误边界

  > 组件内 JavaScript 错误不应该导致整个应用崩溃
  >
  > class 组件中定义了 [`static getDerivedStateFromError()`](https://zh-hans.reactjs.org/docs/react-component.html#static-getderivedstatefromerror) 或 [`componentDidCatch()`](https://zh-hans.reactjs.org/docs/react-component.html#componentdidcatch) 这两个生命周期方法中的任意一个（或两个）时，那么它就变成一个错误边界。当抛出错误后，请使用 `static getDerivedStateFromError()` 渲染备用 UI ，使用 `componentDidCatch()` 打印错误信息。

  

#### React-Router

- 安装依赖（用于web端的路由）

  `npm install react-router-dom -s`

- `<Link />`

  - `to`：跳转的路由地址

- `<Route />`

  路由组件，一般存放在 `/pages` 文件夹里

  ```jsx
  <Route path="/about" component={About} />
  <Route path="/home" component={Home} />
  ```

  

  - `path`：路由地址
  - `component`：对应的组件

- `<BrowserRouter/>`

  上面的标签都需要包裹在这个标签内部才能实现组件跳转的效果



- `<NavLink`

  > `NavLink` 可以实现路由链接的高亮，通过 `activeClassName` 指定样式名

  - `activeClassName` ：样式名默认为 `active`，通用这个属性自定义样式名

- 封装 `NavLink`

  - `children` 属性指定标签体内容
  - `{...this.props}` 批量绑定属性

- `<Switch>`

  > 默认会查找完所有的路由，用`<Switch>` 包裹后匹配成功后就不往后找了，提高匹配效率

  ```jsx
  <Switch>
      <Route path="/home" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/news" component={News} />
  </Switch>
        
  ```

  

- `<Rdirect>`

  > 如果都没有匹配到路由，那么就跳到 `Rdirect` 指定的路径去

  ```jsx
  <Switch>
      <Route path="/home" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/news" component={News} />
      <Redirect to="/home" />
  </Switch>
  ```

- 多级路径刷新样式丢失问题

  > 加载静态资源默认是在 public 文件夹下找，找不到就返回 `index.html`

  - 引入是不要使用相对路径

    ```html
    <link rel="stylesheet" href="/css/bootstrap.css">
    ```

  - 使用 `%PUBLIC%`

    ```html
    <link rel="stylesheet" href="%PUBLIC%/css/bootstrap.css">
    ```

  - 使用 hash 模式

    > 因为hash模式将#后边的都视为前端资源，不会加入到服务器地址上去，而 history 模式只将最后一级地址视为前端资源。

    ```jsx
    <HashRouter>
        <App />
    </HashRouter>,
    ```

- 路由精准匹配与模糊匹配

  - 模糊匹配（默认）

    Link 的 to 属性 必须包含 Route 的 path 属性（从前往后的顺序）

  - 严格匹配

    > 设置 exact 属性

    `<Route exact path="/bxx/home" component={Home} />`

    一般不会开启，会影响二级路由

- 嵌套路由

  > 嵌套路由需要带上父级路由
  
  ```jsx
  <div>
      <ul className="nav nav-tabs">
          <li>
              <MyNavLink to="/home/news">News</MyNavLink>
          </li>
          <li>
              <MyNavLink to="/home/message">Message</MyNavLink>
          </li>
      </ul>
      <Switch>
          <Route path="/home/news" component={News} />
          <Route path="/home/message" component={Message} />
          <Redirect path="/home/news" />
  
      </Switch>
  </div>
  ```
  
- 路由传参

  - `params` 传参

    1. 注册路由（声明接收）

       ```jsx
       <Route path="/home/message/detail/:id/:title" component={Detail} />
       ```

    2. 路由链接（携带参数）

       ```jsx
       <Link to={`/home/message/detail/${obj.id}/${obj.title}`}>{obj.title}</Link>
       ```

    3. 接受参数

       ```jsx
       const { id, title } = this.props.match.params
       ```

       

  - `search` 传参

    1. 路由链接（携带参数）

       ```jsx
       <Link to={`/home/message/detail/?id=${obj.id}&title=${obj.title}`}>{obj.title}</Link>
       ```

    2. 注册路由（无需声明，正常注册）

       ```jsx
       <Route path="/home/message/detail" component={Detail} />
       ```

    3. 接受参数

       ```jsx
       const { search } = this.props.location  //"?id=01&title='消息1'"，需要借助 querystring 解析为对象
       const { id, title } = qs.parse(search.slice(1))
       ```

  - `state` 传参

    1. 路由链接（携带参数）

       ```jsx
       <Link to={{ pathname: '/home/message/detail', state: { id: obj.id, title: obj.title } }}>{obj.title}</Link>
       ```

    2. 注册路由（无需声明，正常注册）

       ```jsx
       <Route path="/home/message/detail" component={Detail} />
       ```

    3. 接收参数

       ```jsx
       const { id, title } = this.props.location.state || {}
       ```

       备注：刷新也可以保留住参数，因为使用的是 `history` 模式

- 路由的 `push` 与 `replace`

  > 默认为 `push` ，以入栈的形式进行地址的历史记录

  可以设置为

  ```jsx
  <Link replace={true} to={{ pathname: '/home/message/detail', state: { id: obj.id, title: obj.title } }}>{obj.title}</Link>
  ```

  入栈的地址将会代替栈顶的地址，而不是压在上面

- 编程式路由

  > 借助 this.props.history 对象上的 API 操作路由跳转、前进、后退

  - `push()`
  - `replace()`
  - `goBack()`
  - `goForward()`
  - `go()`

  ```jsx
  //编程式路由导航
  replaceShow = (id, title) => {
      //replace携带params参数
      // this.props.history.replace(`/home/message/detail/${id}/${title}`)
  
      //replace携带search参数
      // this.props.history.replace(`/home/message/detail/?id=${id}&title=${title}`)
  
      //replace携带state参数
      this.props.history.replace('/home/message/detail', { id: id, title: title })
  }
  
  pushShow = (id, title) => {
      //push携带params参数
      // this.props.history.push(`/home/message/detail/${id}/${title}`)
  
      //push携带search参数
      // this.props.history.push(`/home/message/detail/?id=${id}&title=${title}`)
  
      //push携带state参数
      this.props.history.push('/home/message/detail', { id: id, title: title })
  }
  ```

  ```
  history:
  	go: f go(n)
  	goBack: f goBack()
  	goForward: f goForward()
  	push: f push(path, [state])
  	replace: f replace(path, [state])
  	
  location:
  	pathname: "/about"
  	search: "?...&..."
  	state: obj
  
  match:
  	params: {}
  	path: "/about"
  	url: "/about"
  ```

- `withRouter`

  > `withRouter` 可以加工一般组件，让一般组件具备路由组件所特有的API
  >
  > 一般组件的 `props` 只会有父组件转递过来的属性，不会有 `history` `location` `match` 等属性
  >
  > `withRouter` 返回的是一个新组件

  - 普通组件

     ![image-20210713101655842](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210713101655842.png)

  - 路由组件

    ![image-20210713101831990](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210713101831990.png)

  - 普通组件转化为路由组件

    ```jsx
    export default withRouter(Header)
    ```

    



- `BrowserRouter` 与 `HashRouter` 的区别

  1. 底层原理不一样

     > `BrowserRouter` 使用的式 H5 的 `history API` ，不兼容 IE9 以下的版本
     >
     > `HashRouter` 使用的是 `URL` 的哈希值

  2. url 表现形式不一样

     > `Browser` 的路径中没有 # ，如 `http://localhost:3000/home/message/detail`
     >
     > `Hash` 的路径中包含 # ，如`http://localhost:3000/#/home/message/detai`

  3. 刷新后对 `state` 参数的影响

     > `Browser` 没有任何影响，因为 state 保存在 history 对象中
     >
     > `Hash` 刷新后会导致路由 state 参数的丢失

  4. `HashRouter` 可以用于解决一些路径错误相关的问题

#### react-router-config

> 辅助react-router的插件，主要是使用配置文件集中式管理路由



#### antd的使用

> 基于 react 的 UI 库

[中文官网](https://ant-design.gitee.io/index-cn)

- 引入UI组件

  ```jsx
  import { Button } from 'antd'
  <Button type="primary">Primary Button</Button>
  ```

- 引入样式

  ```js
  import 'antd/dist/antd.css'
  ```

- 图标单独引入

  ```jsx
  import { WechatOutlined, SearchOutlined } from '@ant-design/icons';
  <WechatOutlined />
  ```

- 样式的按需引入

  > 需要修改脚手架的配置

  1. 导入依赖

     ```js
     yarn add react-app-rewired customize-cra babel-plugin-import
     ```

     `react-app-rewired`	修改了配置，原来的启动命令无法使用了，这个库安装新的启动命令

     `customize-cra`	根据 `config-overrides.js` 去修改 `webpack` 配置

     `babel-plugin-import`	实现按需引入

  2. 增加配置文件`config-overrides.js`

     ```js
     //配置具体的修改规则
     const { override, fixBabelImports } = require('customize-cra');
     
     //按需引入
     module.exports = override(
       fixBabelImports('import', {
         libraryName: 'antd',
         libraryDirectory: 'es',
         style: 'css',
       }),
     );
     ```

  3. 修改启动命令

     ```json
     "scripts": {
         "start": "react-app-rewired start",
         "build": "react-app-scripts build",
         "test": "react-app-scripts test",
     },
     ```

  4. 将自己的样式引入删掉

- 自定义主题

  1. 导入 `less` 的依赖

     `yarn add less less-loader`

     注意 `less` 的版本问题

  2. 修改 `config.overries.js` 文件

     ```js
     //配置具体的修改规则
     const { override, fixBabelImports, addLessLoader } = require('customize-cra');
     
     //按需引入
     module.exports = override(
       fixBabelImports('import', {
         libraryName: 'antd',
         libraryDirectory: 'es',
         style: true,
       }),
     
       addLessLoader({
         javascriptEnabled: true,  //允许js修改主题颜色
         modifyVars: { '@primary-color': '#1DA57A' },  //修改变量@primary-color，这个变量就是 antd 定义的主题颜色
       }),
     );
     ```

     

#### Redux

- `Redux` 是什么

  1. redux是一个专门用于做**状态管理**的JS库(不是react插件库)。
  2. 它可以用在react, angular, vue等项目中, 但基本与react配合使用。

  3. 作用: 集中式管理react应用中多个组件**共享**的状态。

     类似与 vue 中的 vuex

- 什么情况下使用 `redux`

  1. 某个组件的状态，需要让其他组件可以随时拿到（共享）。
  2. 一个组件需要改变另一个组件的状态（通信）
  3. 总体原则：能不用就不用，如果不用比较吃力才考虑用

- 工作流程

   ![image-20210713164246408](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210713164246408.png)

- 基本使用

  - 安装依赖

    `yarn add redux`

  - `store.js`

    ```js
    //引入createStore，专门用于创建 redux 中最为核心的 store 对象
    import { createStore } from 'redux'
    
    //引入为 Count 组件服务的 reducer
    import countReducer from './count_reducer'
    
    //暴露 store
    export default createStore(countReducer)
    ```

  - `reducer.js`

    ```js
    /**
     * 1. 该文件是用于创建一个为 Count 组件服务的 reducer，reducer的本质就是一个函数
     * 2. reducer 函数会接到两个参数，分别为：之前的状态(preState)，动作对象(action)
     */
    
    import { INCREMENT, DECREMENT } from './constant'
    
    // 初始化状态
    const initState = 0
    // reducer是纯函数
    export default function countReducer(preState = initState, action) {
      const { type, data } = action
      switch (type) {
        case INCREMENT:
          return preState + data
        case DECREMENT:
          return preState - data
        default:
          return preState
      }
    }
    ```

    

  - `constant.js`

    ```js
    /**
     * 该模块是用于定义 action 对象中的 type 类型的常量值，目的只有一个：便于管理的同时防止单词写错
     *
     */
    
    export const INCREMENT = "increment"
    export const DECREMENT = "decrement"
    ```

  - 入口文件中引入

    ```js
    import React from 'react';
    import ReactDOM from 'react-dom';
    import './index.css';
    import App from './App';
    import store from './redux/store'
    
    ReactDOM.render(<App />, document.getElementById('root'));
    
    //监测redux中状态的改变，如redux的状态发生了改变，那么重新渲染App组件
    store.subscribe(() => {
      ReactDOM.render(<App />, document.getElementById('root'))
    })
    ```

  - 组件中使用

    > 组件可以调用 action 和 getState()，所以引入下面两个文件

    ```jsx
    import store from '../../redux/store'
    import { createIncrementAction, createDecrementAction, createIncrementAsyncAction } from '../../redux/count-action'
    ```

    

- 异步

  1. 需要导入新的依赖`redux-thunk`

     `yarn add redux-thunk`

  2. 在 `store.js` 中引入

     ```js
     //引入createStore，专门用于创建 redux 中最为核心的 store 对象
     import { createStore, applyMiddleware } from 'redux'
     
     //引入为 Count 组件服务的 reducer
     import countReducer from './count_reducer'
     import thunk from 'redux-thunk'
     
     //暴露 store
     export default createStore(countReducer, applyMiddleware(thunk))
     ```

  3. 在 `action` 中定义异步操作

     ```js
     // 异步action，就是指action的值为函数,异步action中一般都会调用同步action，异步action不是必须要用的。
     export const createIncrementAsyncAction = (data, time) => {
       return (dispatch) => {
         setTimeout(() => {
           dispatch(createIncrementAction(data))
         }, time)
       }
     }
     ```

     

- `react-redux`

  > `react-redux` 将所有组件分为容器组件和UI组件两大类

  - 模型图

    ![image-20210714141300273](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210714141300273.png)

    1. 所有UI组件都应该包裹在一个容器组件内，它们是父子关系
    2. 容器组件是真正和 `redux` 打交道的，里面可以随意的使用 `redux` 的 `api`
    3. UI组件中不能使用任何 `redux` 的API
    4. 容器组件会传给 UI 组件：(1) `redux`中所保存的状态。(2) 用于操作状态的方法
    5. 容器给UI组件传递的 状态和操作状态的方法，均通过 `props` 传递

  - 使用步骤

    1. 导入 `react-redux` 依赖

    2. 在容器组件中引入 `redux` 的 `action`

    3. 封装 `redux` 的状态和操作状态的方法

       ```js
       /* 
         1.mapStateToProps函数返回的是一个对象；
         2.返回的对象中的key就作为传递给UI组件props的key,value就作为传递给UI组件props的value
         3.mapStateToProps用于传递状态
       */
       function mapStateToProps(state) {
         return { count: state }
       }
       
       
       /* 
         1.mapDispatchToProps函数返回的是一个对象；
         2.返回的对象中的key就作为传递给UI组件props的key,value就作为传递给UI组件props的value
         3.mapDispatchToProps用于传递操作状态的方法
       */
       function mapDispatchToProps(dispatch) {
         return {
           jia: number => dispatch(createIncrementAction(number)),
           jian: number => dispatch(createDecrementAction(number)),
           jiaAsync: (number, time) => dispatch(createIncrementAsyncAction(number, time)),
         }
       }
       ```

       

    4. 使用 `connect` 链接 UI 组件和 redux

       ```js
       import { connect } from 'react-redux'
       import CountUI from '../../components/Count'
       export default connect(mapStateToProps, mapDispatchToProps)(Count)
       ```

    5. .容器组件绑定时传递 `store`

       ```jsx
       <div>
           {/* 给容器组件传递store */}
           <Count store={store} />
       </div>
       ```

  - 优化

    1. 容器组件

       1. 将容器组件和 UI 组件放在一个文件
       2. `mapStateToProps` 和 `mapDispatchToProps` 简化

    2. 传递 `store`

       > 上面的方法，每有一个容器组件就需要传递一下 `store`

       入口文件导入 `react-redux` 的 `Provider` 组件包裹 `App` 组件，让所有 `App` 的后代容器组件都能接收到 `store`

       ```jsx
       import React from 'react';
       import ReactDOM from 'react-dom';
       import './index.css';
       import App from './App';
       import store from './redux/store'
       import { Provider } from 'react-redux'
       
       ReactDOM.render(
         <Provider store={store}>
           <App />
         </Provider>,
         document.getElementById('root')
       );
       ```

  - 多组件开发

    - 目录结构

       ![image-20210714160825387](images/image-20210714160825387.png)

    - 汇总 `reducer`

      ```js
      // 汇总所有的reducer变为一个总的reducer
      const allReducer = combineReducers({
        he: countReducer,
        rens: personReducer
      })
      ```

  - `redux` 开发者工具

    > 追踪状态的改变

    1. 浏览器下载插件`Redux DevTools`
    
    2. 项目安装依赖 `redux-devtools-extension`
    
    3. `store.js` 中引入并使用
    
       ```js
       
       // 引入createStore，专门用于创建 redux 中最为核心的 store 对象
       import { createStore, applyMiddleware, combineReducers } from 'redux'
       
       // 引入为 Count 组件服务的 reducer
       import countReducer from './reducer/count'
       import personReducer from './reducer/person'
       // 引入 redux-thunk 支持异步
       import thunk from 'redux-thunk'
       
       // 引入 redux-devtools-extension
       +import { composeWithDevTools } from 'redux-devtools-extension'
       
       // 汇总所有的reducer变为一个总的reducer
       const allReducer = combineReducers({
         he: countReducer,
         rens: personReducer
       })
       
       // 暴露 store
       export default createStore(allReducer, +composeWithDevTools(applyMiddleware(thunk)))
       ```
    
       

- 纯函数与高阶函数

  - 纯函数

    > 只要是同样的输入，必定得到同样的输出

    1. 不得改写参数数据
    2. 不会产生副作用，例如网络请求、输入输出设备
    3. 不能调用 `Date.now()` 或者 `Math.random` 等不纯的方法

    **注意**：`redux` 的 `reducer` 必须是一个纯函数

  - 高阶函数

    > 参数是函数或者返回值是函数，能实现更加动态更加扩展的功能

    常见的高阶函数

    1. 定时器
    2. 数组的`forEach()	map()	filter()	reduce()	find()	bind()`
    3. `promise`
    4. `react-redux` 中的 `connect` 函数



#### `setState`

> 该方法有两种形式，去修改 `state`

1. `setState(obj, [callback])`

   例如：

   ```jsx
   //1.获取原来的count值
   const { count } = this.state
   //2.更新状态（对象式） this.setState(obj, [callback])
   this.setState({ count: count + 1 }, () => {
       console.log(this.state.count) //该回调调用的时机是状态更新后
   }) //该方法时同步方法，引起状态的改变时异步的
   // console.log(this.state.count) //状态还没有改变
   ```

   优点：简单，如果修改后的值不依赖原来状态，则使用该形式

2. `setState(fun, [callback])`

   例如：

   ```jsx
   // 3. 更新状态（函数式）  this.setState(fun, [callback])
   this.setState((state, props) => { //能拿到state和props
       return { count: state.count + 1 }
   })
   ```

   优点：能够接收 `state` 和 `props` 参数，如果修改的状态依赖原来状态，则使用该形式更方便，对象式其实是函数式的语法糖。



#### 懒加载

> 将组件分别打包，需要的该组件的时候再去下载包含这个组件的包，避免首屏加载所有一俩加载时间过长

- 引入组件

  ```js
  //懒加载引入组件
  const Home = lazy(() => import('./pages/Home'))
  const About = lazy(() => import('./pages/About'))
  ```

- 注册组件

  需要使用 `<Suspense fallback={<h1>loadding</h1>}> </Suspense>` 包裹所有懒加载组件，用于网速慢时，组件还没有下载好页面的显示

  `fallback` 属性用于指定一个 `loading` 组件，该组件不能使用懒加载。



#### Hook

> 函数式组件可以使用 `state` ，生命周期，等类组件的特性

- `State Hook`

  > 让函数组件也可以有 `state` 状态，并对状态进行读写操作

  - 语法

    `const [xxx, setXxx] = React.useState(initValue)`

    对状态进行读取操作就使用变量 `xxx`

    修改状态就通过调用函数 `setXxx(newValue)`

  - `useState()` 说明

    参数：第一次初始化指定的值在内部作缓存

    返回值：包含2个参数的数组，第一个参数为内部当前状态值，第二个为更新状态的函数

  - `setXxx()` 2中写法

    1. `setXxx(newValue)`
    2. `setXxx(oldValue => newValue)`

- `Effeck Hook`

  > 可以替代类组件中生命周期的操作，执行带有副作用的操作

  - 语法

    ```js
    React.useEffect(() => {
        console.log('@')  //组件挂载后会调用，检测的状态改变后也会调用	componentDidmount ，可以在这里执行任何带有副作用的操作
        return ()=>{}	//返回的这个函数对应这 componentWillUnmount
    }, [count])  //[] 代表谁也不检测，不写第二个参数代表检测所有状态, 数组可以写状态，检测状态 componentDidUpdate
    ```

    参数说明

    1. 第一个参数是一个回调函数，当组件挂载后(componentDidmount)会执行，或者当检测的状态更新时也会执行该函数
    2. 第二个参数时一个数组，里面需要检测的状态，空数组代表不检测任何状态，不写代表检测所有状态。

  - 所以 `Effeck Hook` 对应这类组件的3个钩子

    `componentDidMount`

    `componentWillUnmount`

    `componentDidupdate`

  - React中的副作用操作:

    1. 发ajax请求数据获取
    2. 设置订阅 / 启动定时器
    3. 手动更改真实DOM

- `RefHook`

  ```
  (1). RefHook可以在函数组件中 存储/查找 组件内的标签或任意其它数据
  (2). 语法: const refContainer = React.useRef()
  (3). 作用:保存标签对象,功能与React.createRef()一样，只是下面使用的时候不用加 this
  ```

  ```js
  const myRef = React.useRef()
  function show() {
      alert(myRef.current.value)
  }
  return (<input type="text" ref={myRef} /><br />)
  ```




#### `render props`

> 向组件内部动态传入带内容的结构（标签）
>
> vue 中使用的是 slot：`<A> <B />  </A>`
>
> React 中使用的是 `children props` 和 `render props`

- `children props`

  ```jsx
  <A>
  	<B />
  </A>
  
  {this.props.children}
  
  // 问题： 如果 B 组件需要 A 组件内的数据是做不到的
  ```

  

- `render props`

  ```jsx
  <A render={(data) => <C data={data} />} />
  class A{
      state = {
          data: ...
      }
      render(){
          const {data} = this.state
          return(
          	{this.props.render(data)}
          )
      }
  }
  
  class C: 读取A组件的数据显示 {this.props.data}
  ```


#### 扩展

- `Portals`

  > 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的优秀方案

  ```js
  ReactDOM.createPortal(child, container)
  ```

  - 第一个参数是 React 元素
  - 第二个参数是 DOM 元素

  使用该方案会导致 React 树和 DOM 树不一致

  > portal 仍存在于 *React 树*， 且与 *DOM 树* 中的位置无关，那么无论其子节点是否是 portal，像 context 这样的功能特性都是不变的，事件冒泡也是遵循 react 中的树结构

- `Profiler`

  > 测量渲染一个 React 应用多久渲染一次以及渲染一次的 “代价”

- `react`中`state`在`constructor`里面和外面同时定义，`constructor` 内的会覆盖外面的

#### Mobx

![image-20210715162522687](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210715162522687.png)

- `@observable`

  给类属性添加可观测功能

- `@action`

  给类方法添加，可观察属性只能通过 `action` 方法修改

- `@computed`

  计算属性，类似 `vue` 的 `computed`

  ```js
  @computed
  get double() {
      return this.timer * 2
  }
  ```

- `makeObservable` 方法，用于构造响应式对象

  ```js
  import { makeObservable, observable, action, computed } from "mobx"
  
  class MobxStore {
    @observable timer = 0
    constructor() {
      makeObservable(this)
      setInterval(() => {
        this.updateTimer()
      }, 1000)
    }
    @action
    updateTimer = () => {
      this.timer += 1
    }
  
    @action
    resetTimer = () => {
      this.timer = 0
    }
    @computed
    get double() {
      return this.timer * 2
    }
  }
  
  const store = new MobxStore()
  
  export default store
  
  ```

- `makeAutoObservable` 

  > 可以自动为属性加上对象的包装函数

  ```js
  import { makeAutoObservable } from "mobx"
  
  class MobxStore {
    timer = 0
    constructor() {
      makeAutoObservable(this)
      setInterval(() => {
        this.updateTimer()
      }, 1000)
    }
  
    updateTimer = () => {
      this.timer += 1
    }
  
  
    resetTimer = () => {
      this.timer = 0
    }
  
    get double() {
      return this.timer * 2
    }
  }
  
  const store = new MobxStore()
  
  export default store
  
  ```



#### react fiber

> react v16版本的核心算法实现

- `Fiber` 对象

  ```js
  {
    
  }
  ```

- 帧的概念

  > 目前大多是设备的屏幕刷新率是60次/秒，即60hz
  >
  > 当每秒绘制的帧数（FPS）达到60时，页面时流畅的，小于这个值用户会觉得卡顿
  >
  > 每帧的预算时间是1/60=16.66(ms)
  >
  > 每个帧的开头包括样式计算/布局/绘制
  >
  > javaScript执行javaScript引擎和页面渲染引擎在同一个渲染线程，GUI渲染和JavaScript执行两者是互斥的
  >
  > 如果某个任务执行时间过长，浏览器就会延迟渲染

  ![image-20211104183738602](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211104183738602.png)

![image-20211104184615557](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211104184615557.png)



![image-20211104185315352](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211104185315352.png)

### webpack配置相关

#### 创建基本webpack项目

1. `npm init -y`

2. `src` 源代码目录和 `dist` 产品目录

3. `src` 目录下创建 `index.html`

4. `src` 目录下创建入口文件 `index.js`

5. 安装 `webpack` 

   - `npm i webpack -D`
   - `npm i webpack-cli -D`

6. 将 `webpack` 命令添加进脚本

   `"build": "webpack"`

7. 创建 `webpack` 配置文件 `webpack.config.js`，里面写入配置

   ```js
   // 向外暴露一个打包的配置对象；因为 webpack 是基于 Node 构建的；所以 webpack 支持所有的 Node API 语法
   
   module.exports = {
       mode: 'production' //development production	开发环境不压缩，生产环境压缩
       //默认打包入口文件 src/index.js
       //默认输出文件是	dist/main.js
   }
   ```

8. 打包

   `npm run build`

9. 语法兼容

   **webpack是基于Node构建的，Node使用的是Chrome V8引擎，所有Chrome浏览器不支持的语法，Node就不支持，webpack也就不支持**

10. `webpack-dev-server`

    - 实时编译

    - 添加到脚本中

      `"webpack-dev-server --open --port 3000 --hot --host 127.0.0.1"`

    - 注意 `webpack` `webpack-cli` `webpack-dev-server` 的版本兼容问题

    - 打包输出的文件默认为 `/main.js` (存放在内存中，文件中看不见)![](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210702144048264.png)

11. `html-webpack-plugin`

    插件作用：在内存中生成 html 的插件

    1. 安装插件

       `npm install html-webpack-plugin -D`

    2. 在 `webpack.config.js` 中配置插件

       1. 导入

          `const HtmlWebPackPlugin = require("html-webpack-plugin")`

       2. 配置插件对象

          ```js
          const htmlPlugin = new HtmlWebPackPlugin({
              template: path.join(__dirname, "./src/index.html"),  //源文件
              filename: 'index.html'  //生成在内存中首页的名称
          })
          ```

       3. 添加插件

          ```js
          plugins: [
              htmlPlugin
          ]
          ```

    3. `html-webpack-plugin` 插件会在内存中的 `html` 的最后自动引入 `main.js` 文件，所以源文件中不用引入 `main.js`文件

#### webpack项目开发react

1. 安装 `react` 依赖包

   `npm install react react-dom -S`

   - `react`

     专门用于创建组件和虚拟 `dom` 的，同时组件的生命周期也在这个包里

   - `react-dom`

     专门进行 `Dom` 操作的，主要应用场景就是 `ReactDom.render()`

2. `index.js` 中引入依赖

   ```js
   import React from 'react'
   import ReactDOM from 'react-dom'
   ```

3. 基本使用

   ```js
   /**
    * 创建虚拟 dom 元素
    * 参数1. 创建元素的类型，字符串，表示元素的名称，例如 "h1" "div"等
    * 参数2. 是一个对象或者 null，表示元素的属性
    * 参数3~n. 子节点
    */
   const myh1 = React.createElement('h1', {id: 'myh1'}, 'hello word')
   
   
   /**
    * 将虚拟 dom 渲染到页面上
    * 接受两个参数
    * 1. 要渲染的那个dom元素
    * 2. 指定页面上的容器（所以index.html中必须要有一个容器）
    */
   ReactDOM.render(myh1, document.getElementById("app"))
   ```

4. `JSX`

   - 概念

     JS 的语法扩展 --> 在JS中混合类似于HTML的语法，X 表示 XML

   - 作用

     由于使用 `React.createElement()` 创建虚拟 `DOM` 元素十分不方便，且难以阅读。渲染页面的 `DOM` 结构，最好的方式就是使用 `HTML` ，但直接在 js 中插入 html 代码会报错，所以需要使用 babel 来转化这些标签。

   - 使用

     - 安装包

       `npm install babel-core babel-loader babel-plugin-transform-runtime -D`

       `npm install babel-preset-env babel-preset-stage-0 babel-preset-react -D`

     - 配置

       在 `webpack.config.js` 中配置

       ```js
       module: {   //所有第三方模块的配置规则
           rules: [
               //exclude排除项
               { test: /\.js|.jsx$/, use: 'babel-loader', exclude: /node_modules/ } 
           ]
       }
       ```

     - 使用

       ```js
       const mydiv = 
        <div>
           这是一个div
           <h1>这是H1</h1>
       </div>
       
       ReactDOM.render(mydiv, document.getElementById("app"))
       ```

- 组件的创建，组件的首字母必须是大写

  1. 函数定义，函数中必须返回一个合法的 JSX 虚拟 DOM 元素

     ```jsx
     function Hello(props){
         return (
         	<div>Hello 组件</div>
         )
     }
     ```

- 组件的传值，通过形参 props，不论实在 vue 还是 React 中 props永远都是只读的

  ```jsx
  //使用 props 形参，接受外界传递过来的数据
  function Hello(props){
      return (
  		<div> Hello {props.name}-{props.age} </div>
      )
  }
  const person = {
      name: "Alice",
      age: 20
  }
  //使用组件并为组件传值
  <Hello name={person.name} age={person.age} />
  
  //使用对象展开符为组件传值
  <Hello {...person} />
  ```

  

- 组件抽取到 `.jsx` 文件中

  ```jsx
  //Hello.jsx
  import React from 'react'
  export default function Hello(props){
    return (
      <div>这是Hello组件-{props.name}-{props.age}</div>
    )
  }
  ```

  引入

  ```js
  import Hello from './components/Hello.jsx'
  ```

  省略 `.jsx` 后缀名配置

  ```js
  //webpack.config.js
  resolve: {
        extensions: ['.js', '.jsx', '.json'],  //这几个文件的后缀名,可以省略不写
  }
  ```

  

- 配置 `@` 为根目录下 `src` 这一层路径

  ```js
  // webpack.config.js
  resolve: {
        extensions: ['.js', '.jsx', '.json'],  //这几个文件的后缀名,可以省略不写
        alias: {
          '@': path.join(__dirname, './src')  //@表示项目根目录中 src 的这一层路径
        }
      }
  ```



#### react 项目配置less

1. 安装依赖

   `npm i less less-loader --save-dev`

   如果报错，降低 `less-loader` 版本

2. 修改 `webpack.config.js` 文件

   可以去 `node_modeles\react-script\config` 下配置

   也可以使用命令 `npm run eject` 将配置文件暴露出来配置

   1. 先添加变量

      ```js
      const lessRegex = /\.less$/;
      const lessModuleRegex = /\.module\.less$/;
      ```

   2. 在 `oneOf` 下添加两项

      ```js
      {
          test: lessRegex,
              exclude: lessModuleRegex,
                  use: getStyleLoaders({
                      importLoaders: 1,
                      sourceMap: isEnvProduction
                      ? shouldUseSourceMap
                      : isEnvDevelopment,
                  },
                                       'less-loader'
                                      ),
                      // Don't consider CSS imports dead code even if the
                      // containing package claims to have no side effects.
                      // Remove this when webpack adds a warning or an error for this.
                      // See https://github.com/webpack/webpack/issues/6571
                      sideEffects: true,
      },
          // Adds support for CSS Modules (https://github.com/css-modules/css-modules)
          // using the extension .module.css
          {
              test: lessModuleRegex,
                  use: getStyleLoaders({
                      importLoaders: 1,
                      sourceMap: isEnvProduction
                      ? shouldUseSourceMap
                      : isEnvDevelopment,
                      modules: {
                          getLocalIdent: getCSSModuleLocalIdent,
                      },
                  },
                                       'less-loader'
                                      ),
          },
      ```

   3. `getStyleLoaders` 下添加一项

      ![image-20210709165536106](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210709165536106.png)



#### react 样式模块化

> 在 webpack.config.js 的 loader 配置中添加 modules: true

![image-20210709175358446](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210709175358446.png)

配置 `css` 的模块化，就在 `cssRegex` 下配置，配置 `less` 模块化就在 `lessRegex` 下配置

**样式模块化**

> 将样式文件像 `js` 一样导入作为对象使用，文件中的每一个样式相当于对象的属性

```jsx
import React, { Component } from 'react';
//将样式作为对象导入
import cssStyles from './App.css';
import lessStyles from './App.less'

class App extends Component {
  render() {
    return (
      <div style={{ textAlign: 'center' }}>
        <div className='cssModule'>css模块化配置</div>
        <div className={cssStyles.cssModule}>css模块化配置</div>
        <div className='lessModule'>less模块化配置</div>
        <div className={lessStyles.lessModule}>less模块化配置</div>
      </div>
    );
  }
}

export default App;
```

- 样式模块化添加多个样式

  ```jsx
  <div className={`${s1} ${s2}`}>hello world</div
  ```




### JS

#### 作用域是什么

> 是一套存储变量，并且之后可以方便找到这些变量的规则

- 编译的三个步骤

  1. 分词/词法分析
  2. 解析/语法分析
  3. 代码生成

  ![image-20210714193751660](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210714193751660.png)

- 变量的声明与赋值

  1. 声明

     > 遇到 `var a`，编译器会询问作用域是否已经有一个该名称的变量存在于同一个作用域的 集合中。如果是，编译器会忽略该声明，继续进行编译；否则它会要求作用域在当前作 用域的集合中声明一个新的变量，并命名为 a

  2. 赋值

     > 引擎会在作用域中查找该变量，如果能够找到就会对 它赋值，如果最后都没有找到就抛出一个异常

  ![image-20210714195409491](images/image-20210714195409491.png)

- `LHS` 和 `RHS`

  > 查询类型

  - `LHS`

    > 变量出现在赋值操作的左侧，并不关心变量当前的值，只是为赋值操作找一个目标

    例：`var a = 2`

  - `RHS`

    > 变量出现在赋值操作的右侧，目的是找到变量源头，拿到变量的值

    例：`console.log(a)`

  - `LHS` 和 `RHS` 面对未声明变量的行为不一样

    `RHS-->ReferenceError`

    `LHS-->非严格模式下，在全局作用域下创建该变量；严格模式下，ReferenceError`

  

- 词法作用域

  > 无论函数在哪里调用，如何被调用，词法作用域只有声明所处位置决定（定义在词法阶段的作用域）

  - 遮蔽效应

    > 作用域在查找到第一个标识符停止，全局变量被遮蔽后可以通过 window.变量名访问，而非全局变量被遮蔽后则无法访问

    词法作用域只会查找一级标识符，遇到多级标识符，通过对象访问规则查询

  - 欺骗词法

    1. `eval`
    2. `with`

    **注意**：不推荐使用，严格模式不兼容，存在性能问题

- 函数作用域

  > 函数作用域的含义是指，属于这个函数的全部变量都可以在整个函数的范围内使用及复 用（事实上在嵌套的作用域中也可以使用）

  - 最小暴露原则，私有化，隐藏作用域
  - 





  

  

  

### React Native

#### 搭建开发环境

[官网流程](https://reactnative.cn/docs/environment-setup)



### 项目

#### 组件

- `page` 组件传参

  ```js
  Table = this.createTable('table', {
      url: '/api/insurance/orderVerify/record/queryList',
      columns,
      pagination: {
        showSizeChanger: true,
        total: 0,
        showTotal: total => `共 ${total} 项`,
      },
    });
  ```

- 表单字段的 `allowClear` 属性

#### 主站

- 业务相关

  - 经纪主体与数科主体

    > 经纪主体主要是付费险业务，经纪主体具有保险牌照
    >
    > 数科主体主要是增险业务，数科主体没有保险牌照

  - 0+12

- `/common/` 公共库目录

  ```
  |- /fetch/										封装 axios 网络请求
  	|- index.js
  |- /footer/										footer 组件
  |- /style/										定义全局样式
  	|- index.less								页面总体布局
  	|- main-font.tff							字体
  	|- media.less								媒体兼容
  	|- reset.less								重置标签基础样式
  	|- util.less								通用功能样式，可复用
  |- /utls/										工具库
  	|- /common/									处理数据的通用函数
  		|- common.js							处理函数逻辑
  		|- index.js								导出
  	|- cookie.js								处理 cookie
  	|- copyright.js								版权和ICP
  	|- device.js								环境判断
  	|- dict.js									字典映射
  	|- index.js									统一入口
  	|- statistic.js								埋点
  	|- storage.js								localStorage
  	|- toast.js									toast 提示封装
  	|- url.js									URL 地址解析
  |- apApi.js										支付
  |- frame.tsx									页面框架组件
  |- message.js									事件管理
  |- router.js									路由
  |- socketServer.js								消息处理
  |- userApi.js									用户类
  |- wxApi.js										微信相关处理
  ```

  - `window.ybtools`
  
    >将所有与业务无关的公用方法拆分到一个单独的 js 文件，打包后再项目中引入。
  
   ![image-20210728162927643](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210728162927643.png)

#### 需求

- cms 对账查询需求

  > table 和 page 组件的使用

- 官网图片替换需求

- h5 复刻 小程序视觉（挂起）

- 官网披露我司愿景

- 调查问卷（一期）

  > 熟悉 login 组件

- 1V1改版

  > 站外拉起小程序跳转站内地址，携带登录态，_getWXMiniScheme() 动态生成跳转链接
  >
  > 问卷的设计，缓存
  >
  > CommonUtil.goToKF(31, 3)	CommonUtil.getKFLink(31, 3)。生成客服链接
  >
  > jenkins 上发布分支

- 公众号落地页优化

  > 预览的实现，通过 iframe
  >
  > 站外拉起小程序跳转站内地址
  
- 官网自查整改

  > 图片文案的替换

- 移动端披露我司信息

  > 页面的布局，表格的使用

- 支付宝解约流程

  > 图片的替换，链接参数的获取

#### 开发规范

- 视图使用二倍图，并使用 `tiny` 压缩
- `commit` 规范

  - 修改信息：MOD：描述

  - 删除信息：DEL：描述

  - 增加信息：ADD：描述

  - 修复问题信息：FIX：描述
- 提交的时候删除注释的代码
- 数据处理不要放到 `render` 中，因为 `render` 不止调用一次

#### mock 的使用

1. 添加 `idoc` 到 `mock/cconfig.js->projectJsonUrl`

   > 主要是projectId 不同，前面的都是一样的

    ![image-20210803175316259](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210803175316259.png)

2. 重新生成 data

   根据 `cconfig.js` 重新执行 `npm run gen-mock` 生成 data 文件夹

3. 修改运行环境为本地

   `webpack.dev.config.js`

    ![image-20210803175610016](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210803175610016.png)

4. 修改代理

   > 设置 dev 运行环境下， 代理指向 '/'

   ![image-20210803175848206](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210803175848206.png)

5. 模拟数据

   > 在 data 文件夹中找到接口，在返回的数据中模拟

    ![image-20210803180041951](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210803180041951.png)



### Git

- 修改 `diff`

  1. `git commit --amend --no-edit`
  2. `arc diff`
  3. 在弹出文件第一行添加描述
  4. 保存关闭文件

- `get reset [id]`

  > 回退到 commit 之前，可以通过 `git log` 查询 `id`
  
- `git commit --amend --no-edit`

- `git commit --amend -m ""`

- `git stash` `git stash pop`

- `.git/arc/default-relative-commit`

  > 该文件里面指定了arc的根分支
  
- `git config --global user.name ""`

  > 设置全局环境下用户名(没有后面字符串就是查询)

- `git config --global user.email ""`

  > 设置全局环境下邮箱

- `git config user.name ""`

  > 设置当前项目下用户名

- `git config user.email ""`

  > 设置当前项目下用户邮箱



### linux命令

- 删除文件/目录

  `rm -rf 文件名/文件目录`



### 区块链

- 钱包
- 矿池
- 交易所

### TypeScript

> 是 js 的超集，最主要的就是增加了声明变量时可以确定类型
>
> example: `let isDone: boolean = false;`

#### 基础类型

- 布尔值：boolean

- 数字：number

  支持二进制(0b)，8进制(0o)，十进制，十六进制(0x)

- 字符串：string

  单引号，双引号，模板字符串

- 数组：`number[]，Array<number>`

- 元组

  > 元组类型允许表示一个已知元素数量和类型的数组

  ```js
  let x: [string,number] = ['hello', 10]
  ```

- 枚举

  > 标准类型的一个补充，更友好的命名

  ```typescript
  enum Color {Red, Green, Blue}
  let c: Color = Color.Green // 1，默认从0开始编号
  ```

  

- Any

  > 为不清楚类型的变量指定一个值

  ```typescript
  let notSure: any = 4
  notSure = 'hello typescript'
  ```

  与 Object 的区别：

  any 能够调用类型上的方法而Object不能调用

  ```typescript
  let list: any[] = [1, true, 'free']
  ```

- Void

  > 表示没有任何类型，一般用于函数没有返回值

  ```typescript
  function foo: void{
      console.log("no return")
  }
  ```

  声明一个 void 变量只能赋予它 `undefined` 和 `null`

- null 和 undefined

  > 这种类型的变量作用不是很大，默认情况下 null 和 undefined 的所有类型的子类型

- never

  > 表示永远不存在的值的类型

  ```typescript
  // 返回的 never 函数必须存在无法到达的终点
  function error(message: string): never{
      throw new Error(message)
  }
  
  // 推断返回值为 never
  function fail(){
      return error("Something failed")
  }
  
  // 返回的 never 函数必须存在无法到达的终点
  function infiniteLoop(): never{
      while(true){}
  }
  ```

- Object

  > 非原始类型，除 number, string, boolean, symbol, null, undefined 之外的类型

- 类型断言

  > 类似与其他语言中的类型转换

  - 尖括号语法

    ```typescript
    let someValue: any = "this is a string"
    let strLength: number = (<string>someValue).length
    ```

  - as 语法

    ```typescript
    let someValue: any = "this is a string"
    let strLength: number = (someValue as string).length
    ```

  JSX 中只能使用 as 语法

#### 变量声明

- var

  > `var`声明可以在包含它的函数，模块，命名空间或全局作用域内部任何位置被访问。声明提升

  闭包的问题

  ```typescript
  for (var i = 0; i < 10; i++) {
      setTimeout(function() { console.log(i); }, 100 * i);
  }// 10 10 10 10 10 10 10 10 10
  ```

- let 

  块作用域，块外是不能访问块内 let 定义的变量的

- const

  与 let 类似，引用的值不可变

- 解构
  - 数组解构
  
    ```js
    let arr = [1,2]
    let [a,b] = arr //a=1,b=2
    
    [a,b] = [b,a] //swap
    
    let [a, ...ret] = [1,2,3,4] //a=1, ret=[2,3,4]
    
    let [,a,,b] = [1,2,3,4] //a=2,b=4
    ```
  
    
  
  - 对象解构
  
    ```js
    let obj = {
      a: 1,
      b: 2
    }
    let {a,b} = obj // a=1, b=2
    let {a: a1, b: b1} = obj // a1=1, b1=2 【属性重命名】
    
    let {a=100, b} = obj //默认值
    
    ```
  
    
  
  - 展开操作符
  
    ```js
    let arr1 = [1,2]
    let arr2 = [3,4]
    let newArr = [0, ...arr1, ...arr2] // [0,1,2,3,4]，这里是对arr1 arr2的浅拷贝，修改newArr并不会修改arr1 arr2
    
    let obj = {
      a: 1,
      b: 2
    }
    let newObj = {...obj, a:3} //{a:3, b:2} 后面的属性会覆盖前面的属性 对象只会展开自身的属性，不会展开方法
    ```
  
    

#### 接口

> ts中接口的作用就是为类型命名和你的代码或第三方代码定义契约。

```typescript
interface LabelledValue{
    label: string
}
```

接口好比一个名字，用来描述要求，上面这个例子就表示一个有 `label` 属性切类型为 `string` 的对象

- 可选属性，用 `?` 表示

  ```typescript
  interface SquareConfig {
    color?: string;
    width?: number;
  }
  ```

- 只读属性

  > 只能在对象刚刚创建的时候修改其值

  ```typescript
  interface Point{
      readonly x: number;
      readonly y: number;
  }
  ```

  `ReadonlyArray<T> `只读数组

  变量使用 `const` 属性使用 `readonly`

- 额外的属性检查

  ```typescript
  interface SquareConfig {
      color?: string;
      width?: number;
  }
  
  function createSquare(config: SquareConfig): { color: string; area: number } {
      // ...
  }
  
  let mySquare = createSquare({ colour: "red", width: 100 }); //这里会报错，colour属于额外属性，接口没有定义
  ```

  绕过额外属性检查

  1. 索引签名

     ```typescript
     interface SquareConfig {
         color?: string;
         width?: number;
         [propName: string]: any;
     }
     ```

  2. 类型断言

     ```js
     let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
     ```

  3. 中间变量

     ```typescript
     let squareOptions = { colour: "red", width: 100 };
     let mySquare = createSquare(squareOptions); // 变量不会进经过额外属性检查
     ```

- 函数类型

  > 接口除了能够描述属性，还能描述函数

  ```typescript
  interface SearchFunc {
    (source: string, subString: string): boolean; // 描述了函数的参数和返回值
  }
  
  let mySearch: SearchFunc;
  mySearch = function(src: string, sub: string) {
    // 函数参数名不需要和接口定义参数名一致,也可以不指定类型，ts会推断出类型
    let result = source.search(subString);
    return result > -1;
  }
  ```

- 可索引类型

  > 例如数组，对象这种可索引类型，arr[1] = "apple"，obj['name']="张三"

  ```typescript
  interface StringArray {
    [index: number]: string; 
    // 可以加readonly设置为只读,防止给索引赋值 
    // readonly [index: number]: string
  } // 这里接口定义了一种索引为数字，值为字符串的索引类型
  
  let myArray: StringArray;
  myArray = ["Bob", "Fred"];
  
  let myStr: string = myArray[0];
  ```

- 类类型

  > 实现接口与 java 的接口作用基本一致，强制一个类去符合某种契约

  ```typescript
  interface ClockInterface {
      currentTime: Date;
      setTime(d: Date); // 接口描述方法，类中实现
  }
  
  class Clock implements ClockInterface {
      currentTime: Date;
      setTime(d: Date) {
          this.currentTime = d;
      }
      constructor(h: number, m: number) { }
  }
  ```

- 继承接口

  > 接口间可以相互继承

  ```typescript
  interface Shape {
      color: string;
  }
  
  interface Square extends Shape {// 也可以继承多个类型 extends Shape, PenStroke
      sideLength: number;
  }
  
  let square = <Square>{};
  square.color = "blue";
  square.sideLength = 10;
  ```

  

- 混合类型

  > 一个对象可以同时作为函数和对象使用，并带有额外属性

  ```typescript
  interface Counter {
      (start: number): string;
      interval: number;
      reset(): void;
  }
  
  function getCounter(): Counter {
      let counter = <Counter>function (start: number) { };
      counter.interval = 123;
      counter.reset = function () { };
      return counter;
  }
  
  let c = getCounter();
  c(10);
  c.reset();
  c.interval = 5.0;
  ```

#### 类

- 类的定义

  > 与面向对象的语言相同，属性/方法/构造器

- 继承

  `extends`

- 公用私有受保护修饰符

  `public` 		  默认

  `private` 		不能在声明类外部访问

  `protect` 		除了自身，还能在派生类中访问

- `readonly` 修饰符

  将属性设置为只读

- 存取器（`get` `set`）

  ```typescript
  class Employee {
      private _fullName: string;
  
      get fullName(): string {
          return this._fullName;
      }
  
      set fullName(newName: string) {
          if (passcode && passcode == "secret passcode") {
              this._fullName = newName;
          }
          else {
              console.log("Error: Unauthorized update of employee!");
          }
      }
  }
  ```

  

- 静态属性

  > 存在于类本身而不是类的实例上

- 抽象类

  > 作为其他派生类的基类使用
  >
  > 抽象类中的方法不包括实现，必须在派生类中实现，与接口类似
  >
  > 抽象类是对事物的抽象，接口是对行为的抽象
  >
  > 继承类是“是不是”的关系，实现接口是“有没有”的关系

  ```java
  interface Alram { // 定义了一个报警的功能
      void alarm();
  }
   
  abstract class Door { // 定义了门及门的基本行为
      void open();
      void close();
  }
   
  class AlarmDoor extends Door implements Alarm {
      void oepn() {
        //....
      }
      void close() {
        //....
      }
      void alarm() {
        //....
      }
  }
  ```

#### 函数

> 函数声明 函数表达式 匿名函数

- 为函数定义类型

  ```typescript
  function add(x: number, y: number): number {
      return x + y;
  }
  
  let myAdd = function(x: number, y: number): number { return x + y; };
  ```

  书写完整函数类型

  ```typescript
  let myAdd: (x: number, y: number) => number =
      function(x: number, y: number): number { return x + y; };
  ```

- 可选参数默认参数

  ```typescript
  function buildName(firstName: string, lastName?: string) {
      // ...
  }
  
  function buildName(firstName: string, lastName = "Smith") {
      // ...
  }
  ```

- 剩余参数

  ```typescript
  function buildName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
  }
  
  let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
  ```

- `this`

  > `this` 在函数被调用的时候才会制定
  >
  > 箭头函数中的 `this` 在函数创建时就指定了

#### 泛型

> 不仅能够支持当前数据类型，还支持未来的数据类型，通过声明的时候通过<>传一个类型参数，内部可以使用该参数实现内部类型的统一，而不用指定某一种固定的类型

- 泛型函数

  ```typescript
  function identity(arg: any): any {
      return arg;
  }
  ```

  使用`any`类型会导致这个函数可以接收任何类型的`arg`参数，这样就丢失了一些信息：传入的类型与返回的类型应该是相同的。如果我们传入一个数字，我们只知道任何类型的值都有可能被返回。

  ```typescript
  function identity<T>(arg: T): T {
      return arg;
  }
  
  let output = identity("myString") //这里没有必要通过<>来强调返回类型的值，ts可以通过查看参数的类型推断出来
  ```

  泛型则可以解决这个问题，传入什么类型的参数，就返回相同类型的值

- 泛型变量

  ```typescript
  function loggingIdentity<T>(arg: T[]): T[] {
      console.log(arg.length);  
      return arg;
  }
  
  // 这种定义和上面是一致的
  function loggingIdentity<T>(arg: Array<T>): Array<T> {
      console.log(arg.length);  // Array has a .length, so no more error
      return arg;
  }
  ```

  上面函数指定了接受参数类型是元素类型为T的数组，返回值类型元素类型为T的数组

- 泛型类型

  ```typescript
  function identity<T>(arg: T): T {
      return arg;
  }
  
  let myIdentity: <T>(arg: T) => T = identity; // 这里的泛型作为一种类型，给myIdentity定义类型
  ```

- 泛型接口

  ```typescript
  interface GenericIdentityFn { // 定义了一个泛型接口
      <T>(arg: T): T;
  }
  
  function identity<T>(arg: T): T {
      return arg;
  }
  
  let myIdentity: GenericIdentityFn = identity;
  ```

- 泛型类

  ```typescript
  class GenericNumber<T> {
      zeroValue: T;
      add: (x: T, y: T) => T;
  }
  
  let myGenericNumber = new GenericNumber<number>();
  myGenericNumber.zeroValue = 0;
  myGenericNumber.add = function(x, y) { return x + y; };
  ```

  泛型指的是实例部分的类型，类的静态类型不能使用泛型类型

- 泛型约束

  ```typescript
  interface Lengthwise { // 接口描述了泛型约束的条件
      length: number;
  }
  
  function loggingIdentity<T extends Lengthwise>(arg: T): T {
      console.log(arg.length);  // Now we know it has a .length property, so no more error
      return arg;
  }
  ```

  泛型继承了接口，所以传入的类型必须是有 `length` 属性的类型

#### 枚举

> 使用枚举我们可以定义一些带名字的常量。 使用枚举可以清晰地表达意图或创建一组有区别的用例

- 数字枚举

  ```typescript
  enum Direction {
      Up = 1,
      Down,
      Left,
      Right
  }
  // 上面定义了一个数字枚举，Up的初始值为1，其余的自动增长，Down=2 Left=3 Right=4
  ```

  枚举的使用：通过枚举属性访问枚举成员，和枚举的名字来访问枚举类型

- 字符串枚举

  > 字符串枚举中，每个成员都必须使用字符串字面量，或者另一个字符串枚举进行初始化，字符串枚举没有初始化不能自动计算值

  ```typescript
  enum Direction {
      Up = "UP",
      Down = "DOWN",
      Left = "LEFT",
      Right = "RIGHT",
  }
  ```

- 异构枚举

  > 混合字符串和数字成员

  ```typescript
  enum BooleanLikeHeterogeneousEnum {
      No = 0,
      Yes = "YES",
  }
  ```
  
- 计算成员和常量成员

  > 计算成员：每个枚举成员都带有一个值，可以是常量，也可以是计算出来的
  >
  > 常量成员：
  >
  > 1. 枚举表达式字面量
  > 2. 对以定义常量枚举成员的引用
  > 3. 一元运算符
  > 4. 二元运算符

  ```typescript
  enum FileAccess {
      // 常量成员
      None,
      Read    = 1 << 1,
      Write   = 1 << 2,
      ReadWrite  = Read | Write,
      // 计算成员
      G = "123".length
  }
  ```

- 联合枚举和枚举成员类型

  > 字面量枚举成员：不带有初始值的常量枚举成员或值被初始化为字符串字面量，数字字面量

  

- 反向映射

  > 正向：key->value
  >
  > 反向：value->key

  ```typescript
  
  enum Enum {
      A
  }
  let a = Enum.A; // 正向
  let nameOfA = Enum[a]; // "A" 反向
  ```

- `const` 枚举

  > 为了避免额外生成代码的开销和额外的非直接的对枚举成员的访问，只能使用常量枚举表达式

  ```typescript
  const enum Enum {
      A = 1,
      B = A * 2
  }
  ```

#### 类型推论

> ts中没有明确指出类型的地方，类型推论会帮助提供类型

```typescript
let x = 3; // 这里没有明确指出 x 的类型
```

- 最佳通用类型

  ```typescript
  let x = [0, 1, null]; // 推断为
  
  
  let zoo = [new Rhino(), new Elephant(), new Snake()]; // 数组没有 Animal 类型，无法推断出该类型，需要指定
  // 如果没有指定，会推断为联合数组类型 (Rhino | Elephant | Snake)[]
  let zoo: Animal[] = [new Rhino(), newElephant(), new Snake()]
  ```

  

#### 类型兼容性

> 名义类型系统：数据类型的兼容性和等价性是通过明确的声明和类型的名称来决定的，如 java, c#
>
> 结构类型系统：基于类型的组成结构，不要求明确的声明，如 typescript

```typescript
interface Named {
    name: string;
}

class Person {
    name: string;
}

let p: Named;
// OK, because of structural typing
p = new Person();
```

上面的代码 `Person` 类没有明确说明继承了 `Named` 接口，这在名义类型系统中会报错，但在结构类型系统中是正确的



- 结构类型系统

  > 如果x要兼容y，那么y至少具有与x相同的属性

  ```typescript
  interface Named {
      name: string;
  }
  
  let x: Named;
  // y's inferred type is { name: string; location: string; }
  let y = { name: 'Alice', location: 'Seattle' };
  x = y;
  //检查y能否赋值给x，y的属性中必须包含名字是 name 的 string 类型的成员，y满足条件，赋值正确
  ```

- 比较两个函数

  ```typescript
  let x = (a: number) => 0;
  let y = (b: number, s: string) => 0;
  
  y = x; // OK, x对应的参数必须能在y中找到对应类型的参数
  x = y; // Error, y对应的参数s, 无法在x中找到对应的参数
  ```

  



### js

#### JS性能优化

##### 防抖与节流

- 防抖

  > 触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间

- 节流

  > 高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率

  ```js
  // 节流
  function throttle(fn, delay) {
      let valid = true
      return function () {
          if (!valid) {
              return false
          }
          valid = false
          setTimeout(() => {
              fn()
              valid = true
          }, delay)
      }
  }
  // 防抖
  function debounce(fn, delay) {
      let timer = null
      return function () {
          if (timer) {
              clearTimeout(timer)
          }
          timer = setTimeout(fn, delay)
      }
  }
  
  function showTop() {
      var scrollTop = document.body.scrollTop || document.documentElement.scrollTop
      console.log("滚动条位置" + scrollTop)
  }
  window.onscroll = throttle(showTop, 1000)
  ```

#### `popstate` 事件

> 当活动历史记录条目更改时，将触发popstate事件



#### 输入框的 `blur` 事件与 `click` 事件冲突

> 原因：blur 事件在 click 之前触发
>
> 解决：
>
> 1. 延时
>
> 2. 可以在mousedown上阻止blur事件发生，然后再在click事件上触发blur事件



#### 模版字符串嵌套

```js
const imgUrl = `url(${require(`${bgImg}`)})`
```



#### `JS` 修饰器(`decorator`)

> 类似于 java 中的注解，修饰器是在编译时就执行的函数，只能修饰类，类的属性，类的方法，不能修饰函数和变量，因为函数和变量会提升

- `@inject("store1","store2")`

  给观察者组件注入可以访问的 `store `

- `@observer`

  定义该组件为观察者，可以使用 `store` 的属性和方法

#### 数组的 `find()` 方法

> 返回符合测试函数条件的第一个元素

和 `filter` 相比， `filter` 返回的是所有符合测试函数条件的数组

而 `find()` 只是返回 `filter` 数组的第一个元素

```js
arr = [
    {name: 'alice', age: 20, sex: '女'},
    {name: 'jack', age: 18, sex: '男'},
    {name: 'bob', age: 22, sex: '男'}
]

var item = arr.find(element => (age <= 20))	
//{name: 'alice', age: 20, sex: '女'}
```



#### 对象结构复制重命名

```js
const {data} = this.state
const {data: newData} = this.state
```

### 函数可读性

- RORO模式

  > 函数始终应该传入一个对象并返回一个对象

### css

#### 兼容问题

- 浏览器兼容问题

  - hack

    1. 火狐浏览器hack写法

       ```css
       // 火狐浏览器样式兼容
       @-moz-document url-prefix() {
           .vjs-slider-vertical .vjs-volume-level:before {
               left: -0.3em;
       
           }
       
           .video-js .vjs-play-progress::before {
               top: -0.1em;
               font-size: 1em
           }
       }
       ```

    2. safari浏览器hack写法

       ```css
       //safari浏览器样式兼容
       @media not all and (min-resolution:.001dpcm) {
           @supports (-webkit-appearance:none) {
       
               .vjs-slider-vertical .vjs-volume-level:before {
                   left: -0.4em;
               }
           }
       }
       ```

  - 样式覆盖

    

  - css前缀

- 移动端兼容问题

  - `@media`

  - 判断 `pc` 端还是移动端

    1. ```javascript
       /Mobi|Android|iPhone/i.test(navigator.userAgent); //不可靠，userAgent字段可修改
       ```

    2. ```javascript
       const isMobile = navigator.userAgentData.mobile; //safari，Firefox不支持
       ```

    3. ```javascript
       /Android|iPhone|iPad|iPod/i.test(navigator.platform)// 已废弃，但所有浏览器都支持
       ```
       
    4. 通过屏幕宽度判断
    
       ```js
       if(window.screen.width<500){
           //移动设备（横屏无法识别）
       }
       ```
    
    5. ```javascript
       if(typeof window.orientation !== 'undefined'){
           // 当前设备时移动设备（只有移动设备有orientation这个侦测屏幕方向的属性）
       }
       ```
    
    6. ```javascript
       function isMobile(){
           return ('ontouchstart' in document.documentElement) // 只有移动设备有触摸事件
       }
       ```

#### 滚动吸顶

`position: sticky;`



#### Flex 默认样式

- 把所有子项变成水平排列
- 默认不自动换行
- 让子项与其内容等宽，并把所有子项的高度变为最高子项的高度

#### 页面跳转出现滚动条闪烁问题

> 不同的页面在同一个元素内滚动，需要将滚动条约束在页面的最外层元素。

#### `css` 中使用 `calc` 符号前后需要空格

#### 解决flex布局中between的布局问题

> 当出现多行数量不同时，显示问题很大

grid 布局可以很好解决该问题

```css
.wrap {
    width: 100px;
    display: grid;
    grid-template-columns: repeat(3, 20px);
    /* grid-column-gap: 20px; */
    row-gap: 20px;
    /* justify-items: start center end; */
    justify-content: space-between;
    border: 1px solid #eee;
}

.wrap>div {
    width: 20px;
    height: 20px;
    background: red;
    text-align: center;
    line-height: 20px;
}
```

 ![image-20211026143939097](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211026143939097.png)

#### 行内样式的缺点

1. 样式不能复用
2. 样式权重太高，样式不好覆盖
3. 表现层与结构层没有分离
4. 不能进行缓存，影响加载效率



#### 多行文字溢出...

```css
display: -webkit-box;
/* autoprefixer: off */
-webkit-box-orient: vertical;
/* autoprefixer: on */
-webkit-line-clamp: 2;
overflow: hidden;
word-break: break-all;
```

#### 边框渐变

```css
.border-block {
  border: 10px solid transparent;
  border-image: linear-gradient(to top, #F80, #2ED);
  border-image-slice: 10;
}
```

边框渐变无法设置圆角，所以无法写出圆角的边框渐变

#### 安卓和iso字体加粗兼容

iso可以在 `font-family` 中 `-` 后写字体的加粗

```css
font-family: PingFangSC-Semibold;
```

而在安卓中只能通过 `font-weight` 进行字体加粗

#### Box-shadow



#### 扫光特效

> 将半透明的光条图切图作为背景图，动画调整`background-position`

```css
animation: saoguang2 1s cubic-bezier(0.33, 0, 0.67, 1.00) .5s infinite;

@keyframes saoguang2 {
  0% {
    background-position: top 0 left -61px;
  }

  100% {
    background-position: top 0 left 92px;
  }
}
```



#### 波纹特效

> 将多个有shadow的按不同的开始时间调整大小和透明度

```css
.water1,
.water2 {
  position: absolute;
  width: 24px;
  height: 24px;
  border: 1px solid rgba(255, 255, 255, 0.90);
  box-shadow: inset 0 0 26px 0 #FFFFFF;
  border-radius: 50%;
  opacity: 0;
}

@-webkit-keyframes wateranimate {
  0% {
    -webkit-transform: scale(0);
    opacity: 0.5;
  }

  100% {
    -webkit-transform: scale(1.5);
    opacity: 0;
  }
}

@keyframes wateranimate {
  0% {
    -webkit-transform: scale(0);
    transform: scale(0);
    opacity: 0.5;
  }

  100% {
    -webkit-transform: scale(1.5);
    transform: scale(1.5);
    opacity: 0;
  }
}
```



#### `accent-color`

选择框选中时的颜色

### html

#### 概念
- 直播回传
  通过直播间链接跳到第三方页面，第三方页面需要将部分数据返回给直播平台
  
- 无障碍
  
  帮着开发者和使用者以及浏览器更好的解读网页
  
- 代码分割

  项目打包后，将将代码分别打包，加载网页时只加载需要的依赖

#### `video.js` 的使用

```js
this.player = videojs('player', {
  controls: true,
  controlBar: {
    children: [ //显示那些控件
      { name: 'playToggle' }, //播放按钮
      { name: 'currentTimeDisplay' }, //当前播放时间
      { name: 'timeDivider' }, //分隔符
      { name: 'durationDisplay' }, //总时长
      { name: 'volumePanel', inline: false }, // 音量按钮
      { name: 'FullscreenToggle' }, // 全屏按钮
      { name: 'progressControl' }, // 进度条

    ],

  },

  preload: 'auto',
});
this.player.src(src);
```



#### 播放器媒体接口

> 常用方法:
>
> load() 加载
>
> play() 播放
>
> pause() 暂停
>
> 常用属性:
>
> currentTime 视频播放的当前进度
>
> duration 视频的总时间 100000/60 (以秒为单位 ，同时带有小数点)
>
> paused 视频播放的状态
>
> 常用事件：
>
> oncanplay: 事件在用户可以开始播放视频/音频（audio/video）时触发。
>
> ontimeupdate: 通过该事件来报告当前的播放进度.
>
> onended: 播放完时触发—重置



#### 浏览器调试

1. 模拟不同网络环境下页面的表现

    ![image-20210722113337298](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20210722113337298.png)

2. 清除localStorage

    ![image-20211125115915982](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211125115915982.png)

3. debugger

    ![image-20211125120043687](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211125120043687.png)

5. 请求参数

    ![image-20211125120241702](https://gitee.com/buxiaoxing/image-bed/raw/master/img/image-20211125120241702.png)

   再使用base64解码

#### serve本地服务器

- 安装

  `npm i serve -g`

- 使用

  `serve [文件夹]`

  或者直接在当前文件夹 `serve`



### 随笔

> - 我知道我终会死去，正如我知道明天的太阳会从东方升起，我只是希望在我垂死之际，除了回忆，还有别的东西帮我克服恐惧，比如这本日记
>
> - 这种不爽就喷的态度太容易污染人了，因为太简单了，不用思考，只需要暴露人性本恶的丑态再动动手指就行，还能博得认同

- 埋点

  - `sensorsTrack` 与 `trackEvent`
  - 产品 `id`

