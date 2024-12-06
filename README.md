# Innomatics-test-tasks

Data Preprocessing Function
```
def get_cleaned_data(df):
    return (
        df
        .assign(
            haversine_dist=lambda df_: df_.apply(
                lambda row: haversine(
                    row['pickup_latitude'], row['pickup_longitude'], 
                    row['dropoff_latitude'], row['dropoff_longitude']
                ), 
                axis=1
            ),
            pickup_datetime = lambda df_: (
                pd.to_datetime(df_.pickup_datetime)
            ),
            pickup_year=lambda df_: (
                df_.pickup_datetime.dt.year
            ),
            pickup_month=lambda df_: (
                df_.pickup_datetime.dt.month_name()
            ),
            pickup_day=lambda df_: (
                df_.pickup_datetime.dt.day
            ),
            pickup_week_day=lambda df_: (
                df_.pickup_datetime.dt.day_name()
            )
        )

    )

```