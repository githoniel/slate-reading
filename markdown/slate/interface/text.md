# Text

Text节点就是包含文字和属性的文字节点，必然是叶子节点, 因为无法包含子节点

## API

### equals

功能: 比较2个节点是否相同，loose模式会忽略text内容比较，要求其他值完全相同，所以包含2次属性遍历，

PS: 性能上可能需要优化

### isText

判断是否Text节点，要求是对象，而且.text属性是string，

PS: 这个不完全安全，是否采用内部标记比较来实现？

### isTextList

判断一个数组是否Text对象数据， 为了性能，判定是数组，长度不为0时第一项必须为Text

### matches

比较节点是否包含，单次属性遍历，不包含text值判定

### decorations

给指定范围的text追加属性，涉及到Range概念, 这里只需要使用Rang的起点和终点offset


分三种情况，

1. rang包含了text

分三种情况，rang位置不包含text, offset包含相等

```
text:      aaaaaaaa
rang: ------------------
```

2. rang位置不包含text

```
# 不包含相等
text:      aaaaaaaa
rang:               ---
# 不包含相等
text:      aaaaaaaa
rang: ---
```

PS: 特殊情况，起点位置是0，则不包含任何内容

3. rang在中间位置，必须分隔text

```
text:   aaaaaaaa
rang: -----
text:   aaaaaaaa
rang:         ------
```

拆分成before/middle/after, 拆分字符长度后，给与middle assign属性, 返回最终叶子节点数组

PS: 注意入参的textNode不能是数组只能是单个Text节点

PR: 存在BUG 边界情况是否允许分割出''空字段？

https://github.com/ianstormtaylor/slate/pull/3735