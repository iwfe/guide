## react 业务及组件代码设计规范

## 业务组件基本编写模式【Shape】

```javascript
    import { Component,PropTypes },React from 'react';
    import {render} from 'react-dom';
    class BusinessLogic extends Component{
        //原则上不要使用context
        constructor(props,context){
            super();
            this.state = {}
        }
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
        render(){
            return <你的逻辑>
        }
    }
```


## 公共组件基本编写模式【structure】

```javascript
    //定义基础类
    class BasicComponent extends Component{
        /*
         * 上升到被多个业务模块使用的组件
         * 尽量实现这个方法，以便其他开发者能够增加动态性
         */
        renderPlugins(){
            let { Plugins } = this.props;
            let dataModel = {...this.props,...this.state};
            return do{
                if(typeof Plugins=='function'){;
                    <Plugins  dataModel={dataModel}/>
                }else{
                    Plugins;
                }
            }
        }
    }
    //组合逻辑
    class SomeComponent extends BasicComponent{
         static propTypes={
            velocity:PropTypes.number,//滚动速度
            imageArray: PropTypes.array// 图片源
         }
         static defaultProps={
            velocity:500,//滚动速度
            imageArray:[],//图片源
        }
        constructor(props){
            super();
            this.state={}
        }
        render(){
            let { Plugins, ...rest} = this.props;
            return <div>
                        <你自己的逻辑 />
                        {Plugins && this.renderPlugins() }
                   </div>
        }
    }
    render(<SomeComponent />,'DOM Container')

```


## 组件设计基本对外API

#### 插件体系

1. 上升为组件的React代码必须根据业务模型提供 **开发者API**

2. UI及功能层面插件

> 定义插件props为Plugins

## state 和 props组件设计界定

### 界定原则

1. state和props数据信息保持最小的重复性

> state和props不要有信息重复。

> **组件的数据来源必须明确而单一，见第一条**

2. 函数式动态性

> 将render里面的动态逻辑抽象为function

3. do expression

> 三目运算符尽量采用do expression

```javascript
    do{
        if(condition1){
            result1
        }else if{
            result2
        }else{
            result3
        }
    }
```


##















