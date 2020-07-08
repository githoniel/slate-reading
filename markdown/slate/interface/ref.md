# path/range/point-Ref

这里类似React hook的Ref概念

一个普通的Path/Range/Pointer，在经过OP(opertion，可以是多次)后，指向的位置就过时了，不准确了

让用户重新取手动计算太费事了

所以引入了PathRef/RangRef/PointerRef，有slate内部更新维护ref对象，保证ref的实时有效性

## 实现

```ts
export const PATH_REFS: WeakMap<Editor, Set<PathRef>> = new WeakMap()
export const POINT_REFS: WeakMap<Editor, Set<PointRef>> = new WeakMap()
export const RANGE_REFS: WeakMap<Editor, Set<RangeRef>> = new WeakMap()
```

通过weakmap+Set实现


