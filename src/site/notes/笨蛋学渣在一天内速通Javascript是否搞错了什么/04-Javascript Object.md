---
{"dg-publish":true,"permalink":"/笨蛋学渣在一天内速通Javascript是否搞错了什么/04-Javascript Object/"}
---

#### 1. 对象
#### 2. 对象引用和复制
#### 3. 垃圾回收
#### 4. 对象方法， "this"

作为对象属性的函数被称为 **方法**。
##### 全局环境下的this
当函数在浏览器全局环境中被简单调用时：
- 非严格模式下`this`指向`window`; 
- 在`use strict`指明严格模式的情况下就是`undefined`
``` js
function f1 () { 
	console.log(this) 
} 
function f2 () { 
	'use strict' 
	console.log(this) 
} 
f1() // window 
f2() // undefined
```
"简单调用"指这是一个单纯的函数，前面没有`.`和对象。

##### 上下文对象调用中的this
```js
const person = {
    name: 'Lucas',
    brother: {
        name: 'Mike',
        fn: function() {
            return this.name
        }
    }
}
console.log(person.brother.fn())
```
在这种嵌套的关系中，`this`指向**最后**调用它的对象（即`.`前面的第一个对象），因此输出将会是：`Mike`

##### bind/call/apply改变this指向
TODO

##### 构造函数和this
TODO

##### 箭头函数中的this指向


#### 5. 构造器和操作符"new"
#### 6. 可选链"?."
#### 7. symbol类型
#### 8. 对象原始值转换

