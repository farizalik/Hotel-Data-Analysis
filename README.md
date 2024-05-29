# Hotel Bookings Analysis

This project involves analyzing hotel booking data using Python. The analysis covers data import, exploration, cleaning, transformation, and insights generation.

## Datasets

The project uses the following datasets:

- `dim_date.csv`
- `dim_hotels.csv`
- `dim_rooms.csv`
- `fact_aggregated_bookings.csv`
- `fact_bookings.csv`

## Project Structure

- Contains all the CSV files used in the analysis.
- Contains Jupyter notebooks for data exploration and analysis.
- Contains Python scripts for data import and cleaning.
- Project documentation.

## Steps

### 1. Data Import and Exploration

Read the bookings data:

```python
import pandas as pd

df_bookings = pd.read_csv('datasets/fact_bookings.csv')
df_bookings.head()
```
## Explore the booking data:
```
df_bookings.shape
df_bookings.room_category.unique()
df_bookings.booking_platform.unique()
df_bookings.booking_platform.value_counts().plot(kind="bar")
df_bookings.describe()
```
### 2. Data Cleaning
## Clean invalid guest records:

```
df_bookings = df_bookings[df_bookings.no_guests > 0]
```
##Remove outliers in revenue generated:
```
avg, std = df_bookings.revenue_generated.mean(), df_bookings.revenue_generated.std()
higher_limit = avg + 3*std
df_bookings = df_bookings[df_bookings.revenue_generated <= higher_limit]
```
### 3. Data Transformation
## Create occupancy percentage column:
```
df_agg_bookings['occ_pct'] = df_agg_bookings.apply(lambda row: row['successful_bookings'] / row['capacity'], axis=1)
df_agg_bookings['occ_pct'] = df_agg_bookings['occ_pct'].apply(lambda x: round(x*100, 2))
```
### 4. Insights Generation
## Generate insights such as average occupancy rate, revenue realized per city, etc.
```
df_agg_bookings.groupby("room_category")["occ_pct"].mean()
df_agg_bookings.groupby("city")["occ_pct"].mean()
df.groupby("day_type")["occ_pct"].mean().round(2)
```
### Visualizations
## Include visualizations created during the analysis:
```
df_bookings.booking_platform.value_counts().plot(kind="bar")
```
