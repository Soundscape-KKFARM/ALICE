# Connection and authentication

Use the ALICE MCP server provided by the installed plugin configuration. That configuration is the source of truth for the transport and server address; do not infer or override them from this Skill.

The public package uses client-managed OAuth account linking, not a personal secret token option or environment variable. The server supports CIMD discovery, authorization code + PKCE (`S256`), and public-client token authentication (`none`). Do not invent a client ID or client secret.

When authentication is required:

1. **Claude Code**: ask the user to open `/mcp`, select ALICE, and complete browser sign-in and consent.
2. **Codex CLI**: ask the user to inspect `/mcp` for the configured server name and run `codex mcp login <server-name>`, then complete browser sign-in. The name may include the plugin namespace.
3. **Public ChatGPT**: use the supported connection flow to connect the deployed MCP server with OAuth. A local environment variable does not link the public connection.
4. After installing or updating the plugin, start a new client session. If a manual bearer-token override remains, ask the user to remove that override for this server before OAuth linking; do not edit client settings or substitute credentials automatically.

If linking is unavailable or fails, report that boundary and ask the user to complete supported setup outside the conversation. Do not claim the public host is deployed, an account is linked, or access is granted without client evidence. Never request, display, log, or save credentials or OAuth tokens in chat, source, plugin files, or diagnostics.

## Authorization boundaries

- Every authenticated `/mcp` request requires a granted `mcp:read` scope. An identity scope alone does not grant tool access. A legacy personal secret token without this grant cannot access MCP; do not bypass the check or auto-grant scope. Other Soundscape API token uses are separate.
- A connection-level HTTP `401` means no usable authentication was accepted. Follow the client's OAuth discovery and sign-in flow.
- An HTTP `403` means endpoint admission denied the request before a tool result. `insufficient_scope` requires a new appropriate OAuth grant containing `mcp:read`; retrying the same credential or changing an ID cannot fix it. Do not assume every `403` is a scope error.
- An `isError` result with `error.code: "permission_denied"` means the authenticated token cannot run that tool's REST-equivalent operation or use the requested platform code. OAuth linking does not remove organization or operation restrictions.
- A JSON-RPC error is a protocol or dispatch failure, such as calling an unknown tool; it is distinct from the boundaries above.
