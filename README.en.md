# CLIProxyAPI Usage Dashboard

English | [简体中文](README.md)

CLIProxyAPI Usage Dashboard is a standalone browser page for viewing CLIProxyAPI usage statistics from the management API.

The page is a single static HTML app. It reads usage records from CLIProxyAPI, stores them in browser-side SQLite through `sql.js` and IndexedDB, then shows aggregate and detail views by account/auth source, model, token usage, cache hit rate, and request records.

## Features

- Reads `GET /v0/management/usage-queue?count=N`
- Also reads `/api-key-usage` when available
- Groups usage by account/auth source and model
- Shows call count, input tokens, output tokens, cached tokens, total tokens, and cache hit rate
- Keeps a local SQLite database in the browser
- Supports manual sync and auto sync
- Supports SQLite import/export for backup or migration
- Runs as a static page without a backend service

## Requirements

- CLIProxyAPI with management API enabled
- Usage statistics enabled in CLIProxyAPI
- A browser that supports IndexedDB
- Network access from the browser to your CLIProxyAPI management endpoint

The default management endpoint expected by the page:

```text
http://127.0.0.1:8317/v0/management
```

## Usage

1. Download or clone this repository.
2. Open `usage.html` in your browser.
3. Enter your CLIProxyAPI management API address.
4. Enter your Management key.
5. Click sync to read records from CLIProxyAPI.

You can also open the app directly through `static/usage.html`.

## Important Notes

- The Management key is not included in this repository. Enter your own key in the browser when using the page.
- Usage queue records are consumed by the management endpoint after they are read, so sync or export before clearing browser data.
- Browser data is local to the browser/profile where you opened the page.
- Use the SQLite export button if you want a durable backup.
- If your browser blocks `file://` requests, serve this folder with any static web server and open the local URL instead.


## Security

Do not commit your Management key or other private CLIProxyAPI credentials. This project intentionally ships with an empty Management key field.

## License

MIT
