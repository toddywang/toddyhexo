---
title: lodash 解析
date: 2017-11-21 18:27:37
tags: lodash
author: Toddy
---

## "Array" 方法

>_.chunk(array, [size=1]);
将数组（array）拆分成多个 size 长度的区块，并将这些区块组成一个新数组。 如果array 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。
参数
array (Array): 需要处理的数组
[size=1] (number): 每个数组区块的长度
返回
(Array): 返回一个包含拆分区块的新数组（愚人码头注：相当于一个二维数组）。

```bash
例子

_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

源码：
```bash
function chunk(array, size, guard) {
    if ((guard ? isIterateeCall(array, size, guard) : size === undefined)) {
        size = 1;
    } else {
        size = nativeMax(toInteger(size), 0);
    }
    var length = array == null ? 0 : array.length;
    if (!length || size < 1) {
        return [];
    }
    var index = 0,
        resIndex = 0,
        result = Array(nativeCeil(length / size));

    while (index < length) {
        result[resIndex++] = baseSlice(array, index, (index += size));
    }
    return result;
}
```