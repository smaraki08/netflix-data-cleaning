# Cleaning the Netflix Dataset

A data cleaning project built with Python and Pandas. It takes the raw Netflix titles dataset from Kaggle, inspects it, fixes missing values, standardises data types, and exports a clean CSV ready for analysis.

Project page: https://roadmap.sh/projects/cleaning-netflix-dataset

## Dataset

- **Source:** Netflix Movies and TV Shows dataset on Kaggle (`netflix_titles.csv`)
- **Size:** 8,807 rows x 12 columns

| Column | Description |
|---|---|
| `show_id` | Unique ID for each title |
| `type` | Movie or TV Show |
| `title` | Title name |
| `director` | Director(s) |
| `cast` | Cast members |
| `country` | Country of production |
| `date_added` | Date the title was added to Netflix |
| `release_year` | Original release year |
| `rating` | Content rating (e.g. TV-MA, PG-13) |
| `duration` | Length in minutes (movies) or seasons (TV shows) |
| `listed_in` | Genres / categories |
| `description` | Short synopsis |

## Project Structure

```
.
├── Clean_the_Netflix_Dataset.ipynb   # Cleaning notebook
├── netflix_titles.csv                # Raw dataset (download from Kaggle)
├── cleaned_netflix_data.csv          # Cleaned output
└── README.md
```

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook / Google Colab

## Cleaning Steps

1. **Load the data** with `pd.read_csv()`.
2. **Inspect the DataFrame** using `.head()`, `.info()` and `.describe()` to understand column types and spot problems.
3. **Handle missing values.** `isnull().sum()` showed the following gaps:
   - `director`, `cast`, `country`: many missing values, filled with `"Missing data"`
   - `date_added` (10), `rating` (4), `duration` (3): a few missing values each, filled with `0`

   A bar chart of missing values per column was used to visualise the gaps.
4. **Fix mixed-type columns.** `duration` mixes numbers and text (`"90 min"`, `"2 Seasons"`), so the numeric part is extracted and converted to a float.
5. **Parse dates.** Column names are stripped of whitespace and `date_added` is converted to a proper datetime with `pd.to_datetime(..., errors='coerce')`.
6. **Verify.** `isnull().sum()` is re-run to confirm no missing values remain.
7. **Export** the cleaned DataFrame with `to_csv('cleaned_netflix_data.csv', index=False)`.

## How to Run

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd <your-repo-name>
   ```
2. Install the dependencies:
   ```bash
   pip install pandas numpy matplotlib jupyter
   ```
3. Download `netflix_titles.csv` from Kaggle and place it in the project folder.
4. In the notebook, change the file path from `/content/netflix_titles.csv` (Colab) to `netflix_titles.csv` if running locally.
5. Launch Jupyter and run all cells:
   ```bash
   jupyter notebook Clean_the_Netflix_Dataset.ipynb
   ```
6. The cleaned file `cleaned_netflix_data.csv` is generated in the same folder.

## What I Learned

- Inspecting a dataset before changing it
- Making a deliberate decision for each column's missing values instead of blindly using `.dropna()`
- Converting mixed-type text columns into usable numeric data
- Parsing dates into proper datetime objects
- Exporting a clean dataset for later analysis
