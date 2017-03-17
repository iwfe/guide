## react 代码设计规范


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
         * 必须实现这个方法，以便增加动态性
         */
        renderPlugins(){
            let { Plugins } = this.props;
            if(typeof Plugins=='function'){
                return <Plugins />
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

```