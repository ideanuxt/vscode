## Platform 启动流程

`src/vs/code/electron-main/window.ts`

加载 `'vs/code/electron-browser/workbench/workbench.html` 文件。

```js
load() ->
this._win.loadURL()
```

## Workbench 启动流程
