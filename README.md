# SmoothieBar

## Description

A utility to display beautiful time bar-charts in the browser.

## Usage

See [example file](http://htmlpreview.github.com/?http://github.com/davidrapin/SmoothieBar/blob/master/example/index.html).

	<html>
	<head>
		<title>SmoothieBar Test</title>
		<script type="text/javascript" src="http://d3js.org/d3.v3.min.js"></script>
		<script type="text/javascript" src="./smoothiebar.js"></script>
		<script type="text/javascript">
		window.onload = function() {
		
		var chart = new SmoothieBar("chart", {
			dataLoader: function(wantedItems, callback) {
				var data = { "dataset 1", [], "dataset 2": [] };
				for (var i=0; i&lt;wantedItems; ++i) {
					data["dataset 1"].push(Math.random() * 50);
					data["dataset 2"].push(Math.random() * 50);
				}
				callback(data);
			}
		});
		chart.start();

		};
		</script>
	</head>
	<body>
		<h1>Chart example</h1>
		<div id="chart"></div>
	</body>

## Documentation

**SmoothieBar(id, params)**: Constructor.
 
* **id**: the id of the HTML element to add the chart to.
* **params**: the parameters ofthe chart
  * **dataLoader** (default: a random integer generator) see bellow.
  * **wantedItems** (default: `10`) the number of bars in the chart.
  * **totalHeight** (default: `200`) the total height of the chart (in pixels).
  * **totalWidth** (default: `1.0`) the width of the chart as a ration of the actual width of the containing element (between `0.0` and `1.0`).
  * **colorRange** (default: `["#051", "#0f3"]`) the rage of colors used as bar colors for different datasets.
  * **axisColor** (default: `"#051"`) the colors of axis and axis text.
  * **axisFontSize** (default: `12`) the font size used for axis and legend texts.
  * **legendLineHeight** (default: `11`) the line height used in legends.
  * **yAxisFormat** (default: `SmoothieBar.getFormat("")`) the Y axis format function (receives a number and returns a string)
  * **timeFormat** (default: function) the time formating function (receives a date object and returns a string)
  * **yAxisRight** (default: `false`) whether the Y axis should be on the right (`true`) or on the left (`false`).
  * **padding** (default: `{top: 15, right: 10, bottom: 17, left: 35}`) padding around the chart for the axis and legend (in pexiels).
  * **barColumnRatio** (default: `0.8`) the width of a bar as a ratio of the total column width, to add spacing between bars (between `0.0` anbd `1.0`).
  * **stackScaleMax** (default: `-1`) the maximum value of the Y axis (a positive number to set the value, or a negative number for automatic).
  * **frameDuration** (default: `1000`) the duration between new values, in milliseconds (the data callback is called every `frameDuration` milliseconds).
  * **transitionDuration** (default: `400`) the duration of the frame animation, in milliseconds. Cannot be longer than `frameDuration`.
  * **transitionEase** (default: `"linear"`) the type of frame transition animation. Can be [any type defined by d3.js](https://github.com/mbostock/d3/wiki/Transitions#wiki-d3_ease) (`"linear"` or `"bounce"` look best).

**start()**: Starts the chart animation.

**stop()**: Stops the chart animation.

**SmoothieBar.getFormat(suffix)**: Returns a format number function using scientific units, and the .

* **suffix** (default: none)



### The dataLoader function

The `dataLoader` function set in the parameters receives two arguments: the number of items wanted by the chart and a callback to call with the data, when the data is ready.

If the `dataLoader` parameter is left undefined, a random integer dataset generator is used, generating three datasets.

Typically, the first parameter (`wantedItems`) is equal to the number of bars in the chart on the first call, and the equal to 1 ever after (adding values to the chart one at a time).

