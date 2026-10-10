# Guide Connect MCP

A practical setup guide to connect `IDA Pro` with `Codex` in VS Code using the `ida-pro-mcp` server on macOS.

This repo is designed as a quick reference for installing, connecting, and troubleshooting the MCP server.

## What this guide covers
- Install `ida-pro-mcp`
- Enable the IDA plugin
- Activate `idalib` on macOS
- Configure Codex in VS Code
- Connect `IDA Pro` to MCP
- Troubleshoot connection issues

## Quick Start

### 1) Clone the repo
```bash
git clone https://github.com/mrexodia/ida-pro-mcp.git
cd ida-pro-mcp
```

### 2) Activate IDA Python library
```bash
uv run "/Applications/IDA Professional 9.4.app/Contents/MacOS/idalib/python/py-activate-idalib.py"
```

### 3) Install dependencies
```bash
uv sync
```

### 4) Install IDA plugin
```bash
pip uninstall ida-pro-mcp
pip install https://github.com/mrexodia/ida-pro-mcp/archive/refs/heads/main.zip
ida-pro-mcp --install
```

### 5) Choose transport
- `Streamable HTTP (recommended)`
- `Global (user-level)`

### 6) Configure Codex MCP
Create a workspace config such as `.vscode/settings.json`:

```json
{
  "github.copilot.advanced": {
    "mcpServers": {
      "ida-pro-mcp": {
        "type": "http",
        "url": "http://127.0.0.1:13337/mcp"
      }
    }
  }
}
```

Then open a binary in IDA Pro and run Codex chat:

```text
@ida-pro-mcp list_funcs
```

## Prerequisites
- macOS
- Python 3.11+
- IDA Pro Professional (not Free)
- VS Code + Codex
- `uv` installed

## Troubleshooting

### Codex says there is no MCP tool
- Make sure IDA Pro is running
- Make sure the database is open in IDA
- Verify MCP server is listening on `127.0.0.1:13337`
- Restart VS Code and Codex

### Check service port
```bash
curl http://127.0.0.1:13337/mcp
```

### If the plugin fails to activate
```bash
uv run "/Applications/IDA Professional 9.4.app/Contents/MacOS/idalib/python/py-activate-idalib.py"
```

## Recommended workflow
1. Open IDA Pro
2. Open the binary you want to analyze
3. Confirm MCP plugin is enabled
4. Open VS Code + Codex
5. Run `@ida-pro-mcp list_funcs`

## Useful links
- https://github.com/mrexodia/ida-pro-mcp
- https://modelcontextprotocol.io/
- https://hex-rays.com/ida-pro/

## License
This project is for documentation and setup guidance.
