# Vibe MCP

Model Context Protocol integrations for extended AI capabilities.

![Vibe MCP](./assets/vibe/mcp.png)

---

## Overview

MCP (Model Context Protocol) allows Vibe to connect to external tools and services. Extend AI capabilities with databases, APIs, and custom tools.

---

## What is MCP?

MCP is a protocol that lets AI models interact with external systems:
- **Filesystem** - Read/write local files
- **Database** - Query databases directly
- **HTTP** - Make API requests
- **Custom** - Your own tools

---

## Supported Integrations

### Filesystem
```json
{
  "name": "filesystem",
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/dir"]
}
```

### PostgreSQL
```json
{
  "name": "postgres",
  "type": "stdio", 
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-postgres", "postgres://user:pass@localhost/db"]
}
```

### Browser Automation
```json
{
  "name": "browser",
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
}
```

---

## Configuration

### Add MCP Server

1. Go to **Sources → MCP**
2. Click **Add Server**
3. Select server type or enter custom
4. Configure connection
5. Save and connect

### Server Types

| Type | Description |
|------|-------------|
| `stdio` | Local command-line tool |
| `sse` | Server-Sent Events endpoint |
| `websocket` | WebSocket connection |

---

## Using MCP Tools

### In Vibe Chat
```
User: Show me all orders from the database

AI: (uses postgres MCP to query)
Orders:
| id | customer | total |
|----|----------|-------|
| 1  | John     | 99.00 |
```

### Available Actions

- **Read** - Query data
- **Write** - Insert/Update/Delete
- **Search** - Full-text search
- **Analyze** - Run computations

---

## MCP Panel

Access MCP panel in Vibe:
1. Click **MCP** button in toolbar
2. View connected servers
3. Test tools
4. View logs

---

## Creating Custom MCP Server

### 1. Create Server Script
```javascript
// my-server.js
const { Server } = require('@modelcontextprotocol/sdk/server');
const { StdioServerTransport } = require('@modelcontextprotocol/sdk/server/stdio');

const server = new Server({
  name: 'my-custom-server',
  version: '1.0.0'
}, {
  capabilities: {
    tools: {}
  }
});

server.setRequestHandler('tools/list', async () => {
  return {
    tools: [{
      name: 'my_tool',
      description: 'Does something useful',
      inputSchema: {
        type: 'object',
        properties: {
          param: { type: 'string' }
        }
      }
    }]
  };
});

server.setRequestHandler('tools/call', async (request) => {
  const { name, arguments: args } = request.params;
  if (name === 'my_tool') {
    return { content: [{ type: 'text', text: 'Result' }] };
  }
});

const transport = new StdioServerTransport();
await server.connect(transport);
```

### 2. Register in Vibe
```json
{
  "name": "my-server",
  "type": "stdio",
  "command": "node",
  "args": ["/path/to/my-server.js"]
}
```

---

## Troubleshooting

### Connection Failed
- Check server is installed
- Verify command/path
- Check logs for errors

### Tool Not Working
- Verify input format
- Check server logs
- Test with simpler parameters

### Server Not Listed
- Restart Vibe
- Check configuration
- Review server status
