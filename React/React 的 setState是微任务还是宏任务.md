#面试题 


## setState是同步
---
- setState本质是同步任务，只是React把它做成异步的样子
- 因为考虑到性能，多次setState的时候，React会批量去处理，然后渲染一次
	- 只有在React 上下文和合成事件中，才会出现伪异步的情况
	- 不在React上下文中触发的，会以同步的方式执行
-


## 总结
---
- setState是同步执行，state是同步更新
- 因为是它是在微任务promise.then()之前执行，state已经计算完成了
- setState不是微任务也不是宏任务