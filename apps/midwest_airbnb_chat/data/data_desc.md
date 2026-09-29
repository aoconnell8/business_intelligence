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
| `host_id` | text | Airbnb's id for the listing's host. 6,970 distinct hosts across 14,887 listings, so some hosts operate multiple listings. Never `NULL`. Stored as text; compare it to a quoted string. |
| `host_name` | text | Host's displayed name (for example "Rebecca"). 25 `NULL`. 3,327 distinct values; some entries contain non-standard Unicode characters. |
| `host_since` | text | Inside Airbnb's date the host joined Airbnb, stored as ISO text. Entirely `NULL` in this extract (0 of 14,887 rows populated) — the column exists in the schema but was not populated when this course's database was built. |
| `host_is_superhost` | text | Airbnb's superhost flag, stored as `t` or `f` text rather than a true boolean. 25 `NULL`. |
| `neighbourhood` | text | Inside Airbnb's `neighbourhood_cleansed` column: standardized neighborhood or community area name (for example "Hyde Park"). 119 distinct values across all three cities. Never `NULL`. |
| `latitude` | real | Listing's latitude. Ranges from about 39.88 to 46.24, consistent with Chicago, Columbus, and the Twin Cities. Never `NULL`. |
| `longitude` | real | Listing's longitude. Ranges from about -94.53 to -82.79. Never `NULL`. |
| `property_type` | text | Airbnb's specific property category (for example "Barn", "Yurt", "Private room in home"), more granular than `room_type`. 62 distinct values. Never `NULL`. |
| `accommodates` | integer | Maximum number of guests the listing sleeps. Ranges from 1 to 16. Never `NULL`. |
| `bedrooms` | real | Number of bedrooms. 2,976 `NULL` (often studios or listings where the host didn't specify). Ranges from 1 to 16. |
| `beds` | real | Number of beds. 668 `NULL`. Ranges from 1 to 32. |
| `bathrooms_text` | text | Free-text bathroom description (for example "1 bath", "Shared half-bath"). 71 `NULL`. 32 distinct values. |
| `minimum_nights` | integer | Minimum nights required per booking, set by the host. 15 `NULL`. Ranges from 1 to 365. |
| `availability_365` | integer | Number of nights available for booking in the 365 days following the snapshot date. Ranges from 0 to 365. Never `NULL`. |
| `number_of_reviews` | integer | Total lifetime review count for the listing. Ranges from 0 to 2,246. Never `NULL`. |
| `number_of_reviews_ltm` | integer | Review count in the last twelve months ("ltm"). Ranges from 0 to 1,220. Never `NULL`. |
| `first_review` | text | Date of the listing's first review, stored as an ISO text string, not a date. 1,761 `NULL` (listings with no reviews yet). Ranges from 2009-07 to 2026. |
| `last_review` | text | Date of the listing's most recent review, ISO text string. 1,761 `NULL`. Ranges from 2014-08 to 2026. |
| `review_scores_rating` | real | Overall guest rating on Airbnb's 1-to-5 scale. 1,761 `NULL` (tied to listings with no reviews). 138 distinct values. |
| `reviews_per_month` | real | Average number of reviews per month since the listing's first review, Airbnb's proxy for booking frequency. 1,761 `NULL`. Ranges from 0.01 to 77.72. |
| `instant_bookable` | text | Inside Airbnb's flag for whether a listing can be booked without host approval, normally `t`/`f` text. Entirely `NULL` in this extract. |
| `estimated_revenue_l365d` | real | Inside Airbnb's estimated revenue in U.S. dollars over the last 365 days. Ranges from 0 to 1,114,800. Never `NULL`. |
| `amenities_count` | integer | Not an Inside Airbnb column — computed for this course as the number of items in each listing's `amenities` list. Ranges from 0 to 100. Never `NULL`. |
