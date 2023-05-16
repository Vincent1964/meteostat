# Meteostat to InfluxDB

## Introduction

"Meteostat to InfluxDB" is a tool written in python to fetch the hourly weather forecast data from [meteostat.net](https://meteostat.net) and writes it into InfluxDB. Both InfluxDB 1 and Influx DB2 are supported.

The following weather data is collected:

|**tag**|**Description**|**data type**|
|-------|---------------|-------------|
| time    | Time of observation (YYYY-MM-DD hh:mm:ss)  | string        |
| temp    | Air temperature in °C                      | float         |
| dwpt    | Dew point in °C                            | float         |
| rhum    | Relative humidity in percent (%)           | integer       |
| prcp    | One-hour precipitation total in mm         | float         |
| snow    | Snow depth in mm                           | integer       |
| wdir    | Wind direction in degrees (°)              | integer       |
| wspd    | Average wind speed in km/h                 | float         |
| wpgt    | Peak wind gust in km/h                     | float         |
| pres    | Sea-level air pressure in millibar         | float         |
| tsun    | One-hour sunshine total in minutes (min)*  | integer       |
| coco    | Weather condition code**                   | integer       |

*) not always available
**) more information on the weather condition code (coco) can be found [here](https://dev.meteostat.net/formats.html#weather-condition-codes).

Forecast data is fetched for the next days and the script does not remove the historical data from InfluxDB.

To collect weather data for a location the coordinates (latitude, longitude, altitude) can be used. Alternatively, a single weather station can be selected.

## Why storing weather data in InfluxDB?

To fetch the actual weather forecast and store it in a local database seems not to make sense. Storage also creates historical weather data. This data also could be fetched on demand from Meteostat but depending the use case it requires too much requests.

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

## Running the script and check results

1.  Start the script with:

    ```shell
    python3 meteostat.py meteostat.ini
    ```
2.  Check if weather data is stored in InfluxDB.

## Visualization with Grafana

Data source configuration for InfluxDB 1.8:

-   the "Query Language" InfluxQL has to be selected
-   DEPRECATED: these dashboards will not be developed/extended any further

Data source configuration for InfluxDB \>=2.2.0 (not tested):

-   the "Query Language" Flux has to be selected
-   the bucket with the fritzbox data has to be set as default bucket (all dashboards use the default bucket)

## About Meteostat
Meteostat is one of the largest vendors of open weather and climate data. Access long-term time series of thousands of weather stations and integrate Meteostat data into your products, applications and workflows. Thanks to our open data policy, Meteostat is an ideal data source for research and educational projects.

You can help Meteostat provide free weather and climate data by making a [donation](https://dev.meteostat.net/donate.html)

## Disclaimer
The owner of this repository and author of the content is not af affiliated to Meteostat or RapidAPI.

## License
This project is licensed under the [Apace License Version 2.0](https://github.com/Vincent1964/meteostat/blob/main/LICENSE).
