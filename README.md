# Liftaven MCP

An SEO workspace for understanding search performance and improving your website.

Connect your existing Liftaven workspace to search and analytics tools. Start with connection_status; the existing remote server controls permissions and exposes its current tool catalogue.

## Remote MCP

Use **https://mcp.liftaven.com/mcp** in a client that supports remote MCP with OAuth. Sign in to Liftaven and explicitly approve the connection.

## Claude Desktop and other stdio clients

Requires Node.js 22 or newer. Add this configuration:

```json
{
  "mcpServers": {
    "liftaven": {
      "command": "npx",
      "args": [
        "-y",
        "liftaven-mcp"
      ]
    }
  }
}
```

Or install the `.mcpb` file from [Releases](https://github.com/liftaven/mcp-server/releases) in your desktop client's Extensions settings. The connector opens your browser for sign-in. If the consent page asks you to sign in, use its new-tab link, then return and refresh the consent page.

## Privacy and permissions

Your product password and provider credentials are not requested by this package. The pinned [mcp-remote](https://www.npmjs.com/package/mcp-remote) bridge handles OAuth, PKCE and local token storage. It connects only to the fixed endpoint above; command-line endpoint overrides are not supported. OAuth tokens are stored locally by mcp-remote and should be treated as credentials.

Manage connected providers and permissions in Liftaven.

## Development and publishing

Run `npm ci` and `npm test`. GitHub Actions publishes a new package version using the organization’s `NPM_TOKEN` secret, then builds and releases the desktop bundle. Keep package.json, manifest.json, server/config.json and server.json versions aligned.

Marketplace approval is separate from npm publication. See the product’s submission notes for endpoint tests and review prerequisites.

[Website](https://liftaven.com) · [Issues](https://github.com/liftaven/mcp-server/issues)
