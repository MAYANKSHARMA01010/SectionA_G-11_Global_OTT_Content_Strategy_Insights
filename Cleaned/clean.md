# Data Cleaning & Feature Engineering Notes

The dataset (`cleaned_dataset.xlsx`) has undergone rigorous cleaning and feature engineering to ensure analytical quality and distinct structural insights.

## Data Cleaning Process

### Handling Missing Values
To maintain dataset integrity, missing values were handled as follows:
-   **Director**: Blanks (~29.9%) were replaced with `'Not Specified'` to retain records without removing titles.
-   **Cast**: Blanks (~9.36%) were replaced with `'Not Specified'`.
-   **Country**: Blanks (~9.41%) were replaced with `'Unknown'` to avoid skewing regional analysis with incorrect imputations.

### Standardization
-   **Date Standardization**: The `date_added` column was standardized to a consistent datetime format.
-   **Duration splitting**: The `duration` field was separated into `duration_value` (numeric) and `duration_unit` (text) to allow for quantitative analysis of runtimes and season counts.

## Feature Engineering (Derived Columns)

To enable deeper analysis, several columns were derived from the original metadata:

| Derived Column | Description | Purpose |
| :--- | :--- | :--- |
| **`primary_country`** | Extracted the first listed country from the `country` column. | Standardizes regional analysis by assigning a single primary origin to each title. |
| **`primary_genre`** | Extracted the first listed genre from `listed_in`. | Simplifies genre segmentation and identifies dominance patterns (e.g., Drama, Comedy). |
| **`rating_group`** | Grouped detailed ratings (e.g., TV-MA, PG-13) into broader categories: `Adults`, `Teens`, `Kids`, `Other`. | Enables structured audience segmentation and targeting analysis. |
| **`duration_value`** | Numeric part of the duration (e.g., `90` from "90 min"). | Allows for statistical calculations on content length. |
| **`duration_unit`** | Unit part of the duration (e.g., `min`, `Season`). | Distinguishes between Movies (minutes) and TV Shows (seasons). |
| **`duration_bin`** | Categorized duration into groups (e.g., 'Short', 'Regular', 'Long' for Movies; 'Miniseries', 'Standard', 'Long Running' for TV Shows). | Facilitates format structure analysis. |
| **`year_added`** | Extracted year from `date_added`. | Critical for analyzing identifying growth phases (e.g., aggressive expansion vs. stabilization). |
| **`month_added`** | Extracted month from `date_added`. | Used to detect seasonal release trends. |
| **`content_lag`** | Calculated as `year_added` - `release_year`. | Measures "freshness" - the time difference between a title's original release and its addition to Netflix. |

## Data Dictionary (Key Fields)

-   `show_id`: Unique identifier.
-   `type`: Movie or TV Show.
-   `title`: Content title.
-   `director`: Producer/Director.
-   `cast`: Key actors.
-   `country`: Country of origin (all listed).
-   `date_added`: Date added to Netflix.
-   `release_year`: Original release year.
-   `rating`: Standard content rating.
-   `duration`: Original duration string.
-   `listed_in`: All genres listed.
-   `description`: Content synopsis.
