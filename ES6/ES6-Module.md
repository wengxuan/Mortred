# ES6-Module

### 严格模式(strict)

ES6模块自动采用严格模式，不管是否在模块头加了"use strict"

### export——模块对外接口

> 输出变量(variable)

    export var year = 2017;
    export var month = "Sep";
    
    // or
    var year = 2017;
    var month = "Sep";
    export {year, month};
    
> 函数或类(function/Class)

**别丢了大括号(Don't miss braces)**

    export function add(m, n) {
      return m + n;
    }
    // or
    function f() {}
    export {f};
    
    // mul func
    function v1() {...}
    function v2() {...}
    export {v1, v2};
    // use 'as' rename function
    // export {v1 as V1Func, v2 as V2Func};
    
> export输出接口与对应的值是动态绑定，通过该接口可以获取模块实时值

    export var foo = 'bar';
    setTimeout(() => foo = 'baz', 500);
    
### import加载模块

    import {year, month} from './date';
    // import {year, month} from './date.js';
    
    import { year as curYear } from './date';
    
    // from后使用绝对或相对路径(behind 'from' use absolute/relative path)

模块的导入，不带有路径，必须要有配置文件告诉js引擎模块的位置
    
    import { foo } from 'my_module';
    foo();
    
> import在编译阶段执行，在代码运行之前，会提升到整个模块头部

    foo();
    import { foo } from 'my_module';
    
由于import是静态执行，所有不能使用表达式和变量这些只有在运行中才能得到结果的语法结构

    // error
    import { 'f' + 'oo' } from 'my_module';
    let module = 'my_module';
    import { foo } from module;
    if (x === 1) {
      import { foo } from 'module1';
    } else {
      import { foo } from 'module2';
    }
    
 > import语句会执行所加载的模块，重复执行同一句import，只会执行一次
    
    // exec once
    import 'lodash';
    import 'lodash';
    
    
 
    
