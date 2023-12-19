# keybinding

1. 监听键盘事件 [keybindingService](https://github.com/clovery/vscode/blob/main/src/vs/workbench/services/keybinding/browser/keybindingService.ts#L255)
2. 注册快捷键 [KeybindingsRegistry](https://github.com/clovery/vscode/blob/main/src/vs/platform/keybinding/common/keybindingsRegistry.ts#L243) 
3. 解析注册的快捷键，调用处理器

## 流程

```ts
// vs/workbench/services/keybinding/browser/keybindingService.ts
export class WorkbenchKeybindingService extends AbstractKeybindingService {
  constructor() {
    // 监听键盘事件
    // https://github.com/clovery/vscode/blob/main/src/vs/workbench/services/keybinding/browser/keybindingService.ts#L255
    this._register(dom.addDisposableListener(window, dom.EventType.KEY_DOWN, (e: KeyboardEvent) => {
      const keyEvent = new StandardKeyboardEvent(e);
      this._dispatch(keyEvent, keyEvent.target);
    }));
  }
}

// vs/platform/keybinding/common/abstractKeybindingService.ts
export abstract class AbstractKeybindingService extends Disposable implements IKeybindingService {
  protected _dispatch(e: IKeyboardEvent, target: IContextKeyServiceTarget): boolean {
    return this._doDispatch(this.resolveKeyboardEvent(e), target, /*isSingleModiferChord*/false);
  }

  private _doDispatch(keybinding: ResolvedKeybinding, target: IContextKeyServiceTarget, isSingleModiferChord = false): boolean {
    // 解析获取注册的快捷键
		const contextValue = this._contextKeyService.getContext(target);
		const keypressLabel = keybinding.getLabel();
    const resolveResult = this._getResolver().resolve(contextValue, currentChord, firstPart);

    // 执行 command
    this._commandService.executeCommand(resolveResult.commandId).then(undefined, err => this._notificationService.warn(err));
  }
}

// vs/workbench/services/commands/common/commandService.ts
export class CommandService extends Disposable implements ICommandService {

  executeCommand<T>(id: string, ...args: any[]): Promise<T> {
    return this._tryExecuteCommand(id, args)
  }

  private _tryExecuteCommand(id: string, args: any[]): Promise<any> {
    // 获取命令
    const command = CommandsRegistry.getCommand(id)
    // 调用注册的 handler
    this._instantiationService.invokeFunction(command.handler, ...args)
  }
}
```

## 快捷键

### 保存

注册 `vs/workbench/contrib/files/browser/fileCommands.ts`

```ts
export const SAVE_FILE_COMMAND_ID = 'workbench.action.files.save'

KeybindingsRegistry.registerCommandAndKeybindingRule({
  when: undefined,
  weight: KeybindingWeight.WorkbenchContrib,
  primary: KeyMod.CtrlCmd | KeyCode.KEY_S,
  id: SAVE_FILE_COMMAND_ID,
  handler: accessor => {
    return saveSelectedEditors(accessor, { reason: SaveReason.EXPLICIT, force: true /* force save even when non-dirty */ });
  }
});
```

### 撤销 undo


`vs/editor/editorExtensions.ts` 定义 `UndoCommand` 用来管理撤销操作。

```ts
export const UndoCommand = registerCommand(new MultiCommand({

}))
```

不同的实现 implementations。

1. explorer
2. code-editor
