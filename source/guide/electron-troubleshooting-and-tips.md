title: Troubleshooting and Tips
---

## Read & Write Local Files
One great benefit of using Electron is the ability to access the user's file system. This enables you to read and write files on the local system. To help avoid Chromium restrictions and writing to your application's internal files, make sure to take use of electron's APIs, specifically the app.getPath(name) function. This helper method can get you file paths to system directories such as the user's desktop, system temporary files, etc.

We can use the userData directory, which is reserved specifically for our application, so we can have confidence other programs or other user interactions should not tamper with this file space.

```
import path from 'path'
import { remote } from 'electron'

const filePath = path.join(remote.app.getPath('userData'), '/some.file')
```

## Debugging Main Process
When running your application in development you may have noticed a message from the main process mentioning a remote debugger. Ever since the release of electron@^1.7.2, remote debugging over the Inspect API was introduced and can be easily accessed by opening the provided link with Google Chrome or through another debugger that can remotely attach to the process using the default port of 5858, such as Visual Studio Code.

```bash
┏ Electron -------------------

  Debugger listening on port 5858.
  Warning: This is an experimental feature and could change at any time.
  To start debugging, open the following URL in Chrome:
      chrome-devtools://devtools/bundled/inspector.html?experiments=true&v8only=true&ws=127.0.0.1:5858/22271e96-df65-4bab-9207-da8c71117641

┗ ----------------------------
```
When using native modules, after npm install bindings change

Example using npm serialport

Since serialport is compiled cpp bindings breaks after npm install....see link below

https://electronjs.org/docs/tutorial/using-native-node-modules

Run 

npm install --save-dev electron-rebuild 

# Every time you run "npm install", run this:
 ./node_modules/.bin/electron-rebuild 

# On Windows if you have trouble, try:
 .\node_modules.bin\electron-rebuild

Then make this available globally

/src/index.template.html

Add after </body>

<script>
    const SerialPort = require('serialport')
</script>

You can test if it's working on any page with

SerialPort.list((err, ports) => { console.log(ports) })

For Production, make sure to add "-b builder" flag

quasar build -m electron -t mat -b builder
