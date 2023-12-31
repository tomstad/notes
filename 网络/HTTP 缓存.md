#面试题 



- http的缓存机制（强缓存 + 协商缓存）
- 刷新操作方式，对缓存的影响



## 缓存
---
把一些没有必要在获取的东西，再重新获取

- 为什么需要缓存
	- cpu的计算都很快（毫秒级别），但是网络请求是最慢的，再怎么也需要个（几百毫秒）
	- 有些很关键的性能优化得从网络去入手（为了访问得更快）
		- 减少体积
		- 减少请求次数




## 强制缓存
---
- 客户端发出初次请求
- 服务端认为这个资源可以被缓存
- 返回资源并加上Cache-Contorl
- 这个资源就会被存在本地
- 当我们发出去第二次请求，如果Cache-Contorl设置的时间没有结束
- 浏览器会帮我们从本地去取这个资源，不会发送至服务端
- 但缓存失效时，我们会再次请求服务端



### Cache-Contorl

- max-age
- no-cache
- no-store
- private
- public


### Expires
- 也是控制缓存过期
- 被Cache-Contorl替代




## 协商缓存（对比缓存）
---
服务端缓存策略
服务端判断客户端资源，是否和服务端的一样

- 客户端发起初次请求
- 服务端认为需要缓存这个资源
- 返回资源和资源标识
- 再次请求到服务端的时候，服务端会对比这个标识，是否有更新，
- 如果没有，则返回304，从本地拿资源（体积小）
- 如果有，则返回新的资源和新的资源标识



### Etag（资源的唯一标识）服务端返回
### If-None-Match （资源的唯一标识）客户端发送的时候带上
### Last-Modified （资源最后修改时间）服务端返回
### If-Modified-Since （资源最后修改时间）客户端发送的时候带上





### Last-Modified和Etag的区别

- Etag的优先级更高
- Last-Modified 只精准到毫秒等级
- 资源被修改，内容不变，Etag会更加精确。




## 两者的关系
---
- 如果Cache-Contorl设置的缓存过期了
- 会去查看是否有Etg和Last-Modified
- 如果有的话会先去匹配





## 刷新网页对Http缓存的影响
---

- 正常操作 （就是首次进页面）强缓存有效，协商缓存有效
- 手动刷新（F5刷新）强缓存失效，协商缓存有效
- 强制刷新 （ctrl + f5）强制缓存失效，协商缓存失效