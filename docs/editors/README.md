# 编辑器实例化

src/vs/workbench/browser/parts/editor/editorPanes.ts

```js
this.doInstantiateEditorPane();
```

- NativeTextFileEditor
- WebviewEditor

修改内容，回填到文件的处理逻辑

src/vs/workbench/browser/parts/editor/editorPanes.ts
这个文件负责确定编辑器的类型，并实例化。编辑器必须实现抽象类 EditorPane 定义的接口。

EditorPanes.doOpenEditor 打开编辑器，

调用 this.getEditorPaneDescriptor 方法，获取对应的编辑器。

可以通过搜索 `new SyncDescriptor(FileEditorInput)` 关键字，找到对应的 EditorPane。

createEditorControl 方法，使用 CodeEditorWidget 绘制编辑器

## NativeTextFileEditor

文件 src/vs/workbench/contrib/files/electron-sandbox/textFileEditor.ts 定义了 NativeTextFileEditor 类，该类继承自 TextFileEditor。NativeTextFileEditor 覆盖了父类中的 handleSetInputError 方法，对错误进行了特殊处理。

## 绘制 TextFileEditor

文件 src/vs/workbench/contrib/files/browser/editors/textFileEditor.ts 定义了 TextFileEditor 类，该类继承自 AbstractTextCodeEditor。

```
src/vs/workbench/browser/parts/editor/textCodeEditor.ts
	class AbstractTextCodeEditor extends AbstractTextEditor
		// 交给 CodeEditorWidget 绘制编辑器的视图部分
		this.createEditorControl(CodeEditorWidget)
	// src/vs/workbench/browser/parts/editor/textEditor.ts
	class AbstractTextEditor -> AbstractEditorWithViewState -> EditorPane
		this.createEditor

src/vs/editor/browser/widget/codeEditorWidget.ts
	class CodeEditorWidget
		_attachModel() -> this._createView -> new View

src/vs/editor/browser/view.ts
	ViewLines 负责绘制整个文件内容
```

## 恢复工作台状态

src/vs/workbench/browser/parts/editor/editorPart.ts

.createContentArea()
.doCreateGridControlWithPreviousState()

EditorGroupView 类传构造器入参 form，是之前状态保存的数据。

## 撤销重做

src/vs/editor/browser/coreCommands.ts
src/vs/platform/undoRedo/common/undoRedoService.ts
