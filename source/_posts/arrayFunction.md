---
title: javascript 数组方法归纳
date: 2021-10-27 23:14:09
author: cookie
img: ../images/57.jpg
top: true
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/34.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: javascript 数组方法归纳
categories: javascript
tags:
  - javascript
  - function
---
## 1、javascript 数组函数汇总

*   `toString()` 把数组转化为字符串，并返回结果。
*   `indexOf()` 搜索数组中的元素，并返回它所在的位置。
*   `lastIndexOf()` 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。
*   `forEach()` 数组每个元素都执行一次回调函数。
*   `concat()` 连接两个或多个数组，并返回已连接数组的副本。
*   `join()` 把数组的所有元素放入一个字符串中。
*   `reverse()` 反转数组的元素顺序。
*   `slice()` 选取数组的一部分，并返回一个新数组。
*   `sort()` 对数组的元素进行排序。
*   `splice()` 从数组中添加或删除元素。
*   `pop()` 删除数组的最后一个元素并返回删除的元素。
*   `push()` 向数组的末尾添加一个或更多元素，并返回新数组的长度。
*   `shift()` 删除并返回数组的第一个元素。
*   `unshift()` 向数组的开头添加一个或更多元素，并返回新的长度。
*   `includes()` 判断一个数组是否包含一个指定的值。
*   `fill()` 使用一个固定值来填充数组。
*   `find()` 返回符合传入测试（函数）条件的数组元素。
*   `findIndex()` 返回符合传入测试（函数）条件的数组元素索引。
*   `isArray()` 判断对象是否为数组。
*   `map()` 通过指定函数处理数组的每个元素，并返回处理后的数组。
*   `some()` 检测数组元素中是否有元素符合指定条件。
*   `every()` 检测数组元素的每个元素是否都符合条件。
*   `filter()` 检测数值元素，并返回符合条件所有元素的值。

| 方法 | 描述 |
| --- | --- |
| **concat()** | 连接两个或多个数组，并返回已连接数组的副本。 |
| copyWithin() | 将数组中的数组元素复制到指定位置或从指定位置复制。 |
| entries() | 返回键/值对数组迭代对象。 |
| **every()** | 检查数组中的每个元素是否通过测试。 |
| **fill()** | 用静态值填充数组中的元素。 |
| **filter()** | 使用数组中通过测试的每个元素创建新数组。 |
| find() | 返回数组中第一个通过测试的元素的值。 |
| findIndex() | 返回数组中通过测试的第一个元素的索引。 |
| **flat()** | 创建一个新数组，其中所有子数组元素以递归方式连接到指定深度。 |
| **flatMap()** | 使用映射函数映射每个元素，然后将结果压缩成一个新数组 |
| **forEach()** | 为每个数组元素调用函数。 |
| **from()** | 从对象创建数组。 |
| includes() | 检查数组是否包含指定的元素。 |
| **indexOf()** | 在数组中搜索元素并返回其位置。 |
| **isArray()** | 检查对象是否为数组。 |
| **join()** | 将数组的所有元素连接成一个字符串。 |
| keys() | 返回 Array Iteration 对象，包含原始数组的键。 |
| **lastIndexOf()** | 在数组中搜索元素，从末尾开始，并返回其位置。 |
| **map()** | 使用为每个数组元素调用函数的结果创建新数组。 |
| **of()** | 创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。 |
| **pop()** | 删除数组的最后一个元素，并返回该元素。 |
| **push()** | 将新元素添加到数组的末尾，并返回新的长度。 |
| **reduce()** | 将数组的值减为单个值（从左到右）。 |
| reduceRight() | 将数组的值减为单个值（从右到左）。 |
| **reverse()** | 反转数组中元素的顺序。 |
| **shift()** | 删除数组的第一个元素，并返回该元素。 |
| **slice()** | 选择数组的一部分，并返回新数组。 |
| **some()** | 检查数组中的任何元素是否通过测试。 |
| **sort()** | 对数组的元素进行排序。 |
| **splice()** | 从数组中添加/删除元素。 |
| **toString()** | 将数组转换为字符串，并返回结果。 |
| **unshift()** | 将新元素添加到数组的开头，并返回新的长度。 |
| valueOf() | 返回数组的原始值。 |
| values() | 返回一个新的数组迭代器对象，该对象包含数组中每个索引的值。 |

## 2、改变原数组的方法

| 方法 | 描述 |
| --- | --- |
| **pop()** | 删除数组的最后一个元素，并返回该元素。 |
| **push()** | 将新元素添加到数组的末尾，并返回新的长度。 |
| **shift()** | 删除数组的第一个元素，并返回该元素。 |
| **unshift()** | 将新元素添加到数组的开头，并返回新的长度。 |
| **sort()** | 对数组的元素进行排序。 |
| **reverse()** | 反转数组中元素的顺序。 |
| **splice()** | 从数组中添加/删除元素。 |

## 3、ES6数组新方法

| 方法 | 描述 |
| --- | --- |
| **from()** | 从对象创建数组。 |
| **of()** | 创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。 |
| copyWithin() | 将数组中的数组元素复制到指定位置或从指定位置复制。 |
| **fill()** | 用静态值填充数组中的元素。 |
| find() | 返回数组中第一个通过测试的元素的值。 |
| findIndex() | 返回数组中通过测试的第一个元素的索引。 |
| includes() | 检查数组是否包含指定的元素。 |
| entries() | 返回键/值对数组迭代对象。 |
| keys() | 返回 Array Iteration 对象，包含原始数组的键。 |
| values() | 返回一个新的数组迭代器对象，该对象包含数组中每个索引的值。 |
| **flat()** | 创建一个新数组，其中所有子数组元素以递归方式连接到指定深度。 |
| **flatMap()** | 使用映射函数映射每个元素，然后将结果压缩成一个新数组 |

## 4、数组方法归纳详解

### 数组迭代方法

#### forEach()

```javascript
    array.forEach(function(currentValue, index, arr), thisValue)

```

| 参数 | 描述 |
| --- | --- |
| `function(currentValue, index, arr)` | 必需。回调函数 |
| `currentValue` | 必需。当前元素 |
| `index` | 可选。 当前元素的索引值 |
| `arr` | 可选。当前元素所属的数组对象 |
| `thisValue` | 可选。传递给函数的值一般用”this”值。 如果这个参数为空，”undefined”会传递给”this”值。 |
| `返回值` | undefined |

forEach() 本身是不支持 continue 与 break 语句的，我们可以通过 some 和 every 来实现的。  
使用 return 语句实现 continue 关键字的效果：

##### continue 实现

```javascript
    var arr = [1,2,3,4,5]
    arr.forEach(item => {
      if(item === 3) return
      console.log(item)
    })
    // 输出 ： 1 2 4 5
    
    arr.some(item => {
      if(item === 3) return // 注意：不能使用 return false
      console.log(item)
    })
    // 输出 ： 1 2 4 5

```

##### break 实现

```javascript
    var arr = [1,2,3,4,5]
    arr.every(item => {
      console.log(item)
      return item !== 3
    })
    // 输出 ： 1 2 3

```

#### map()

```javascript
    array.map(function(currentValue,index,arr), thisValue)

```

| 参数 | 描述 |
| --- | --- |
| `function(currentValue, index,arr)` | 必需。回调函数 |
| `currentValue` | 必需。当前元素 |
| `index` | 可选。 当前元素的索引值 |
| `arr` | 可选。当前元素所属的数组对象 |
| `thisValue` | 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue，或者传入 null、undefined，那么回调函数的 this 为全局对象。 |
| `返回值` | 返回一个新数组，数组中的元素为原数组元素调用函数处理后的值。 |

#### filter()

##### 相等于一个数组元素过滤器，将符合条件的数组元素组成一个新的数组返回

##### filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素

注意：filter() 不会对空数组进行检测。  
注意：filter() 不会改变原始数组。

```javascript
    array.filter(function(currentValue,index,arr), thisValue)

```

| 参数 | 描述 |
| --- | --- |
| `function(currentValue, index,arr)` | 必需。回调函数 |
| `currentValue` | 必需。当前元素 |
| `index` | 可选。 当前元素的索引值 |
| `arr` | 可选。当前元素所属的数组对象 |
| `thisValue` | 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined” |
| `返回值` | 返回数组，包含了符合条件的所有元素。如果没有符合条件的元素则返回空数组。 |

#### some()

##### some() 方法用于检测数组中的元素是否满足指定条件（函数提供）

some() 方法会依次执行数组的每个元素：

*   如果有一个元素满足条件，则表达式返回true，剩下的元素不会再执行检测。
*   如果没有满足条件的元素，则返回false。

注意：filter() 不会对空数组进行检测。  
注意：filter() 不会改变原始数组。

```javascript
    array.some(function(currentValue,index,arr), thisValue)

```

| 参数 | 描述 |
| --- | --- |
| `function(currentValue, index,arr)` | 必需。回调函数 |
| `currentValue` | 必需。当前元素的值 |
| `index` | 可选。 当前元素的索引值 |
| `arr` | 可选。当前元素所属的数组对象 |
| `thisValue` | 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined” |
| `返回值` | 布尔值。如果数组中有元素满足条件返回 true，否则返回 false。 |

#### every()

##### every() 方法用于检测数组所有元素是否都符合指定条件（通过函数提供）。

every() 方法使用指定函数检测数组中的所有元素：

*   如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。
*   如果所有元素都满足条件，则返回 true。

注意： every() 不会对空数组进行检测。  
注意： every() 不会改变原始数组。

```javascript
    array.every(function(currentValue,index,arr), thisValue)

```

| 参数 | 描述 |
| --- | --- |
| `function(currentValue, index,arr)` | 必需。回调函数 |
| `currentValue` | 必需。当前元素的值 |
| `index` | 可选。 当前元素的索引值 |
| `arr` | 可选。当前元素所属的数组对象 |
| `thisValue` | 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined” |
| `返回值` | 布尔值。如果所有元素都通过检测返回 true，否则返回 false。 |