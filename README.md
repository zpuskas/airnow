# airnow

Command line tool to fetch the current observations or the forecast of the PM2.5
AQI (fine particle air quality index) from [AirNow.gov](https://www.airnow.gov),
aimed at CLI users and various automation tasks.

## Configuration

User needs to create a `~/.config/airnow` configuration file and set the following
variables:
* API_KEY: API key to access data from AirNow.
* ZIP_CODE: ZIP code to request the AQI for.

Example:

```
API_KEY="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
ZIP_CODE="98101"
```

## API key

In order to use this script one has to obtain an API key. This is free and can
be done via the [developer tools](https://docs.airnowapi.org/login) page.

Note that the API is rate limited to 500 requests per hour, but that's okay,
since the current data changes hourly and the forecasts are generated once a
day. This should be plenty for most people.

If the same data is used multiple times, consider using some form of caching.
DON'T USE THE SCRIPT TO SCRAPE! [Bulk data downloads](https://docs.airnowapi.org/files)
are available for this purpose using the same registration.

## Usage

Usage:

````
airnow [-f] [-c] [-n] [-u]

  -c    Use colors in the output
  -f    Fetch forecast instead of current observation
  -h    Print help message
  -n    Print AQI information only, with date if forecast
  -u    Print AQI information only when AQI is unhealthy (>50)
````

Examples:

```
$ airnow
[||    ] 100 Moderate
```

```
$ airnow -f
2022-10-08 [|     ]  25 Good
2022-10-09 [|     ]  29 Good
2022-10-10 [|     ]  33 Good
2022-10-11 [|     ]  42 Good
2022-10-12 [|     ]  50 Good
```

Coloring assumes a 256 color terminal. Coloring scheme matches the one specified
by [Air Quality 101](https://docs.airnowapi.org/aq101).

## Dependencies

* [bash](https://www.gnu.org/software/bash/)
* [coreutils](https://www.gnu.org/software/coreutils/coreutils.html)
* [curl](https://curl.se/)
* [jq](https://stedolan.github.io/jq/)

## License

Copyright (c) 2022 Zoltan Puskas  
Licensed under GPLv3
