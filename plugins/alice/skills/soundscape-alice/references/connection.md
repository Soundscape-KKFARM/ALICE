# Connection and authentication

Use the ALICE MCP server provided by the installed plugin configuration. That MCP configuration is the source of truth for the transport type and server address; do not copy, infer, or override them from this Skill.

The bearer token is a Soundscape personal secret token:

- Claude Code sends the value saved in the plugin's `soundscape_rise_token` option. Claude Code prompts for it when the plugin is enabled and stores it in the system's secure credential store; the user changes it with `/plugin configure alice`.
- Codex reads it from the client process environment variable `SOUNDSCAPE_RISE_TOKEN`, which must be set before launching Codex.

After configuring or changing the token, start a new client session so plugin and MCP configuration are reloaded.

Never paste the token into a conversation, commit it, put it in plugin files, or include it in diagnostics. If the token is absent, empty, expired, or unavailable to the client, stop and ask the user to configure it securely outside the conversation.

Connection authentication and tool authorization are separate boundaries:

- A connection-level authentication failure means the client did not present a usable bearer token.
- An HTTP `403` means endpoint admission denied the request before a tool result was returned.
- An `isError` result with `error.code: "permission_denied"` means the authenticated token cannot run that tool's REST-equivalent operation or use the requested platform code.
- A JSON-RPC error is a protocol or dispatch failure, such as directly calling an unexposed analytics name; it is distinct from both of the above.

Do not attempt an OAuth login flow for this plugin configuration and do not substitute another credential source automatically.
