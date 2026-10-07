# Album drafts and release requests

Use this workflow only for the album operations the user requested. Keep the selected organization and album explicit; opening or editing a draft does not authorize submitting it.

## Select and prepare the draft

1. Find an existing album with `albums_list` or `album_get`. Only `album_get` may accept a UPC where its schema permits it; use the returned encrypted album ID for later operations. For a new album, obtain the intended active contract from `projects_list` and `project_contract_get`, then use `album_create` with its schema-defined `body.contract_id`. Do not choose a different contract silently.
2. Read `album_draft_get` and, when song details are needed, `album_songs_list`. Use `album_edit_start` only when an editable draft must be opened for an existing released, returned, or taken-down album. If the current state does not permit editing, explain it instead of attempting a different operation to bypass the restriction.
3. Resolve missing artist, genre, language, rights-holder, and store-policy inputs with the resource tools. Use the contract's eligible stores and territory policies for distribution; the analytics platform list does not define release eligibility.
4. Use `album_draft_update` and `album_song_update` for the authorized fields. Omitted fields stay unchanged; explicit null or empty values can clear or remove data where the field contract says so. Do not invent rights, credits, licenses, dates, or identifiers to make a release check pass.
5. Add songs with `album_song_create` only for an unreleased draft that allows it. `album_song_remove` cannot remove the last song. `album_songs_reorder` requires every draft song ID exactly once in the intended order; read all song pages before building that list.
6. Use `song_performer_add` and `song_contributor_add` for requested credits, and their corresponding remove tools only for the identified credit. Resolve role codes from the appropriate role catalog. Preserve the current tool's name, role, and ID matching rules.
7. Use `album_draft_platforms_replace` with the complete intended store list, not just the newly added store. The saved list may include contract-required stores and omit ineligible stores; report the returned saved list when it affects the request.
8. Complete the authorized media and license uploads before checking readiness. A returned upload URL or queued job is not a completed asset.

`album_draft_discard` removes all unsubmitted changes in that draft. Before using it or a removal tool, make the affected data and consequence explicit unless the user's instruction already covers them. Do not add a second confirmation when the exact action and scope are already authorized.

## Check and submit

1. Run `album_release_check` for album-level readiness and `song_release_check` for each song in the submission. An album check alone does not establish that every song passes. A successful check does not submit anything.
2. If a check fails, explain the safe, relevant correction and obtain only missing values. Make authorized corrections, then rerun the affected checks. Never bypass validation or substitute made-up information.
3. Submit with `album_release_submit` only when the user has authorized submission of this album and draft. A request to prepare materials or check readiness is insufficient. Use the schema-required `body`, including `{}` when there is no reviewer comment.
4. Report a successful submission as a request sent for review. It is not proof of approval, delivery, or a live release. Read `album_get`, `album_request_histories_list`, or `album_deliveries_list` only when needed to answer the requested status question.

## Cancel or request takedown

- Use `album_release_cancel` only for the identified pending release request; cancellation can fail if the current review state no longer allows it.
- Use `album_takedown_request` only when the user authorizes removal of the selected released album. A successful call requests review; it does not prove stores have removed the album.
- Use `album_takedown_cancel` only for the selected pending takedown request.
- On a state conflict or an uncertain mutation response, read the relevant current status before deciding whether to retry. Never resubmit, cancel, discard, or request takedown speculatively.
