# location

```ts
export type Location = Path | Point | Range
export type Span = [Path, Path]
```

span的好处是Pointer要求必须挂于叶子节点上，有offset，span无需