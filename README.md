# China Policy Data — Shanghai grants & subsidies

A free, machine-readable feed of Shanghai government grant, subsidy and policy notices, refreshed daily. Built for researchers, consultants and AI agents working on the China market.

**Live feed:** https://shituapp.com/dot/api/programs.json
**Landing page:** https://shituapp.com/dot/en/api.html

## What's inside

~150 notices collected from nine official Shanghai sources — science & technology commission, commerce commission, human resources bureau, development & reform commission, IP office, transport commission and the municipal government portal.

Each record includes:

| Field | Meaning |
|---|---|
| `id` | Stable id derived from the URL |
| `title` | Notice title as published (Chinese) |
| `url` | Link to the official notice — always authoritative |
| `source` / `sourceId` | Issuing body and internal source key |
| `published` | Publication date |
| `deadline` / `daysLeft` | Application deadline when the notice states one |
| `isOpen` | Whether the deadline is still in the future |
| `score` | Relevance score for foreign-invested SMEs (0–10, heuristic) |
| `snippet` | Short excerpt of the notice text |

## Quick start

```bash
curl -s https://shituapp.com/dot/api/programs.json \
  | jq '.meta, (.programs[] | select(.isOpen) | {title, deadline, url})'
```

Any agent or workflow with HTTP access can read the feed directly. Example prompt:

> Fetch https://shituapp.com/dot/api/programs.json and list every program whose `isOpen` is true, sorted by deadline. For each, output title, deadline, daysLeft and the official URL.


## Use it from an AI agent

The feed is plain JSON over HTTPS, so any agent or workflow tool with HTTP access can read it directly.

```
Fetch https://shituapp.com/dot/api/programs.json and list every program
whose isOpen is true, sorted by deadline. For each, output title,
deadline, daysLeft, category and the official URL.
```

For MCP users: wrap the URL in a generic `fetch` / `http` tool — no scraper or browser needed. A machine-readable site summary is also published at https://shituapp.com/dot/llms.txt

## English overlay for open programmes

Records include `titleEn` and `summaryEn` for currently open programmes when available, so agents can answer questions without translating the Chinese titles first. `title` and `url` remain the authoritative fields.

## Update cadence

The hosted feed is regenerated every morning at ~08:10 China time. A GitHub Action in this repo pulls the latest copy into `data/programs.json` at 08:30 China time, so the snapshot here stays current.

## License

The compilation (structure, metadata, relevance scores) is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The underlying notices are public government information; the original Chinese notice at each `url` is authoritative.

Attribution appreciated: *Source: Shanghai Subsidy Radar (https://shituapp.com/dot/)*.

## Related

- Free 2-page English checklist (PDF): https://shituapp.com/dot/en/checklist.html
- 3-minute daily English brief, free 7-day trial: https://shituapp.com/dot/en/checklist.html
- Custom feeds, webhook alerts, white-label digests: support@shituapp.com

## Disclaimer

No warranty of completeness or parsing accuracy. Confirm with the official Chinese notice before applying. Not legal, tax or investment advice.
