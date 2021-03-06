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
    
    
    import { foo } from 'my_module';
    import { bar } from 'my_module';

    // equasls
    import { foo, bar } from 'my_module';
    
### 模块整体加载

    // circle.js
    export function area(radius) {
      return Math.PI * radius * radius;
    }
    export function circumference(radius) {
      return 2 * Math.PI * radius;
    }
    
    // main.js
    import * as circle from './circle';

    console.log(circle.area(2));
    console.log(circle.curcumference(3));
    
**circle对象不允许运行时改变**

### export default

前面的例子，用户需要知道需加载的变量名或函数名才行，否则还需查看模块的export的名称

为方便，就要用到export default，为模块指定默认输出

    // foo.js
    export default function() {
      cosole.log('foo');
    }
    
    // main.js
    import Hoo from './foo';
    Hoo();

此时不需要知道原函数什么名字，可以任意指定，注意import后不需要大括号

export default可用在非匿名函数上，此时原函数将对模块外部失效

    export default function foo() {...}
    
    // or
    function foo() {...}
    export default foo;
    
export default一个模块只能有一个默认输出，因此import后不需要大括号

    export default function foo() {...}
    import Hoo from './foo';
    
    export function foo() {...}
    import {foo} from './foo';

export default命令其实只是输出一个叫做default的变量，所以它后面不能跟变量声明语句

    // correct
    export var a = 1;

    // correct
    var a = 1;
    export default a;

    // false
    export default var a = 1;

### export 与 import的复合写法

    export { foo, bar } from 'my-module';
    
    // equals
    import { foo, bar } from 'my-module';
    export { foo, bar };

### 模块继承

> 模块circleplus继承circle

    // circleplus.js
    export * from 'circle';
    export var e = 2.71828182846;
    export default function(x) {
      return Math.exp(x);
    }
    
    import * as math from 'circleplus';
    import exp from 'circleplus';
    console.log(exp(math.e));
    
import exp为circleplus模块的默认方法

### import()动态加载(提案)

### refs: http://es6.ruanyifeng.com/#docs/module
