# grafana-json-api-infinity-datasource-apache-echarts

# 🚀 JSON API and Infinity Data Source tutorial for Grafana | How to display unemployment rate 🚀

JSON API and Infinity data sources demonstration for beginners. Using API, you can display data from any open dataset. Follow the video to get started!

https://github.com/coding-to-music/grafana-json-api-infinity-datasource-apache-echarts

From / By https://www.youtube.com/watch?v=B4Uj1n4Cr88&ab_channel=VolkovLabs

https://github.com/yesoreyeram/grafana-infinity-datasource (Infinity Datasource)

https://github.com/VolkovLabs/volkovlabs-echarts-panel (Apache ECharts Plugin)

https://github.com/grafana/grafana-json-datasource  (JSON API Plugin)

## Environment variables:

```java

```

## user interfaces:

- Grafana http://localhost:3000

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

https://api.bls.gov/publicAPI/v2/timeseries/data/LAUCN040010000000005

```json
{"status":"REQUEST_SUCCEEDED","responseTime":218,"message":[],"Results":{
"series":
[{"seriesID":"LAUCN040010000000005","data":[{"year":"2023","period":"M01","periodName":"January","latest":"true","value":"17585","footnotes":[{"code":"P","text":"Preliminary."}]},{"year":"2022","period":"M12","periodName":"December","value":"16945","footnotes":[{"code":"P","text":"Preliminary."}]},{"year":"2022","period":"M11","periodName":"November","value":"16890","footnotes":[{}]},{"year":"2022","period":"M10","periodName":"October","value":"16902","footnotes":[{}]},{"year":"2022","period":"M09","periodName":"September","value":"17149","footnotes":[{}]},{"year":"2022","period":"M08","periodName":"August","value":"17117","footnotes":[{}]},{"year":"2022","period":"M07","periodName":"July","value":"16084","footnotes":[{}]},{"year":"2022","period":"M06","periodName":"June","value":"16615","footnotes":[{}]},{"year":"2022","period":"M05","periodName":"May","value":"16951","footnotes":[{}]},{"year":"2022","period":"M04","periodName":"April","value":"16987","footnotes":[{}]},{"year":"2022","period":"M03","periodName":"March","value":"17428","footnotes":[{}]},{"year":"2022","period":"M02","periodName":"February","value":"17233","footnotes":[{}]},{"year":"2022","period":"M01","periodName":"January","value":"17241","footnotes":[{}]},{"year":"2021","period":"M12","periodName":"December","value":"17063","footnotes":[{}]},{"year":"2021","period":"M11","periodName":"November","value":"17154","footnotes":[{}]},{"year":"2021","period":"M10","periodName":"October","value":"17178","footnotes":[{}]},{"year":"2021","period":"M09","periodName":"September","value":"17331","footnotes":[{}]},{"year":"2021","period":"M08","periodName":"August","value":"17232","footnotes":[{}]},{"year":"2021","period":"M07","periodName":"July","value":"16202","footnotes":[{}]},{"year":"2021","period":"M06","periodName":"June","value":"16899","footnotes":[{}]},{"year":"2021","period":"M05","periodName":"May","value":"17219","footnotes":[{}]},{"year":"2021","period":"M04","periodName":"April","value":"17137","footnotes":[{}]},{"year":"2021","period":"M03","periodName":"March","value":"16938","footnotes":[{}]},{"year":"2021","period":"M02","periodName":"February","value":"16725","footnotes":[{}]},{"year":"2021","period":"M01","periodName":"January","value":"16860","footnotes":[{}]}]}]
}}
```

## Unemployment Rate


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


```
const series = data.series.map((s) => {
  const sData = s.fields.find((f) => f.type === 'number').values.buffer;
  const sTime = s.fields.find((f) => f.type === 'time').values.buffer;

  return {
    name: s.refId,
    type: 'line',
    showSymbol: false,
    areaStyle: {
      opacity: 0.1,
    },
    lineStyle: {
      width: 1,
    },
    data: sData.map((d, i) => [sTime[i], d.toFixed(2)]),
  };
});

```

```
const series = data.series.map((s) => {
  const sData = s.fields.find((f) => f.type === 'number').values.buffer;
  const sTime = s.fields.find((f) => f.type === 'time').values.buffer;

  return {
    name: s.refId,
    type: 'line',
    showSymbol: false,
    areaStyle: {
      opacity: 0.1,
    },
    lineStyle: {
      width: 1,
    },
    data: sData.map((d, i) => [sTime[i], d.toFixed(2)]),
  };
});

/**
 * Enable Data Zoom by default
 */
setTimeout(() => echartsInstance.dispatchAction({
  type: 'takeGlobalCursor',
  key: 'dataZoomSelect',
  dataZoomSelectActive: true,
}), 500);

/**
 * Update Time Range on Zoom
 */
echartsInstance.on('datazoom', function (params) {
  const startValue = params.batch[0]?.startValue;
  const endValue = params.batch[0]?.endValue;
  locationService.partial({ from: startValue, to: endValue });
});

return {
  backgroundColor: 'transparent',
  tooltip: {
    trigger: 'axis',
  },
  legend: {
    left: '0',
    bottom: '0',
    data: data.series.map((s) => s.refId),
    textStyle: {
      color: 'rgba(128, 128, 128, .9)',
    },
  },
  toolbox: {
    feature: {
      dataZoom: {
        yAxisIndex: 'none',
        icon: {
          zoom: 'path://',
          back: 'path://',
        },
      },
      saveAsImage: {},
    }
  },
  xAxis: {
    type: 'time',
  },
  yAxis: {
    type: 'value',
    min: 'dataMin',
  },
  grid: {
    left: '2%',
    right: '2%',
    top: '2%',
    bottom: 24,
    containLabel: true,
  },
  series,
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
volkovlabs-echarts-panel @ 4.2.0
```

This will output a list of all the plugins installed in your Grafana instance, along with their versions.

## To list installed data sources, run the following command:

```
docker-compose exec grafana grafana-cli datasources list
```

This will output a list of all the data sources installed in your Grafana instance, along with their types and IDs.
