# node

Node = Editor | Element | Text

NodeTree是一个标准树形结构

子节点key是`children`

Text必然是叶子节点
Editor必然是Root节点


```ts
export type NodeEntry<T extends Node = Node> = [T, Path]
```

# API

## ancestor

根据path获取节点, 是text则报错

PS: 是否有必要判定Text

## ancestors

根据path,给出所有祖先, 支持多级

## child

获取指定index位置的子节点

## *children

## common

寻找两条路径的common path然后获取节点

## descendant

根据路径寻找descendant

## descendants

nodes的结果中,过滤掉0节点的根

## elements

nodes遍历, 过滤出elements

## first

给定path的第一个节点, 可以跨层

## fragment

根据Rang拆分出Node下的Fragment, Rang必须包含到叶子节点

PR: 二次判定Range.includes(range, path)是否PERF

PR: 整个算法有性能优化空间

## get

根据Path获取Node

# has

同上 返回true/false

# isNode

RT

# isNodeList

RT, 照例判断第一个值

# last

给定path的末尾节点, 可以跨层

# leaf

get(path), 不是text则报错

PS: 是否有必要判定Text

# levels

给定Path, 按照path遍历输出经过的节点

# matches

糅合Element/Text的matches

# nodes

数遍历算法, 非递归实现, 使用一个visited Set用于记录path, 特殊的是参数

1. 有传递from/to 并不影响他从Root开始遍历
2. to要求节点必须在他之前
3. form要求节点从根走到from的分叉开始
4. pass允许设置条件，限制往下一级遍历，条件发生于往下层走的时候

PR: 为什么会允许遍历出[]?

# parent

给定path的parent

PS: 判定P是否text是否没有必要?

# string

递归所有Node下面子Text节点的String值的拼接, 高度优先

PS: 并不使用nodes遍历

# texts

递归所有texts节点, 使用nodes遍历