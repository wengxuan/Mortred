# ES6 核心内容 #

ES6转码器 [https://babeljs.io/](https://babeljs.io/ "babel")

ES6常用特性： `let, const, class, extends, super, arrow function, template string, destructuring, default, rest arguments`


- ***let & const***

`let` 块级作用域

`const` 常量

- ***class extends super***

引入类Class的概念，写法更清晰易懂
<!-- lang: js -->
	class Animal {
	    constructor(){
	        this.type = 'animal'
	    }
	    says(say){
	        console.log(this.type + ' says ' + say)
	    }
	}
	
	let animal = new Animal()
	animal.says('hello') //animal says hello
	
	class Cat extends Animal {
	    constructor(){
	        super()
	        this.type = 'cat'
	    }
	}
	
	let cat = new Cat()
	cat.says('hello') //cat says hello

`this`关键字则代表实例对象。简单地说，`constructor`内定义的方法和属性是实例对象自己的，而`constructor`外定义的方法和属性则是所有实例对象可以共享的。
Class之间可以通过`extends`关键字实现继承。
`super`关键字，它指代父类的实例（即父类的`this`对象）。子类必须在`constructor`方法中调用`super`方法，否则新建实例时会报错。这是因为子类没有自己的`this`对象，而是**继承父类的`this`对象，然后对其进行加工**。如果不调用`super`方法，子类就得不到`this`对象。

- ***arrow function***




### Refs: ###

[https://segmentfault.com/a/1190000004365693](https://segmentfault.com/a/1190000004365693)
