# Query contracts

## Public tools and compatibility

- `me` takes `{}` and returns the authenticated profile, `organizations_status`, and `organizations`. Successful organization discovery returns an unpaged array. Each item contains encrypted `id`, nullable `name`, `type`, `permission_type`, and `financial`. When organization access is denied or temporarily unavailable, the profile remains available and `organizations` is null.
- `tools` takes optional `search`. Empty or whitespace-only search returns `{"names":[...]}` in name order. Keyword search is case-insensitive over names and descriptions and returns `{"tools":[{"name":"...","description":"..."}]}`; no match returns `{"tools":[]}`. An exact case-sensitive name takes precedence and returns `{"tool":{"name":"...","description":"...","input_schema":{...}}}`.
- Each `analytics_*` tool below is directly callable. Put its fields at the tool argument root, not inside a `name`/`arguments` wrapper.
- `query` remains a compatibility entry point and takes `{"name":"analytics_name","arguments":{...}}`. Both fields are required. `name` must be one of the six names below, and `arguments` must be an object matching that analysis schema. Its result is the selected analysis tool's `content` and `structuredContent` directly, without another nested result.

For a known analysis and known parameters, call its exposed `analytics_*` tool directly. If the schema is in doubt, inspect that exact name through `tools` first. Use `query` only when the connection lacks the direct tool.

## Shared identifiers and dates

- `organization_id` is the encrypted value supplied by the user or returned in `me.organizations[].id`. Preserve it exactly.
- Analytics dates are UTC strings in `YYYY-MM-DD` form.
- If `end` is omitted, the service uses the Asia/Taipei calendar date minus two days. If `start` is omitted, it uses six days before the resolved `end`, producing a seven-day inclusive period.
- `start` must not be after `end`; the range is at most 366 days; `start` cannot be earlier than two years before the current Asia/Taipei date.
- `codes` are case-sensitive, unique platform codes. At most four are accepted. When omitted, the service uses `SPO`, `ITM`, `youtubemusic`, and `KKB` in that order. Ordinary accounts can query only those four codes.

## Analysis names and arguments

Every analysis below requires `organization_id`. These fields are direct tool inputs. Only when using the compatibility `query` wrapper do they go inside `query.arguments`, never beside `query.name`.

### `analytics_platforms`

- Required: `organization_id`.
- Optional: `lang`, a preferred locale for platform display names.
- Use returned `code` values verbatim in later analytics calls.

### `analytics_summary`

- Required `target`: `platform`, `artist`, `song`, or `album`.
- Optional `cards`: any unique subset of `total_play_count`, `top_value`, and `fastest_growing`; omission requests all cards. At most three.
- Also accepts the shared `start`, `end`, and `codes` fields.

### `analytics_trend`

- Required `target`: `platform`, `artist`, `song`, or `album`.
- Optional `ids` applies only to entity targets. Use at most three artist IDs or five song or album IDs.
- Also accepts the shared `start`, `end`, and `codes` fields.

### `analytics_ranking`

- Required `target`: `artist`, `song`, or `album`; `platform` is invalid.
- Optional `metric`: `play_count` or `royalty`; default `play_count`.
- Also accepts the shared `start`, `end`, and `codes` fields.

### `analytics_platform_breakdown`

- Optional `metric`: `play_count` or `royalty`; default `play_count`. Do not pass `target`.
- Also accepts the shared `start`, `end`, and `codes` fields.

### `analytics_scatter`

- Required `target`: `platform`, `artist`, `song`, or `album`.
- Optional `ids` follows the same entity-target limits as `analytics_trend`.
- Also accepts the shared `start`, `end`, and `codes` fields.

All public tool inputs and analysis argument objects are closed. Do not pass undocumented fields. When supplied, `codes`, `cards`, and `ids` must be nonempty arrays with unique entries.
