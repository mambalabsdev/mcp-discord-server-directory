# Discord Server Directory MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-discord-server-directory/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-discord-server-directory) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-discord-server-directory%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-discord-server-directory&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-discord-server-directory)](https://www.npmjs.com/package/@mambalabsdev/mcp-discord-server-directory) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-discord-server-directory)](https://www.npmjs.com/package/@mambalabsdev/mcp-discord-server-directory) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-discord-server-directory)](https://github.com/mambalabsdev/mcp-discord-server-directory/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-discord-server-directory)

An MCP server for the Mamba Labs Discord Server Directory actor on Apify. Public Discord servers by keyword, as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes search terms, a category, or discord.com/servers links and returns one row per public Discord server with name, description, member and online counts, and directory link, plus the invite link, keywords, and category when details are on.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-discord-server-directory": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-discord-server-directory"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `search_discord_servers` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find the 20 largest Discord servers about Python programming, with their member counts."
- "List public Discord servers about crypto trading with over 10,000 members and their invite links."

## Tool

`search_discord_servers`. One tool. Example arguments:

```json
{
  "search_terms": [
    "minecraft"
  ],
  "max_servers_per_search": 12
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `search_terms` | array | no | Keywords to search, one per line, such as minecraft or python. Discord answers at most 72 servers per search term. |
| `category` | string | no | Optional. One of gaming, music, education, science & tech, or entertainment. With search terms it limits each search to that category. With no search term it browses the whole category, most popular first, up to 1000 servers. |
| `servers` | array | no | Optional. discord.com/servers links or server ids, to read one server's directory page each: invite link, keywords, category, boosts, and creation date. Invite links (discord.gg) are not accepted, because they are not directory pages. |
| `max_servers_per_search` | number | no | Servers to return per search term or category, in Discord's order. Default 24. A search term returns at most 72; a category browse up to 1000. |
| `details` | boolean | no | yes or no. Default no. yes reads each found server's directory page and adds the invite link, keywords, category, boost count, creation date, and reasons to join, at the detail row price. |
| `match_query` | boolean | no | yes or no. Default yes. For a rare or misspelled term Discord's search returns loosely related servers. yes skips a results page where no server holds a word of the search term in its name or description; those servers are not charged. On a page with a match, every server is kept in Discord's order. |
| `min_members` | number | no | Optional. Skip servers with fewer members than this. Skipped servers are not charged. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `server-row`, one server from a search | $0.0035 | $0.003325 | $0.00315 | $0.002975 |
| `server-detail-row`, one server with its page read | $0.005 | $0.00475 | $0.0045 | $0.00425 |
| `apify-actor-start`, per run start | $0.005 | $0.005 | $0.005 | $0.005 |

Search summaries, loosely related servers, servers below your member minimum, servers with no directory page, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/discord-server-directory](https://apify.com/mambalabs/discord-server-directory)

## License

MIT. See [LICENSE](LICENSE).
