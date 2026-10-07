# Tool selection

Use the ALICE tools and input schemas supplied by the current client. Visible names may include a plugin or server namespace. Call the selected tool directly; do not assume every connection exposes every operation listed here.

| User intent | Public call | Required input |
| --- | --- | --- |
| Read the authenticated profile | `me` | `{}` |
| Change display name or locale | `me_update` | schema-defined `body` |
| Find accessible organizations and projects | `organizations_list` | optional `offset`, `limit` |
| Read projects and contract release policies | `projects_list`, `project_contract_get` | selected organization and schema-defined project or contract ID |
| Find or manage artists and rights holders | `organization_artists_list`, `organization_artist_get`, `artists_search`, `organization_artist_add`, `organization_artist_update`, `recording_rights_holders_*` | selected organization and schema-defined IDs or `body` |
| Prepare an album and its songs | `albums_list`, `album_get`, `album_create`, `album_draft_*`, `album_edit_start`, `album_song_*`, `album_songs_*`, `song_performer_*`, `song_contributor_*` | selected organization, entity IDs, and schema-defined inputs |
| Check, submit, cancel, or track review and delivery | `album_release_*`, `song_release_check`, `album_takedown_*`, `album_request_histories_list`, `album_deliveries_list` | selected organization and album or song IDs |
| Upload files or inspect media processing | exposed cover/avatar upload tools, `song_authorization_*`, `asset_upload_*`, `asset_multipart_upload_*`, `album_draft_assets_list` | selected target and schema-defined file or `body` |
| Retrieve a pitching survey link | `pitching_plan_survey_get` | `organization_id` |
| Discover allowed analytics platform codes | `analytics_platforms` | `organization_id` |
| Read KPI cards | `analytics_summary` | `organization_id`, `target` |
| Read daily series and totals | `analytics_trend` | `organization_id`, `target` |
| Rank artists, songs, or albums | `analytics_ranking` | `organization_id`, `target` |
| Compare each platform's share | `analytics_platform_breakdown` | `organization_id` |
| Compare current and prior performance | `analytics_scatter` | `organization_id`, `target` |

## Minimal call sequence

1. Reuse IDs already established for the intended organization and task. Do not call `me` for unrelated profile data or to discover organizations.
2. If the organization is missing, call `organizations_list`. It returns `organizations`, `count`, `has_more`, and a next-page `offset` when more data exists. `count` describes one page. Follow the returned offset only as far as needed to resolve the request; a first page cannot prove the full list has one item or no matching name.
3. Select a unique exact name match or the sole relevant organization after checking the necessary pages. If the target remains ambiguous, ask using distinguishable names and IDs only where needed. A denied or failed listing does not establish that the account has no organizations.
4. Use accessible projects from the organization result or `projects_list` when needed. Use resource and entity tools only to obtain missing inputs; do not assume an organization ID also identifies its project, contract, album, song, or artist.
5. For analytics, call `analytics_platforms` only when a requested platform needs a code or its availability is unclear. Preserve returned codes exactly. Analytics platform availability and release-store eligibility are different; use contract policies for the latter.
6. Run the requested operation with the current schema. Add another view or readback only when required by the user's request, the workflow, or an uncertain outcome.

## Availability and permission

Tool annotations describe behavior; they do not grant account or project access and do not replace the user's instruction. Reads require access to the selected resource. Draft and release changes generally require editor access to the organization or project, and some artist or rights-holder operations have further restrictions. Use the current result to determine whether an operation is permitted; never elevate access, switch organizations to evade a denial, or guess from a role name that every operation is allowed.
