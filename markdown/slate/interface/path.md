# Path

描述指定node在node tree中的位置，用number[]表示

# API

## ancestors

获取祖先列表

[0, 1, 2] => [[], [0], [0, 1]]

## common

寻找最大共同祖先

## compare

比较2个path的前后次序， -1/0/1

> => 1
= => 0
< => -1

从第一个不同的值开始判定

## endsAfter

后字节

## endAt

子序列节点

## endsBefore

前节点

## equals/isAfter/isAncestor/isBefore/isChild/isCommon/isDescendant/isParent/isSibling

RT

## relative

子结构


## isPath

数据结构判定

PS： 是否内置隐藏字段

## next

寻找兄弟节点，就是末尾+1

## parent

父亲节点，slice(0, -1)

## previous

寻找前兄弟节点，末尾-1

## level

平级展开

[0, 1, 2] => [[], [0], [0, 1], [0, 1, 2]]

## transform

转换path, 和OP有关，目前单元测试只有move_node

