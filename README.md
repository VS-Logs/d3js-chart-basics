# D3.js Chart Basics

*Click <img src="https://github.com/learning-zone/d3js-interview-questions/blob/master/assets/star.png" width="18" height="18" align="absmiddle" title="Star" /> if you like the project. Pull Request are highly appreciated.*

<br/>

## Table of Contents

* *[D3.js Functions List](d3-functions-list.md)*  

<br/>

## Q. How data binding work in d3.js?

D3 includes the following important methods for data binding.

|Method	  |Description |
|---------|--------------------|
|data()	  | Joins data to the selected elements|
|enter()  |	Creates a selection with placeholder references for missing elements|
|exit()	  |  Removes nodes and adds them to the exit selection which can be later removed from the DOM|
|datum()  |	Injects data to the selected element without computing a join.|

**data():**

The data() function is used to join the specified array of data to the selected DOM elements and return the updated selection. D3 works with different types of data like Array, CSV, TSV, JSON, XML etc.

```html
<body>
    <p>D3 Data Binding Example </p>

    <script>
        var myData = [1, 2, 3, 4, 5];
     
         var p = d3.select("body")
                   .selectAll("p")
                   .data(myData)
                   .text(function (d, i) {
                        return d;
                    });
    </script>
</body>
```

**enter():**

The enter() method dynamically creates placeholder references corresponding to the number of data values. The output of enter()can be fed to append() method and append() will create DOM elements for which there are no corresponding DOM elements on the page.

```html
<body>
<script>
    var data = [4, 1, 6, 2, 8, 9];
    var body = d3.select("body")
                .selectAll("span")
                .data(data)
                .enter()
                .append("span")
                .text(function(d) { return d + " "; });
</script>
</body>
```

**exit():**

While enter() is used to add new reference nodes, exit is used to remove a node.

```html
<body>
    <p>D3 exit Example</p>
    <p></p>
    <p></p>
    <script>
    
    var myData = ["Hello World!"];

    var p = d3.select("body")
                .selectAll("p")
                .data(myData)
                .text(function (d, i) {
                    return d;
                })
                .exit()
                .remove();
    </script>
</body>
```

**datum():**

The datum() function is used for static visualization which does not need updates. It binds data directly to an element.

```html
<body>
    <p>D3 datum Example</p>
    <script>

    d3.select("body")
        .select("p")
        .datum(100)
        .text(function (d, i) {
            return d;
        });
    </script>
</body>
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is SVG?

SVG or Scalable Vector Graphics (SVG) is an XML, the markup language for determining two-dimensional vector graphics. SVG is crucial for graphics what XHTML to text.

```html
<!-- Rectangle -->
<div>Rectangle</div>
<svg width="200" height="200">
    <rect x="5" y="5" width="190" height="190" fill="#1e90ff"></rect>
</svg>


<!-- Line -->
<div>Line</div>
<svg height="200" width="200">
    <line x1="0" y1="0" x2="200" y2="200" style="stroke:rgb(255,0,0);stroke-width:2" />
</svg>


<!-- Circle -->
<div>Circle</div>
<svg height="200" width="200">
    <circle cx="100" cy="100" r="45" stroke="#333" stroke-width="2" fill="orange" />
</svg>


<!-- Text -->
<div>Text</div>
<svg height="200" width="250">
    <text x="10" y="120" font-family="sans-serif" font-size="25" style="fill: #333;">SVG Text Example</text>
</svg>


<!-- Polyline -->
<div>Polyline</div>
<svg height="200" width="200">
    <polyline points="10 35, 30 10, 50 35" stroke="green" fill="transparent" stroke-width="2" />
</svg>
```

[Live Example](https://learning-zone.github.io/d3js-interview-questions/a.svg.html)

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the difference between canvas and SVG in d3.js?

SVG is abbreviated as **Scalable Vector Graphics**. It is a vector-based graphics and used the XML based format for graphics providing the support for interaction. SVG images are way better than bitmap images.  In SVG images, the vector image is composed of a fixed set of shapes and while scaling these images it preserves the shape of the image.

Canvas is an HTML element, which is used to draw graphics on the web page. It is referred to as a bitmap with an immediate mode graphics application programming interface. For drawing on it. The element canvas is used as a container for graphics. In Canvas, we need the script to draw the graphics.

```html
<canvas id="myCanvas" width="800" height="800"></canvas>
```

```js
var canvas = document.getElementById('myCanvas');
var context = canvas.getContext('2d');
context.fillStyle = '#c00';
context.fillRect(10, 10, 100, 100);
```

**Canvas vs SVG in D3:**

With SVG, data binding is easy - we can assign a datum to an individual svg element and then use that datum to set its attributes/update it/etc. This is built upon the statefulness of svg - we can re-select a circle and modify it or access its properties.

With Canvas, canvas is stateless, so we can\'t bind data to shapes within the canvas as the canvas only comprises of pixels. As such we can\'t select and update elements within the canvas because the canvas doesn\'t have any elements to select.

In D3js the `enter`/`update`/`exit` cycle (or basic append statements) are needed for svg in idiomatic D3: we need to enter elements to see them and we style them often based on their datum. With canvas, we don\'t need to enter anything, same with `exiting`/`updating`. There are no elements to append in order to see, so we can draw visualizations without the `enter`/`update`/`exit` or the append/insert approaches used in d3 svg visualizations.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain selections in d3.js?

D3 Selections allow data-driven transformation of the document object model (DOM): set attributes, styles, properties, HTML or text content, etc. Using the data join\'s enter and exit selections, you can also add or remove elements to correspond to data.

|Method	                    |Description |
|---------------------------|---------------------------------------------------------------------------------------|
|d3.select(css-selector)	|Returns the first matching element in the HTML document based on specified css-selector|
|d3.selectAll(css-selector)	|Returns all the matching elements in the HTML document based on specified css-selector|

*Example:*

```html
<div class="container">
    <h2>Select DOM Elements using D3</h2>
    <section id="chart">
        <div class="item">Barot Bellingham</div>
        <div class="item">Hassum Harrod</div>
        <div class="item">Jennifer Jerome</div>
        <div class="item">Richard Tweet</div>
        <div class="item">Lorenzo Garcia</div>
        <div class="item">Xhou Ta</div>
    </section>
</div>
```

```js
    d3.selectAll('.item:nth-child(2n)')
            .style("color", "green");
```

[Live Example](https://learning-zone.github.io/d3js-interview-questions/b.selection.html)

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain about d3.js Scales?

D3.js provides scale functions to perform data transformations. These functions map an input domain to an output range. D3 provides the following scaling methods for different types of charts.

|Scale Type  |	Method	          |   Description |
|------------|------------------- |----------------|
|Continuous	 |d3.scaleLinear()    |Construct continuous linear scale where input data (domain) maps to specified output range.|
|            |d3.scaleIdentity()  |Construct linear scale where input data is the same as output.|
|            |d3.scaleTime()	  |Construct linear scale where input data is in dates and output in numbers.|
|            |d3.scaleLog()	      |Construct logarithmic scale.|
|            |d3.scaleSqrt()	  |Construct square root scale.|
|            |d3.scalePow()	      |Construct exponential scale.|
|Sequential	 |d3.scaleSequential()|Construct sequential scale where output range is fixed by interpolator function.|
|Quantize	 |d3.scaleQuantize()  |Construct quantize scale with discrete output range.|
|Quantile	 |d3.scaleQuantile()  |Construct quantile scale where input sample data maps to discrete output range.|
|Threshold	 |d3.scaleThreshold() |Construct scale where arbitrary input data maps to discrete output range.|
|Band	     |d3.scaleBand()	  |Band scales are like ordinal scales except the output range is continuous and numeric.|
|Point	     |d3.scalePoint()	  |Construct point scale.|
|Ordinal	 |d3.scaleOrdinal()	  |Construct ordinal scale where input data includes alphabets and are mapped to discrete numeric output range.|

Example

```html
<div class="container">
    <h1>D3 Color Scales</h1>
    <div id="chart"></div>
</div>
```

```js
var bardata = [90, 45, 25, 15, 10, 7];
     
var height = 400,
    width = 600,
    barWidth = 50,
    barOffset = 5;

var colors = d3.scale.linear()
    .domain([0, bardata.length])
    .range(['#C61C6F', '#B58929']);

var yScale = d3.scale.linear()
    .domain([0, d3.max(bardata)])
    .range([0, height]);

var xScale = d3.scale.ordinal()
    .domain(d3.range(0, bardata.length))
    .rangeBands([0, width]);

d3.select('#chart').append('svg')
    .attr('width', width)
    .attr('height', height)
    .style('background', '#C9D7D6')
    .selectAll('rect').data(bardata)
    .enter().append('rect')
    .style('fill', function (d, i) {
        return colors(i);
    })
    .attr('width', xScale.rangeBand() - 10)
    .attr('height', function (d) {
        return yScale(d);
    })
    .attr('x', function (d, i) {
        return xScale(i);
    })
    .attr('y', function (d) {
        return height - yScale(d);
    });
```

[Live Example](https://learning-zone.github.io/d3js-interview-questions/i.scales.html)

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What are the slider available in d3.js?

The slider available in d3.js are

* Default slider

```js
d3.slider()
```

* Slider with start value

```js
d3.slider().value(25)
```

* Slider with slide event

```js
d3.slider().on("slide", function(evt, value) {
  d3.select('#slider3text').text(value);
})
```

* Slider with default axis

```js
d3.slider().axis(true)
```

* Slider with custom axis

```js
d3.slider().axis( d3.svg.axis().orient("top").ticks(6) )
```

* Slider with min, max, and step values

```js
d3.slider().axis(true).min(2000).max(2100).step(5)
```

* Vertical Slider

```js
d3.slider().value(50).orientation("vertical")
```

**Example:**

```html
<p id="value"></p>
<div id="slider"></div>
```

```js
var slider = d3
    .sliderHorizontal()
    .min(0)
    .max(10)
    .step(1)
    .width(300)
    .displayValue(false)
    .on('onchange', val => {
      d3.select('#value').text(val);
    });

  d3.select('#slider')
    .append('svg')
    .attr('width', 500)
    .attr('height', 100)
    .append('g')
    .attr('transform', 'translate(30,30)')
    .call(slider);
```

[Live Example](https://learning-zone.github.io/d3js-interview-questions/slider.html)

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is difference between domain, range and scale in d3.js?

**Domain:**

```js
D for Domain, D for Data.
```

Domain represents the boundaries within which your data lies. e.g. If I had an array of numbers with no number smaller than 1 and no number larger than 100, my domain would be 1 to 100.

**Range**  
You usually make use of a range when you want to transform the value of a raw data point into a corresponding pixel coordinate.

**Scale**  
Now that you know what a domain and range is, you need a way to convert your data into corresponding values in the domain. And thats exactly what scales do.

The most common types of scales are – quantitative scales and ordinal scales.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the role of “Path Data Generator” in d3.js?

D3.js includes a set of Path Data Generators helper classes for generating SVG Path instructions.

```js
d3.svg.line()
```

Path generator includes

* `d3.svg.line()` - create a new line generator
* `d3.svg.line.radial()` - create a new radial line generator
* `d3.svg.area()` - create a new area generator
* `d3.svg.area.radial()` - create a new radial area generator
* `d3.svg.arc()` - create a new arc generator
* `d3.svg.symbol()` - create a new symbol generator
* `d3.svg.chord()` - create a new chord generator
* `d3.svg.diagonal()` - create a new diagonal generator
* `d3.svg.diagonal.radial()` - create a new radial diagonal generator

*Example:*

```js
//The data for our line
var lineData = [ { "x": 1,   "y": 5},  { "x": 20,  "y": 20},
                 { "x": 40,  "y": 10}, { "x": 60,  "y": 40},
                 { "x": 80,  "y": 5},  { "x": 100, "y": 60}];

//This is the accessor function we talked about above
var lineFunction = d3.svg.line()
                         .x(function(d) { return d.x; })
                         .y(function(d) { return d.y; })
                         .interpolate("linear");

//The SVG Container
var svgContainer = d3.select("body").append("svg")
                                    .attr("width", 200)
                                    .attr("height", 200);

//The line SVG Path we draw
var lineGraph = svgContainer.append("path")
                            .attr("d", lineFunction(lineData))
                            .attr("stroke", "blue")
                            .attr("stroke-width", 2)
                            .attr("fill", "none");
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What d3.js enter method does?

D3.js enter method returns the virtual enter selection from the data operator.  This method is only applicable to Data Operator as such data operator is the only one that returns three virtual selections.

```js
var numbers = [15, 8, 42, 4, 32];
```

When our dataset contains more items than there are available DOM elements, the surplus data items are stored in a sub set of this selection called the *enter* selection.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Mention the command used to create simple axis in d3.js?

The command to create simple axis in d3.js is

```js
var xAxis = d3.svg.axis().
```

|Axis Method	 |               Description          |
|----------------|------------------------------------|
|d3.axisTop()	 |Creates top horizontal axis.        |
|d3.axisRight()	 |Creates vertical right-oriented axis.|
|d3.axisBottom() |Creates bottom horizontal axis.      |
|d3.axisLeft()	 |Creates left vertical axis.          |

*Example:*

```html
<div class="container">
    <h1>Axes in D3</h1>
    <div id="chart"></div>
</div>
```

```js
var width = 500, height = 500;
var data = [10, 20, 30, 40, 50];
var svg = d3.select("body")
    .append("svg")
    .attr("width", width)
    .attr("height", height);

var xscale = d3.scaleLinear()
    .domain([0, d3.max(data)])
    .range([0, width - 100]);

var yscale = d3.scaleLinear()
        .domain([0, d3.max(data)])
        .range([height/2, 0]);

var x_axis = d3.axisBottom()
        .scale(xscale);

var y_axis = d3.axisLeft()
        .scale(yscale);
    svg.append("g")
       .attr("transform", "translate(50, 10)")
       .call(y_axis);

var xAxisTranslate = height/2 + 10;
    svg.append("g")
       .attr("transform", "translate(50, " + xAxisTranslate  +")")
       .call(x_axis);
```

[Live Example](https://learning-zone.github.io/d3js-interview-questions/j.axis.html)

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is SVG group element?

SVG group element is used to group SVG element together; each SVG group element is a container which consists of child SVG elements.  It is defined by `<g>` and `</g>`.

## Q. How to apply multiple classes at once in D3?

To set multiple classes at once you can use the object literal as

```js
selection.classed({ 'foo':true, 'bar': false})
```

## Q. What is a transition in d3.js?

Transition in d3.js gradually interpolate attributes and styles over time, transition is used for animation purpose.  It is based on only two key frames, start, and end.  The starting key frame defines the current state of the DOM, while the ending key frame is a set of styles, attributes and other properties specified.

|Method	               |Description                                           |
|----------------------|------------------------------------------------------|
|selection.transition()|this schedules a transition for the selected elements |
|transition.duration() |duration specifies the animation duration in milliseconds for each element |
|transition.ease()	   |ease specifies the easing function, example: linear, elastic, bounce |
|transition.delay()	   |delay specifies the delay in animation in milliseconds for each element |

*Example:*

```html
<!doctype html>
<html>
<head>
    <style>
        #container {
            height: 100px;
            width: 100px;
            background-color: black;

        }
    </style>
<script src="https://d3js.org/d3.v4.min.js"></script>
</head>
<body>
<div id="container"></div>
<script>
    d3.select("#container")
      .transition()
      .duration(1000)
      .style("background-color", "red");
</script>
</body>
</html>
```

[Live Example](https://learning-zone.github.io/d3js-interview-questions/s.transitions.html)

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the command to interpolate two objects in d3.js?

To interpolate two objects in d3.js command `d3.interpolateObject(a,b)` is used. Object interpolation is useful particularly for data space interpolation, where data is interpolated rather than attribute values.

## Q. What is the command “d3.ascending (a, b)” is used?

This command is comparator function that is used for a natural order, and can be used along with the built-in-array sort method to arrange elements in ascending order.

## Q. How XML file is called in d3.js?

By using the command `d3.xml(url[mimeType][,callback])` XML file can be called. This command will create a request for
the XML file at the specified url. If a call back is declared, the request will be immediately processed with the GET method and the call back will be invoked when the file is loaded, or request fails.

## Q. What happens if no call back is specified for XML file in d3.js?

If no call back is specified, the returned request can be issued using xhr.get and handled using xhr.on.

## Q. Mention the command to join the specified array of data in d3.js?

To join the specified array of data in d3.js you can use the command `selection.data([values[,key]])`.  The values here specifies the data for each group in the selection while a key function determines how data is connected to elements.

## Q. What does the command d3.csv.parseRows(string[,accessor]) ?

This command parses the specified string, which is the content of a CSV file, returning an array of arrays representing the parsed rows.

## Q. What is the use of “Enter” and “Exit” selection in d3.js?

By using `enter()` and `exit()` selection in d3.js, you can create new nodes for incoming data and eliminate outgoing nodes that are no longer required.

## Q. What is the best way to create the stacked barchart using d3.js?

```js
var data = [
  {"ORDER": 1, "apples": 3840, "bananas": 1920, "cherries": 960},
  {"ORDER": 2, "apples": 1600, "bananas": 1440, "cherries": 960},
  {"ORDER": 3, "apples":  640, "bananas":  960, "cherries": 640},
  {"ORDER": 4, "apples":  320, "bananas":  480, "cherries": 640}
];

var h = 200;
var w = 200;
var svg = d3.select('body').append('svg').attr('width',w).attr('height',h);
var g = svg.append('g');


var x = d3.scaleBand().rangeRound([0, w-50]);
var y = d3.scaleLinear().range([h-50, 0]).domain([0,10000]);
var color = ['#bae4bc','#7bccc4','#43a2ca'];

var stack = d3.stack()
    .keys(["apples", "bananas", "cherries"])
    .order(d3.stackOrderNone)
    .offset(d3.stackOffsetNone);
    
var series = stack(data);

x.domain(data.map(function(d) { return d.ORDER; }));

g.append("g")
    .selectAll("g")
    .data(series)
    .enter().append("g")
        .attr("fill", function(d,i) { return color[i]; })
    .selectAll("rect")
    .data(function(d) { return d; })
    .enter().append("rect")
        .attr("x", function(d) { return x(d.data.ORDER); })
        .attr("y", function(d) { return y(d[1]); })
        .attr("height", function(d) { return y(d[0]) - y(d[1]); })
        .attr("width", x.bandwidth());

```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is difference between d3.scale.linear() and d3.scaleLinear()?

**version 3: d3.scale.linear()**  
Constructs a new linear scale with the default domain [0,1] and the default range [0,1]. Thus, the default linear scale is equivalent to the identity function for numbers; for example linear(0.5) returns 0.5.

**version 4: d3.scaleLinear()**  
Constructs a new continuous scale with the unit domain [0, 1], the unit range [0, 1], the default interpolator and clamping disabled. Linear scales are a good default choice for continuous quantitative data because they preserve proportional differences. Each range value y can be expressed as a function of the domain value x: y = mx + b.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. How to set initial zoom level in d3.js?

**D3v4:**

```js
var zoom = d3.zoom().on("zoom", zooming);

vis = svg.append("svg:svg")
     .attr("width", width)
     .attr("height", height)
     .call(zoom) // here
     .call(zoom.transform, d3.zoomIdentity.translate(100, 50).scale(0.5))
     .append("svg:g")
     .attr("transform","translate(100,50) scale(.5,.5)");
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. How to resize an SVG when the window is resized in d3.js?

```css
.svg-container {
  display: inline-block;
  position: relative;
  width: 100%;
  padding-bottom: 100%; /* aspect ratio */
  vertical-align: top;
  overflow: hidden;
}
.svg-content-responsive {
  display: inline-block;
  position: absolute;
  top: 10px;
  left: 0;
}

svg .rect {
  fill: gold;
  stroke: steelblue;
  stroke-width: 5px;
}
```

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/5.7.0/d3.min.js"></script>
<div id="chartId"></div>
```

```js
d3.select("div#chartId")
   .append("div")
   // Container class to make it responsive.
   .classed("svg-container", true) 
   .append("svg")
   // Responsive SVG needs these 2 attributes and no width and height attr.
   .attr("preserveAspectRatio", "xMinYMin meet")
   .attr("viewBox", "0 0 600 400")
   // Class to make it responsive.
   .classed("svg-content-responsive", true)
   // Fill with a rectangle for visualization.
   .append("rect")
   .classed("rect", true)
   .attr("width", 600)
   .attr("height", 400);
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. How to get mouse position in d3.js?

```js
var svg = d3.select('body').append('svg')
    .attr('width', width)
    .attr('height', height)
    .on('mousemove', function() {
      console.log( d3.event.clientX, d3.event.clientY ) // log the mouse x,y position
    });
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. How to format the date in d3.js?

```js
> formatDate = d3.time.format("%b-%Y")
> formatDate(parseDate('2020-01-01'))
"Jan-2020"
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. How to calculate the area of the polygon in d3.js?

The `d3.polygonArea()` method returns the signed area of the specified polygon. If the vertices of the polygon are in counterclockwise order (assuming a coordinate system where the origin ⟨0,0⟩ is in the top-left corner), the returned area is positive; otherwise it is negative, or zero.

```js
var d = [
  [-1, 415.44],
  [146.93, 304.47],
  [195.45, 152.13],
  [-1, 134.64]
];

var area = d3.polygonArea(d);

console.log(area) // Output: 36157.2759
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. How to handle events in d3.js?

The `on()` method adds an event listener to all selected DOM elements.

Syntax

```js
d3.selection.on(type[, listener[, capture]]);
```

The first parameter is an event type as string such as "click", "mouseover" etc. The second parameter is a callback function which will be executed when an event occurs and the third optional parameter capture flag may be specified.

The following table lists important event handling method and objects.

|Event Methods	      |Description                                                                                |
|---------------------|-------------------------------------------------------------------------------------------|
|selection.on()	      |  Add or remove event listeners to capture event types like click, mouseover, mouseout etc.|
|selection.dispatch() |	Captures event types like click, mouseover, mouseout. Typenames is the eventname, listener is the event listener |
|d3.event	          | Event object to access standard event fields such as timestamp or methods like preventDefault|
|d3.mouse(container)  |Gets the x and y coordinates of the current mouse position in the specified DOM element.|
|d3.touch()	          | Gets the touch coordinates to a container|

*Example:* Event Handling

```html
<!doctype html>
<html>
<head>
    <style>
        div {
            height: 100px;
            width: 100px;
            background-color: steelblue;
            margin: 5px;
        }
    </style>
    <script src="https://d3js.org/d3.v4.min.js"></script>
</head>
<body>
<div> </div>
<script>
    d3.selectAll("div")
      .on("mouseover", function(){
          d3.select(this)
            .style("background-color", "orange");

          // Get current event info
          console.log(d3.event);

          // Get x & y co-ordinates
          console.log(d3.mouse(this));
      })
      .on("mouseout", function(){
          d3.select(this)
            .style("background-color", "steelblue")
      });
</script>
</body>
</html>
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>
