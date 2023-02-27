
## 开始

### Develop
- 代码仓库：http://47.243.225.90:3000/im/im-pc.git
- 修改配置文件：/src/config/index.ts中的接口地址
- Get dependencies from npm

  ```bash
  npm install 
  ```


- Run and preview at local (web)

  ```
  npm run start:renderer

- Run and preview at local (electron)

  ```bash
  npm run start:main
  ```

- Build (web)

  ```
  npm run build:renderer
  ```

- Build (electron)
> you need update `utils/open_im_sdk_wasm/api/database/instance.js` wasm import path first.
>
> ```javascript
> - SQL = await initSqlJs({ locateFile: () => '/sql-wasm.wasm' });
> + SQL = await initSqlJs({ locateFile: () => '../../sql-wasm.wasm' });
> ```

  ```bash
  npm run build:main
  ```
