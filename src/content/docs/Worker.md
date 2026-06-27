---
title: Worker
---

## 创建 Worker 线程

```js
const worker = new Worker("/worker.js");
```

## 数据发送与接收

```js
// 主线程
worker.postMessage("Greeting from Main.js");

worker.addEventListener("message", (e) => {
  console.log(e.data);
});

// Worker 线程
self.postMessage("Greeting from Worker.js");

self.addEventListener("message", (e) => {
  console.log(e.data);
});
```

## 错误处理

- `error`：Worker 内部出现错误出发
- `messageerror`：`message` 事件接收到无法被反序列化的参数时触发

```js
// 主线程
worker.addEventListener("error", (err) => {
  console.log(err.message);
});

worker.addEventListener("messageerror", (err) => {
  console.log(err.message);
});

// Worker 线程
self.addEventListener("error", (err) => {
  console.log(err.message);
});

self.addEventListener("messageerror", (err) => {
  console.log(err.message);
});
```

## 关闭 Worker 线程

```js
// 主线程
worker.terminate();

// Worker 线程
self.close();
```

## Worker 线程引用其他 js 文件

```js
importScripts("./utils.js");
```

## ESModule 模式

```js
const worker = new Worker("/worker.js", {
  type: "module",
});
```