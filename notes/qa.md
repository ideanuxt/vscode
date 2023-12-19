## UI 组件 (Part) 是如何注册的

类 `Part` 初始化时，调用 `layoutService.registerPart(this)` 实现。

## layoutService

文件 `vs/workbench/services/layout/browser/layoutService.ts` 定义接口 `IWorkbenchLayoutService`。

文件 `vs/workbench/browser/layout.ts` 中，定义 `Layout` 类，实现接口 `IWorkbenchLayoutService`。

## Parts

在文件 `/vs/workbench/services/layout/browser/layoutService.ts` 定义了枚举类型的 `Parts`。

## 更改默认主题配置

`vs/workbench/common/theme.ts`

## 🤔

- viewport 尺寸改变，parts 如何重新计算布局？

点击 activitybarPart 的某项，sidebarPart 切换到对应的视图，二者如何关联的

CompositeActionViewItem 创建 composite bar 的成员。

- [ ] 如何实现一套代码，多平台运行？
