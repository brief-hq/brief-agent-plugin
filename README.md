# Brief Agent Plugin

Brief is a product strategy agent that answers from the workspace's decisions,
personas, strategy, customers, and competitive landscape.

Brief connects your agent to your team's product strategy, customer research,
past decisions, and current priorities. Your agent can check that context while
it works and save important decisions back to Brief for the rest of your team.

## Install

Install this repository as an Agent Plugin in a client that supports the
[Agent Plugins standard](https://agent-plugins.org/):

```text
https://github.com/brief-hq/brief-agent-plugin
```

Verified source install:

- GitHub Copilot CLI: `copilot plugin install brief-hq/brief-agent-plugin`

The released artifact loads the Brief skill and MCP server in GitHub Copilot
CLI. Full OAuth and tool-call verification is still pending.

VS Code and Kiro source installs are not yet verified from the released
artifact. Until their verification passes, configure Brief as a remote MCP
server at `https://app.briefhq.ai/mcp` instead.

When your client first connects to Brief, it opens a browser so you can sign in
and choose your workspace. You do not need to create or paste an API key.

## Use Brief with your agent

Ask your agent questions such as:

- "What product context should I know before changing onboarding?"
- "Have we already decided how this should work?"
- "Check this approach against our customer research and current priorities."
- "Record the decision we just made and why we made it."
- "Find everything we know about enterprise permissions."

The plugin teaches your agent when to load product context, search your Brief
workspace, ask for strategic guidance, and record decisions.

## What the plugin includes

- A Brief skill that guides your agent during product and engineering work.
- A secure connection to Brief at `https://app.briefhq.ai/mcp`.
- Browser-based sign-in handled by your client.

The standard connection file is `mcp.json`. The public repository also includes
the equivalent `.mcp.json` filename used by released VS Code, GitHub Copilot,
and OpenClaw plugin hosts.

The plugin contains no credentials. Access is limited to the Brief workspace
you authorize.

## Links

- [Brief](https://usebrief.com)
- [Documentation](https://usebrief.com/docs/mcp-setup/)
- [Support](https://usebrief.com/support/) or support@briefhq.ai
- [Privacy Policy](https://usebrief.com/privacy-policy/)
- [Terms of Service](https://usebrief.com/terms-of-service/)
- [Agent Plugins](https://agent-plugins.org/)
- [Agent Plugins compatible clients](https://agent-plugins.org/compatible-clients)

## License

ISC — see [LICENSE](./LICENSE).
