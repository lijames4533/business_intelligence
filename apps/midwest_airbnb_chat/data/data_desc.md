# Midwest Airbnb Listings: Data Dictionary

**Dataset:** `listings` table in `midwest_airbnb.db` (SQLite), 14,887 rows and 29 columns
**Source:** Inside Airbnb (https://insideairbnb.com/get-the-data/), the detailed `listings.csv.gz` file for each of three regions: Chicago (snapshot 2026-07-20), Columbus (snapshot 2026-07-23), and Twin Cities MSA (snapshot 2026-07-21). Column meanings follow Inside Airbnb's data dictionary and assumptions (https://insideairbnb.com/data-assumptions/).
**Course:** ISA 401, Miami University

> One row is one listing that showed a nightly price on the snapshot date; listings with no price were dropped. Empty cells are stored as SQL `NULL`.

---

## Field Definitions

| Field | Type | Description |
|---|---|---|
| `city` | text | Which Inside Airbnb region the listing came from: `Chicago` (7,439 rows), `Columbus` (2,587), or `Twin Cities` (4,861). The Twin Cities file covers the Minneapolis-St. Paul metro area, not just the two cities. |
| `snapshot_date` | text | Date Inside Airbnb compiled the file, stored as an ISO text string, not a date: `2026-07-20` for Chicago, `2026-07-23` for Columbus, `2026-07-21` for Twin Cities. Every row of a city shares the same value. |
| `id` | text | Airbnb's listing id. Unique across the table (14,887 distinct values). Stored as text even though it looks numeric, so compare it to a quoted string. |
| `name` | text | Listing title as shown on Airbnb (for example "Tiny Studio Apartment 94 Walk Score"). Never empty. |
| `price` | real | Nightly price in U.S. dollars on the snapshot date, with the dollar sign and commas removed. Ranges from 2.56 to 11,412; never `NULL` (rows without a price were dropped). |
| `room_type` | text | Airbnb's four listing categories: `Entire home/apt` (11,652 rows), `Private room` (2,951), `Hotel room` (246), or `Shared room` (38). |
| `host_id` | text | Unique identifier for the host who manages the listing. A host may manage multiple listings. |
| `host_name` | text | Display name of the listing's host. |
| `host_since` | text | Date when the host joined Airbnb, typically stored as an ISO date (`YYYY-MM-DD`). |
| `host_is_superhost` | text | Whether the host has Superhost status: `t` for yes or `f` for no. |
| `neighbourhood` | text | Cleaned neighbourhood name assigned by Inside Airbnb. This corresponds to Inside Airbnb's `neighbourhood_cleansed` field. |
| `latitude` | real | Geographic latitude of the listing. |
| `longitude` | real | Geographic longitude of the listing. |
| `property_type` | text | Type of property advertised, such as an entire rental unit, private room, house, hotel, or condominium. |
| `accommodates` | integer | Maximum number of guests the listing can accommodate. |
| `bedrooms` | real | Number of bedrooms available in the listing. May be `NULL` for some listings. |
| `beds` | real | Number of beds available in the listing. May be `NULL` for some listings. |
| `bathrooms_text` | text | Bathroom description, including the number and sometimes the bathroom type, such as `1 bath` or `1.5 shared baths`. |
| `minimum_nights` | integer | Minimum number of nights required for a reservation. |
| `availability_365` | integer | Number of days in the next 365 days that the listing is available for booking, ranging from 0 to 365. |
| `number_of_reviews` | integer | Total number of reviews received by the listing. |
| `number_of_reviews_ltm` | integer | Number of reviews received during the last 12 months. |
| `first_review` | text | Date of the listing's first review, stored as an ISO date when available. May be `NULL` when the listing has no reviews. |
| `last_review` | text | Date of the listing's most recent review, stored as an ISO date when available. May be `NULL` when the listing has no reviews. |
| `review_scores_rating` | real | Listing's overall review rating. May be `NULL` when the listing does not have a rating. |
| `reviews_per_month` | real | Average number of reviews received per month. May be `NULL` when the listing has no review history. |
| `instant_bookable` | text | Whether guests can book the listing instantly without prior host approval: typically `t` for yes or `f` for no. |
| `estimated_revenue_l365d` | real | Estimated booking revenue generated during the last 365 days, in U.S. dollars. |
| `amenities_count` | integer | Number of amenities listed for the property. This field was computed for this course by counting the items in each listing's amenities list. |
