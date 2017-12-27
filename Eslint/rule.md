此规则用于避免代码在`语法`或`逻辑`上出错

* **确保能终止的for循环**

避免出现for死循环

规则设置：[for-direction](https://eslint.org/docs/rules/for-direction)

```js
'for-direction': 'error',
```

* **get方法必须有return返回值**

规则设置：[getter-return](https://eslint.org/docs/rules/getter-return)

```js
'getter-return': 'error',
```

* **循环中不使用await**

除非循环中的执行语句不是独立的，否则在循环中使用await是多余、影响性能的操作

规则设置：[no-await-in-loop](https://eslint.org/docs/rules/no-await-in-loop)

```js
'no-await-in-loop': 'off',
```

* **不使用比较运算符与-0比较**

可用`Object.is(x, -0)`方案

规则设置：[no-compare-neg-zero](https://eslint.org/docs/rules/no-compare-neg-zero)

```js
'no-compare-neg-zero': 'error',
```

* **条件语句中不执行赋值操作**

`if/for/while/do...while`中不使用赋值，否则令人疑惑这是否是个错误还是故意的；默认规则下通过括号包裹赋值语句，可以跳过限制

规则设置：[no-cond-assign](https://eslint.org/docs/rules/no-cond-assign)

```js
'no-cond-assign': 'error',
```

* **尽量不用console的报错提示方法**

此规则可使成品少出现`console.warn/error`这样的日志

规则设置：[no-console](https://eslint.org/docs/rules/no-console)

```js
'no-console': 'off',
```

* **不使用常量作为条件语句的判断条件**

除非是特别需求（死循环不断执行，一定条件跳出），否则使用常量作为判断条件是多余的

规则设置：[no-constant-condition](https://eslint.org/docs/rules/no-constant-condition)

```js
'no-constant-condition': [
  'error',
  {
    checkLoops: false
  }
]
```

* **正则表达式中禁止出现控制字符**

Control characters are special, invisible characters in the ASCII range 0-31, 一般不会使用这些字符

规则设置：[no-control-regex](https://eslint.org/docs/rules/no-control-regex)

```js
'no-control-regex': 'error',
```

* **禁止出现debugger**

@fixed

规则设置：[no-debugger](https://eslint.org/docs/rules/no-debugger)

```js
'no-debugger': 'error',
```

* **函数禁止出现重复的形参名**

function(a, b, a) {}

规则设置：[no-dupe-args](https://eslint.org/docs/rules/no-dupe-args)

```js
'no-dupe-args': 'error',
```

* **一个对象内禁止出现重复的key**

规则设置：[no-dupe-keys](https://eslint.org/docs/rules/no-dupe-keys)

```js
'no-dupe-keys': 'error',
```

* **switch case中禁止出现相同的条件分支**

规则设置：[no-duplicate-case](https://eslint.org/docs/rules/no-duplicate-case)

```js
'no-duplicate-case': 'error',
```

* **禁止出现空的代码块**

规则设置：[no-empty](https://eslint.org/docs/rules/no-empty)

```js
'no-empty': [
  'error',
  {
    allowEmptyCatch: true
  }
],
```

* **正则表达式中禁止出现空的字符类块**

禁止出现如下结构：`/^abc[]/.test("abcdefg")`；中括号内为空，没有存在意义

规则设置：[no-empty-character-class](https://eslint.org/docs/rules/no-empty-character-class)

```js
'no-empty-character-class': 'error',
```

* **catch中不对捕获的异常变量进行重新赋值**

规则设置：[no-ex-assign](https://eslint.org/docs/rules/no-ex-assign)

```js
'no-ex-assign': 'error',
```

* **禁止出现多余的boolean转换**

@fixed

规则设置：[no-extra-boolean-cast](https://eslint.org/docs/rules/no-extra-boolean-cast)

```js
'no-extra-boolean-cast': 'error',
```

* **禁止出现多余的括号**

@fixed ，有时添加括号便于理解代码结构逻辑

规则设置：[no-extra-parens](https://eslint.org/docs/rules/no-extra-parens)

```js
'no-extra-parens': [
  "error",
  "functions"
],
```

* **禁止出现多余的分号**

@fixed

规则设置：[no-extra-semi](https://eslint.org/docs/rules/no-extra-semi)

```js
'no-extra-semi': 'error',
```

* **禁止对声明函数进行重新赋值**

foo变量：声明函数function foo() {}不可重新赋值， 但函数表达式var foo = function() {}可以

规则设置：[no-func-assign](https://eslint.org/docs/rules/no-func-assign)

```js
'no-func-assign': 'error',
```

* **禁止在嵌套块中声明函数**

默认规则是只针对function

规则设置：[no-inner-declarations](https://eslint.org/docs/rules/no-inner-declarations)

```js
'no-inner-declarations': 'error',
```

* **禁止出现无效的正则表达式**

规则设置：[no-invalid-regexp](https://eslint.org/docs/rules/no-invalid-regexp)

```js
'no-invalid-regexp': 'error',
```

* **禁止出现特殊的空白字符**

规则设置：[no-irregular-whitespace](https://eslint.org/docs/rules/no-irregular-whitespace)

```js
'no-irregular-whitespace': [
  'error',
  {
    skipComments: false,
    skipRegExps: true,
    skipTemplates: true
  }
],
```

* **禁止直接调用全局对象作为方法**

error：var math = Math()

规则设置：[no-obj-calls](https://eslint.org/docs/rules/no-obj-calls)

```js
'no-obj-calls': 'error',
```

* **禁止直接调用对象原型的方法**

@ff 会用到 hasOwnProperty 来避免对于原型链的循环

规则设置：[no-prototype-builtins](https://eslint.org/docs/rules/no-prototype-builtins)

```js
'no-prototype-builtins': 'off',
```
* **禁止正则表达式中出现多个空格**

@fixed

规则设置：[no-regex-spaces](https://eslint.org/docs/rules/no-regex-spaces)

```js
'no-regex-spaces': 'error',
```

* **禁止数组中出现空项**

`error：var items = [,,]`

规则设置：[no-sparse-arrays](https://eslint.org/docs/rules/no-sparse-arrays)

```js
'no-sparse-arrays': 'error',
```

* **禁止在普通字符串出现模板字符串引入变量标识${}**

规则设置：[no-template-curly-in-string](https://eslint.org/docs/rules/no-template-curly-in-string)

```js
'no-template-curly-in-string': 'error',
```

* **禁止出现奇怪、令人疑惑的多行表达式**

比如以`.`/`,`结尾等，具体见规则设置

规则设置：[no-unexpected-multiline](https://eslint.org/docs/rules/no-unexpected-multiline)

```js
'no-unexpected-multiline': 'error',
```

* **禁止出现用不可能执行的语句**

比如return后的语句

规则设置：[no-unreachable](https://eslint.org/docs/rules/no-unreachable)

```js
'no-unreachable': 'error',
```

* **禁止finally中出现控制流语句**

finally中不直接进行返回/抛出异常

规则设置：[no-unsafe-finally](https://eslint.org/docs/rules/no-unsafe-finally)

```js
'no-unsafe-finally': 'error',
```

* **禁止直接对一些关系运算左运算符作非的操作**

@fixed 加上括号避免出现未知的运算顺序

规则设置：[no-unsafe-negation](https://eslint.org/docs/rules/no-unsafe-negation)

```js
'no-unsafe-negation': 'error',
```

* **使用isNaN()而非关系运算符判断是否为NaN**

规则设置：[use-isnan](https://eslint.org/docs/rules/use-isnan)

```js
'use-isnan': 'error',
```

* **必要的js注释**

规则设置：[valid-jsdoc](https://eslint.org/docs/rules/valid-jsdoc)

```js
'valid-jsdoc': [
  'warn',
  {
    requireReturn: false,
    requireReturnDescription: false
  }
],
```

* **typeof表达式后比较的是一个可用的字符串**

typeof返回的所有类型："undefined", "object", "boolean", "number", "string", "function" and "symbol"

规则设置：[valid-typeof](https://eslint.org/docs/rules/valid-typeof)

```js
'valid-typeof': 'error',
```
