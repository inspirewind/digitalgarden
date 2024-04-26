---
{"dg-publish":true,"permalink":"/笨蛋学渣想发NAR是否搞错了什么/JavaScript/05-Javascript 数据类型/"}
---

#### 1. 原始类型的方法


#### 2. 数字类型
#### 3. 字符串
#### 4. 数组
#### 5. 数组方法
#### 6. 可迭代对象
#### 7. Map and Set

##### Map

##### Set
在 JavaScript 和 Python 中，`Set` 是一个常用的数据结构，用于存储唯一的元素集合。虽然两种语言中 `Set` 的基本概念相同，但具体的 API 存在一些差异。下面的表格对比了 JavaScript 和 Python 中 `Set` 的主要 API：

| 功能描述 | JavaScript API | Python API |
| ---- | ---- | ---- |
| 创建空集合 | `new Set()` | `set()` |
| 添加元素 | `set.add(value)` | `set.add(value)` |
| 删除元素 | `set.delete(value)` | `set.discard(value)` |
| 检查元素是否存在 | `set.has(value)` | `value in set` |
| 集合长度/大小 | `set.size` | `len(set)` |
| 清空集合 | `set.clear()` | `set.clear()` |
| 遍历集合 | `set.forEach(callback)` | 使用循环如 `for value in set:` |
| 转换为数组/列表 | `Array.from(set)` | `list(set)` |
| 删除元素（有返回值） | N/A | `set.remove(value)` |
| 元素个数 | `set.size` | `len(set)` |
| 并集操作 | 使用构造函数和扩展运算符: `new Set([...setA, ...setB])` | `setA.union(setB)` 或 `setA \| setB` |
| 交集操作 | 使用构造函数和方法: `new Set([...setA].filter(x => setB.has(x)))` | `setA.intersection(setB)` 或 `setA & setB` |
| 差集操作 | 使用构造函数和方法: `new Set([...setA].filter(x => !setB.has(x)))` | `setA.difference(setB)` 或 `setA - setB` |
| 对称差分 | 使用构造函数和方法: `new Set([...setA].filter(x => !setB.has(x)).concat([...setB].filter(x => !setA.has(x))))` | `setA.symmetric_difference(setB)` 或 `setA ^ setB` |
| 判断子集 | N/A | `setA.issubset(setB)` |
| 判断超集 | N/A | `setA.issuperset(setB)` |

#### 8. WeakMap and WakeSet

通常，当对象、数组之类的数据结构在内存中时，它们的子元素，如对象的属性、数组的元素都被认为是可达的。
类似的，如果我们使用对象作为常规 `Map` 的键，那么当 `Map` 存在时，该对象也将存在。它会占用内存，并且不会被（垃圾回收机制）回收。
``` js
let john = { name: "John" };

let map = new Map();
map.set(john, "...");

john = null; // 覆盖引用

// john 被存储在了 map 中，
// 我们可以使用 map.keys() 来获取它
```

现在，如果我们在 weakMap 中使用一个对象作为键，并且没有其他对这个对象的引用 —— 该对象将会被从内存（和map）中自动清除。
``` js
let john = { name: "John" };

let weakMap = new WeakMap();
weakMap.set(john, "...");

john = null; // 覆盖引用

// john 被从内存中删除了！
```

`WeakMap` 不支持迭代以及 `keys()`，`values()` 和 `entries()` 方法。所以没有办法获取 `WeakMap` 的所有键或值。
`WeakMap` 只有以下的方法：
- `weakMap.get(key)`
- `weakMap.set(key, value)`
- `weakMap.delete(key)`
- `weakMap.has(key)`

#### 9. Object,keys, values, entries

#### 10. 解构赋值

#### 11. 日期和时间

#### 12. JSON方法， toJSON