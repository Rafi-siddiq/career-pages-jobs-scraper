<!-- Landing README for a public GitHub repo. The Actor runs on Apify; this repo is for discovery and issues. -->
[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-0d9488?style=for-the-badge)](https://apify.com/rsiddiq95/career-pages-jobs-scraper)

# Company Career Pages Jobs Scraper

Get **every open job** from company careers pages hosted on **Greenhouse, Lever and Ashby**: title, department, team, location, remote / hybrid, employment type, **salary range**, posting date, job link and apply link. Paste careers-page URLs or just company names, filter by keyword, location, department, remote and date, and export to JSON, CSV or Excel.

It reads the hiring systems' official public job-board APIs, the same feeds that power the companies' own careers pages. No login, no browser, no proxies: fast and reliable.

## What can this careers page scraper do?

- 🏢 **Greenhouse, Lever and Ashby** in one Actor, with one consistent output format.
- 🔗 **URLs or names.** Paste `https://boards.greenhouse.io/airbnb`, `https://jobs.lever.co/palantir`, `https://jobs.ashbyhq.com/ramp`, or just `airbnb`: a plain name is checked on all three systems.
- 💰 **Salary ranges** as published by the company (Ashby, Greenhouse pay transparency, and Lever when set).
- 🔎 **Filters:** title keywords, excluded words, locations, departments or teams, remote only, posted since.
- 📝 **Full descriptions** as clean plain text (optional).
- 🆓 **Companies that aren't found are free.** You only pay for jobs returned.

## Who uses it?

- **Recruiters and staffing agencies** watching target companies for new openings.
- **Sales teams** finding companies hiring for roles that signal a need for their product (for example, companies hiring "data engineer" or "RevOps").
- **Job seekers and job boards** building alerts or niche job lists.
- **Analysts and investors** tracking hiring by team and location as a growth signal.

## How to scrape company jobs

1. Add **Companies**: careers-page URLs or company slugs.
2. Optionally add **filters** (keywords, locations, departments, remote only, posted since).
3. Click **Start** and download the results.

**Where do I find the slug?** It's the part after the domain in the company's job board link: `boards.greenhouse.io/`**`airbnb`**, `jobs.lever.co/`**`palantir`**, `jobs.ashbyhq.com/`**`ramp`**. If a company's careers page is on its own domain, click any job and look for one of these links in the address bar or the "Apply" button.

## Input example

```json
{
    "companies": ["https://boards.greenhouse.io/airbnb", "https://jobs.lever.co/palantir", "ramp"],
    "keywords": ["engineer"],
    "excludeKeywords": ["intern"],
    "locations": ["United States", "Remote"],
    "postedSince": "2026-09-01",
    "maxJobsPerCompany": 500,
    "includeDescription": false
}
```

## Output example

```json
{
    "resultType": "job",
    "query": "https://jobs.ashbyhq.com/ramp",
    "system": "ashby",
    "company": "ramp",
    "jobId": "f564dcf9-9390-4a3f-896f-8047a5086040",
    "title": "Mobile Engineer, Android",
    "department": "Engineering",
    "team": "Mobile",
    "location": "New York, NY (HQ)",
    "allLocations": ["New York, NY (HQ)", "Remote (Canada)", "San Francisco, CA", "Remote (US)"],
    "workplaceType": "Hybrid",
    "isRemote": true,
    "employmentType": "Full-time",
    "salary": "$189K – $330K • Offers Equity",
    "postedAt": "2025-07-31T21:58:34.674Z",
    "updatedAt": null,
    "jobUrl": "https://jobs.ashbyhq.com/ramp/f564dcf9-9390-4a3f-896f-8047a5086040",
    "applyUrl": "https://jobs.ashbyhq.com/ramp/f564dcf9-9390-4a3f-896f-8047a5086040/application",
    "scrapedAt": "2026-10-31T06:38:02.923Z"
}
```

A Greenhouse job's salary looks like `"USD 156,000–195,000 (Pay Range)"`. With **Include job descriptions** on, each row also has `descriptionText`.

## What each system provides

| Field | Greenhouse | Lever | Ashby |
|---|---|---|---|
| Department / team | Department | Department, team | Department, team |
| Workplace type (remote / hybrid / on-site) | When the company sets it | ✅ | ✅ |
| Employment type | – | ✅ | ✅ |
| Salary | When published (pay transparency) | When published | When published |
| Posted date | First published | Created | Published |

## Use it from AI agents (Claude, ChatGPT, Cursor)

AI assistants can run this Actor as a tool through [Apify's MCP server](https://docs.apify.com/platform/integrations/mcp). Add this server URL to any MCP client:

```
https://mcp.apify.com?tools=rsiddiq95/career-pages-jobs-scraper
```

Then just ask, for example: *"Which engineering jobs are Airbnb, Ramp and Palantir hiring for in the United States right now, and what do they pay?"* Agent runs cost the same per result as runs from the console.

## How much does it cost?

Pay per job returned. See the **Pricing** tab. Companies that aren't found, or have no jobs matching your filters, are free. A whole company of 200 jobs takes a few seconds.

## Limitations

- Only companies whose careers pages run on **Greenhouse, Lever or Ashby**. Companies on Workday, iCIMS, SmartRecruiters and others aren't supported yet.
- A plain name is matched to the job-board slug exactly. If a company isn't found, use its careers-page URL.
- Different companies sometimes use the same slug on different systems. When a plain name is found on more than one, the Actor uses the board with the most open jobs and says so in the log. A careers-page URL always picks the exact board.
- On Greenhouse, pay ranges need one extra request per job. Turn off **Include Greenhouse pay ranges** for faster runs on very large boards.

## FAQ

**Is this allowed?**
These are public job-board APIs that Greenhouse, Lever and Ashby provide so jobs can be shown on careers sites and job boards. No login or personal data is involved.

**Something isn't working.**
Open an issue on the **Issues** tab here or on the Actor page, with your input.

## Works well with

- **[Google Sheets Sync](https://apify.com/rsiddiq95/google-sheets-sync):** schedule a daily run and upsert by `jobId`, so your sheet keeps every open role up to date without duplicates.
- **[PayListed](https://paylisted.vercel.app):** a live job board of AI and data roles with published salaries, built on this Actor's data.

## Links

- Apify Store page: https://apify.com/rsiddiq95/career-pages-jobs-scraper
- Tutorial: [How to get every open job from a company's careers page (Greenhouse, Lever, Ashby)](https://dev.to/rafisiddiq/how-to-get-every-open-job-from-a-companys-careers-page-greenhouse-lever-ashby-c7j)
- Questions and bug reports: open an issue here or on the Actor's Issues tab.
