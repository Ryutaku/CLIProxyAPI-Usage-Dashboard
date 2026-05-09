# CLIProxyAPI 用量统计面板

[English](README.en.md) | 简体中文

CLIProxyAPI 用量统计面板是一个独立的浏览器静态页面，用于从 CLIProxyAPI 管理接口查看用量统计。

这个页面是单文件静态 HTML 应用。它会从 CLIProxyAPI 读取用量记录，通过 `sql.js` 和 IndexedDB 把数据保存在浏览器侧 SQLite 中，并按账号/认证来源、模型、token 用量、缓存命中率和请求记录展示汇总与明细。

## 功能

- 读取 `GET /v0/management/usage-queue?count=N`
- 在接口可用时同时读取 `/api-key-usage`
- 按账号/认证来源和模型分组统计用量
- 展示调用次数、输入 token、输出 token、缓存 token、总 token 和缓存命中率
- 在浏览器中维护本地 SQLite 数据库
- 支持手动同步和自动同步
- 支持 SQLite 导入/导出，方便备份或迁移
- 作为静态页面运行，不需要额外后端服务

## 使用要求

- 已启用管理 API 的 CLIProxyAPI
- 已在 CLIProxyAPI 中启用用量统计
- 支持 IndexedDB 的浏览器
- 浏览器可以访问你的 CLIProxyAPI 管理接口

页面默认使用的管理接口地址：

```text
http://127.0.0.1:8317/v0/management
```

## 使用方法

1. 下载或克隆这个仓库。
2. 在浏览器中打开 `usage.html`。
3. 输入你的 CLIProxyAPI 管理 API 地址。
4. 输入你的 Management key。
5. 点击同步，从 CLIProxyAPI 读取用量记录。

也可以直接打开 `static/usage.html`。

## 重要说明

- 仓库中不包含 Management key。使用时请在浏览器中输入你自己的密钥。
- 用量队列记录被管理接口读取后会从服务端队列中移除，所以请在清理浏览器数据前先同步或导出。
- 浏览器数据只保存在当前浏览器/用户配置中。
- 如需长期备份，请使用 SQLite 导出功能。
- 如果浏览器阻止 `file://` 请求，可以用任意静态 Web 服务器托管这个目录，再打开本地 URL。


## 安全

不要提交你的 Management key 或其他 CLIProxyAPI 私有凭据。本项目默认让 Management key 输入框保持为空。

## 许可证

MIT
