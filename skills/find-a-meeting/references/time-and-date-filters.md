# Time and date filters

How `day`, `date`, `after`, `before` and `remaining_only` behave in `find_meetings_by_zip` and `find_online_meetings`, and how to handle time zones.

## Rules

1. **`day` or `date`, never both.** Sending both returns the error "Use either day or date, not both."
2. **`day`** is a weekday name with a capital letter: `Sunday` to `Saturday`. Use it for a standing question such as "Friday meetings".
3. **`date`** is `YYYY-MM-DD`, `today` or `tomorrow`. Use it for a specific day.
4. **With neither**, the search uses today, worked out in each meeting's own time zone.
5. **`after` and `before`** are `HH:MM` in 24 hour form and are inclusive. They are compared with each meeting's start time in that meeting's own time zone. They are not in the person's time zone.
6. **`remaining_only: true`** drops meetings whose start has already passed on the requested date, judged in each meeting's zone. It works with `date` or with no day at all. It cannot be combined with `day`.

## Phrases to filters

| The person says | Arguments |
| --- | --- |
| "tonight" | `date: "today"`, `after: "17:00"`, `remaining_only: true` |
| "right now" or "soonest" | `date: "today"`, `remaining_only: true`, `sort: "time"` |
| "tomorrow morning" | `date: "tomorrow"`, `before: "12:00"` |
| "Friday evenings" | `day: "Friday"`, `after: "17:00"` |
| "after work" | Ask what time they finish, or use `after: "17:00"` and say that you assumed it |
| "lunchtime" | `after: "11:00"`, `before: "13:30"` |
| "this weekend" | Two calls: `day: "Saturday"` and `day: "Sunday"` |

The clock times in this table are reasonable readings of everyday phrases. Say which window you used so the person can correct it.

## Local searches

In a ZIP search almost every meeting shares the ZIP's time zone, so the filters behave the way the person expects. Still show the zone with each time.

## Online searches across time zones

Online results come from groups in many zones. The response says so in `time_filter_basis`: times across different zones are not directly chronological. A filter of `after: "18:00"` returns meetings that start at or after 6 pm in each group's own zone, which is a different moment for each zone.

When the person means a window in their own zone:

1. Ask for or infer their time zone. If unknown, ask. Do not guess from the conversation.
2. Search with a wide window, or with no `after` and `before`. For a late evening or early morning window, search the neighbouring day as well, since a meeting on Friday night in one zone can be Saturday in another.
3. For each meeting, convert `time` in `time_zone` to the person's zone for the actual date. Use the date so that daylight saving time is handled correctly.
4. Keep the meetings that fall inside the person's window. Sort by the converted time.
5. Show both: the original time with its zone, and the converted time.

If you cannot convert reliably, for example because the date is ambiguous, show the original times and zones and say that you did not convert them.

`sort` exists only on the ZIP search. Order online results yourself after converting.

## Paging

`limit` defaults to 20 and goes up to 50. When `next_offset` is not null there are more results. Call again with `offset` set to that value and the same filters. For a time zone conversion you may need several pages to cover the window. Stop when you have enough good matches or after about three pages, and tell the person there are more.
