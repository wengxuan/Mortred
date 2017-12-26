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

除非循环中的执行不是独立的，否则在循环中使用await是多余影响性能的操作

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
