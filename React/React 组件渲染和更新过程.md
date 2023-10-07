#面试题 


### 渲染过程

- 实例props state
- 通过render函数 把js模拟的DOM结构通过createElement转换成vnode
- 通过patch 函数渲染到DOM上 （patch(elm, vnode) 或者 patch(vnode, newvnode)）



### 更新过程

- setState() -> 保存组件放到dirtyComponents组件中（可能有子组件）
- 把dirtyComponents中的组件通过render函数，转换成vnode
- 再通过patch(vnode, newvnode)更新组件