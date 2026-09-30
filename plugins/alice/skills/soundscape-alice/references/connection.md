# Connection and authentication

Use the ALICE MCP server provided by the installed plugin configuration. That MCP configuration is the source of truth for the transport type and server address; do not copy, infer, or override them from this Skill.

Both Claude Code and Codex read the bearer token from the client process environment variable `SOUNDSCAPE_RISE_TOKEN`. Configure that variable with a Soundscape personal secret token before launching the client, then start a new client session so plugin and MCP configuration are reloaded.

Never paste the token into a conversation, commit it, put it in plugin files, or include it in diagnostics. If the variable is absent, empty, expired, or unavailable to the client process, stop and ask the user to configure the environment securely outside the conversation.

Connection authentication and tool authorization are separate boundaries:

- A connection-level authentication failure means the client did not present a usable bearer token.
- An HTTP `403` means endpoint admission denied the request before a tool result was returned.
- An `isError` result with `error.code: "permission_denied"` means the authenticated token cannot run that tool's REST-equivalent operation or use the requested platform code.
- A JSON-RPC error is a protocol or dispatch failure, such as directly calling an unexposed analytics name; it is distinct from both of the above.

Do not attempt an OAuth login flow for this plugin configuration and do not substitute another credential source automatically.
