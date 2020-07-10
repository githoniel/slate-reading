# createEditor 

实现一些默认的接口

## apply(op)

1. transform ref
2. 旧有dirtyPath transform后，合并到新的dirtyPath, 注意newDirtyPath不处理
3. Editor.transform(editor, op)
4. editor.operations.push(op)
5. Editor.normalize(editor)
6. FLUSHING阶段， 有一个Promise.resolve延后操作
7. editor.onChange()
8. editor.operations = []

## addMark

Selection存在而且展开则设置mark，否则缓存Mark触发onChange()

## deleteBackward/deleteForward

RT

## insertText

1. 当前Selection插入

PR: 没有Selection无任何操作，是否给出警告

2. 如果属于一个inline节点的内的末尾，在插入inline后，

PS：看单元更好理解

3. 带masks，则插入新的text节点，否则只是写入text

## normalizeNode

格式化Node，格式化要求参考https://docs.slatejs.org/concepts/10-normalizing#built-in-constraints

1. children为空则添加一个text=''的text节点，无视void(规则第一条)

PS: void只是阻止遍历，不应当用于阻止选中

2. 判定是否允许子节点有inlines

- 根节点不允许（规则第五条）
- 元素节点则要求块节点的第一个节点决定子元素是否inline(规则第三条)

3. 循环遍历子元素

- 不允许的inlines节点将被移除 
- isInline节点前如果没有Text则插入空Text(规则第四条前半部分)
- 是末尾节点而且是inline则插入一个空节点

4. pre和当前都是text节点，处理文本合并(规则第二条)

- loose equal则合并
- 前置text=''则移除
- 是末尾text=''则移除

## removeMark

RT

# getDirtyPaths

OP带来的dirtyPath