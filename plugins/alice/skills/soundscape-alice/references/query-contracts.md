# Query contracts

## Analytics inputs

Call the exposed `analytics_*` tool directly with its fields at the argument root. Use its current client-provided schema; do not invent an argument wrapper, region filter, or other undocumented field.

Use `organizations_list` for organization discovery. It is separate from the profile returned by `me`.

## Shared identifiers and dates

- `organization_id` is the encrypted value supplied by the user or returned in `organizations_list.organizations[].id`. Preserve it exactly.
- Analytics dates are UTC strings in `YYYY-MM-DD` form.
- If `end` is omitted, the service uses the Asia/Taipei calendar date minus two days. If `start` is omitted, it uses six days before the resolved `end`, producing a seven-day inclusive period.
- `start` must not be after `end`; the range is at most 366 days; `start` cannot be earlier than two years before the current Asia/Taipei date.
- `codes` are case-sensitive, unique platform codes. At most four are accepted. When omitted, the service uses `SPO`, `ITM`, `youtubemusic`, and `KKB` in that order. Use `analytics_platforms` to resolve a requested platform and check which codes the account can query.

## Analysis names and arguments

Every analysis below requires `organization_id`. Use the direct tool input fields listed by the current connection.

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
