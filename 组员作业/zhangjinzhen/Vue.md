## Vue
>- 框架 需要ie9+ ，都不需要考虑兼容
>- 数组方法：push pop shift unshift splice slice concat indexof sort reverse forEach map join

### 一、框架中常用的数组方法
#####  1 .find   查询
-  方法是es6中的方法(不兼容)     
-  1.在数组中查找，如果返回true表示找到了，找到后会将当前item返回，如果没找到则返回undefined
- 2.查找到后停止循环

```
	var obj = arr.find(function (item) {
	    // if(item.name == 2) return true
	    return item.name == 6;
	});
	console.log(obj);
```


##### 2.map 映射 
-  将一个数组 变成另一个模样   修改
- 1.返回值是新数组，不会改变原数组，会将返回的值替换掉当前项

```
	/*var arr = [{name:1},{name:2},{name:3},{name:2}];
	var temp = {age:2};
	var newArr = arr.map(function (item) {
	    if(item.name == 2) return temp;
	    return item;
	});*/
	
	/*for(var i = 0;i <arr.length;i++){
	 var cur = arr[i];
	 if(cur.name == 2){
	 arr[i] = temp;
	 }
	 }*/
	 var fruits = ['苹果','香蕉','橘子'];  // ['<li>苹果</li>','<li>香蕉</li>','<li>橘子</li>']
	var newArr = fruits.map(function (item) {
	    return `<li>${item}</li>`;//用返回的值替换掉原项
	});
	console.log(newArr.join(''));
```

##### 3.filter 过滤
-  返回一个新数组
-  在函数中返回true表示这一项留下,返回false表示这一项删除掉

```
	var arr = [{name:1},{name:2},{name:3},{name:2}];
	//声明式（不关心怎么实现，按照方法来用就可以）
	var newArr = arr.filter(function (item) {
	    return item.name != 2;  //如果想删除某一项 都用!=
	});
	console.log(newArr);
	//命令式
	/*for(var i =0;i<arr.length;i++){
	    var cur = arr[i];
	    if(cur.name == 2){arr.splice(i,1); i--}
	}
	console.log(arr);*/
```

**find filter map的区别**

##### 4.for in/forEach/for of的区别
- for in 
	- 3.可以用来遍历数组和对象 
	- 1.key是字符串类型的  
	- 2.for in会遍历私有和公有属性(不想遍历的私有属性也会被遍历出来)
- for of 
	- 1.可以跳出循环 
	- 2.只会遍历数组中的内容 
	- 3.缺点 不能遍历对象
```
	var arr = [1,2,3,4];
	arr.name = 'jw';
	for(var value of arr){ // value代表数组的每一项
	   if(value == 3) break; //可以跳出循环
	   console.log(100);
	}
```

##### 5.reduce 收敛
>- 返回的结果是 多次叠加后的操作，你可以自己制定首次默认的第一项是多少

```
	var arr = [1,2,3,4,5,6];
	var n = 0;
	var result = arr.reduce(function (prev,next) {
	    //上一个默认是数组的第一项，下一个默认是数组的第二项
	    //上一个变成第一次返回的结果，下一个就是第三项
	    console.log(prev,next);
	    return prev+next;
	},50);
	console.log(result);
	//二维数组  二维数组扁平化
	var arr = [['北京'],['上海'],['广州']];//=> ['北京'，'上海','广州']
	var result = arr.reduce(function (prev,next) {
	    // prev ['北京'] next['上海']
	    // prev['北京','上海'] next['广州']
	    return prev.concat(next);
	});
	console.log(result);
	// filter forof reduce map find
```

### 二、Vue基础
#### 1、框架模式
##### 1.1、MVC
- M model数据
- V view 视图
- C controller 控制器

>  当用户改变页面时，会触发控制器,控制器会调用数据,将数据展示到对应的视图上 v->c->m->v

##### 1.2、MVVM（vue的框架模式）
- M:model 数据
- V:view 视图
- VM viewModel 视图模型

>  先将数据绑定在视图上，会监听视图的改变，视图改变后会触发数据的变化,这种实现是通过viewModel

 **压缩和不压缩的区别**
- 压缩后在写代码时，没有任何的警告。一般开发时选择未压缩版


#### 2、vue常用指令
- v-model(双向数据绑定，只能在表单元素上使用,将数据绑定在表单元素上,如果表单内容更改，会导致数据变化);
- v-html(可以将字符串的html转换成html);
- v-once(数据绑定一次，随后数据变化，不更新视图变化);
- v-text(和{{}}用法一致，用来将数据显示在视图上,防止单个元素闪烁);
- v-for(循环数组，对象，字符串 v-for="value of或者in均可 items");
- v-on(可以绑定事件 v-on:事件名="函数名",可以把v-on简写成@符号);
- v-show/v-if(控制元素的显示和隐藏,v-show控制的是样式 v-if控制的是dom的增加和删除)
#### 3、修饰符 
- .stop 阻止冒泡事件(停止向上传递)
- .capture 增加给父级的让事件从外到内执行，会在发生冒泡事件
- .self 由自己触发，不包括自己的子集
- .prevent 阻止默认行为
- .once 只绑定一次事件(在执行事件后移除事件)
- .code 根据键盘码触发事件 .enter .space .delete ....

#### 4、绑定动态属性
- 动态属性用“v-bind”绑定 可以简写成“:”
- 在绑定动态属性中有两个特殊class ,style

##### 4.1、class
- 对象绑定
```
.a{background:"red"}
.b{color:"green"}
<div :class="{a:flag,b:flag1}"></div>
data:{flag:true,flag1:true}
```
- 数组绑定
```
.a{background:"red"}
.b{color:"green"}
<div :class="[c1,c2]"></div>
data:{c1:'a',c2:'b'}
```
##### 4.2、样式绑定
```
<div :style="[s1,s2]"></div>
data:{s1:{background:'red'},s2:{color:'red'}}
```



#### 5、生命周期
- 针对的是组件，根组件也是组件，仍然遵循这个流程

```
	var vm = new Vue({
	        data: {msg: 'hello'},
	        // beforeCreate() {alert('创建之前');},  不使用
	        created() {alert('创建完成')},       // 创建完成，可以获取数据                                                                           
	        beforeMount() {alert('挂载之前');},
	        mounted() {alert('挂载完成');},        // 在mounted中也可以获取数据
	        beforeUpdate() {alert('更新之前');},
	        updated() {alert('更新完成');},
	        beforeDestroy() {alert('销毁之前')},
	        destroyed() {alert('销毁完成')},
	        message: '实例属性'
	    });
```