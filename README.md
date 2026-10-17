# YouTube Top 5000 Channels Analysis

An exploratory data analysis (EDA) of the top 5,000 YouTube channels using **Python, pandas, NumPy, Matplotlib and Seaborn**. The notebook ranks channels by subscribers, uploads and views, looks at music (VEVO) channels, and measures how subscribers, views, uploads, rank and grade relate to each other.

## Project Structure

```
.
├── youtube_project.ipynb        # Analysis notebook
├── yt.csv                       # Dataset (5,000 rows x 6 columns)
├── YouTube_Project_Report.pdf   # Detailed project report
└── README.md                    # This file
```

> The notebook reads the CSV from `./drive/MyDrive/yt.csv` (Google Colab with Drive mounted). To run locally, place the CSV next to the notebook and change the path to `yt.csv`.

## Dataset

| Column | Description |
|---|---|
| Rank | Channel rank as text (e.g. `1st`, `1,471st`) |
| Grade | Channel grade: A++, A+, A, A-, B+ (6 rows are blank) |
| Channel name | Name of the channel |
| Video Uploads | Number of videos uploaded (stored as text) |
| Subscribers | Number of subscribers (stored as text) |
| Video views | Total views of the channel |

## What the Notebook Does

1. Loads the data, drops duplicates (none found) and inspects its structure.
2. Converts `Subscribers` and `Video Uploads` to numbers (non-numeric values become 0).
3. Lists the top 10 channels by subscribers, uploads and views.
4. Counts channels per grade and prints summary statistics.
5. Lists the top 10 VEVO (music artist) channels by subscribers and by views.
6. Plots and measures correlations: subscribers vs views, subscribers vs uploads, views vs uploads.
7. Calculates `Average Views` (views / uploads).
8. Converts Grade to a number (A++ = 5 ... B+ = 1), cleans Rank to numbers, and builds a correlation matrix.
9. Plots subscribers, average views and uploads by grade.

## Key Results

| Metric | Result |
|---|---|
| Rows / columns | 5,000 / 6 |
| Most subscribers | PewDiePie (65,995,310) |
| Most views | T-Series (47.5 billion) |
| Most uploads | AP Archive (422,326) |
| Top VEVO channel by subscribers and views | JustinBieberVEVO |
| Grade counts | B+ 2,956, A- 1,024, A 963, A+ 41, A++ 10, blank 6 |
| Median subscribers / views | 1.20M / 482M |
| Correlation: subscribers vs views | 0.79 (strong) |
| Correlation: subscribers vs uploads | 0.02 (negligible) |
| Correlation: views vs uploads | 0.09 (negligible) |
| Correlation: Rank vs Grade | -0.86 |

## How to Run

```bash
pip install numpy pandas matplotlib seaborn jupyter
jupyter notebook youtube_project.ipynb
```

Python 3.12+ is recommended, because the notebook nests same-type quotes inside f-strings.

## Known Limitations

- Non-numeric Subscribers and Video Uploads values are silently set to 0, which can distort rankings, means and ratios.
- The Average Views step drops a column named `avg_views` that is not in the loaded data, so it raises a `KeyError` on a fresh run. Later cells reuse `Average Views` that was only created on a different DataFrame.
- Dividing by `Video Uploads` gives infinity for channels with 0 uploads.
- The "music artist" list filters on the text "VEVO", so it misses artists without a VEVO channel (for example Ed Sheeran) and is case-sensitive.
- The same conversion code is repeated in many cells, and the `Average Views` vs Grade plot appears twice.
- `plt.figure(figsize=(100,10))` is called after the plot, creating an empty figure.

See `YouTube_Project_Report.pdf` for details and recommended fixes.

## Tech Stack

Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter / Google Colab
