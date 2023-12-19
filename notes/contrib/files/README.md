# Explorer

导入

```ts
// vs/workbench/workbench.common.main.ts
// Explorer
import 'vs/workbench/contrib/files/browser/explorerViewlet';
import 'vs/workbench/contrib/files/browser/fileActions.contribution';
import 'vs/workbench/contrib/files/browser/files.contribution';
```

## 目录结构

```txt
├── browser
│   ├── editors
│   │   ├── binaryFileEditor.ts
│   │   ├── fileEditorHandler.ts
│   │   ├── fileEditorInput.ts
│   │   ├── textFileEditor.ts
│   │   ├── textFileEditorTracker.ts
│   │   └── textFileSaveErrorHandler.ts
│   ├── explorerService.ts
│   ├── explorerViewlet.ts
│   ├── fileActions.contribution.ts
│   ├── fileActions.ts
│   ├── fileCommands.ts
│   ├── fileImportExport.ts
│   ├── files.contribution.ts
│   ├── files.ts
│   ├── files.web.contribution.ts
│   ├── media
│   │   └── explorerviewlet.css
│   └── views
│       ├── emptyView.ts
│       ├── explorerDecorationsProvider.ts
│       ├── explorerView.ts
│       ├── explorerViewer.ts
│       ├── media
│       │   └── openeditors.css
│       └── openEditorsView.ts
├── common
│   ├── dirtyFilesIndicator.ts
│   ├── explorerModel.ts
│   ├── files.ts
│   └── workspaceWatcher.ts
├── electron-sandbox
│   ├── fileActions.contribution.ts
│   ├── fileCommands.ts
│   ├── files.contribution.ts
│   └── textFileEditor.ts
└── test
    └── browser
        ├── editorAutoSave.test.ts
        ├── explorerModel.test.ts
        ├── explorerView.test.ts
        ├── fileActions.test.ts
        ├── fileEditorInput.test.ts
        ├── fileOnDiskProvider.test.ts
        └── textFileEditorTracker.test.ts
```

[`vs/workbench/contrib/files/browser/views/explorerView.ts`](https://github.com/clovery/vscode/blob/main/src/vs/workbench/contrib/files/browser/views/explorerView.ts)

```
export class ExplorerView extends ViewPane {

}
```

## 选中文件

src/vs/workbench/contrib/files/browser/views/explorerView.ts

`createTree() -> this.tree.onDidOpen() -> this.editorService.openEditor()`


打开编辑器
src/vs/workbench/services/editor/browser/editorService.ts

`group.openEditor()'

src/vs/workbench/browser/parts/editor/editorGroupView.ts

FileEditorInput 位于 src/vs/workbench/contrib/files/browser/editors/fileEditorInput.ts，当打开文件，如果没有自定义编辑器类，则交给 FileEditorInput 处理。
