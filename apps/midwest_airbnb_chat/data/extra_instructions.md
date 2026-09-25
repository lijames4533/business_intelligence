# Extra Instructions

Rules the LLM follows when it writes SQL for `listings`.

- `price` is the nightly price in U.S. dollars. When the user asks what something costs, use `price` and round money to whole dollars in the answer.

- `host_is_superhost` and `instant_bookable` are stored as text values: `t` means yes and `f` means no. Use those values when filtering instead of SQL boolean values.

- When the user refers to Chicago, Columbus, or the Twin Cities, match those requests to the values stored in the `city` column: `Chicago`, `Columbus`, and `Twin Cities`.

- When calculating an average `review_scores_rating`, exclude rows where `review_scores_rating` is `NULL` unless the user specifically asks to include unrated listings.

- When searching listing names, perform the comparison case-insensitively so capitalization does not prevent a relevant listing from matching.