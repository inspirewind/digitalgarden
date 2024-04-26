---
{"dg-publish":true,"permalink":"/笨蛋学渣想发NAR是否搞错了什么/JavaScript/02-Javascript 基础知识/"}
---

#### 1. Hello, world!

使用`<script>`标签将JavaScript 程序插入到 HTML 文档的任何位置。
```html
<!DOCTYPE HTML>
<html>
<body>
	<p>script 标签之前...</p>
	<script>
		alert('Hello, world!');
	</script>
	<p>...script 标签之后</p>
	
</body>
</html>
```

`<script>` 标签有一些现在很少用到的特性（attribute），如`type`，`language`等。
脚本文件可以通过 `src` 特性（attribute）添加到 HTML 文件中。
``` html
<script src = "main.js"></script>
```
也可以提供一个完整的URL地址：
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```

将更复杂的脚本存放在单独的文件中。使用独立文件的好处是浏览器会下载它，然后将它保存到浏览器的 [缓存](https://en.wikipedia.org/wiki/Web_cache) 中。之后，其他页面想要相同的脚本就会从缓存中获取，而不是下载它。所以文件实际上只会下载一次。这可以节省流量，并使得页面（加载）更快。

#### 2. 代码结构
##### 语句：
语句是执行行为（action）的语法结构和命令。语句之间可以使用分号进行分割。

##### 分号：
当存在换行符（line break）时，在大多数情况下可以省略分号。
**但存在 JavaScript 无法确定是否真的需要自动插入分号的情况。**

``` js
alert("Hello");
[1, 2].forEach(alert);
```
这段代码先显示`Hello`，再显示`1`，最后显示`2`

但如果删除 `alert` 语句后的分号：
``` js
alert("Hello")
[1, 2].forEach(alert);
```
只有第一个`Hello`会显示出来，然后浏览器报错：`TypeError: Cannot read properties of undefined (reading '2')`

##### 注释：
单行注释`//`
多行注释`/*. */`，多行注释不支持嵌套注释

#### 3. 现代模式， "use strict"

长久以来，JavaScript 不断向前发展且并未带来任何兼容性问题。新的特性被加入，旧的功能也没有改变。这么做有利于兼容旧代码，但缺点是 JavaScript 创造者的任何错误或不完善的决定也将永远被保留在 JavaScript 语言中。这种情况一直持续到 2009 年 ECMAScript 5 (ES5) 的出现。ES5 规范增加了新的语言特性并且修改了一些已经存在的特性。为了保证旧的功能能够使用，大部分的修改是默认不生效的。你需要一个特殊的指令 —— `"use strict"` 来明确地激活这些特性。

当它处于脚本文件的顶部时，则整个脚本文件都将以“现代”模式进行工作。
请确保 `"use strict"` 出现在脚本的最顶部，否则严格模式可能无法启用。只有注释可以出现在 `"use strict"` 的上面。没有类似于 `"no use strict"` 这样的指令可以使程序返回默认模式。

当你使用 [[笨蛋学渣想发NAR是否搞错了什么/JavaScript/01-Javascript简介#开发者控制台\|开发者控制台]] 运行代码时，请注意它默认是不启动 `use strict` 的。

现代 JavaScript 支持 “class” 和 “module” —— 高级语言结构（本教程后续章节会讲到），它们会自动启用 `use strict`。因此，如果我们使用它们，则无需添加 `"use strict"` 指令。

#### 4. 变量

在 JavaScript 中创建一个变量，我们需要用到 `let` 关键字。

TODO

#### 5. 数据类型

#### 6. 交互：alert、prompt 和 confirm
#### 7. 类型转换
#### 8. 基础运算符，数学运算
#### 9. 值的比较

在 JavaScript 中，`NaN` (Not a Number) 表示一个非数值的特殊标识，用于指示数值运算未能返回正常的数值结果。根据 IEEE 754 浮点数算术标准，**`NaN` 不等于包括它自身在内的任何值**。这是为了确保当不准确或不适当的运算尝试执行时，能够正确处理和标记，而不是默默地失败或产生误导性的结果。
如果我们想要判断一个值是否为`NaN`，在 ES6 中引入了 `Number.isNaN()` 方法，它提供了一种更严格的检测方式，只有当类型为数字且值为 `NaN` 时，才返回 `true`。
#### 10. 条件分支：if 和 '?'
#### 11. 逻辑运算符
#### 12. 空值合并运算符 '??'
空值合并运算符（nullish coalescing operator）是较新的Javascript特性，旧式浏览器可能需要[[笨蛋学渣想发NAR是否搞错了什么/JavaScript/03-代码质量#6. Polyfill和转译器\|polyfills]]，语法为`??`。
当一个值不是`null`也不是`undefined`时，称这个值是已定义的。
`a??b`的结果是：
- 如果`a`是已定义的，则结果为`a`
- 如果`a`不是已定义的（即它是`null`或`undefined`），则结果为`b`

纵观 JavaScript 发展史，或 `||` 运算符先于 `??` 出现。它自 JavaScript 诞生就存在了，因此开发者长期将其用于这种目的。

另一方面，空值合并运算符 `??` 是最近才被添加到 JavaScript 中的，它的出现是因为人们对 `||` 不太满意。

它们之间重要的区别是：

- `||` 返回第一个 **真** 值。
- `??` 返回第一个 **已定义的** 值。

换句话说，`||` 无法区分 `false`、`0`、空字符串 `""` 和 `null/undefined`。它们都一样 —— 假值（falsy values）。如果其中任何一个是 `||` 的第一个参数，那么我们将得到第二个参数作为结果。

不过在实际中，我们可能只想在变量的值为 `null/undefined` 时使用默认值。也就是说，当该值确实未知或未被设置时。

例如，考虑下面这种情况：
``` js
let height = 0

alert(height || 100); //100
alert(height ?? 100); //0
```
- `height || 100` 首先会检查 `height` 是否为一个假值，它是 `0`，确实是假值。
    - 所以，`||` 运算的结果为第二个参数，`100`。
- `height ?? 100` 首先会检查 `height` 是否为 `null/undefined`，发现它不是。
    - 所以，结果为 `height` 的原始值，`0`。

实际上，高度 `0` 通常是一个有效值，它不应该被替换为默认值。所以 `??` 运算得到的是正确的结果。

#### 13. 循环：while 和 for

#### 14. "switch" 语句
#### 15. 函数
#### 16. 函数表达式
#### 17. 箭头函数，基础知识