### Vue 数值问题：

 <input v-model="xxx" id="y"> 然后你用 $('#y').val('xxxx’), 改不了vue对应的xxx的值的，

> 原因是：
> 走vue的路子的话 你改的是虚拟dom 再通过diff算法比对由vue自己去改真实dom  。 用jq的话就直接改了真实dom，vue是不会知道你干了啥玩意的


### 解决情况：

> 用 directives 自定义组件解决。详情在下得乐项目 ```admin/posts/_form```


### 具体解决过程：
> 待补充
