#面试题 

```js
Promise.resolve().then(()=>{
	console.log(0);
	return Promise.resolve(4)
}).then((res)=>{
	console.log(res);
})

Promise.resolve().then(()=>{
	console.log(1);
}).then(()=>{
	console.log(2);
}).then(()=>{
	console.log(3);
}).then(()=>{
	console.log(5);
})
```
答案：0 1 2 3 4 5；


## 分析
---

### then 的交替执行

- 如果有多个 fulfilled promise实例，同时执行then链式调用
- then会交替执行
- 这是编译器的优化，防止一个Promise占据太多时间


### then中返回promise实例

- 相当于多出了一个promise实例
- 也会遵循“交替执行”
- 它和直接申明一个promise实例，结果有些差异
	- 会慢两拍


### 慢两拍

- 第一拍：等待pending状态变成fulfilled状态
- 第二拍：then函数挂载到MicroTaskQueue（微任务队列）

以上面代码演示：
```js
Promise.resolve().then(()=>{
	// 第一拍 等待pending状态变成fulfill状态
	const p = Promise.resolve(0);
	
	Promise.resolve().then(()=>{
		// 第二拍 then函数挂载到微任务队列
		p.then((res)=>{
			console.log(res);
		}).then(()=>{
			console.log(1)
		}).then(()=>{
			console.log(2)
		}).then(()=>{
			console.log(3)
		}).then(()=>{
			console.log(4)
		})
	})
})
```


### 分析结果

- 输出0
- 交替执行
- 输出1
- 遇到then返回promise实例
- 慢第一拍
- 输出2
- 慢第二拍
- 输出3
- then挂载完毕
- 交替执行
- 输出4
- 交替执行
- 输出5


## 总结
---

- Event Loop、宏任务、微任务
- then交替执行
- then返回Promise实例会慢两拍