# Comparison template

A layout for answers built from `get_fellowship_info`. Fill every part from the tool's output for this call. Leave a part out when the record has nothing for it.

## One program

```text
<name>
What it is: <approach, in the record's terms>
Who can take part: <eligibility>
Find meetings: <directory_url>
Online: <online_url, if different from the directory>
In this service: <schedule_coverage, in plain words>
```

## Several programs

Use the same block for each, in the order the tool returned them. Then add:

```text
How this service can help next:
- Live meeting search here: <programs whose schedule_coverage describes a live directory>
- Official finder links only: <the others>
```

Close with one line saying that each group sets its own participation guidelines and that the program's own site is the authority.

## Wording for orientation

Take orientation from the `approach` text.

| The record says | Say |
| --- | --- |
| Twelve Step, spiritual and not tied to one religion | "A Twelve Step fellowship. It describes itself as spiritual and not tied to one religion." |
| Twelve Step with no statement about religion | "A Twelve Step fellowship." Add nothing about religion. |
| Secular, science informed | "A secular program." |
| Christ centered | "A Christian program. Its Christian content is explicit." |

Do not shorten these into "religious" and "not religious". The programs do not describe themselves that way.

## Things to leave out

- Success rates, comparisons of effectiveness and research claims. The service returns none.
- Advice on which program suits which substance or person, beyond what `approach` and `eligibility` state.
- Your own summary of a program's literature or steps.

## Reading `schedule_coverage`

| The text describes | Meaning for the person |
| --- | --- |
| A live directory for one metro area, with other areas using the official locator | Meeting search works here for that area only |
| A public aggregator with coverage that is not exhaustive | Meeting search works here for many US areas, with gaps |
| Official locator only | Use the program's own finder link |
