# Doubao App

Drive the **Doubao (豆包) AI desktop app** via Chrome DevTools Protocol. This adapter controls the Electron-based Doubao client directly.

## Prerequisites

1. Install the Doubao desktop app from [doubao.com](https://www.doubao.com/).
2. Launch with remote debugging enabled:

```bash
/Applications/Doubao.app/Contents/MacOS/Doubao \
  --remote-debugging-port=9226
```

3. Set the CDP endpoint:

```bash
export OPENCLI_CDP_ENDPOINT="http://127.0.0.1:9226"
```

## Commands

| Command | Description |
|---------|-------------|
| `opencli doubao-app status` | Check if the Doubao app is running and reachable |
| `opencli doubao-app new` | Start a new conversation |
| `opencli doubao-app send "message"` | Send a message to the active chat |
| `opencli doubao-app read` | Read all messages in the current conversation |
| `opencli doubao-app ask "message"` | Send a prompt and wait for the reply |
| `opencli doubao-app screenshot` | Capture a screenshot of the app window |
| `opencli doubao-app dump` | Dump the current page DOM snapshot |

## How It Works

The adapter connects to Doubao's Electron renderer via CDP and uses `data-testid` selectors to interact with the chat UI. Text injection uses React's internal value setter for reliable textarea updates.

## Limitations

- macOS only (Electron app path)
- Requires Doubao to be launched with `--remote-debugging-port`
- `read` returns messages visible in the current conversation only
