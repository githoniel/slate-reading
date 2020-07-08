# point

point用于指定`Text`中的位置，包含
- path: 树中text的位置
- offset: string的offset

# API

## compare 

比较2个点的前后次序， -1/0/1

> => 1
= => 0
< => -1

先判定path前后顺序，同一个节点再根据offset判定前后

## isAfter/isBefore/equals

1/-1/0

## isPoint

是对象，offset===numbner, path是正确path类型

PS: 不是特别严格，是否特殊标志位

## transform

根据操作，执行poit转换，使用immer不影响原点

PS：只改变点位置，不产生副作用，根据操作类型，移动point

PS: 魔术字符串为啥不enum, 缺单元测试


## PointEntry

Rang中编译point时返回ces

export type PointEntry = [Point, 'anchor' | 'focus']

