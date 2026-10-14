# School term dates and holidays (UK and Australia) as JSON and CSV

Free sample dataset of **school term dates, half terms and school holidays** for **New South Wales, Victoria and
Queensland (2026)** and several **UK councils (2026/27)**, as clean JSON and CSV. Every record links to the official
education department or council page it comes from and carries its licence and last-verified date.

The data comes from [School Holidays & Term Dates API](https://apify.com/messnomore/school-holidays-api), which covers more regions (10 UK councils plus
Northern Ireland, Western Australia and Tasmania, every Malaysian state with Kumpulan A and B), future school years and
UK bank holidays, and is re-checked against the official pages every week.

## Files

| File | Rows | Contents |
| --- | --- | --- |
| [`data/school-term-dates-au-2026.json`](data/school-term-dates-au-2026.json) / [`.csv`](data/school-term-dates-au-2026.csv) | 24 | Australia (NSW, VIC, QLD) school terms and holidays, 2026 |
| [`data/school-term-dates-uk-2026-27.json`](data/school-term-dates-uk-2026-27.json) / [`.csv`](data/school-term-dates-uk-2026-27.csv) | 28 | UK council school terms, half terms and holidays, 2026/27 |

## Coverage

| Country | Region | School year | Records | Licence |
| --- | --- | --- | --- | --- |
| AU | New South Wales (`AU-NSW`) | 2026 | 8 | CC BY 4.0 |
| AU | Queensland (`AU-QLD`) | 2026 | 8 | CC BY 4.0 |
| AU | Victoria (`AU-VIC`) | 2026 | 8 | CC BY 4.0 |
| GB | Buckinghamshire (`GB-BKM`) | 2026/27 | 9 | Open Government Licence v3.0 |
| GB | Falkirk (`GB-FAL`) | 2026/27 | 10 | Open Government Licence v3.0 |
| GB | Staffordshire (`GB-STS`) | 2026/27 | 9 | Open Government Licence v3.0 |

Government (state or council) schools only. Catholic, independent and academy schools can set different dates; check
the `scope` field.

## Fields

| Field | Description |
| --- | --- |
| `country` | ISO country code (`AU`, `GB`). |
| `region`, `regionCode` | State or council name and a stable code (ISO 3166-2 where one exists). |
| `scope` | Which schools the dates apply to. |
| `schoolYear` | `2026` (Australia) or `2026/27` (UK). |
| `type` | `term`, `half_term` or `holiday`. |
| `name` | Name used by the publisher, e.g. "Term 1" or "Autumn half term". |
| `start`, `end` | Inclusive dates, `YYYY-MM-DD`. |
| `days` | Calendar days from start to end, inclusive. |
| `derived` | `true` when the holiday was worked out from the term dates because the source lists only terms. |
| `notes` | Extra detail from the source, such as staff development days. |
| `sourceName`, `sourceUrl` | The official page the record comes from. |
| `licence` | Licence of the source data. |
| `lastVerified` | Date the record was last checked against the source. |

Example record:

```json
{
  "country": "AU",
  "region": "New South Wales",
  "regionCode": "AU-NSW",
  "scope": "Government (state) schools. Catholic and independent schools may differ.",
  "schoolYear": "2026",
  "type": "term",
  "name": "Term 1",
  "start": "2026-02-02",
  "end": "2026-04-02",
  "days": 60,
  "derived": false,
  "notes": "School development days Tuesday 27 January to Friday 30 January; students start Monday 2 February",
  "sourceName": "NSW Department of Education",
  "sourceUrl": "https://education.nsw.gov.au/schooling/calendars/2026",
  "licence": "CC BY 4.0",
  "lastVerified": "2026-10-12"
}
```

## Getting more regions, future years and weekly updates

This repository is a snapshot and is not updated automatically. For other regions, future years, Malaysian school
holidays or data that is re-checked every week, use the
[School Holidays & Term Dates API](https://apify.com/messnomore/school-holidays-api) (pay per record, no subscription). Example API call:

```bash
curl -X POST "https://api.apify.com/v2/acts/messnomore~school-holidays-api/run-sync-get-dataset-items" \
  -H "Authorization: Bearer YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"country": "AU", "regions": ["NSW"], "years": [2026, 2027], "types": ["term", "holiday"]}'
```

Guide: [School term dates API for UK councils, Australia and Malaysia](https://wong13977-oss.github.io/school-term-dates-api/).

## Licence and attribution

See [DATA-LICENSE.md](DATA-LICENSE.md). In short: Australian records are licensed under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) by the state education departments, and UK records contain
public sector information licensed under the
[Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
Always check the source page before relying on a date: schools and councils can change them.
