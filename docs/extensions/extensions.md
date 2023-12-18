# extensions

```
installVSIXAction.run(vsixPaths?: URI[]) -> this.extensionsWorkbenchService.install(vsix)
-> extensionService.install(vsix)
```

## 安装扩展

vs/platform/extensionManagement/node/extensionManagementService.ts

## 读取 extension package.json 数据

```
getManifest(vsix: string)

'extension/package.json'
```

installFromZipPath(...)

## 调用扩展

## vscode 对象

[@types/vscode](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/vscode) 声明该对象的接口定义。

[src/vs/workbench/api/common/extHost.api.impl.ts](https://github.com/clovery/vscode/blob/387e2f39ebbbf50d4b488f900b2a745972764015/src/vs/workbench/api/common/extHost.api.impl.ts?_pjax=%23js-repo-pjax-container%2C%20div%5Bitemtype%3D%22http%3A%2F%2Fschema.org%2FSoftwareSourceCode%22%5D%20main%2C%20%5Bdata-pjax-container%5D#L99) 负责该对象的具体实现。

```ts
export function createApiFactoryAndRegisterActors(accessor: ServicesAccessor): IExtensionApiFactory {

}
```

