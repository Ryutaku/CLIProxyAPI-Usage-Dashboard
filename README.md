# CLIProxyAPI Usage Dashboard

CLIProxyAPI Usage Dashboard 是一个独立的浏览器静态页面，用于从 CLIProxyAPI 管理接口查看用量统计。

CLIProxyAPI Usage Dashboard is a standalone browser page for viewing CLIProxyAPI usage statistics from the management API.

这个页面是单文件静态 HTML 应用。它会从 CLIProxyAPI 读取用量记录，通过 `sql.js` 和 IndexedDB 把数据保存在浏览器侧 SQLite 中，并按账号/认证来源、模型、token 用量、缓存命中率和请求记录展示汇总与明细。

The page is a single static HTML app. It reads usage records from CLIProxyAPI, stores them in browser-side SQLite through `sql.js` and IndexedDB, then shows aggregate and detail views by account/auth source, model, token usage, cache hit rate, and request records.

## 功能 / Features

- 读取 `GET /v0/management/usage-queue?count=N`
- Reads `GET /v0/management/usage-queue?count=N`
- 在接口可用时同时读取 `/api-key-usage`
- Also reads `/api-key-usage` when available
- 按账号/认证来源和模型分组统计用量
- Groups usage by account/auth source and model
- 展示调用次数、输入 token、输出 token、缓存 token、总 token 和缓存命中率
- Shows call count, input tokens, output tokens, cached tokens, total tokens, and cache hit rate
- 在浏览器中维护本地 SQLite 数据库
- Keeps a local SQLite database in the browser
- 支持手动同步和自动同步
- Supports manual sync and auto sync
- 支持 SQLite 导入/导出，方便备份或迁移
- Supports SQLite import/export for backup or migration
- 作为静态页面运行，不需要额外后端服务
- Runs as a static page without a backend service

## 使用要求 / Requirements

- 已启用管理 API 的 CLIProxyAPI
- CLIProxyAPI with management API enabled
- 已在 CLIProxyAPI 中启用用量统计
- Usage statistics enabled in CLIProxyAPI
- 支持 IndexedDB 的浏览器
- A browser that supports IndexedDB
- 浏览器可以访问你的 CLIProxyAPI 管理接口
- Network access from the browser to your CLIProxyAPI management endpoint

页面默认使用的管理接口地址：

The default management endpoint expected by the page:

```text
http://127.0.0.1:8317/v0/management
```

## 使用方法 / Usage

1. 下载或克隆这个仓库。
2. 在浏览器中打开 `usage.html`。
3. 输入你的 CLIProxyAPI 管理 API 地址。
4. 输入你的 Management key。
5. 点击同步，从 CLIProxyAPI 读取用量记录。

1. Download or clone this repository.
2. Open `usage.html` in your browser.
3. Enter your CLIProxyAPI management API address.
4. Enter your Management key.
5. Click sync to read records from CLIProxyAPI.

也可以直接打开 `static/usage.html`。

You can also open the app directly through `static/usage.html`.

## 重要说明 / Important Notes

- 仓库中不包含 Management key。使用时请在浏览器中输入你自己的密钥。
- The Management key is not included in this repository. Enter your own key in the browser when using the page.
- 用量队列记录被管理接口读取后会从服务端队列中移除，所以请在清理浏览器数据前先同步或导出。
- Usage queue records are consumed by the management endpoint after they are read, so sync or export before clearing browser data.
- 浏览器数据只保存在当前浏览器/用户配置中。
- Browser data is local to the browser/profile where you opened the page.
- 如需长期备份，请使用 SQLite 导出功能。
- Use the SQLite export button if you want a durable backup.
- 如果浏览器阻止 `file://` 请求，可以用任意静态 Web 服务器托管这个目录，再打开本地 URL。
- If your browser blocks `file://` requests, serve this folder with any static web server and open the local URL instead.

本地静态服务器示例：

Example local static server:

```powershell
python -m http.server 8080
```

然后打开：

Then open:

```text
http://127.0.0.1:8080/usage.html
```

## 安全 / Security

不要提交你的 Management key 或其他 CLIProxyAPI 私有凭据。本项目默认让 Management key 输入框保持为空。

Do not commit your Management key or other private CLIProxyAPI credentials. This project intentionally ships with an empty Management key field.

## 许可证 / License

MIT
