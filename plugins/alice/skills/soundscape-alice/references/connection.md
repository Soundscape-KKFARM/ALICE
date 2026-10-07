# Connection and authentication

Use the ALICE connection supplied by the installed plugin and the client's supported OAuth sign-in flow. Do not inspect or expose private client configuration, invent connection settings, or substitute credentials.

When authentication is required:

1. **Claude Code**: ask the user to open `/mcp`, select ALICE, and complete browser sign-in and consent.
2. **Codex CLI**: ask the user to check the visible ALICE server name in `/mcp` and run `codex mcp login <server-name>`, then complete browser sign-in and consent. The name may include a plugin namespace.
3. **ChatGPT or another supported client**: use its ALICE connection or account-linking flow and complete Soundscape sign-in and consent.
4. After installing or updating the plugin, start a new client session if the tools have not appeared.

If linking is unavailable or fails, state the limitation and direct the user to the client's supported setup. Do not claim an account is linked or access is granted without client evidence. Never request, display, log, or save credentials or OAuth tokens.

## Authorization boundaries

- Sign-in and consent do not remove account, organization, project, or operation restrictions. Never change permissions or bypass a denial.
- A connection-level `401` requires the client's sign-in or reconnect flow; do not request a token from the user.
- A `403` means access was denied and can have several causes. Follow any safe client-provided consent or access instruction; do not claim every denial is fixed by signing in again.
- A tool's `permission_denied` category means that operation was not permitted. Do not switch IDs, credentials, or accounts to evade it.
- If a tool is missing or a call cannot be dispatched, report that limitation. Do not assume account data or an operation's outcome from it.
