# Austria Jobs API: karriere.at and jobs.at in Python and Node

Get Austrian jobs from **karriere.at and jobs.at** as clean, deduplicated JSON with company, location, Bundesland and salary text. The [Austria Jobs Scraper](https://apify.com/swissalpinedata/austria-jobs-scraper) on Apify reads the public search endpoints of both boards.

Pay per result, no subscription, no login and no proxy setup. New Apify accounts get free monthly credit, which covers a few thousand results.

## Quick start

1. Create a free account on [Apify](https://apify.com) and copy your API token from Settings, Integrations.
2. `export APIFY_TOKEN=your_token`
3. Run one of the examples below.

### Python

```bash
pip install apify-client
python example.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("swissalpinedata/austria-jobs-scraper").call(run_input={
    "query": "Softwareentwickler",
    "location": "Wien",
    "maxItems": 20
})

for item in client.dataset(run.default_dataset_id).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
node example.mjs
```

```js
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("swissalpinedata/austria-jobs-scraper").call({
  "query": "Softwareentwickler",
  "location": "Wien",
  "maxItems": 20
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### curl

```bash
curl -X POST "https://api.apify.com/v2/acts/swissalpinedata~austria-jobs-scraper/run-sync-get-dataset-items" \
  -H "Authorization: Bearer $APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query": "Softwareentwickler", "location": "Wien", "maxItems": 20}'
```

## Example output

One record looks like this:

```json
{
  "source": "karriere_at",
  "job_id": "10028680",
  "url": "https://www.karriere.at/jobs/10028680",
  "apply_url": null,
  "title": "Senior Database Developer (m/w/d) SQL Server · T-SQL · Performance Engineering",
  "company": "Sportsbook Software GmbH",
  "location": "Wien 22. Bezirk (Donaustadt)",
  "state": "Wien",
  "employment_type": "Vollzeit",
  "workload": null,
  "salary": "ab 68.000 € jährlich",
  "published_at": "2026-09-13",
  "home_office": true,
  "snippet": null,
  "description": null,
  "scraped_at": "2026-09-22T20:37:20.359941+00:00"
}
```

## What you can build

* Austrian job market research
* Recruiting leads by Bundesland
* Niche job boards
* Salary text analysis

## Schedules and integrations

On Apify you can save this input as a task, run it on a schedule (for example every morning) and send new results to Google Sheets, Slack, a webhook, Make, n8n or Zapier without writing code. All input fields are documented on the [actor page](https://apify.com/swissalpinedata/austria-jobs-scraper).

## More Swiss and DACH data APIs

* [swiss-jobs-api](https://github.com/swissalpinedata/swiss-jobs-api): Swiss Jobs API
* [arbeitsagentur-jobs-api](https://github.com/swissalpinedata/arbeitsagentur-jobs-api): Arbeitsagentur Jobsuche API
* [zefix-api-python](https://github.com/swissalpinedata/zefix-api-python): Zefix API in Python
* [flatfox-api-python](https://github.com/swissalpinedata/flatfox-api-python): Flatfox API
* [personio-jobs-api](https://github.com/swissalpinedata/personio-jobs-api): Personio, Workable, Recruitee, SmartRecruiters and Teamtailor jobs API in Python and Node

## License

The example code in this repo is MIT licensed. The data comes from public sources; you are responsible for using it in line with the GDPR and the terms of the source sites.
