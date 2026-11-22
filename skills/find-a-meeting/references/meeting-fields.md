# Meeting fields

What each field on a meeting record means and how to say it. The same record shape comes back from `find_meetings_by_zip`, `find_online_meetings` and `get_meeting_details`. Values listed were observed in the service's output. Report an unfamiliar value as written.

## Identity

| Field | Meaning |
| --- | --- |
| `id` | The ID to pass to `get_meeting_details`, such as `aa-atlanta:85512` or `na-bmlt:23147` |
| `fellowship` | `AA` or `NA` for live records |
| `name` | The meeting's listed name. Repeat it as written |
| `source_organization` | The body that publishes the listing, for example an NA area or the Metro Atlanta AA office |

## Schedule

| Field | Meaning |
| --- | --- |
| `weekday` | The recurring day |
| `time` | Start time, 24 hour form, in the meeting's own zone |
| `time_zone` | IANA zone name, such as `America/New_York` |
| `end_time`, `duration` | One or both may be null. Give whichever is present |
| `schedule_kind` | `recurring_directory_listing`. The record is a standing schedule, not a confirmed occurrence |
| `date` | The calendar date when the search used `date`. Null for a weekday search |

Say times the way people do ("6:00 pm Eastern") and keep the zone.

## Place and joining

| Field | Meaning |
| --- | --- |
| `format` | `in_person`, `online` or `hybrid` |
| `location`, `address` | The venue name and street address. Empty or null for online meetings |
| `distance_miles` | Straight line from the ZIP centre point. Null for online meetings and in `get_meeting_details` |
| `directions_url` | A map link built from the address |
| `online_url` | The public joining link as listed |
| `online_instructions` | Listed joining notes, which may include a meeting number or passcode |
| `phone` | A listed dial in or contact number |
| `notes` | Free text from the group, such as which door to use |

Pass on `online_url`, `online_instructions` and `phone` exactly as listed, and only to the person asking. They are public listing data. Do not add contact details from anywhere else.

`notes` can describe a different format from the `format` field, for example a note that says the meeting is hybrid. When they differ, show both and tell the person to confirm with the source.

## Who the meeting is for

| Field | Meaning |
| --- | --- |
| `eligibility.open` | True for an open meeting, false for a closed one, null when the listing does not say |
| `eligibility.notes` | The source's own tags, such as `Open`, `O` or `C` |
| `type_codes` | The source's format codes |
| `format_definitions[]` | For NA records, each code with a `name` and `description` from the source, such as discussion, speaker, book study, or wheelchair accessible. May be an empty list for AA records |

How to say it:

- **Open.** Anyone may attend, including family, friends and people who are curious.
- **Closed.** For people who identify with the fellowship's purpose. The service's fellowship information describes closed AA meetings as being for people with a desire to stop drinking.
- **Null.** "The listing does not say whether it is open or closed."

When `format_definitions` explains a code, use its `name`. When a code has no definition in the record, do not guess its meaning. Show the code and point to the source link.

## Accessibility

| `accessibility.wheelchair` | Say |
| --- | --- |
| `listed_accessible` | "The listing marks it wheelchair accessible." |
| `unknown` | "The listing does not say whether it is wheelchair accessible." |

Never turn `unknown` into "not accessible". The record's own `notice` says unlisted accessibility is unknown and that specific access needs should be confirmed with the organization. If the `notes` mention stairs or an upper floor, pass that on next to the accessibility line.

## Freshness

| Field | Meaning |
| --- | --- |
| `freshness.retrieved_at` | When the service fetched the feed. Not when the group confirmed its schedule |
| `freshness.source_updated_at` | When the source record last changed, or null |
| `freshness.update_age_days` | Days since that change, or null |
| `freshness.status` | `source_update_unknown` when the source gives no update date. `source_record_older_than_180_days` when the record has not changed in over 180 days |
| `source_last_contact` | A date the source records for its last contact with the group, when it has one |

How to say it:

- `source_update_unknown`: "The directory does not show when this listing was last updated."
- `source_record_older_than_180_days`: "This listing has not been updated in the directory for more than six months." Give the year of `source_updated_at` if it helps.

An old record is not wrong by itself, since many meetings keep the same slot for years. It is a reason to confirm before travelling.

## Source links

| Field | Use |
| --- | --- |
| `source_url` | The record's own page or query. Always include it |
| `directory_url` | The fellowship's directory for that area |
| `source_root`, `source_record_id` | Provenance for the record. Not needed in an answer |
