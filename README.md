# electron開始手順
1. `npm init`
  色々確認されるが、entry pointは必ず`main.js`とする
  author、descriptionもアプリ化のために書く必要があるらしい
2. `npm install --save-dev electron`  
3. `package.json`のscriptsを以下のように変更
  ```json
  "scripts": {
    "start": "electron ."
  },
  ```
4. `index.html`を追加(内容は好きにしてよい)
5. `main.js`を追加。内容は以下のようにする
  ```js
  const { app, BrowserWindow } = require("electron");

  const createWindow = () => {
    const mainWindow = new BrowserWindow({
      width: 800,
      height: 600,
    });

    mainWindow.loadFile("index.html");
  };

  app.whenReady().then(() => {
    createWindow();

    app.on("activate", () => {
      if (BrowserWindow.getAllWindows().length === 0) createWindow();
    });
  });

  app.on("window-all-closed", () => {
    if (process.platform !== "darwin") app.quit();
  });
  ```
6. `npm start`とうつと、index.htmlの内容が反映された画面が出てくることを確認

# デベロッパーツール設置方法
- `main.js`の`createWindow`関数内で以下のように記述
  ```js
  mainWindow.openDevTools();
  ```

# アプリ化手順
```
npm install --save-dev @electron-forge/cli
npx electron-forge import
npm run make
```
