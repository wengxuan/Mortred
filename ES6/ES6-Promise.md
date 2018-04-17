# Promise #

### 0. Promise初衷 ###

- 将老的嵌套回调逻辑进行优化

<!-- lang:javascript-->
    // old
    runAnimation(0)
    setTimeout(function() {
      runAnimation(1)
      setTimeout(function() {
        runAnimation(2)
      }, 1000)
    }, 1000)

    // new
    function delay(interval) {
      return new Promise(function(resolve) {
        setTimeout(resolve, interval)
      })
    }
    runAnimation(0)
    delay(1000)
      .then(function() {
        runAnimation(1)
        return delay(1000)
      })
      .then(function() {
        runAnimation(2)
      })

### 1. Promise构造函数  ###

- 构造函数参数为一个函数

<!-- lang:javascript-->
    // 伪代码
    const p = new Promise (
      // 两个参数
      ( resolve, reject ) => {
        if (success)
          resolve(response)
        else if (error)
          reject(new Error())
      }
    )

### 2. Promise.prototype.then() / catch()  ###

- then() / catch()方法返回Promise对象 可链式调用

<!-- lang:javascript-->
    // 一般写法是then后接catch
    p.then(
      // resolve传递的参数
      (res) => {
        doSomething(res)
      }
    ).catch(
      // reject传递的参数
      (error) => {
        handleError(error)
      }
    )

### 3. Promise.all() / race()  ###

<!-- lang:javascript-->
    // 所有状态都变成fulfilled/resolve, p为fulfilled
    // 其中一个被rejected, 则p为rejected
    const p = Promise.all([p1, p2, p3])
    p.then(...).catch(...)

    // 第一个率先改变的决定p的状态
    const p = Promise.race([p1, p2, p3])
    p.then(...).catch(...)

### 4. Promise.resolve() ###

- 将现有对象参数转为Promise对象, 包括Promise实例 / jQuery生成的deferred对象 / thenable对象 / 字符串 / 无参数

<!-- lang:javascript-->
    // thenable对象
    let thenable = {
      then: function(resolve, reject) {
        resolve(42)
      }
    }

### 4. 链式处理 ###

<!-- lang:javascript-->
    var val = 1

    // 我们假设step1, step2, step3都是ajax调用后端或者是
    // 在Node.js上查询数据库的异步操作
    // 每个步骤都有对应的失败和成功处理回调
    // 需求是这样，step1、step2、step3必须按顺序执行
    function step1(resolve, reject) {
      console.log('步骤一：执行')
      if (val >= 1) {
        resolve('Hello I am No.1')
      } else if (val === 0) {
        reject(val)
      }
    }

    function step2(resolve, reject) {
      console.log('步骤二：执行')
      if (val === 1) {
        resolve('Hello I am No.2')
      } else if (val === 0) {
        reject(val)
      }
    }

    const step3 = {
      then: function(resolve, reject) {
        console.log('步骤三：执行')
        if (val === 1) {
          resolve('Hello I am No.3')
        } else if (val === 0) {
          reject(val)
        }
      }
    }
    /* or
    function step3(resolve, reject) {
      console.log('步骤三：执行')
      if (val === 1) {
        resolve('Hello I am No.3')
      } else if (val === 0) {
        reject(val)
      }
    }
    */

    new Promise(step1).then(function(val){
      console.info(val)
      return new Promise(step2) // 返回Promise对象
    }).then(function(val){
      console.info(val)
      return Promise.resolve(step3) // thenable对象
      // return new Promise(step3) // 返回Promise对象
    }).then(function(val){
      console.info(val)
      return val                // 返回字符串
    }).then(function(val){
      console.info(val)
      return val
    })

### 5. 条件处理 ###

<!-- lang:javascript-->
    function myPromiseFunction() {
      //Change the resolved value to take a different path
      return Promise.resolve(true)
    }

    function conditionalChaining(value) {
      if (value) {
        //do something
        return doSomething().then(doSomethingMore).then(doEvenSomethingMore)
      } else {
        //do something else
        return doSomeOtherThing().then(doSomethingMore).then(doEvenSomethingMore)
      }
    }

    function doSomething() {
      console.log("Inside doSomething function")
      return Promise.resolve("This message comes from doSomeThing function") // resolve返回的Promise对象
    }

    function doSomeOtherThing() {
      console.log("Inside doSomeOtherthing function")
      return Promise.resolve("This message comes from doSomeOtherThing function")
    }

    function doSomethingMore(message) {
      console.log(message)
      return Promise.resolve("Leaving doSomethingMore")
    }

    function doEvenSomethingMore(message) {
      console.log("Inside doEvenSomethingMore function")
      return Promise.resolve()
    }

    myPromiseFunction().then(conditionalChaining).then(function () {
      console.log("All done!")
    }).
    catch (function (e) {

    })

### Refs ###

[ECMAScript 6 入门](http://es6.ruanyifeng.com/#README)

[Introduction to ES6 Promises – The Four Functions You Need To Avoid Callback Hell](http://jamesknelson.com/grokking-es6-promises-the-four-functions-you-need-to-avoid-callback-hell/)

[JavaScript Promise 告别异步乱嵌套](https://segmentfault.com/a/1190000002395343)

[How to handle the if-else in promise then?](https://stackoverflow.com/questions/33257412/how-to-handle-the-if-else-in-promise-then)
