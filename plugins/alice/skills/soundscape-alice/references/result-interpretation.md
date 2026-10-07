# Result interpretation

## Values

- Money is fixed-point TWD. Compute the displayed amount as `amount / 10^scale`; the current `scale` is 6. Preserve exact decimal precision instead of converting through an imprecise float.
- `percentage` and `growth_rate` are ratios. Multiply by 100 only when presenting them as percentages and label the conversion.
- A missing optional value is not the same as zero. Do not fill an omitted play count, royalty, image, total, or comparison with `0` unless the result explicitly supplies zero.
- Treat returned periods as the service-resolved period, even when the request omitted dates.

## Organization and partial results

- `me.organizations_status: "ok"` with `organizations: []` means no accessible active organizations. The array has no pagination.
- `permission_denied` with `organizations: null` means the token cannot read the organization list; it does not prove the account has none. Keep the readable profile separate and return only profile fields relevant to the question.
- `temporarily_unavailable` with `organizations: null` means the organization list could not be determined; do not guess from previous partial results or automatically retry in a loop.
- If an analytics result has `partial: true`, call it incomplete and include relevant `hints`. `exact_result_pending` means the service already retried internally and the exact result is still pending. `partial_data` and `stale_period` qualify the returned values; do not call them final. Do not turn absent optional fields into zero.

## Error boundaries

- A successful HTTP and JSON-RPC envelope can still contain a tool error: inspect `isError` and its safe `structuredContent.error.code`.
- `invalid_argument`: report the rejected input and ask only for the field needed to correct it.
- `permission_denied`: the token does not permit the requested operation or platform code. Changing an ID or retrying cannot bypass it.
- `not_found`: the organization is absent, inaccessible, or has no analytics project. Do not distinguish those cases without other evidence.
- `temporarily_unavailable`: say the analysis is temporarily unavailable; retry later if the user still needs it. Do not assume a fixed retry interval.
- `internal_error`: say the query failed without inventing a cause or exposing internal details.
- JSON-RPC protocol errors, such as invalid tool names or a nonempty tool-list cursor, are separate from `isError` tool results. An HTTP authentication or admission failure is separate again.

When a tool error contains a safe user-facing message, preserve its meaning and omit internal protocol metadata.
