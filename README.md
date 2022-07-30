# React Native Debugger

*Sunny came home with a list of names*<br>
*She didn't believe in transcendence*<br>
*"It's time for a few small repairs" she said*<br>
*Sunny came home with a vengence*<br>

[![Backers on Open Collective](https://opencollective.com/react-native-debugger/backers/badge.svg)](#backers) [![Sponsors on Open Collective](https://opencollective.com/react-native-debugger/sponsors/badge.svg)](#sponsors) [![CI Status](https://github.com/jhen0409/react-native-debugger/workflows/CI/badge.svg)](https://github.com/jhen0409/react-native-debugger) [![Dependency Status](https://david-dm.org/jhen0409/react-native-debugger.svg)](https://david-dm.org/jhen0409/react-native-debugger) [![devDependency Status](https://david-dm.org/jhen0409/react-native-debugger/dev-status.svg)](https://david-dm.org/jhen0409/react-native-debugger?type=dev)

![React Native Debugger](https://user-images.githubusercontent.com/3001525/29451479-6621bf1a-83c8-11e7-8ebb-b4e98b1af91c.png)

> Run the redux example of [react-navigation](https://github.com/react-navigation/react-navigation/tree/master/example) with Redux DevTools setup

This is a standalone app for debugging React Native apps:

- Based on official [Remote Debugger](https://reactnative.dev/docs/debugging#chrome-developer-tools) and provide more functionality.
- Includes [React Inspector](docs/react-devtools-integration.md) from [`react-devtools-core`](https://github.com/facebook/react/tree/master/packages/react-devtools-core).
- Includes Redux DevTools, made [the same API](docs/redux-devtools-integration.md) with [`redux-devtools-extension`](https://github.com/zalmoxisus/redux-devtools-extension).
- Includes [Apollo Client DevTools](docs/apollo-client-devtools-integration.md) ([`apollographql/apollo-client-devtools`](https://github.com/apollographql/apollo-client-devtools)) as devtools extension.

## Installation

To install the app, you can download a prebuilt binary from the [release page](https://github.com/jhen0409/react-native-debugger/releases).

## Documentation

- [Getting Started](docs/getting-started.md)
- [Debugger Integration](docs/debugger-integration.md)
- [React DevTools Integration](docs/react-devtools-integration.md)
- [Redux DevTools Integration](docs/redux-devtools-integration.md)
- [Apollo Client DevTools Integration](docs/apollo-client-devtools-integration.md)
- [Shortcut references](docs/shortcut-references.md)
- [Network inspect of Chrome Developer Tools](docs/network-inspect-of-chrome-devtools.md)
- [Enable open in editor in console](docs/enable-open-in-editor-in-console.md)
- [Config file in home directory](docs/config-file-in-home-directory.md)
- [Troubleshooting](docs/troubleshooting.md)
- [Contributing](docs/contributing.md)

# Getting Started

- Make sure all debugger clients of React Native are closed, usually are `http://localhost:<port>/debugger-ui`
- Make sure RNDebugger is open and wait state.
- RNDebugger will try connect to debugger proxy, use port `8081` by default, you can create a new debugger window (macOS: `Command+T`, Linux/Windows: `Ctrl+T`) to specify the port if you want.
- Enable `Debug JS Remotely` of [developer menu](https://reactnative.dev/docs/debugging#accessing-the-in-app-developer-menu) on your app

## Launch by CLI or React Native packager (`macOS` only)

### The `rndebugger:` URI scheme

Launch RNDebugger by typing the following command:

```bash
$ open "rndebugger://set-debugger-loc?host=localhost&port=8081"
```

The `host` / `port` means React Native packager. You may need to set `port` if you customize the packager port. (`8081` by default)

From [`Debugging using a custom JavaScript debugger`](https://reactnative.dev/docs/debugging#debugging-using-a-custom-javascript-debugger) of React Native docs, you can use `REACT_DEBUGGER` env on react-native packager, it will try to launch RNDebugger when you turn on `Debug JS Remotely`. For example, [Artsy's Emission](https://github.com/artsy/emission/blob/45417ca425f2cba7d2da21902ef8ff1cd093a024/package.json#L28) using the env for launch RNDebugger:

```bash
$ REACT_DEBUGGER="open -g 'rndebugger://set-debugger-loc?port=8001' ||" react-native start
```

Special case of Expo (CRNA):

```bash
$ REACT_DEBUGGER="unset ELECTRON_RUN_AS_NODE && open -g 'rndebugger://set-debugger-loc?port=19001' ||" npm start
```

**_NOTE_** Currently the `REACT_DEBUGGER` env doesn't work with Haul bundler, please track [issue #141](https://github.com/jhen0409/react-native-debugger/issues/141) for more information.

### Use [`react-native-debugger-open`](../npm-package)

If you don‘t need to add a dependency, you can use the package, it can help with:

- Replace `open debugger-ui with Chrome` to `open React Native Debugger` in react-native packager, saving you from closing the debugger-ui page everytime it automatically opens :)
- Detect react-native packager port then send to the app, if you launch packager with custom `--port` or use Expo, this will be very useful

## Use Redux DevTools Extension API

Using the same API as [`redux-devtools-extension`](https://github.com/zalmoxisus/redux-devtools-extension#1-with-redux) is very simple:

```js
const store = createStore(
  reducer /* preloadedState, */,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__(),
)
```

See [`Redux DevTools Integration`](redux-devtools-integration.md) section for more information.

## Platform support

- [React Native](https://github.com/facebook/react-native) >= 0.43
- [React Native for macOS](https://github.com/ptmt/react-native-macos) (formerly react-native-desktop) >= 0.14.0

## Examples for use RNDebugger

- [`Redux counter`](../examples/counter-with-redux)
- [`MobX counter`](../examples/counter-with-mobx) - with [`mobx-remotedev`](https://github.com/zalmoxisus/mobx-remotedev).

The examples were bootstrapped with [`create-react-native-app`](https://github.com/react-community/create-react-native-app).

## LICENSE

[MIT](LICENSE.md)
