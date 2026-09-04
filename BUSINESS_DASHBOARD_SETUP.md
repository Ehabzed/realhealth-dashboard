# Business dashboard — setup

`business.html` — one page, three tabs (Sales / Content / Health). Built on the same pattern as the client dashboards: content lives in a Google Sheet tab, the page renders it, no code changes to update a number.

**Nothing here is live until you do the three steps below.** The page is on the `business-dashboard` branch, not `main`.

## 1. Add a `Business` tab to your personal sheet
Sheet `1WKj4hxG9GeLZq0LPn6wIWJFifmNvmwH9n2qpbLoDRqk` — same one the personal dashboard already uses, so no new auth.

Same 7 columns as Curated: `Section | Group | Order | Title | Detail | Tag | Extra`

| Section | Meaning |
|---|---|
| `metric` | Title is the key, Detail is the value. Tag `good`/`warn`/`bad` colours it. Keys: `calls`, `asks`, `revenue`, `car`, `draft_age`, `draft_count`, `published`, `ready_to_record`, `days_since_publish` |
| `pipeline` | Sales pipeline rows. Title, Detail, Extra (right-aligned) |
| `cpipeline` | Content pipeline rows |
| `belief` | Belief coverage, last 30 days |
| `overdue` | Health items that are overdue. Everything else stays on the health dashboard |

Starter rows:
```
metric		1	calls		0	bad
metric		2	asks		2	bad
metric		3	revenue		$2,000	warn
metric		4	car		33%	warn
metric		5	draft_age	3 days	bad
metric		6	draft_count	9 drafts waiting
metric		7	ready_to_record	2	bad
```

## 2. Add the endpoint to Code.gs
See the vault note **"Apps Script business Endpoint"** for the code. Returns `{updated, rows:[{section,group,order,title,detail,tag,extra}]}`.

Then **Deploy → Manage deployments → pencil → New version → Deploy.** Saving is not deploying.

## 3. Paste your token
In `business.html`, replace `PASTE_PERSONAL_TOKEN_HERE` with the personal dashboard token.

⚠️ **This repo is public.** The token grants read access to your business numbers. If that isn't acceptable, the alternative is a separate token for this page that you can rotate independently — a one-cell change in the registry.

## Then merge
```
git checkout main && git merge business-dashboard && git push
```

## Two numbers that still can't be measured
**Retention** and **referrals** have no data source yet.
- The "How did you find me?" question was added to the Baseline Typeform on 2026-09-04, so **referrals become countable from the next signup onward.**
- **Retention needs a client status and end-date recorded somewhere countable.** It currently only exists in vault prose.

Both tiles are deliberately absent rather than shipped empty.
