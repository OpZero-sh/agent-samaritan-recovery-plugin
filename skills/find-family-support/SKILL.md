---
name: find-family-support
description: "Find peer support for relatives and friends of someone who drinks or uses drugs, such as Al-Anon, Nar-Anon and SMART Family & Friends, and find open meetings a supporter may attend. Use when someone says things like 'my husband drinks and I don't know what to do', 'support group for parents of an addict', 'my son is using', 'help for families', 'is there Al-Anon near me', 'can I go to a meeting with my brother', or 'how do I get my friend into treatment'."
---

# Find family support

Help someone who is worried about another person find support for themselves, and point them to official ways to look for treatment if they ask. The person writing is the one you are helping. Do not assess, label or plan for the person they are worried about.

The tools come from this plugin's `recovery` connector. They return official links. They do not contact anyone.

## First, check for urgency

- If anyone is in immediate danger, has overdosed or may be in a medical emergency in the US: call 911.
- If the person writing, or the person they love, is thinking about suicide: call or text 988, or chat at https://988lifeline.org/chat/.
- If the person writing says they are not safe at home, tell them 911 is for immediate danger and 988 offers crisis support by call or text.

Say it once, plainly, and do not move on until you have.

## When to use

- A partner, parent, child, sibling or friend asks where they can get support.
- Someone asks whether they can attend a meeting with or for another person.
- Someone asks how to find treatment for another person.

Use `find-a-meeting` when the person wants meeting times for themselves in AA or NA, and `explore-peer-support` to compare programs.

## Workflow

1. **Listen, briefly.** One sentence that takes in what they said, in their words. Do not ask for the other person's name, age, substance, history or address.
2. **Call `find_recovery_resources` with `need: "family_support"`.** It returns groups for relatives and friends, each with a `name`, a `purpose` and a `url`. At the time of writing these were Al-Anon Family Groups, Nar-Anon Family Groups and SMART Family & Friends. Use whatever the call returns.
3. **Present every group returned, evenly.** One line each from `purpose`, plus the link. Do not rank them. If the person said drinking or drugs, you may note which group's stated purpose matches, and still show the others.
4. **If they want to go to a meeting with the other person,** explain open meetings: an open meeting welcomes people who come to support someone or who are interested. Offer a search through `find-a-meeting`, and show only meetings whose `eligibility.open` is true.
5. **If they ask about treatment for the other person,** call `find_recovery_resources` with `need: "treatment_locator"`. Give the official treatment locator link. The response's `crisis_resources` also lists the SAMHSA National Helpline, which gives treatment referral and information and is not an emergency service. Say that provider costs and eligibility vary.

## What the answer looks like

- A short opening line.
- The family groups, each with what it is for and its meeting finder link.
- If relevant, the open meeting option and the treatment locator.
- One closing line: these are official finder links, so the group's own site has current meeting times.

Keep it to what they asked. Do not add advice.

## What never to say

- Do not diagnose the other person or call them an addict or an alcoholic. Use the words the person used.
- Do not tell the person what to do about the relationship, whether to confront, leave, stay or set conditions.
- Do not promise that the other person will change, agree to treatment or recover.
- Do not suggest tracking, searching or checking up on the other person, or attending a closed meeting on their behalf.
- Do not explain how to force someone into treatment. If they ask, say that rules differ by state and that the helpline or a local provider can explain the options where they live.

## Privacy

- The tools take no information about either person. A ZIP is optional and only gives a location reference.
- Do not put anything the person tells you about a family member into a tool argument.
- If they name someone, do not repeat the name back more than you need to, and do not use it later.

## Empty results and errors

- `find_recovery_resources` returns curated links, so an empty list is unlikely. If the call fails, say the lookup did not work and try once more. Do not list groups from memory as if the service returned them.
- The service has no live schedules for family groups. It returns their official finders only. Say so if the person asks for times.

## Limits to state honestly

- The family groups listed are peer support groups. They are not counseling.
- The list is short and curated by the service, with a `curation_checked_on` date. Other family support exists.
- Agent Samaritan is not a counseling or crisis service.

## Examples

**"My husband's drinking is getting worse and I'm exhausted."**
Acknowledge it in one sentence. Call `find_recovery_resources` with `need: "family_support"`. Present each group with its purpose and finder link. Mention that these groups are for her own support, whatever he decides. Offer nothing further unless she asks.

**"Can I go to an NA meeting with my brother?"**
Explain open meetings. Offer to search with `find-a-meeting` for NA meetings near their ZIP and show only those marked open. Also give the family group links from `find_recovery_resources`.

**"How do I get my daughter into rehab?"**
Call `find_recovery_resources` with `need: "treatment_locator"`. Give the official treatment locator and the helpline, and say that costs and eligibility vary by provider. Add the family support links for the parent. Do not advise on how to persuade or compel her.
