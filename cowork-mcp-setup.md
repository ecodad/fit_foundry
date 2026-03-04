# Claude Cowork — MCP & Extension Setup Guide

## Prerequisites

Before configuring any MCP servers, ensure **Node.js** is installed (includes `npm` and `npx`):

```bash
node --version
npm --version
npx --version
```

Download Node.js (LTS) from [nodejs.org](https://nodejs.org) if not already installed.

**Config file location** (used for manual MCP setup):
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`

---

## 1. Indeed MCP

Indeed is a built-in connector in Claude Cowork — no config file edits required.

**Setup:**
1. Open Claude Desktop and switch to the **Cowork** tab
2. Click **"+"** at the bottom of the chat → **Connectors**
3. Toggle **Indeed** on

**Capabilities:** Job search, company data, salary lookups, resume retrieval.

> Note: Must be toggled on per conversation.

---

## 2. Dice MCP

Dice provides a third-party MCP server requiring manual configuration.

**Setup:**
1. Open `claude_desktop_config.json` (see path above)
2. Add the following to the `mcpServers` object (get the exact server config from [Dice's setup guide](https://www.dice.com/career-advice/how-to-connect-the-dice-mcp-server-to-your-ai-assistant)):

```json
{
  "mcpServers": {
    "dice": {
      // paste Dice-provided config here
    }
  }
}
```

3. Save the file and fully quit and restart Claude Desktop
4. Verify via **Settings → Developer** — a hammer/tools icon should appear in the chat

**Capabilities:** Tech-focused job search with filters for location, remote/hybrid, visa sponsorship, and posting date. No Dice login required.

---

## 3. Puppeteer

Puppeteer can be configured via Desktop Extensions (no JSON editing) or manually.

### Option A — Desktop Extensions (easier)
1. In Claude Desktop, go to **Settings → Extensions**
2. Find **Puppeteer** and click **Install**

### Option B — Manual config
1. Open `claude_desktop_config.json`
2. Add the following to `mcpServers`:

```json
{
  "mcpServers": {
    "puppeteer": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    }
  }
}
```

3. Save and restart Claude Desktop

**Capabilities:** Screenshots, page navigation, form filling, JavaScript execution in browser pages.

---

## 4. Claude in Chrome

Claude in Chrome requires both a Chrome extension and a Desktop connector.

**Setup:**
1. Install the extension from the [Chrome Web Store](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn)
2. Sign in with your Claude credentials
3. Pin the extension: click the puzzle piece icon in Chrome's toolbar → click the thumbtack next to **Claude**
4. In Claude Desktop → **Settings → Connectors** → toggle **Claude in Chrome** on
5. Enable per conversation via **"+"** → **Connectors** → **Claude in Chrome**

**Capabilities:** Browser control from Cowork — clicking, scrolling, reading page content, form interaction.

**Limitations:**
- Chrome only (not other Chromium-based browsers or mobile)
- Requires model: Haiku 4.5, Sonnet 4.5, or Opus 4.5
- Must be enabled per conversation

---

## Summary

| Tool | Setup Method | Cowork Role |
|---|---|---|
| Indeed MCP | Connectors UI toggle | Job/company search |
| Dice MCP | Manual JSON config | Tech job search |
| Puppeteer | Extension or JSON config | Browser automation |
| Claude in Chrome | Chrome extension + Desktop toggle | Live browser control |
