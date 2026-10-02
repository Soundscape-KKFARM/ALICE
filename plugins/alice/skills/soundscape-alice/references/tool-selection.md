# Tool selection

The updated ALICE connection exposes `me`, `tools`, `query`, and six directly callable `analytics_*` tools. The client may add a plugin and server namespace to their visible names. Prefer the direct analytics tools listed by the current connection.

| User intent | Public call | Required input |
| --- | --- | --- |
| Identify the authenticated account or find accessible organizations | `me` | `{}` |
| Discover analytics names or inspect a schema | `tools` | optional `search` |
| Discover allowed analytics platform codes | `analytics_platforms` | `organization_id` |
| Read KPI cards | `analytics_summary` | `organization_id`, `target` |
| Read daily series and totals | `analytics_trend` | `organization_id`, `target` |
| Rank artists, songs, or albums | `analytics_ranking` | `organization_id`, `target` |
| Compare each platform's share | `analytics_platform_breakdown` | `organization_id` |
| Compare current and prior performance | `analytics_scatter` | `organization_id`, `target` |

## Minimal call sequence

1. Use an encrypted organization ID already supplied or established in the conversation. Do not call `me` routinely when it is available.
2. If the ID is missing, call `me` once. Only `organizations_status: "ok"` makes its `organizations` array usable. An empty array means no accessible active organizations. `permission_denied` or `temporarily_unavailable` with null does not mean an empty account.
3. When the user gives an organization name, select only a unique exact match. If the name does not match, matches several entries, or relevant names are null, ask the user to choose with distinguishable name and encrypted ID. With no name, select a single organization; ask when several are plausible.
4. If the analytics name and parameters are known, call that `analytics_*` tool directly. If the name is unknown, call `tools` with `{"search":"keyword"}` to get matching names and descriptions; use `{}` for a names-only catalog when no keyword exists. If the input schema is uncertain, call `tools` with an exact, case-sensitive name to receive `tool.input_schema`. A keyword match does not include the schema.
5. When a usable platform code is missing, call `analytics_platforms` with the selected `organization_id`. Preserve returned codes exactly. The `tools` catalog cannot establish platform availability or account permission.
6. Run the one requested analysis. Add another view only when the user requested it or the first result cannot answer the question.

## Compatibility

If the current connection exposes only `me`, `tools`, and `query`, use `query` with `{"name":"analytics_name","arguments":{...}}` for the same analysis. Do not call an unexposed tool or assume the remote server has been updated. This wrapper has the same authorization and input rules; it does not bypass a denied direct call.
