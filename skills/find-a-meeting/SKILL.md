---
name: find-a-meeting
description: "Find a peer recovery meeting near a US ZIP code or online, by fellowship, day, time, distance or access needs, and check one meeting's details before going. Use when someone says things like 'find an AA meeting near 30303', 'NA meetings tonight', 'is there a meeting I can get to after work', 'online meeting right now', 'wheelchair accessible meeting', 'open meeting on Friday', 'SMART Recovery near me', 'Celebrate Recovery near me', or 'is this meeting still on'. Live schedules cover Metro Atlanta AA and participating US NA service bodies. Other areas and fellowships get official locator links."
---

# Find a meeting

Help a person find a peer recovery meeting that fits their day, and tell them plainly how current the listing is. Someone may be asking in a hard moment. Answer fast, lead with the next meeting they can reach, and do not ask why they want one.

The tools come from this plugin's `recovery` connector. They read public meeting directories. They store no attendance, book nothing and contact no group.

## First, check for urgency

A meeting is peer support. It is not medical care or a crisis service. If the person says they are in danger, may hurt themselves, or may be in withdrawal or overdose:

- Immediate danger or a medical emergency in the US: call 911.
- Crisis support at any hour: call or text 988, or chat at https://988lifeline.org/chat/.
- Finding treatment: https://findtreatment.gov/ or the SAMHSA National Helpline at 1-800-662-4357. The helpline gives referrals and information. It is not an emergency service.

Say it once, plainly. Then offer the soonest meeting as well, if they want one.

## When to use

- A meeting near a ZIP, today or on a given day or time.
- An online or hybrid meeting.
- Checking one listing again before going.

Use `explore-peer-support` to compare fellowships, and `find-family-support` when the person is looking for themselves as a relative or friend of someone else.

## Coverage, in one paragraph

Live schedules exist for two sources only: AA in Metro Atlanta, and NA meetings published by participating US service bodies. For AA anywhere else, and for SMART Recovery and Celebrate Recovery everywhere, the service returns the fellowship's official locator link instead of meetings. An empty result never means no meetings exist. Details are in [references/coverage-and-sources.md](references/coverage-and-sources.md).

## Workflow

1. **Get the minimum.** A five digit US ZIP for a local search. Nothing at all is required for an online search. Ask which fellowship only if the person has a preference. Otherwise search `all` and show what comes back without ranking fellowships. Never ask about the person's history, substance, diagnosis, faith or exact address.
2. **Choose the tool.**
   - Near a place: `find_meetings_by_zip` with `zip`.
   - Online: `find_online_meetings`.
3. **Set the filters.** Rules and examples are in [references/time-and-date-filters.md](references/time-and-date-filters.md).

   | Argument | Use |
   | --- | --- |
   | `fellowship` | `AA`, `NA`, `SMART`, `Celebrate Recovery` or `all` (default). |
   | `day` or `date` | A weekday name, or a date (`YYYY-MM-DD`, `today`, `tomorrow`). Never both. With neither, the search uses today in each meeting's time zone. |
   | `after`, `before` | `HH:MM` in 24 hour form, inclusive, in each meeting's own time zone. |
   | `remaining_only` | True drops meetings that already started on the requested date. Use it for "tonight" or "right now". Not allowed with `day`. |
   | `format` (ZIP search only) | `in_person` (default, includes hybrid), `online`, `hybrid`, `any`. |
   | `radius_miles` (ZIP search only) | Default 15, up to 100. |
   | `sort` (ZIP search only) | `time` or `distance`. |
   | `limit`, `offset` | Default 20, up to 50. Use 3 to 5 for a first answer. Page with `next_offset`. |

4. **Read `status`, `source_results` and `coverage_notice` before the meetings.** If a source failed or was outside coverage, say so in the answer.
5. **Check freshness on each meeting you plan to show.** If `freshness.status` says the source record is old or its update date is unknown, say so beside that meeting.
6. **Refresh a chosen meeting** with `get_meeting_details` and its exact `id` (for example `aa-atlanta:85512` or `na-bmlt:23147`) when the person picks one or asks if it is still on.
7. **Answer** in the shape below.

## What the answer looks like

For each meeting, a short block:

- Name and fellowship.
- Weekday and start time with the time zone, and the end time or duration if given.
- In person: location name, address, and distance. Distance is a straight line from the middle of the ZIP area, not a driving distance.
- Online: the public joining link and any joining instructions, exactly as listed.
- Open or closed, from `eligibility.open`. If it is null, say the listing does not say.
- Accessibility exactly as recorded. `listed_accessible` means the source lists wheelchair access. `unknown` means the source does not say. It does not mean inaccessible.
- Any `notes` from the listing that help someone find the door.
- The source link.

Then, every time, one plain line: these are recurring directory listings and may be out of date, so confirm with the meeting's source page or the fellowship's local line before travelling, especially around holidays. Field meanings are in [references/meeting-fields.md](references/meeting-fields.md).

Present fellowships side by side when the search was for `all`. Do not rank them, recommend one, or describe one as more effective.

## Privacy and anonymity

- Do not ask the person to say whether they are an alcoholic or an addict, or whether they have been to a meeting before.
- Do not ask for or record a name. Meetings in these fellowships are anonymous.
- If the person mentions someone they saw at a meeting, do not repeat or use the name.
- Give only links and phone numbers that appear in the listing. Do not look up or guess a host's personal contact.
- Do not offer to contact a meeting, register the person or save their attendance. The tools cannot do it.

## Empty results and errors

- **`status` is `coverage_unavailable`, or `meetings` is empty.** Say the service has no live schedule for that fellowship or area. Give the link from `official_locators` for each fellowship asked about. Offer an online search, or a wider radius if the ZIP is near covered areas.
- **`source_results` shows `outside_coverage` or `locator_only`.** Same as above for that fellowship. Still show meetings from the sources that answered.
- **"Use either day or date, not both."** Remove one and call again.
- **The ZIP is rejected or the error names the ZIP geocoder.** The ZIP must be five digits and must exist. Keep leading zeros. Ask the person to check it.
- **`get_meeting_details` returns `status: "not_found"`.** The source no longer lists that meeting. Say so and search again. Do not repeat the old schedule as if it were current. IDs come only from search results.
- **A request for a kind of meeting**, such as women's, beginners, speaker or a language. There is no filter for it. Search, then look at each meeting's name, `notes` and `format_definitions`. Show the ones the listing marks that way. If none is marked, say the listings do not mark it and give the fellowship's own finder from `official_locators`.

## Limits to state honestly

- Listings are recurring schedules. They do not confirm that a given meeting will happen on a given day.
- The time the service fetched the feed is not the time the group last confirmed its schedule.
- Online results are a limited set from the same sources, not a worldwide directory.

## Examples

**"Find an AA meeting near 30303 tonight after 6."**
Call `find_meetings_by_zip` with `zip: "30303"`, `fellowship: "AA"`, `date: "today"`, `after: "18:00"`, `remaining_only: true`, `sort: "time"`, `limit: 5`. Give the next three with time, place, distance, open or closed, accessibility and source link. Note any listing whose source record is old. Close with the confirm line.

**"Any NA meetings online Friday evening? I'm on Pacific time."**
Call `find_online_meetings` with `fellowship: "NA"`, `day: "Friday"`. Filters apply in each meeting's own zone, so fetch a wide window and convert each start time to Pacific yourself, as the reference describes. Show both the original time and zone and the Pacific time.

**"SMART Recovery meetings near 02108?"**
Call `find_meetings_by_zip` with `zip: "02108"`, `fellowship: "SMART"`. The result is locator only. Say the service has no live SMART schedule, give the official SMART meeting finder link from `official_locators`, and offer to search other fellowships nearby without suggesting the person should switch.
