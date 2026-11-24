# Tarkle is installed

Connect your Tarkle account:

1. Turn the plugin on: `hermes plugins enable tarkle`
2. Add the Tarkle server with sign-in: `hermes mcp add tarkle --url https://mcp.tarkle.tech/mcp --auth oauth`
3. Sign in to Tarkle in the browser tab that opens and approve the connection. On a machine without a browser, open the link Hermes prints on another device and paste the redirect URL back into Hermes.
4. Keep Hermes asking before Tarkle changes anything. Step 2 replaces the plugin's server settings, so put them back before you start a chat:
   `hermes config set mcp_servers.tarkle.trust untrusted`
   `hermes config set mcp_servers.tarkle.timeout 300`
5. Ask Hermes: "List my Tarkle workspaces."

No API key is needed. If the sign-in expires, run `hermes mcp login tarkle`.

Without an account, sign up at https://tarkle.tech.
