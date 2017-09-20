# ES6学习笔记 #
学习资料： [http://es6.ruanyifeng.com/#README](http://es6.ruanyifeng.com/#README)

### 1. let & const  ###
- ***let*** 声明的变量只在所在的代码块内生效；***let*** 变量先声明，后使用；不允许重复声明；
- 避免在块级作用域中声明函数，如果需要，应写成函数表达式的形式（而非函数声明语句）

<!-- lang:javascript-->
	// 函数声明语句
	{
	 	let a = 'secret';
		function f() {
			return a;
		}
	}
	// 函数表达式
	{
	    let a = 'secret';
	    let f = function () {
	        return a;
	    };
	}
- ***const*** 声明只读常量，一旦声明，必须立即初始化，且不能改变；只在声明所在的块级作用域内有效；先声明，后使用；不允许重复声明；对于复合类型（对象、数组），***const*** 只保证指针固定，其指向的数据结构是可变的；如果想冻结对象，使用***Object.freeze*** 方法

<!-- lang:javascript-->
	const foo = Object.freeze({});	
	// 常规模式时，下面一行不起作用；
	// 严格模式时，该行会报错
	foo.prop = 123;
	
	// 彻底冻结对象方法	
	var constantize = (obj) => {
		Object.freeze(obj);
		Object.keys(obj).forEach( (key, i) => {
			if ( typeof obj[key] === 'object' ) {
				constantize( obj[key] );
			}
		});
	}
- 为了保持兼容性，***var*** 命令和***function*** 命令声明的全局变量，依旧是顶层对象的属性；另一方面规定，***let*** 命令、***const*** 命令、***class*** 命令声明的全局变量，不属于顶层对象的属性。

<!-- lang:javascript-->
	var a = 1;
	// 如果在Node的REPL环境，可以写成global.a
	// 或者采用通用方法，写成this.a
	window.a // 1
	
	let b = 1;
	window.b // undefined

### 2. 变量的解构赋值  ###
ES6允许按一定**模式**，从数组和对象中提取值，对变量进行赋值，即解构（Destructuring）。

- 数组解构赋值

<!-- lang:javascript-->
	let [a, b, c] = [1, 2, 3];
解构不成功，变量的值就等于***undefined***：

<!-- lang:javascript-->
	// foo的值都会等于undefined
	let [foo] = [];
	let [bar, foo] = [1];
解构不完全，等号左边模式只匹配一部分等号右边的数组：

<!-- lang:javascript-->
	let [x, y] = [1, 2, 3];
	x // 1
	y // 2
	
	let [a, [b], d] = [1, [2, 3], 4];
	a // 1
	b // 2
	d // 4
等号右边不是可遍历的解构，将会报错。
解构赋值允许指定默认值：

<!-- lang:javascript-->
	let [foo = true] = [];
	foo // true
	
	let [x, y = 'b'] = ['a']; // x='a', y='b'
	let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
如果一个数组成员不严格等于***undefined***，默认值不会生效

<!-- lang:javascript-->
	let [x = 1] = [undefined];
	x // 1
	
	let [x = 1] = [null];
	x // null      相当于默认值是1，但又给x赋了新值null
- 对象解构赋值

数组的元素是按次序排列的，而对象属性没有次序，变量必须与属性同名。

<!-- lang:javascript-->
	let { bar, foo } = { foo: "aaa", bar: "bbb" };
	foo // "aaa"
	bar // "bbb"
也可通过下面形式可使变量名与属性名不一致

<!-- lang:javascript-->
	let { foo: baz } = { foo: "aaa", bar: "bbb" };
	baz // "aaa"
	foo // error: foo is not defined
上面代码中，foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。

下面一个例子说明下什么是变量，什么是模式：

<!-- lang:javascript-->
	var node = {
	  loc: {
	    start: {
	      line: 1,
	      column: 5
	    }
	  }
	};
	
	var { loc, loc: { start }, loc: { start: { line }} } = node;
	line // 1
	loc  // Object {start: Object}
	start // Object {line: 1, column: 5}
上面代码有三次解构赋值，最后一次对line属性的解构赋值之中，只有line是变量，loc和start都是模式，不是变量。

有冒号的，冒号前的都是模式，不具有值。

对象的解构也可以指定默认值。

<!-- lang:javascript-->
	var {x = 3} = {};
	x // 3
	
	var {x, y = 5} = {x: 1};
	x // 1
	y // 5
- 字符串解构赋值

字符串被转为类似数组的对象，并且还有其属性

<!-- lang:javascript-->
	const [a, b, c, d, e] = 'hello';
	a // "h"
	b // "e"
	c // "l"
	d // "l"
	e // "o"
	
	let {length : len} = 'hello';
	len // 5
- 数值和布尔值解构赋值

解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于***undefined*** 和***null*** 无法转为对象，所以对它们进行解构赋值，都会报错。

<!-- lang:javascript-->
	let {toString: s} = 123;
	s === Number.prototype.toString // true
	
	let {toString: s} = true;
	s === Boolean.prototype.toString // true
	
	let { prop: x } = undefined; // TypeError
	let { prop: y } = null; // TypeError
- **函数参数解构赋值**

<!-- lang:javascript-->
	function add([x, y]){
	  return x + y;
	}
	
	add([1, 2]); // 3
函数参数的解构也可以使用默认值。

<!-- lang:javascript-->
	function move({x = 0, y = 0} = {}) {
	  return [x, y];
	}
	
	move({x: 3, y: 8}); // [3, 8]
	move({x: 3}); // [3, 0]
	move({}); // [0, 0]
	move(); // [0, 0]
下面的写法会得到不一样的结果

<!-- lang:javascript-->
	function move({x, y} = { x: 0, y: 0 }) {
	  return [x, y];
	}
	
	move({x: 3, y: 8}); // [3, 8]
	move({x: 3}); // [3, undefined]
	move({}); // [undefined, undefined]
	move(); // [0, 0]
上面代码是为函数move的参数指定默认值，而不是为变量x和y指定默认值，所以会得到与前一种写法不同的结果。

- **用途**

###### 交换变量的值

<!-- lang:javascript-->
	let x = 1;
	let y = 2;
	
	[x, y] = [y, x];
###### 从函数返回多个值

<!-- lang:javascript-->
	// 返回一个数组
	
	function example() {
	  return [1, 2, 3];
	}
	let [a, b, c] = example();
	
	// 返回一个对象
	
	function example() {
	  return {
	    foo: 1,
	    bar: 2
	  };
	}
	let { foo, bar } = example();
###### 提取JSON数据

<!-- lang:javascript-->
	let jsonData = {
	  id: 42,
	  status: "OK",
	  data: [867, 5309]
	};
	
	let { id, status, data: number } = jsonData;
	
	console.log(id, status, number);
	// 42, "OK", [867, 5309]
###### 函数参数默认值

<!-- lang:javascript-->
	jQuery.ajax = function (url, {
	  async = true,
	  beforeSend = function () {},
	  cache = true,
	  complete = function () {},
	  crossDomain = false,
	  global = true,
	  // ... more config
	}) {
	  // ... do stuff
	};
###### 遍历Map结构

<!-- lang:javascript-->
	var map = new Map();
	map.set('first', 'hello');
	map.set('second', 'world');
	
	for (let [key, value] of map) {
	  console.log(key + " is " + value);
	}
	// first is hello
	// second is world
