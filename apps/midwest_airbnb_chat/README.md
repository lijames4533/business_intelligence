---
sdk: docker
app_port: 7860
title: ISA 401 Midwest Airbnb Chat
emoji: 🔎
colorFrom: red
colorTo: gray
pinned: false
license: mit
short_description: Ask questions about Midwest Airbnb listings
---

# ISA 401 Midwest Airbnb Chat

**Ask a question in plain English, get the SQL and a table back**

**Live app:** <https://lik44-midwest-airbnb-chat.onrender.com>

------------------------------------------------------------------------

## What is this app?

The app connects to a SQLite database (`data/midwest_airbnb.db`), hands the `listings` table to querychat, and lets an LLM translate your question into SQL. Every answer shows the query it ran, so you can check the logic and reuse the SQL yourself.

**Example queries:** 

- Which Columbus neighbourhood has the priciest entire homes? 

(screenshots/Which Columbus neighbourhood has the priciest entire homes.png) 

- How many listings could host a party of ten?

(screenshots/How many listings could host a party of ten.png)

- Show me the average price by room type in Chicago.

(screenshots/Show me the average price by room type in Chicago.png)

# Midwest Airbnb Listings: Data Dictionary

**Dataset:** `listings` table in `midwest_airbnb.db` (SQLite), 14,887 rows and 29 columns **Source:** Inside Airbnb (<https://insideairbnb.com/get-the-data/>), the detailed `listings.csv.gz` file for each of three regions: Chicago (snapshot 2026-07-20), Columbus (snapshot 2026-07-23), and Twin Cities MSA (snapshot 2026-07-21). Column meanings follow Inside Airbnb's data dictionary and assumptions (<https://insideairbnb.com/data-assumptions/>). **Course:** ISA 401, Miami University

> One row is one listing that showed a nightly price on the snapshot date; listings with no price were dropped. Empty cells are stored as SQL `NULL`.

### Key Fields

| Field | Type | Description |
|------------------------|------------------------|------------------------|
| `city` | text | Which Inside Airbnb region the listing came from: `Chicago` (7,439 rows), `Columbus` (2,587), or `Twin Cities` (4,861). The Twin Cities file covers the Minneapolis-St. Paul metro area, not just the two cities. |
| `snapshot_date` | text | Date Inside Airbnb compiled the file, stored as an ISO text string, not a date: `2026-07-20` for Chicago, `2026-07-23` for Columbus, `2026-07-21` for Twin Cities. Every row of a city shares the same value. |
| `id` | text | Airbnb's listing id. Unique across the table (14,887 distinct values). Stored as text even though it looks numeric, so compare it to a quoted string. |
| `name` | text | Listing title as shown on Airbnb (for example "Tiny Studio Apartment 94 Walk Score"). Never empty. |
| `price` | real | Nightly price in U.S. dollars on the snapshot date, with the dollar sign and commas removed. Ranges from 2.56 to 11,412; never `NULL` (rows without a price were dropped). |
| `room_type` | text | Airbnb's four listing categories: `Entire home/apt` (11,652 rows), `Private room` (2,951), `Hotel room` (246), or `Shared room` (38). |

------------------------------------------------------------------------

## Required Secret

The app calls OpenAI (`gpt-5.6-luna (reasoning off)`) through [ellmer](https://ellmer.tidyverse.org/), so it needs one environment variable:

``` bash
export OPENAI_API_KEY="your-api-key-here"
```

## On Render, add `OPENAI_API_KEY` under the web service's **Environment** settings. Never commit the key to the repository; `.Renviron` is listed in `.gitignore` for that reason.

## Running Locally

**With R (4.6.0, querychat 0.3.0):**

``` r
# from inside apps/midwest_airbnb_chat/
shiny::runApp(".", port = 7860)
```

**With Docker:**

``` bash
docker build -t midwest_airbnb_chat .
docker run --rm -p 7860:7860 -e OPENAI_API_KEY=$OPENAI_API_KEY midwest_airbnb_chat
```

Then open <http://localhost:7860>.

------------------------------------------------------------------------

## Technology Stack

- [**Shiny**](https://shiny.posit.co/) - Web application framework for R
- [**querychat**](https://github.com/posit-dev/querychat) - Natural language data querying
- [**ellmer**](https://ellmer.tidyverse.org/) - LLM client for R
- [**RSQLite**](https://rsqlite.r-dbi.org/) - SQLite driver for R

------------------------------------------------------------------------

## Course Information

This application was developed for **ISA 401** at **Miami University**. The polished version of the same idea, built on BLS wage data, is the [OEWS Jobs Explorer](https://huggingface.co/spaces/fmegahed/querychat_demo).
