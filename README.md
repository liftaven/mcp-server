# Liftaven MCP

**SEO research that leads to reviewed website improvements.**

Liftaven helps founders, small teams and website owners turn search data into a practical next step. Start with a public website check, add Search Console and Analytics for context, and keep research, conversations and content drafts together. When an improvement is ready, review it in the workspace before applying it through a connected editor.

[Website](https://liftaven.com) · [MCP repository](https://github.com/liftaven/mcp-server) · [Agent skill](https://github.com/liftaven/agent-skill) · [npm package](https://www.npmjs.com/package/liftaven-mcp)

## What this connector does

This package connects a local stdio MCP client to the hosted [Liftaven MCP server](https://mcp.liftaven.com/mcp). Hosted tools run on Cloudflare; the local package bridges the connection and opens browser-based OAuth. You do not need to deploy a Worker or paste a product password into your assistant.

| Tool | What it does |
| --- | --- |
| `connection_status` | Check connected providers and account readiness before requesting reports. |
| Discovered provider tools | Inspect the current MCP catalogue, then select the appropriate Search Console, Analytics or other connected-provider operation. |
| Website proposal workflow | Prepare supported changes for review in Liftaven. The assistant cannot approve its own proposal. |

Tool availability depends on connected providers and account permissions. Inspect the live catalogue instead of assuming every provider is connected. Supported sitemap submissions are actions and should happen only when requested. Website proposals retain human review; recommendations do not guarantee rankings or traffic.

## Example workflow

1. Check the connected website, provider accounts and available tools.
2. Compare the latest complete 28 days with the previous 28 using the same property, filters and dimensions.
3. Rank a few opportunities by evidence, inspect the current page, and propose a concrete improvement for review.

### Things to ask your assistant

> Review my last 28 complete days of search performance. Which three pages deserve attention first, and why?

> Compare search clicks with landing-page engagement. Separate what the data shows from your explanation.

> Prepare a title improvement for this page, with supporting evidence, for me to review in Liftaven.

## Connect a remote MCP client

1. Open the client’s custom MCP or connector settings.
2. Enter `https://mcp.liftaven.com/mcp` as the remote server URL.
3. Complete Liftaven sign-in in your browser and review the permissions on the consent screen.
4. Return to the client and load the available tools.

Use a client that supports Streamable HTTP MCP and OAuth. Custom-connector availability depends on the client and your account. A public repository or npm release does not mean the integration has been approved for a client’s marketplace.

## Claude Desktop and other stdio clients

Requires **Node.js 22 or newer** and an existing Liftaven account. Add this entry to your client’s MCP configuration:

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

You can also run `npx -y liftaven-mcp` from a terminal to start the bridge. It speaks MCP over stdio; it is not an interactive chat interface. For desktop clients that support MCPB extensions, download the `.mcpb` file from [Liftaven releases](https://github.com/liftaven/mcp-server/releases).

## Permissions and account access

The live catalogue reflects the providers connected to your Liftaven workspace. Check `connection_status` first and review the consent screen before approving access.

Only approve a connection you intended to start. If sign-in opens a new tab, finish it, return to the consent screen and refresh. [Manage providers and agent access in Liftaven](https://liftaven.com/app/agents).

The package uses pinned [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) for OAuth, PKCE and local token storage. Tokens on your computer are credentials. The connector uses the fixed endpoint above and rejects command-line endpoint overrides. Product passwords and underlying provider credentials are not requested by this package.

## Troubleshooting

- **No tools or insufficient permissions:** reconnect through browser consent and check the selected account.
- **An empty list:** confirm that the account owns the expected items. Empty results are different from a failed request.
- **A link asks you to sign in:** open it with the owning product account; a private product link is not a public share link.
- **The browser blocks authorization:** inspect the browser’s displayed error and restart an expired request from the client. Never send cookies or tokens in an issue.

## Add the companion skill

The [Liftaven agent skill](https://github.com/liftaven/agent-skill) explains how to select the right records, interpret results and respect the workflow’s limits:

```sh
npx skills add liftaven/agent-skill
```

## Learn more about Liftaven

- [SEO workspace](https://liftaven.com/)
- [Connected website editors and integrations](https://liftaven.com/integrations)
- [AI and MCP setup](https://liftaven.com/agents)
- [SEO resources](https://liftaven.com/learn)
- [Current plans](https://liftaven.com/pricing)

## Development and support

```sh
npm ci
npm test
npm run bundle
```

[Report a connector issue](https://github.com/liftaven/mcp-server/issues) with your client, Node.js version and a redacted error. Keep `package.json`, `manifest.json`, `server/config.json`, `server.json` and the lockfile version aligned for releases. GitHub Actions publishes versioned npm packages and MCPB assets. See [LICENSE](https://github.com/liftaven/mcp-server/blob/main/LICENSE) for the MIT license.
