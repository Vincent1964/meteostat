# Meteostat to InfluxDB

## Introduction

"Meteostat to InfluxDB" is a tool written in python to fetch weather forecast data from [meteostat.net](https://meteostat.net) and writes it into InfluxDB. Both InfluxDB 1 and Influx DB2 are supported.

The following weather data is collected:

|**tag**|**Description**|**data type**|
|-------|---------------|-------------|
| time    | Time of observation (YYYY-MM-DD hh:mm:ss)  | string        |
| temp    | The air temperature in °C                  | float         |
| dwpt    | The dew point in °C                        | float         |
| rhum    | The relative humidity in percent (%)       | integer       |
| prcp    | The one-hour precipitation total in mm     | float         |
| snow    | The snow depth in mm                       | integer       |
| wdir    | The wind direction in degrees (°)          | integer       |
| wspd    | The average wind speed in km/h             | float         |
| wpgt    | The peak wind gust in km/h                 | float         |
| pres    | The sea-level air pressure in hPa          | float         |
| tsun    | The one-hour sunshine total in minutes (m) | integer       |
| coco    | The weather condition code                 | integer       |

Forecast data is fetched for the next 5 days and the tool does not remove historical data from the InfluxDB.

To collect weather data for a location the coordinates (latitude, longitude, altitude) can be used. Alternatively, a single weather station can be selected.

## Requirements
-   python3.7 or newer
-   Influxdb (InfluxDB 1.8 or higher)
-   InfluxDB 2.0 python client
-   Meteostat API key & RapidAPI account

Meteostat weather data is collected via RapidAPI for this an account is needed. To get an account sign up on [RapidAPI](https://rapidapi.com/signup) and get an API key. Before you can use the API key, you'll need to subscribe to a [Meteostat plan](https://rapidapi.com/meteostat/api/meteostat/pricing). There exist a free plan that includes 500 monthly calls for free.

## Environment
- Grafana >=9.10

## Install the script
1.  Get the script (meteostat.py) and the ini file template (meteostat.template.ini).
2.  Rename the template to meteostat.ini and place it in a folder that fits to your system.
3.  Edit the template and fill in required information.

## Running the script

4.  Start the script with:

    ```shell
    python3 meteostat.py meteostat.ini
    ```
5.  Check if weather data is stored in InfluxDB.

## Visualization with Grafana

Data source configuration for InfluxDB 1.8:

-   the "Query Language" InfluxQL has to be selected
-   DEPRECATED: these dashboards will not be developed/extended any further

Data source configuration for InfluxDB \>=2.2.0:

-   the "Query Language" Flux has to be selected
-   the bucket with the fritzbox data has to be set as default bucket (all dashboards use the default bucket)

## License
This project is licensed under the [Apace License Version 2.0](https://github.com/Vincent1964/meteostat/blob/main/LICENSE).