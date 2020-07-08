# Operation

操作

- NodeOperation
  - InsertNodeOperation
  - MergeNodeOperation
  - MoveNodeOperation
  - RemoveNodeOperation
  - SplitNodeOperation
  - SetNodeOperation

- TextOperation
  - InsertTextOperation
  - RemoveTextOperation

- SetSelectionOperation

# API

## isNodeOperation/isOperation/isSelectionOperation/isTextOperation

RT，是否通过隐藏字段实现？

## isOperationList

照例，数组和第一项

## inverse

获得反向操作

PS：关乎设计，如何保证反操作的简明转换

PS: 单测涉及到hyperscript
