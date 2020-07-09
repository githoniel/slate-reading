# Editor

所有编辑器的状态都将丢在Editor上，可以通过插件自己增加helper或者覆盖原有方法

## 基础属性

```ts
children: Node[] // 当前Editor的子节点，就是文档内容
selection: Range | null // 一个Selection只能是一个Range 不支持多个
operations: Operation[] // 所有applied过的操作
marks: Record<string, any> | null // 当前光标的属性，如果在光标处添加内容，就是注入marks的格式
```

## 函数覆写

目前函数覆写类似单向洋葱结构，采用一层闭包来实现

```ts
const { isInline, isVoid } = editor

editor.isInline = element => {
  return element.inline === true ? true : isInline(element)
}

editor.isVoid = element => {
  return element.void === true ? true : isVoid(element)
}

return editor
```

## API

### isEmpty



###  isNormalizing

是否在isNormalizing

### isStart

// TODO

### isVoid/isInline

需要外部实现，这里只实现了判定是否元素

### last

获取edge: end Path后获取node

### leaf

location获取leaf节点

### levels

遍历at位置的自身和所有父节点，直到根

### marks

// TODO

### next

// TODO

### node

根据location获取node

### nodes

// TODO

### normalize

// TODO

### parent

获取path所在的节点的父节点

### path

通过location获取path

type Location = Path | Point | Range

1. path

如果传入edge，则根据edge去获取Node.first/Node.last的path
不传入则原路返回

2. Range

如果传入edge，则根据edge去获取Range.start/Rang.end的Point的path
没有则取common的Path

3. point 

直接取path

### pathRef

创建pathRef

### pathRefs

获取editor对应的pathRef Set 

## point

获取location的起点或者终点point，必须传入edge

1. path

根据edge去获取Node.first/Node.last的path， 判断是否是TextNode，否则报错
再根据edge取开头或者结尾的offset

2. Range

根据edge取头尾

3. Point

原路

## pointRef

创建pointRef

## pointRefs

获取editor对应的pointRef Set 

## positions 

遍历所有Point可放置的位置

1. 必须指定at或者Editor有selection否则undefined
2. Void的节点不会进入遍历，但是直接返回所在节点的第一个textNode

```
All Element nodes must contain at least one Text descendant. If an element node does not contain any children, an empty text node will be added as its only child.
```

所以void节点也必须包含一个TextNode

3. inline节点则不处理
4. 有inline/TextNode的节点则开始处理, 调用Editor.string获取文本，判定为获取到新block， 怪异的hasInlines是为了block步进做判定

PR: 此处是否有PERF优化点, 单元测试覆盖也不够

5. advance包含大量UTF Dirty判定

PR: PUNCTUATION是否包含中文标点
PR: CHAMELEON只包含英文引号

## previous

//TODO

PR: 测试案例太简单

## range

根据location给出rang

## rangeRef

创建rangeRef

## rangeRefs

获取editor对应的rangeRef Set

## removeMark

只是一个接口，由上层实现

移除选取text的属性，无选区或者选区折叠则应用到editor.mark里，下次输入生效

## start

获取location的point edge=start

## string

获取location所在的文本

## transform

根据OP做节点操作

PR: OP经过type运算后应当as做类型缩小
PR: 单测就没有

- insert_node: 插入path所在位置的前面
PR: insert_node是否支持插入path的开头或者结尾？

- insert_text: 指定path必须是leaf节点，在offset位置插入文本

- merge_node: path位置的node和他的前置节点合并
1. 都是text节点
前置节点合并当前节点内容，当前节点删除
2. 都是非Text节点
前置节点的child添加当前节点
3. 否则禁止合并

PS: 设计的目的还是为了保证Pointer转换的稳定性

PR: position用于合并后的Pointer转换，这个值意义是什么暂时不清楚，合并后同path point offset += position

- move_node: node从path移动到new Path

1. 首先移动到自己的后台节点导致循环应用自然是不允许的
2. 先移除path的节点，做新path op转换后，插入新节点

- remove_node: RT

对选区来说比较复杂，如果，转换后可能选区点丢失, 2个点不同时丢失，意味着要保持选取

1. 遍历textNode节点，找出path左右两侧的节点
2. 前侧存在取前侧，后侧存在取后侧，否则取空放弃

- remove_text: RT

- set_node: 设置node属性

text/children是特殊属性不得设置

- set_selection: 设置选区

采用Object.assign来设置，所以可以单独设置anchor或者focus

- split_node: 拆分节点, 可以传入properties，合并给后加入的节点

1.textNode，position代表文字拆分的offset, 直接拆分文本即可，新增节点属性继承，加上properties
2.非text节点，position代表拆分的子节点序号，新增节点属性继承，加上properties

PS: position所在的文字/节点，属于后插入的节点

## unhangRange

hang是一种特殊的Rang状态

参考https://github.com/ianstormtaylor/slate/issues/3683，对选区而言会造成困扰，unhangRange通过转换rang来修正这个问题

PR: 代码中要求start.offset === end.offset === 0， 不符合issue解释

PR: 代码也只处理了end， 对start不做处理

PR: 为何before要用first当起点，貌似focus足够


## void

寻找当前位置以上的分支上的第一个void

## withoutNormalizing

中途关闭Normalizing执行fn后还原

PS: 此函数末尾会执行一次Normalize







