# Swift Galleries API and MCP server for ChatGPT and Claude

Swift Galleries publishes no API or MCP server (checked 17 November 2026). Cotlet.dev connects ChatGPT, Claude and other AI agents to your own Swift Galleries studio account with 30 hosted tools for clients, room photos, wall designs, sales reports and order downloads.

## What you can ask

> Set up a client with images and a room photo.

> Calibrate the room photo to scale.

> Design suggested walls from your templates.

> Download the order zip for your lab.

> Summarise online and in-person sales.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Swift Galleries tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"swift-galleries":{"command":"python3","args":["swift_galleries_agent.py","serve"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t swift-galleries-mcp .
docker run -i --rm -e COTLET_API_KEY swift-galleries-mcp
```

Tools: `swift_galleries_guide`, `swift_galleries_status`, `swift_galleries_open`, `swift_galleries_read`, `swift_galleries_click`, `swift_galleries_type`, `swift_galleries_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install swift-galleries-mcp        # or run it once: uvx swift-galleries-mcp connect
swift-galleries-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 swift_galleries_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 swift_galleries_agent.py status    # is Swift Galleries ready in your Cotlet.dev account
python3 swift_galleries_agent.py guide     # Swift Galleries screens and sign-in link
python3 swift_galleries_agent.py read      # open Swift Galleries, read the page, close the browser
python3 swift_galleries_agent.py tools     # list Cotlet.dev tools
python3 swift_galleries_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Swift Galleries users

**Does Swift Galleries have an API or MCP server?**

The live page reports no published API, developer documentation, MCP server or official ChatGPT or Claude connector, checked 17 November 2026.

**Does the agent send orders to my lab?**

No. Download the order zip and place the order with your lab yourself.

**Is this an official Swift Galleries integration?**

No. Cotlet.dev is independent and is not affiliated with Swift Galleries.

## Access and source

Request access at https://cotlet.dev/signup?app=swift-galleries.

Live integration details: https://cotlet.dev/integrations/swift-galleries-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=swift-galleries
