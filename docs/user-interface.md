# User Interface

## 代码目录

`vs/workbench/browser/parts`


```
layoutService
```

`vs/workbench/browser/workbench.ts` -> `renderWorkbench`

创建不同的 `Parts`，之后调用 `Part.create`，来渲染不同的 `Part`。

`Part` 类位于 `vs/workbench/part.ts` 文件，其 `create` 方法，负责绘制 `UI` 部分。

## StatusbarPart

位于 `vs/workbench/browser/parts/statusbar/statusbarPart.ts` 文件，继承自 `Part`。

`vs/workbench/browser/parts/activitybarPart.ts` 界面最左侧的部分，宽度固定 48。

## 界面组成部分

定义枚举 Parts

vs/workbench/services/layout/browser/layoutService.ts#L16


## titlebar

`titlebar` 位于 `vs/workbench/browser/parts/titlebar`

编辑器上方的 Tabs，src/vs/workbench/browser/parts/editor/editorGroupView.ts 创建 DOM 节点，src/vs/workbench/browser/parts/editor/tabsTitleControl.ts 文件处理逻辑。

## 资料

- [User Interface](https://code.visualstudio.com/docs/getstarted/userinterface)
