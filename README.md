# Innomatics-test-tasks

Data Preprocessing Function
```
from math import radians, sin, cos, sqrt, atan2
def haversine(lat1, lon1, lat2, lon2):
    # Earth's radius in kilometers
    EARTH_RADIUS = 6371.0  
    lat1, lon1, lat2, lon2 = map(radians, [lat1, lon1, lat2, lon2])

    dlat = lat2 - lat1
    dlon = lon2 - lon1
    
    a = sin(dlat / 2)**2 + cos(lat1) * cos(lat2) * sin(dlon / 2)**2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))
    return EARTH_RADIUS * c

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