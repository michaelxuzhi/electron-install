### 这是electron的安装过程笔记，2019.05.24
#### 1、安装node.js     例如：安装在 F://node 下；
#### 2、cmd控制台:     
    F: 
#### 回车，进入F盘，
    cd node
#### 回车，进入node文件夹，
    node -v
#### 回车，查看node版本，
    npm -v
#### 回车，查看npm版本，若出现版本号，表示安装成功；
#### 3、在cmd控制台，node文件夹下，把npm仓库切换到国内taobao仓库，速度会快很多，命令如下：
      npm install -g cnpm --registry=https://registry.npm.taobao.org
#### 4、在node文件夹下，安装electron，命令如下：
      cnpm install -g electron
#### 5、输入命令：
      electron -v
#### 查看electron版本，若出现版本号，表示安装成功；
#### 6、输入命令：
    cnpm install -g electron-packager
#### 打包输出工具；
#### 7、下载并安装electron客户端；
#### 8、新建一个项目文件夹，自命名，例如：test1；
#### 9、在 test1 中创建：pakage.json、index.html、main.js 三个文件；
#### 10、通过拖拽 test1 文件夹到 electron客户端，或者在cmd控制台中使用命令打开文件，
    F:\electron1\electron.exe E:\electronCodes\test1
#### 前段为客户端地址，后段为文件地址

附录：pakage.json、index.html、main.js

pakage.json：
```json
{
  "name"    : "test1",
  "version" : "0.1.0",
  "main"    : "main.js"
}
```

index.html：
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using node <script>document.write(process.versions.node)</script>,
    Chrome <script>document.write(process.versions.chrome)</script>,
    and Electron <script>document.write(process.versions.electron)</script>.
  </body>
</html>
```

main.js：
```js
const electron = require('electron');
// Module to control application life.
const {app} = electron;
// Module to create native browser window.
const {BrowserWindow} = electron;

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let win;

function createWindow() {
  // Create the browser window.
  win = new BrowserWindow({width: 800, height: 600});

  // and load the index.html of the app.
  win.loadURL(`file://${__dirname}/index.html`);

  // Open the DevTools.
  win.webContents.openDevTools();

  // Emitted when the window is closed.
  win.on('closed', () => {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    win = null;
  });
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow);

// Quit when all windows are closed.
app.on('window-all-closed', () => {
  // On OS X it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  // On OS X it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (win === null) {
    createWindow();
  }
});

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```
