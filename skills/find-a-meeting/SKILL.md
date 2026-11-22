---
name: find-a-meeting
description: "Use when someone wants a local or online peer recovery meeting by fellowship, day, time, distance or access needs."
---

Choose `find_meetings_by_zip` for a five-digit US ZIP or `find_online_meetings` for an online or hybrid option. Pass a recurring weekday or a specific date, never both. Local time filters apply in each meeting’s source time zone. If the user means a time window in their own zone across multiple online zones, fetch candidates across the relevant hours and days, convert with the date, and then filter, or explain when the available sources cannot establish a match.

For each useful result, give local weekday and time, original time zone, fellowship and the current source. Use straight-line distance for physical meetings and a public join link for online meetings when supplied. Describe accessibility exactly as recorded; missing information means unknown. Call `get_meeting_details` with the returned meeting ID to refresh a chosen listing. If a fellowship or location has only an official locator, give that locator as a next step. Meetings outside this service’s coverage may exist even when a search returns no rows.
