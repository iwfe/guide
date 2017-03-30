1. 空白
    1. 缩进
    2. 换行
    3. 空行
2. 变量
    1. 声明、获取（let、const）
    2. 驼峰
    3. 自解释
3. 符号
    1. 逗号
    2. 分号
    3. 引号
4. 模块
    1. 定义、引入
    2. 多模块

5. 注释
    1. 单行
    2. 多行
    3. 文件

空白
--
>缩进[建议]

    // bad
    switch (variable) {
    
      case '1':
        // do...
        break;
    
      case '2':
        // do...
        break;
    
      default:
        // do...
    
    }
    
    // good
    switch (variable) {
    
    ....case '1':
            // do...
            break;
    
    ....case '2':
            // do...
            break;
    
    ....default:
            // do...
    
    }
    
>换行

    // bad
    if( x > 10 && y < 5 && z && ...){
        
    }
    
    // better
    if(
        x > 10
        && y < 5
        && z
        && ...){
            
    }
    
    // good
    let xx = x > 10,
        yy = y < 5
        
    if(
        xx
        && yy
        && z
        && ...){
            
    }
    
    // bad 
    if(true) return 'ok';
    
    // good
    if(true){
        return 'ok';
    }
    
>空行（逻辑类似的分组，同时将不同逻辑的隔开；注释之前添加；return语句之前添加）

    // bad
    function fun(){
        let x = 0,
            y = 10;
        // x 大于 0时，...
        if( x > 0 ){
            // do...
        }
        // y 大于 5时，...
        if( y < 5 ){
            // do...
        }
        return {x,y};
    }
    
    // good
    function fun(){
        let x = 0,
            y = 10;
            
        // x 大于 0时，...
        if( x > 0 ){
            // do...
        }
        
        // y 大于 5时，...
        if( y < 5 ){
            // do...
        }
        
        return {x,y}
    }
    
变量
--

>声明、获取

    // 声明

    // bad
    var age = 30;
    
    // good
    let age = 30;
    
    // bad
    var PI = 3.1415926;
    
    // good
    const PI = 3.1415926
    
    --------------------------------------------------------
    
    // 获取
    
    // bad
    let company = {
        name:'iwjw',
        age:4
    }
    
    let name = company.name,
        age = company.age;
    
    // good
    let {name,age} = company;
    
    
    
    
>驼峰（类、构造函数大驼峰；常量全大写；其余变量小驼峰）

    class Person {
        
    }
    
    function Person {
        
    }
    
    const MAX_VALUE = 100;
    
    let myName = 'iwjw'

>自解释（变量名有意义）

    //Boolean（is、has开头）
    
    // bad
    let open = true;
    
    //good
    let isOpen = true;
    
    // bad
    let child = false;
    
    // good
    let hasChild = false;
    
    --------------------------------------------------------
    
    // 函数

    // bad
    function age(){
        return age;
    }
    
    // good
    function getAge(){
        return age;
    }
    
    --------------------------------------------------------
    
    // 事件
    
    // bad
    function submit(){
        
    }
    
    // good
    function onSubmit(){
        
    }
    
    // or
    
    function handleSubmit(){
        
    }
    
符号
--
>逗号（对象属性值最后不需要加逗号）

    // bad
    let company = {
        name:'iwjw',
        age:4,
    }
    
    // good
    let company = {
        name:'iwjw',
        age:4
    }


>分号

小组内部决定

>引号（单引号、双引号、反引号）

模块
--
>导入、导出（使用ES6模式，不要使用require，module.exports）

    export
    
    import

>多模块（建立index.js，统一导出）

    // index.js
    
    import a from 'a.js';
    import b from 'b.js';
    import c from 'c.js';
    
    export {a,b,c}
    
    //若名字较长，换行
    
    export {
        aaaaaaaaaaaaaaaa,
        bbbbbbbbbbbbbbbb,
        cccccccccccccccc
    }



注释
--
>单行

    let company = {
        // 公司名字
        name:'iwjw', 
        // 公司成立时间
        age:4 
    }
    
    // 注册路由
    router.map(require('./src/router/index.js'));
    
    let name = 'iwjw', // 公司名字
        age = 4; // 公司成立时间

>多行（类、函数）工具支持才好

    /**
     * [function description]
     * @param  {[type]} val [description]
     * @return {[type]}     [description]
     */

>文件

    /*
    * @Author: name
    * @Date:   2017-03-10 10:25:50
    * @Last Modified by:   name
    * @Last Modified time: 2017-03-10 11:10:10
    */