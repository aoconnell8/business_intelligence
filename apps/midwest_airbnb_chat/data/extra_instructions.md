# Extra Instructions

Rules the LLM follows when it writes SQL for `listings`.

- `price` is the nightly price in U.S. dollars. When the user asks what something costs, use `price` and round money to whole dollars in the answer.
- `host_is_superhost` is stored as the text values `'t'` and `'f'`, not a true boolean, so filter with `host_is_superhost = 't'`, never `= TRUE`. Do not use `instant_bookable` in any query; every row in this extract is `NULL`, so it can never distinguish listings.

- `city` values are exactly `'Chicago'`, `'Columbus'`, or `'Twin Cities'`. When the user types a city name, match it case-insensitively and allow partial matches, for example `WHERE LOWER(city) LIKE '%' || LOWER('minneapolis') || '%'` should still resolve to `'Twin Cities'` since that file covers the whole metro, not just the two named cities.

- Search `name` case-insensitively, for example `WHERE LOWER(name) LIKE '%' || LOWER('studio') || '%'`, since Airbnb titles mix capitalization inconsistently.

- When averaging or reporting `review_scores_rating`, exclude `NULL` rows explicitly with `WHERE review_scores_rating IS NOT NULL` rather than trusting `AVG()` alone, and mention in the answer how many listings had no rating yet, since 1,761 listings have no reviews at all.
