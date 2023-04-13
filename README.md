# grafana-json-api-infinity-datasource-apache-echarts

# 🚀 JSON API and Infinity Data Source tutorial for Grafana | How to display unemployment rate 🚀

JSON API and Infinity data sources demonstration for beginners. Using API, you can display data from any open dataset. Follow the video to get started!

https://github.com/coding-to-music/grafana-json-api-infinity-datasource-apache-echarts

From / By https://www.youtube.com/watch?v=B4Uj1n4Cr88&ab_channel=VolkovLabs

https://github.com/VolkovLabs/volkovlabs-echarts-panel (Apache ECharts Plugin)

https://github.com/yesoreyeram/grafana-infinity-datasource (Infinity Datasource) (AKA yesoreyeram-infinity-datasource)

https://github.com/grafana/grafana-json-datasource  (JSON API Plugin) (AKA marcusolsson-json-datasource)

https://grafana.com/grafana/plugins/marcusolsson-static-datasource/

## Environment variables:

```java

```

## user interfaces:

- Grafana http://localhost:3000
- Grafana http://localhost:4000
- Grafana http://localhost:8086

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/grafana-json-api-infinity-datasource-apache-echarts.git
git push -u origin main
```

### LINKS FROM THE VIDEO
- 👉 U.S. BUREAU OF LABOR STATISTICS https://www.bls.gov/
- 👉 Adjusted Apache ECharts scripts for Grafana https://echarts.volkovlabs.io/
- 👉 Original Apache ECharts resource https://echarts.apache.org/
- 👉 The home of the U.S. Government’s open data https://data.gov/
- 👉 NASA's clearinghouse site for open data provided to the public https://data.nasa.gov/

### CHAPTERS

- 00:00 Intro
- 00:40 Installation of JSON API, Infinity, and Apache ECharts panel 
- 02:17 Open datasets
- 02:41 Public Data API on bls.gov, what JSON data file looks like
- 04:05 Basic setup of Infinity and JSON API
- 05:13 Create a new dashboard with JSON API data source, read the data
- 08:40 Where to get Apache ECharts visualization templates
- 09:55 More visualization tricks
- 11:01 Build the exact visualization using Infinity
- 12:46 Adding parameters to the API request for JSON API
- 14:29 Adding parameters to the API request for Infinity 
- 15:25 Adding second series, JSON API
- 17:59 Adding second series, infinity

### GET IN TOUCH

- Volkov Labs specializes in developing plugins to use Grafana as a Platform. Trusted by the Community.
- 👉 GitHub for issues and questions: https://github.com/VolkovLabs

## Open Weather Map Grafana Dashboard

uses InfluxDB data source

![Open Weather Map Grafana](images/OpenWeatherMap.jpg)

## start stand-alone Grafana via docker

```
docker run -d -p 3000:3000 --name grafana grafana/grafana:latest
```

## BLS Data

https://www.bls.gov/developers/api_signature_v2.htm

HTTP Type:	GET
URL (JSON):	https://api.bls.gov/publicAPI/v2/timeseries/data/
Payload:	series_id
Example Payload:	LAUCN040010000000005

https://api.bls.gov/publicAPI/v2/timeseries/data/LAUCN040010000000005  -- use this in the browser to test

https://api.bls.gov/publicAPI/v2/timeseries/data/LNS14000000  -- use this in the browser to test

https://api.bls.gov/publicAPI/v2/timeseries/data/  - use this in the datasource - will say Method not allowed

/LAUCN040010000000005 -- don't use this, use Series ID	:	LNS14000000

```json
{"status":"REQUEST_SUCCEEDED","responseTime":218,"message":[],"Results":{
"series":
[{"seriesID":"LAUCN040010000000005","data":[{"year":"2023","period":"M01","periodName":"January","latest":"true","value":"17585","footnotes":[{"code":"P","text":"Preliminary."}]},{"year":"2022","period":"M12","periodName":"December","value":"16945","footnotes":[{"code":"P","text":"Preliminary."}]},{"year":"2022","period":"M11","periodName":"November","value":"16890","footnotes":[{}]},{"year":"2022","period":"M10","periodName":"October","value":"16902","footnotes":[{}]},{"year":"2022","period":"M09","periodName":"September","value":"17149","footnotes":[{}]},{"year":"2022","period":"M08","periodName":"August","value":"17117","footnotes":[{}]},{"year":"2022","period":"M07","periodName":"July","value":"16084","footnotes":[{}]},{"year":"2022","period":"M06","periodName":"June","value":"16615","footnotes":[{}]},{"year":"2022","period":"M05","periodName":"May","value":"16951","footnotes":[{}]},{"year":"2022","period":"M04","periodName":"April","value":"16987","footnotes":[{}]},{"year":"2022","period":"M03","periodName":"March","value":"17428","footnotes":[{}]},{"year":"2022","period":"M02","periodName":"February","value":"17233","footnotes":[{}]},{"year":"2022","period":"M01","periodName":"January","value":"17241","footnotes":[{}]},{"year":"2021","period":"M12","periodName":"December","value":"17063","footnotes":[{}]},{"year":"2021","period":"M11","periodName":"November","value":"17154","footnotes":[{}]},{"year":"2021","period":"M10","periodName":"October","value":"17178","footnotes":[{}]},{"year":"2021","period":"M09","periodName":"September","value":"17331","footnotes":[{}]},{"year":"2021","period":"M08","periodName":"August","value":"17232","footnotes":[{}]},{"year":"2021","period":"M07","periodName":"July","value":"16202","footnotes":[{}]},{"year":"2021","period":"M06","periodName":"June","value":"16899","footnotes":[{}]},{"year":"2021","period":"M05","periodName":"May","value":"17219","footnotes":[{}]},{"year":"2021","period":"M04","periodName":"April","value":"17137","footnotes":[{}]},{"year":"2021","period":"M03","periodName":"March","value":"16938","footnotes":[{}]},{"year":"2021","period":"M02","periodName":"February","value":"16725","footnotes":[{}]},{"year":"2021","period":"M01","periodName":"January","value":"16860","footnotes":[{}]}]}]
}}
```

## Unemployment Rate

https://api.bls.gov/publicAPI/v2/timeseries/data/  - use this in the datasource - will say Method not allowed

Series Title	:	(Seas) Unemployment Rate
Series ID	:	LNS14000000

## JSON API query

```
/LNS14000000
```

## JSON API Fields

```
$.Results.series[0].data[*].year
$.Results.series[0].data[*].periodName
$.Results.series[0].data[*].value
```

Below is the  dataframe retrieval

```
data.series.map((s) => {
  if (s.refId === "A") {
    yearA = s.fields.find((f) => f.name === "year").values.buffer;
    monthA = s.fields.find((f) => f.name === "periodName").values.buffer;
    valueA = s.fields.find((f) => f.name === "value").values.buffer;
  }
});

const month_yearA = monthA.map((d, i) => `${d} ${yearA[i]}`);
```

Below is the generic smoothed line from https://echarts.volkovlabs.io/d/tg6gWiKVk/line?orgId=1&editPanel=4

```
return {
  grid: {
    bottom: "3%",
    containLabel: true,
    left: "3%",
    right: "4%",
    top: "4%"
  },
  series: [
    {
      data: [
        820,
        932,
        901,
        934,
        1290,
        1330,
        1320
      ],
      smooth: true,
      type: "line"
    }
  ],
  xAxis: {
    data: [
      "Mon",
      "Tue",
      "Wed",
      "Thu",
      "Fri",
      "Sat",
      "Sun"
    ],
    type: "category"
  },
  yAxis: {
    type: "value"
  }
};
```

Now we replace:
- replace series yAxis data with valueA.reverse() 
- replace series xAxis data with month_yearA.reverse()

```
return {
  grid: {
    bottom: "3%",
    containLabel: true,
    left: "3%",
    right: "4%",
    top: "4%"
  },
  series: [
    {
      data: valueA.reverse(),
      smooth: true,
      type: "line"
    }
  ],
  xAxis: {
    data: month_yearA.reverse(),
    type: "category"
  },
  yAxis: {
    type: "value"
  }
};
```

Add the dataframe retrieval at the beginning

```
data.series.map((s) => {
  if (s.refId === "A") {
    yearA = s.fields.find((f) => f.name === "year").values.buffer;
    monthA = s.fields.find((f) => f.name === "periodName").values.buffer;
    valueA = s.fields.find((f) => f.name === "value").values.buffer;
  }
});

const month_yearA = monthA.map((d, i) => `${d} ${yearA[i]}`);

return {
  grid: {
    bottom: "3%",
    containLabel: true,
    left: "3%",
    right: "4%",
    top: "4%"
  },
  series: [
    {
      data: valueA.reverse(),
      smooth: true,
      type: "line"
    }
  ],
  xAxis: {
    data: month_yearA.reverse(),
    type: "category"
  },
  yAxis: {
    type: "value"
  }
};
```

## Add markpoint for Min and Max values

```
data.series.map((s) => {
  if (s.refId === "A") {
    yearA = s.fields.find((f) => f.name === "year").values.buffer;
    monthA = s.fields.find((f) => f.name === "periodName").values.buffer;
    valueA = s.fields.find((f) => f.name === "value").values.buffer;
  }
});

const month_yearA = monthA.map((d, i) => `${d} ${yearA[i]}`);

return {
  grid: {
    bottom: "3%",
    containLabel: true,
    left: "3%",
    right: "4%",
    top: "4%"
  },
  series: [
    {
      data: valueA.reverse(),
      smooth: true,
      type: "line",
      markPoint: {
        data: [
          {
            name: "Max",
            type: "max"
          },
          {
            name: "Min",
            type: "min"
          }
        ]
      }
    }
  ],
  xAxis: {
    data: month_yearA.reverse(),
    type: "category"
  },
  yAxis: {
    type: "value"
  }
};
```

## Add Markpoint font and dots for data points and Zoom

```
data.series.map((s) => {
  if (s.refId === "A") {
    yearA = s.fields.find((f) => f.name === "year").values.buffer;
    monthA = s.fields.find((f) => f.name === "periodName").values.buffer;
    valueA = s.fields.find((f) => f.name === "value").values.buffer;
  }
});

const month_yearA = monthA.map((d, i) => `${d} ${yearA[i]}`);

return {
  grid: {
    bottom: "3%",
    containLabel: true,
    left: "3%",
    right: "4%",
    top: "4%"
  },
  series: [
    {
      data: valueA.reverse(),
      smooth: true,
      type: "line",
      markPoint: {
        data: [
          {
            name: "Max",
            type: "max",
            label: { fontsize: 19, fontFamily: 'Roboto', color: 'white'},
            symbolSise: 80,
            symbolRotate: 20
          },
          {
            name: "Min",
            type: "min",
            label: { fontsize: 19, fontFamily: 'Roboto', color: 'white'},
            symbolSise: 80
          }
        ]
      }
    }
  ],
  xAxis: {
    data: month_yearA.reverse(),
    type: "category"
  },
  yAxis: {
    type: "value"
  },
  dataZoom: [
    {
      show: true,
      type: 'inside',
      filterMode: 'none',
      xAxisIndex: [0],
      startValue: 0,
      endValue: 200,
    }
  ],
};
```


# Use the grafana-cli tool to list all installed plugins and data sources in your Grafana instance.

## To list installed plugins, run the following command:

```
docker-compose exec grafana grafana-cli plugins ls
```

Output

```
installed plugins:
golioth-websocket-datasource @ 1.0.2
marcusolsson-static-datasource @ 2.2.0
volkovlabs-echarts-panel @ 4.2.0
```

This will output a list of all the plugins installed in your Grafana instance, along with their versions.

## To list installed data sources, run the following command:

This does not work - the cli does not provide this

```
docker-compose exec grafana grafana-cli datasources list
```

This will output a list of all the data sources installed in your Grafana instance, along with their types and IDs.

## Static Data Source for Grafana

https://grafana.com/grafana/plugins/marcusolsson-static-datasource/

## Ensure all datasources and plugins are installed 

https://github.com/VolkovLabs/volkovlabs-echarts-panel (Apache ECharts Plugin)

### These need to be installed using the AKA names specified 

```
- GF_INSTALL_PLUGINS=marcusolsson-static-datasource,golioth-websocket-datasource,volkovlabs-echarts-panel,marcusolsson-json-datasource,yesoreyeram-infinity-datasource
```

https://github.com/yesoreyeram/grafana-infinity-datasource (Infinity Datasource) (AKA yesoreyeram-infinity-datasource)

https://github.com/grafana/grafana-json-datasource  (JSON API Plugin) (AKA marcusolsson-json-datasource)

## To list installed plugins, run the following command:

```
docker-compose exec grafana grafana-cli plugins ls
```

Output

```
installed plugins:
golioth-websocket-datasource @ 1.0.2
marcusolsson-json-datasource @ 1.3.4
marcusolsson-static-datasource @ 2.2.0
volkovlabs-echarts-panel @ 4.2.0
yesoreyeram-infinity-datasource @ 1.3.0
```

## Best way to start and continue calling OpenWeather APIs

https://openweathermap.org/appid

API key is everything you need to call for weather data

Please, use your API key in every API call you make. Our platform only processes the API requests with an API key included. The API keys linked to your account are used to take count of the calls you make to OpenWeather platform.

Example on how to make an API call using your API key

API call

```
http://api.openweathermap.org/data/2.5/forecast?id=524901&appid={API key}
```

- Parameters

`appid`	required	Your unique API key (you can always find it on your account page under the "API key" tab)
Example of API call

```
api.openweathermap.org/data/2.5/forecast?id=524901&appid={API key}
```

## Geocoding API 

is a simple tool that we have developed to ease the search for locations while working with geographic names and coordinates.

Supporting API calls by geographical coordinates is the most accurate way to specify any location, that is why this method is integrated in all OpenWeather APIs. However, this way is not always suitable for all users.
Geocoding is the process of transformation of any location name into geographical coordinates, and the other way around (reverse geocoding). OpenWeather’s Geocoding API supports both the direct and reverse methods, working at the level of city names, areas and districts, countries and states:

- Direct geocoding converts the specified name of a location or zip/post code into the exact geographical coordinates;
- Reverse geocoding converts the geographical coordinates into the names of the nearby locations.

## Direct geocoding

Direct geocoding allows to get geographical coordinates (lat, lon) by using name of the location (city name or area name). If you use the limit parameter in the API call, you can cap how many locations with the same name will be seen in the API response (for instance, London in the UK and London in the US).

## Coordinates by location name

```
http://api.openweathermap.org/geo/1.0/zip?zip="02109",US&appid={API key}
```

```json
{"zip":"02109","name":"Boston","lat":42.36,"lon":-71.0545,"country":"US"}
```

## Gathering weather data

https://api.openweathermap.org/data/2.5/weather?units=metric&lat=latitude&lon=longitude&appid=apiKey


## How to make an API call

API call

```
http://api.openweathermap.org/geo/1.0/direct?q={city name},{state code},{country code}&limit={limit}&appid={API key}

http://api.openweathermap.org/geo/1.0/direct?q=Boston,MA,USA&limit=50&appid={API key}
```

## Parameters
- `q`	required	City name, state code (only for the US) and country code divided by comma. Please use ISO 3166 country codes.
- `appid`	required	Your unique API key (you can always find it on your account page under the "API key" tab)
- `limit`	optional	Number of the locations in the API response (up to 5 results can be returned in the API response)

Example of API call

http://api.openweathermap.org/geo/1.0/direct?q=London&limit=5&appid={API key}

## Example of API response
              
```
[
  {
    "name": "London",
    "local_names": {
      "af": "Londen",
      "ar": "لندن",
      "ascii": "London",
      "az": "London",
      "bg": "Лондон",
      "ca": "Londres",
      "da": "London",
      "de": "London",
      "el": "Λονδίνο",
      "en": "London",
      "eu": "Londres",
      "fa": "لندن",
      "feature_name": "London",
      "fi": "Lontoo",
      "fr": "Londres",
      "gl": "Londres",
      "he": "לונדון",
    },
    "lat": 51.5085,
    "lon": -0.1257,
    "country": "GB"
  },
  {
    "name": "London",
    "local_names": {
      "ascii": "London",
      "ca": "Londres",
      "en": "London",
      "feature_name": "London"
    },
    "lat": 36.4761,
    "lon": -119.4432,
    "country": "US",
    "state": "CA"
  }
]
```
              
## Fields in API response

Please note that the fields present will vary based on a country to which a location belongs as well as a specific location.

- name Name of the found location
- local_names
- local_names.[language code] Name of the found location in different languages. The list of names can be different for different locations
- local_names.ascii Internal field
- local_names.feature_name Internal field
- lat Geographical coordinates of the found location (latitude)
- lon Geographical coordinates of the found location (longitude)
- country Country of the found location
- state (where available) State of the found location
- Coordinates by zip/post code

## How to make an API call

```
http://api.openweathermap.org/geo/1.0/zip?zip={zip code},{country code}&appid={API key}
```

Parameters
zip code	required	Zip/post code and country code divided by comma. Please use ISO 3166 country codes.
appid	required	Your unique API key (you can always find it on your account page under the "API key" tab)

## Example of API call

```
http://api.openweathermap.org/geo/1.0/zip?zip=E14,GB&appid={API key}
```

## Example of API response                

```
{
  "zip": "90210",
  "name": "Beverly Hills",
  "lat": 34.0901,
  "lon": -118.4065,
  "country": "US"
}
```
              
## Fields in API response

- `zip` Specified zip/post code in the API request
- `name` Name of the found area
- `lat` Geographical coordinates of the centroid of found zip/post code (latitude)
- `lon` Geographical coordinates of the centroid of found zip/post code (longitude)
- `country` Country of the found zip/post code

## Reverse geocoding

Reverse geocoding allows to get name of the location (city name or area name) by using geografical coordinates (lat, lon). The limit parameter in the API call allows you to cap how many location names you will see in the API response.

## How to make an API call

```
http://api.openweathermap.org/geo/1.0/reverse?lat={lat}&lon={lon}&limit={limit}&appid={API key}
```

Parameters

- lat, lon	required	Geographical coordinates (latitude, longitude)
- appid	required	Your unique API key (you can always find it on your account page under the "API key" tab)
- limit	optional	Number of the location names in the API response (several results can be returned in the API response)

## Example of API call

```
http://api.openweathermap.org/geo/1.0/reverse?lat=51.5098&lon=-0.1180&limit=5&appid={API key}
```

## Example of API response


```
  [
  {
    "name": "City of London",
    "local_names": {
      "ar": "مدينة لندن",
      "ascii": "City of London",
      "bg": "Сити",
      "ca": "La City",
      "de": "London City",
      "el": "Σίτι του Λονδίνου",
      "en": "City of London",
      "fa": "سیتی لندن",
      "feature_name": "City of London",
      "fi": "Lontoon City",
      "fr": "Cité de Londres",
      "gl": "Cidade de Londres",
      "he": "הסיטי של לונדון",
      "hi": "सिटी ऑफ़ लंदन",
      "id": "Kota London",
      "it": "Londra",
      "ja": "シティ・オブ・ロンドン",
      "la": "Civitas Londinium",
      "lt": "Londono Sitis",
      "pt": "Cidade de Londres",
      "ru": "Сити",
      "sr": "Сити",
      "th": "นครลอนดอน",
      "tr": "Londra Şehri",
      "vi": "Thành phố Luân Đôn",
      "zu": "Idolobha weLondon"
    },
    "lat": 51.5128,
    "lon": -0.0918,
    "country": "GB"
  },
    "lat": 51.4535,
    "lon": -0.018,
    "country": "GB"
  },
  {
    "name": "Islington",
    "local_names": {
      "ascii": "Islington",
      "de": "London Borough of Islington",
      "en": "Islington",
      "feature_name": "Islington",
    },
    "lat": 51.547,
    "lon": -0.1094,
    "country": "GB"
  }
]
```
                  
## Fields in API response

Please note that the fields present will vary based on a country to which a location belongs as well as a specific location.
name Name of the found location
- `local_names`
- `local_names.[language code]` Name of the found location in different languages. The list of names can be different for different locations.
- `local_names.ascii` Internal field
- `local_names.feature_name` Internal field
- `lat` Geographical coordinates of the found location (latitude)
- `lon` Geographical coordinates of the found location (longitude)
- `country` Country of the found location
- `state` (where available) State of the found location
