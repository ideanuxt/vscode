# QuickStart

```sh
# 安装依赖
yarn

# 监听文件改变
yarn watch-client

# start client on MacOS
./scripts/code.sh
```

## 打包

platforms: win32-ia32 | win32-x64 | darwin-x64 | darwin-arm64 | linux-ia32 | linux-x64 | linux-arm

```sh
yarn gulp vscode-darwin-x64
```

## MacOS 描述文件路径

```txt
/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/product.json
```

## eslint

VSCode 使用 `code-import-patterns` 来限定导入规则。

## 参考资料

- [Source Code Organization](https://github.com/microsoft/vscode/wiki/Source-Code-Organization)
- [How to Contribute](https://github.com/microsoft/vscode/wiki/How-to-Contribute)
