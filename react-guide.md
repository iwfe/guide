#  React/JSX 编码规范

## 内容目录

  1. [基本规范](#basic-rules-基本规范)
  2. [ES6写法React class](#创建模块)
  3. [Do Not Use mixins](#不要使用mixins和contexttypes)
  4. [命名](#naming-命名)
  5. [声明模块](#declaration-声明模块)
  6. [代码对齐](#alignment-代码对齐)
  7. [单引号还是双引号](#quotes-单引号还是双引号)
  8. [空格](#spacing-空格)
  9. [属性](#props-属性)
  10. [Refs引用](#refs)
  11. [括号](#parentheses-括号)
  12. [标签](#tags-标签)
  13. [函数/方法](#methods-函数)
  14. [模块生命周期](#ordering-react-模块生命周期)
  15. [语法规范及原则](#syntax-语法建议及原则) 
  16. [组件设计原则](#principles-组件设计原则) 

## Basic Rules 基本规范

  - 每个文件只写一个组件.
  - 推荐使用JSX语法.
  - 不要使用 `React.createElement`.

## 创建模块

```jsx
    // bad
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

    // good
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }
```

```jsx
    // bad
    class Listing extends React.Component {
      render() {
        return <div>{this.props.hello}</div>;
      }
    }

    // bad (relying on function name inference is discouraged)
    const Listing = ({ hello }) => (
      <div>{hello}</div>
    );

    // good
    function Listing({ hello }) {
      return <div>{hello}</div>;
    }
```

## 不要使用mixins和contextTypes

  - 不要使用 mixins
  - 不要使用 contextTypes

## Naming 命名

  - **扩展名**: React模块使用 `.jsx` 扩展名.
  - **文件名**: 文件名使用帕斯卡命名. 如, `ReservationCard.jsx`.

    ```jsx
    // bad
    import reservationCard from './ReservationCard';

    // good
    import ReservationCard from './ReservationCard';

    // bad
    const ReservationItem = <ReservationCard />;

    // good
    const reservationItem = <ReservationCard />;
    ```

  - **模块命名**: 模块使用当前文件名一样的名称. 比如 `ReservationCard.jsx` 应该包含名为 `ReservationCard`的模块. 但是，如果整个文件夹是一个模块，使用 `index.js`作为入口文件，然后直接使用 `index.js` 或者文件夹名作为模块的名称:

    ```jsx
    // bad
    import Footer from './Footer/Footer';

    // bad
    import Footer from './Footer/index';

    // good
    import Footer from './Footer/';
    ```
  - **高阶模块命名**: 对于生成一个新的模块，其中的模块名 `displayName` 应该为高阶模块名和传入模块名的组合. 例如, 高阶模块 `withFoo()`, 当传入一个 `Bar` 模块的时候， 生成的模块名 `displayName` 应该为 `withFoo(Bar)`.

    ```jsx
    // bad
    export default function withFoo(WrappedComponent) {
      return function WithFoo(props) {
        return <WrappedComponent {...props} foo />;
      }
    }

    // good
    export default function withFoo(WrappedComponent) {
      function WithFoo(props) {
        return <WrappedComponent {...props} foo />;
      }

      const wrappedComponentName = WrappedComponent.displayName
        || WrappedComponent.name
        || 'Component';

      WithFoo.displayName = `withFoo(${wrappedComponentName})`;
      return WithFoo;
    }
    ```

  - **属性命名**: 避免使用DOM相关的属性来用作其他的用途。

    ```jsx
    // bad
    <MyComponent style="fancy" />

    // good
    <MyComponent variant="fancy" />
    ```

## Declaration 声明模块

  - 不要使用 `displayName` 来命名React模块，而是使用引用来命名模块， 如 class 名称.

    ```jsx
    // bad
    export default React.createClass({
      displayName: 'ReservationCard',
      // stuff goes here
    });

    // good
    export default class ReservationCard extends React.Component {
    }
    ```

## Alignment 代码对齐

  - 遵循以下的JSX语法缩进/格式. 

    ```jsx
    // good, 有多行属性的话
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // bad 
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // 若能在一行中显示, 直接写成一行
    <Foo bar="bar" />

    ```

## Quotes 单引号还是双引号

  - 对于JSX属性值总是使用双引号(`"`), 其他均使用单引号(`'`).
  > 为什么? HTML属性也是用双引号, 因此JSX的属性也遵循此约定.

    ```jsx
    // bad
    <Foo bar='bar' />

    // good
    <Foo bar="bar" />

    // bad
    <Foo style={{ left: "20px" }} />

    // good
    <Foo style={{ left: '20px' }} />
    ```

## Spacing 空格

  - 总是在自动关闭的标签前加一个空格，正常情况下也不需要换行.

    ```jsx

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

  - 不要在JSX `{}` 引用括号里两边加空格.

    ```jsx
    // bad
    <Foo bar={ baz } />

    // good
    <Foo bar={baz} />
    ```

## Props 属性

  - JSX属性名使用骆驼式风格`camelCase`.

    ```jsx
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo userName="hello"
         phoneNumber={12345678}/>
    ```

  - 如果属性值为 `true`, 可以直接省略.

    ```jsx
    // bad
    <Foo hidden={true} />

    // good
    <Foo hidden />
    ```

  - 避免使用数组的index来作为属性`key`的值，推荐使用唯一ID.

  ```jsx
  // bad
  {todos.map((todo, index) =>
    <Todo {...todo}
         key={index} />
  )}

  // good
  {todos.map(todo => (
    <Todo {...todo}
          key={todo.id}/>
  ))}
  ```

  - 对于所有非必须的属性，总是手动去定义`defaultProps`属性.

  >  propTypes 可以作为模块的文档说明, 并且声明 defaultProps 的话意味着阅读代码的人不需要去假设一些默认值。更重要的是, 显示的声明默认属性可以让你的模块跳过属性类型的检查.

  ```jsx
  // good
  import { Component,PropTypes },React from 'react';
    import {render} from 'react-dom';
    class BusinessLogic extends Component{
        /*
         * 对每个prop含义必须进行注释
         * 说明每个prop的类型
         */
        static propTypes={
            velocity:PropTypes.number,//滚动速度
            imageArray: PropTypes.array// 图片源
         }
        /*
         * props默认参数
         */
        static defaultProps={
            velocity:500,//滚动速度
            imageArray:[],//图片源
        }
        //不要使用context
        constructor(props,context){
            super();
            this.state = {}
        }
        render(){
            return <你的逻辑>
        }
    }
  ```

## Refs

  - 总是在Refs里使用回调函数.

    ```jsx
    // bad
    <Foo  ref="myRef"/>

    // good
    <Foo ref={(ref) => { this.myRef = ref; }}/>
    ```


## Parentheses 括号

  - 将多行的JSX标签写在 `()`里.

    ```jsx
    // bad
    render() {
      return <MyComponent className="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // good
    render() {
      return (
        <MyComponent className="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // good, 单行可以不需要
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

## Tags 标签

  - 对于没有子元素的标签来说总是自己关闭标签.

    ```jsx
    
    // bad
    <Foo className="stuff"></Foo>

    // good
    <Foo className="stuff" />
    
    ```

## Methods 函数

- 使用箭头函数来获取本地变量.
- 
```javaScript

    function ItemList(props) {
      return (
        <ul>
          {props.items.map((item, index) => (
            <Item
              key={item.key}
              onClick={() => doSomethingWith(item.name, index)}
            />
          ))}
        </ul>
      );
    }
```

- 在React模块中不要给私有函数添加 `_` 前缀

```jsx
    // bad
    React.createClass({
      _onClickSubmit() {
        // do stuff
      },
      // other stuff
    });

    // good
    class extends React.Component {
      onClickSubmit() {
        // do stuff
      }
      // other stuff
    }
```

## Ordering React 模块生命周期

  - `class extends React.Component` 的生命周期函数:

  1. 可选的 `static` 方法
  1. `constructor` 构造函数
  1. `componentWillMount` 模块渲染前
  1. `componentDidMount` 模块渲染后
  1. `componentWillReceiveProps` 模块将接受新的数据
  1. `shouldComponentUpdate` 判断模块需不需要重新渲染
  1. `componentWillUpdate` 上面的方法返回 `true`， 模块将重新渲染
  1. `componentDidUpdate` 模块渲染结束
  1. `componentWillUnmount` 模块将从DOM中清除, 做一些清理任务
  1. *点击回调或者事件处理器* 如 `onClickSubmit()` 或 `onChangeDescription()`
  1. *`render` 里的 getter 方法* 如 `getSelectReason()` 或 `getFooterContent()`
  1. *可选的 render 方法* 如 `renderNavigation()` 或 `renderProfilePicture()`
  1. `render` render() 方法

## syntax 语法建议及原则

- @,decorator语法来组装高阶组件
 
 ```jsx
    @connect()
    class Test extends Component{
    }
```

- do expression来处理简单的条件分支逻辑
 
 ```jsx
    do{
        if(condition1){
            <Component1 />
        }else if(condition2){
            <Component2 />
        }else{
            <Component3 />
        }
    }
```


## principles 组件设计原则
- state和props数据信息保持最小的重复性
- state和props不要有信息重复。
- 功能单一及DRY原则
- 代码编写不要出现重复代码

