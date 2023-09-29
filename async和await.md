#面试题 

- ES7语法
- 同步语法，彻底消灭回调函数


- async 定义在函数名称前方
- await 后面追加Promise 和 添加了async的函数



### async 和 await 与promise的关系

- 虽然是同步执行，消灭回调函数
- 并不排斥Promise
- 而是相互相承



- async 函数返回Promise对象
- await 相当于 Promise的then
- try...catch来捕获异常，代替Promise的catch



### 异步的本质

- 虽说 async/await 是消灭异步回调的终极武器
- js还是单线程，还是需要异步回调，还得基于Event Loop
- async/await 只是一个语法糖


await 后面的代码就相当于一个异步回调


```js

async function getName(params) {
  return new Promise((resolve, reject)=>{
    setTimeout(()=>{
      resolve(111)
    },1000)
  })
}

async function as(params) {
}

console.log(1);
const res = await getName();
console.log(res); // 111
console.log(2); // 2

as().then((res)=>{
  console.log(11111);
}) // 11111


```