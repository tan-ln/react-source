浏览器

```
刷新率 60hz (1帧 需要执行 16.66ms)
执行的任务：
  事件处理
  js 执行
  绘制、布局

  空闲时间

  浏览器任务

js 单线程，同步任务一个接一个执行
任务耗时长，超过一帧时间，导致卡顿感知明显甚至卡死

react 适合构建大型页面，对于浏览器的资源占用非常高 ====》react 并发

利用 浏览器空闲时间，执行 react 任务（以任务单元的形式执行）

？1. 是否存在下一个任务单元
  -- No 控制权交还浏览器
  -- Yes 执行任务单元

    ？是否还有剩余时间
      -- No 控制权交还浏览器
      -- Yes 循环步骤 1

```

Hooks

代数效应：把副作用从函数逻辑中抽离出来，使得函数的关注点保持纯粹

## Fiber 调度
基于 `requestIdleCallback` && `requestAnimationFrame`

- `requestAnimationFrame` 回调 在绘制之前执行
- `requestIdleCallback` 在绘制后

空闲时间恰好可以用来执行 `requestIdleCallback` 回调
```js
requestIdleCallback(myNonEssentialWork, { timeout: 2000 })
```

