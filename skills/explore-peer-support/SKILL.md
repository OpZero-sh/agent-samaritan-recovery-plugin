---
name: explore-peer-support
description: "Compare peer recovery programs and find their official directories: AA, NA, SMART Recovery and Celebrate Recovery. Use when someone says things like 'what is the difference between AA and SMART Recovery', 'is there a secular or non religious option', 'is Celebrate Recovery Christian', 'which program is for drugs', 'what is an open meeting', 'do I have to be religious to go to AA', 'what recovery groups are there', or 'where do I find treatment'. Presents each program in its own terms without ranking them."
---

# Explore peer support

Help a person understand the peer recovery programs this service knows about and where each one lists its meetings. The person decides what fits. Your job is an even, accurate description and a working link for each option.

The tools come from this plugin's `recovery` connector. They return directory information. They do not register anyone, contact a group or give medical advice.

## First, check for urgency

Peer support is not treatment and not a crisis service. If the person describes danger, an overdose, withdrawal symptoms or thoughts of suicide:

- Immediate danger or a medical emergency in the US: call 911.
- Crisis support at any hour: call or text 988, or chat at https://988lifeline.org/chat/.
- Finding treatment: https://findtreatment.gov/ or the SAMHSA National Helpline at 1-800-662-4357, which gives referrals and information and is not an emergency service.

Say it once, plainly, then continue with what they asked.

## When to use

- Comparing programs, or asking what one program is.
- Asking for a secular, spiritual or Christian option.
- Asking what open and closed meetings are, or whether there is a requirement to attend.
- Asking where to find official meeting directories or a treatment locator.

Use `find-a-meeting` when the person wants actual meeting times, and `find-family-support` when the person is a relative or friend looking for support for themselves.

## Workflow

1. **Call `get_fellowship_info`.** Pass `fellowship` as `AA`, `NA`, `SMART`, `Celebrate Recovery`, or `all` for a comparison. When the person asks an open question such as "what are my options", use `all`.
2. **For directories or treatment, call `find_recovery_resources`.**

   | Argument | Use |
   | --- | --- |
   | `need` | `meetings` for official meeting finders, `treatment_locator` for the official treatment locator, `family_support` for groups for relatives and friends, `all` for everything. |
   | `fellowship` | Narrows the meeting finders to one program. |
   | `zip` | Optional five digit US ZIP. It gives a location reference only. The tool does not invent a nearby office. |

3. **Answer from what the tools returned.** Each fellowship record has `approach`, `eligibility`, `website`, `directory_url`, `online_url` and `schedule_coverage`. Use the program's own description of its orientation. Do not add claims from memory about how well a program works.
4. **Offer the next step.** If they want times, offer a meeting search. Say which programs have live schedules in this service and which have locator links only, using `schedule_coverage`.

## How to present a comparison

- Give every program the person asked about the same treatment: one or two sentences on its approach in its own terms, who it is for, and its directory link.
- Keep the order the tool returned, or alphabetical order. Do not put a favourite first.
- Label orientation as the record does: spiritual and not tied to one religion, secular, or Christ centered.
- Say "many people try more than one" only if the person asks how to choose. Then suggest visiting an open meeting of each and seeing what fits. Do not choose for them.
- Never say one program is more effective, more serious, easier or better suited to a kind of person.

Rules on anonymity, neutrality and wording are in [references/anonymity-and-neutrality.md](references/anonymity-and-neutrality.md). A short answer layout is in [references/comparison-template.md](references/comparison-template.md).

## What to ask and what not to ask

- You may ask what matters to them in a group, if they seem unsure. Examples: spiritual or secular, in person or online.
- Do not ask what substance or behavior is involved, how long it has been going on, whether they have relapsed, or whether they consider themselves an alcoholic or an addict.
- Do not infer or ask about their religion. If they state a preference, follow it.
- Do not label the person or anyone they mention. Use their own words.

## Empty results and errors

- These two tools return curated information, so empty results are unlikely. If a call fails, say the lookup did not work and try once more. Do not fill in program descriptions from memory as if they came from the service.
- If the person asks about a program that is not one of the four, say this service does not carry it. Offer the treatment locator and, if they wish, a general explanation that you clearly mark as not coming from this service.

## Limits to state honestly

- The service describes four programs. Other mutual support groups exist.
- Program descriptions are short summaries curated by the service, with a `curation_checked_on` date. The program's own website is the authority.
- Nothing here is medical advice or a treatment recommendation. Each group sets its own participation guidelines.

## Examples

**"What's the difference between AA and SMART Recovery?"**
Call `get_fellowship_info` with `fellowship: "all"` and use the AA and SMART records. Describe each in one or two sentences from `approach` and `eligibility`, give each directory link, and note which has live schedules here. Offer to search for meetings of either.

**"Is there something that isn't religious?"**
Call `get_fellowship_info` with `fellowship: "all"`. Report the orientation each record states. Point out the one described as secular and also how the Twelve Step records describe themselves, since the person may want to know. Do not call any program religious unless its record does.

**"Where can I find rehab near me?"**
This service lists peer support, not treatment providers. Call `find_recovery_resources` with `need: "treatment_locator"` and give the official treatment locator link and the helpline from `crisis_resources`. Say that provider costs and eligibility vary.
