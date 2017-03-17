## react 业务及组件代码设计规范


## 基本编写框架【basic structure】

```javascript

    import { Component,PropTypes },React from 'react';
    import {render} from 'react-dom';
    class SomeComponent extends Component{
         static propTypes={
            /*
             * 对每个prop含义必须进行注释
             * 说明每个prop的类型
             */
            velocity:PropTypes.number,//滚动速度
            imageArray: PropTypes.array// 图片源
         }
         static defaultProps={
            /*
             * 依赖外界传递数据的默认参数
             */
            velocity:500,//滚动速度
            imageArray:[],//图片源
        }
        constructor(props){
            super();
            this.state={}
        }
        /*
         * 上升到被多个业务模块使用的组件
         * 尽量实现这个方法，以便其他开发者能够增加动态性
         */
        renderPlugins(){
            let { Plugins } = this.props;
            let dataModel = {...this.props,...this.state};
            if(typeof Plugins=='function'){;
                return <Plugins  dataModel={dataModel}/>
            }else{
                return Plugin;
            }
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

1. 上升为组件的React代码必须根据业务模型提供 *开发者API*

1. UI及功能层面插件

> 定义插件props为Plugins

2. UI层面插件

> 定义插件props为Plugins

## state 和 props组件设计界定

#### 界定原则

1. state和props数据信息保持最小的重复性

> state和props不要有信息重复，它们应该是完成组件渲染的必要数据。

> 组件及业务编写和react的top-level单向数据流保持一致，保持组件内部的数据来源明确而单一，增加程序健壮性















