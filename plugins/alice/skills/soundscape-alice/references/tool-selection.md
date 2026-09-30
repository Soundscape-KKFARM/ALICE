# Tool selection

Use the three public ALICE MCP tools `me`, `tools`, and `query`. The client may add a plugin and server namespace to their visible names. The six `analytics_*` names are `query.name` values, not directly callable MCP tools.

| User intent | Public call | Required input |
| --- | --- | --- |
| Identify the authenticated account or find accessible organizations | `me` | `{}` |
| Discover analytics names or inspect a schema | `tools` | optional `search` |
| Discover allowed analytics platform codes | `query` | `name: analytics_platforms`, `arguments.organization_id` |
| Read KPI cards | `query` | `name: analytics_summary`, organization and target |
| Read daily series and totals | `query` | `name: analytics_trend`, organization and target |
| Rank artists, songs, or albums | `query` | `name: analytics_ranking`, organization and target |
| Compare each platform's share | `query` | `name: analytics_platform_breakdown`, organization |
| Compare current and prior performance | `query` | `name: analytics_scatter`, organization and target |

## Minimal call sequence

1. Use an encrypted organization ID already supplied or established in the conversation. Do not call `me` routinely when it is available.
2. If the ID is missing, call `me` once. Only `organizations_status: "ok"` makes its `organizations` array usable. An empty array means no accessible active organizations. `permission_denied` or `temporarily_unavailable` with null does not mean an empty account.
3. When the user gives an organization name, select only a unique exact match. If the name does not match, matches several entries, or relevant names are null, ask the user to choose with distinguishable name and encrypted ID. With no name, select a single organization; ask when several are plausible.
4. If the analytics name and parameters are known, call `query` directly. If the name is unknown, call `tools` with `{"search":"keyword"}` to get matching names and descriptions; use `{}` for a names-only catalog when no keyword exists. If the input schema is uncertain, call `tools` with an exact, case-sensitive name to receive `tool.input_schema`. A keyword match does not include the schema.
5. When a usable platform code is missing, call `query` with `name: "analytics_platforms"` and the selected `organization_id`. Preserve returned codes exactly. The `tools` catalog cannot establish platform availability or account permission.
6. Run the one requested analysis through `query`. Add another view only when the user requested it or the first result cannot answer the question.
