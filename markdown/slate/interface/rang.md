# Range

一个选择范围，起点叫anchor，终点叫focus

# API

## edges

返回2个边界点，reverse则互换，会判定点的次序

## end

返回重点，会判定点的次序

## equals

起点终点比较

## includes

3合一，一个rang是否包含path/point/rang

注意rang是交叉即可

PS: 无测试rang

## intersection

交叉

PS：无测试

## isBackward

是否反向

anchor > focus

## isCollapsed

折叠

anchor === focus

## isExpanded

anchor !== focus

## isForward

!isBackward

## isRange

判断是组件，而且前后点

PS: 是否内部tag标记

## points

generator 返回 前后2个点

## start

获得起点

## transform

改变Rang

affinity: 'forward' | 'backward' | 'outward' | 'inward' | null 

由于最终关联的是path.transform, 实际默认值就是forward

outward： 两侧扩张
inward: 两侧向内

PR: 奇怪的OP是固定的，必须给起点终点同时做OP

PS: 可以通过设置null来设置空的affinity

