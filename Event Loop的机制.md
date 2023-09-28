#面试题 

## Event Loop（事件循环/事件轮询）
---

- JS是单线程执行
	- 不能同时执行JS和DOM渲染
- 就有了异步的解决方案
- 异步要基于回调来实现
- Event Loop 就是这个异步回调实现方案



## Event Loop 的过程
---

- 同步代码，一行一行的在call stack中执行
- 遇到异步代码，先”记录“起来，等待合适的时机（定时、网络请求）
- 时机到了，放入到callback queue中
- 当call stack 为空时（同步代码执行完了, 逻辑循环结束之后）
- 触发Event Loop机制
- 轮询查找callback queue，如果有回调方法则放入call stack 中执行
- 然后继续轮询（像永动机一样）





### 微任务 + DOM的情况下
1. call stack清空
2. 执行当前的微任务， macroTask
3. 尝试DOM渲染
4. 触发Event Loop 机制