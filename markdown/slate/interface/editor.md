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
4. 有inline/TextNode的节点则开始处理, 调用Editor.string获取文本，判定为获取到新block

PR: 此处是否有PERF优化点，`hasInlines`的节点 必然不会是TextNode

待调试 //TODO

5. advance包含大量UTF Dirty判定










