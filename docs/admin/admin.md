# 后台预览
- 代码仓库：http://47.243.92.177:3000/im/im-admin.git 账号：im_clone   密码：找管理员索取
- 测试账号：在Server的Config.yaml中manager的配置
- 测试密码：在Server的Config.yaml中manager的配置


# 部署文档

## 环境准备

Install `node_modules`:

```bash
npm install
```

or

```bash
yarn
```

## 提供的脚本

Ant Design Pro提供了一些有用的脚本，帮助您快速启动和构建web项目、代码样式检查和测试。“package.json”中提供的脚本。可以安全地修改或添加其他脚本：

### Start project

```bash
npm run serve
```

### Build project

```bash
npm run build
```

### Check code style

```bash
npm run lint
```

You can also use script to auto fix some lint error:

```bash
npm run lint:fix
```

### Test code

```bash
npm test
```