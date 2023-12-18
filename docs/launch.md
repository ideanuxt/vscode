# 启动流程

## Client

```sh
yarn watch
./scripts/code.sh # on MacOS
```

入口文件，完成宿主环境的启动。

```ts
// main.js
const { app, protocol, crashReporter } = require('electron');

app.once('ready', function () {
  onReady();
}

async function onReady() {
  startup();
}

function startup() {
  require('./bootstrap-amd').load('vs/code/electron-main/main', () => {

  })
}

// bootstrap-amd.js
exports.load = function (entrypoint, onLoad, onError) {
  loader([entrypoint], onLoad, onError);
};

// vs/code/electron-main/main.ts
class CodeMain {
  main(): void {
    this.startup();
  }

  private async startup(): Promise<void> {
    await instantiationService.invokeFunction(async accessor => {
      return instantiationService.createInstance(CodeApplication, mainProcessNodeIpcServer, instanceEnvironment).startup();
    }
  }
}

const code = new CodeMain();
code.main();

// vs/code/electron-main/app.ts
export class CodeApplication extends Disposable {
  async startup(): Promise<void> {
    // Open Windows
    const windows = appInstantiationService.invokeFunction(accessor => this.openFirstWindow(accessor, mainProcessElectronServer));
  }

  private openFirstWindow(accessor: ServicesAccessor, mainProcessElectronServer: ElectronIPCServer): ICodeWindow[] {
    return windowsMainService.open();
  }
}
// vs/platform/windows/electron-main/windowsMainService.ts
export class WindowsMainService extends Disposable implements IWindowsMainService {
  open() {
    this.doOpen();
  }

  doOpen() {
    this.openInBrowserWindow();
  }

  openInBrowserWindow() {
    const createdWindow = window = this.instantiationService.createInstance(CodeWindow);
    this.doOpenInBrowserWindow(window)
  }

  doOpenInBrowserWindow(window: ICodeWindow) {
    // Load it
    window.load(configuration);
  }
}

// vs/platform/windows/electron-main/window.ts
export class CodeWindow extends Disposable implements ICodeWindow {
  load(configuration: INativeWindowConfiguration, options: ILoadOptions = Object.create(null)): void {
    // Load URL
    this._win.loadURL(FileAccess.asBrowserUri(this.environmentMainService.sandbox ?
      'vs/code/electron-sandbox/workbench/workbench.html' :
      'vs/code/electron-browser/workbench/workbench.html', require
    ).toString(true))
  }
}
```

## Web

```sh
yarn watch-web
yarn web
```

## 统一的入口文件

最终会执行到 `vs/workbench/browser/workbench.ts`
