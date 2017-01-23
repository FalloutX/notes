# Introduction to Data Visualization & D3 Notes

> Based on the Udacity course of similar name. Last Updated on 16th Jan 2017.

## Intro

- **Retinal Variables** - Ordered and Nominal Values.
    - Ordered Data: Size, Orientation, Color Saturation
    - Nominal Data: Color Hue, Shape, Texture

- **Visual Encodings** - Angle, Color Hue, Color Saturation, Length, Orientation, Position x, Position y, Shape, Size, Texture.
    - Ranking (from most accurate to least accurate) [1985 Graphical Perception Paper by Cleveland and McGill ]
    ```markdown
    - Position, (Most Accurate)
    - Length,
    - Angle, Shape
    - Area,
    - Volume,
    - Color, Density(Saturation) (Least Accurate)
    ```

- [The Facebook Offering : How it Compares | NYTimes](http://www.nytimes.com/interactive/2012/05/17/business/dealbook/how-the-facebook-offering-compares.html?_r=0)

- **Exploratory Data Analysis**

    - A process where you try to discover insights into some data, find erroneous values, structure of data.
    - Its supposed to be an interaction between the Information desinger and the data.

- **Sketching**

    - Trying to determine visual encodings, layout etc.
    - Its supposed to be an Iterative process where the Information designer trying to discover how to best communicate the insights gained through Exploratory Data Analysis.

## Visualization Levels

- WebGL, Canvas, SVG - very low level (like Assembly language of visualization)
    - efficient, performant
    - highly flexible
    - low level
    - hard to develop with, high development overhead.
- D3.js - works with HTML/SVG and can be used with CSS, (like C/C++ level of visualization, mid level).
    - NVD3, Dimple.js, Richshaw - Libraries based on top of D3
        - Higher level of spectrum. (like python level of visualization)
        - Either Charting Libraries like NVD3, Dimple.js
        - Or for a specific kind of data, like Richshaw for time-series data.
    - Raw, Chartio - almost no flexibility, only a predefined set of charts.
        - higher level than NVD3 or Dimple.js, (Excel level of visualization.)

- **Visualization** in Data Science
    - Simple Solutions to solve problems.
    - Choosing the right chart for the given dataset.
    - Visual Encoding + Data Types + Relationships => Chart Type!!!
    - Data Type - Continous/Categorical?
    - Data Dimensions - 1D/2D/3D?
    - Propotions - Pie Charts.
    - Comparisions - Stacked Column Charts/Stacked Bar Graphs.

## Chart Types


- **Bar Chart** - highlights individual values, supports comparisons, and can show rankings or deviations. Its particularly good at showing comparisions in categorial data, but not very good at showing comparision in time-series data, for which line charts are better suited.
- **Boxplot** - shows distributions and quantiles, especially useful when comparing distributions
- **Pie Chart** - shows part-to-whole relationship and best suited for one category; poor for making comparisons
- **Stacked Bar Chart** - shows part-to-whole relationship and best suited for showing composition within categories and totals
- **Bubble Chart** - shows how three or more sets of values vary; shows correlation
- **Line chart** - shows overall changes and patterns, usually over equally spaced intervals of time

    - [Line Graphs and Irregular Intervals: An Incompatible Partnership by Stephen Few](http://www.perceptualedge.com/articles/visual_business_intelligence/line_graphs_and_irregular_intervals.pdf)
- **Map** - values are encoded on physical locations and patterns may be drawn by comparing locations
- **Scatterplot** - shows how two pair sets of values (for example height and shoe size) vary; shows correlation. Also, Scatterplots aren't usually used for ordered datasets such a time series
- **Tables** - Shows data where there is no encodings can be drawn/thought. Sometimes, a very raw form of data.
- **Choropleth** - Geographic representation + Color Encodings.
- **Cartogram** - Geographic representation + Size of the region.
- **Dot Map** - Geographic representaion + Any Shape Encodings.
- Other Amazing Graph types:

    - [Bullet Graph](http://www.perceptualedge.com/articles/misc/Bullet_Graph_Design_Spec.pdf)
    - [Spark Lines](https://www.edwardtufte.com/bboard/q-and-a-fetch-msg?msg_id=0001OR)
    - [Cycle Plots](http://www.perceptualedge.com/articles/guests/intro_to_cycle_plots.pdf)
    - [Connected Scatter Plots](http://www.thefunctionalart.com/2012/09/in-praise-of-connected-scatter-plots.html)
    - [Violin Plots](https://www.wikiwand.com/en/Violin_plot)
    - [Tornado Graphs](https://www.wikiwand.com/en/Tornado_diagram)
    - [Histogram](https://www.wikiwand.com/en/Histogram)
    - [How to Read Histograms](http://flowingdata.com/2014/02/27/how-to-read-histograms-and-use-them-in-r/)

## Design Principles

- **Pre-attentive Attributes**
    - Color (Hue or Saturation)
    - Form (Shape)
    - Movement
    - Spatial Position.
    - Also, the use of Negative Space.
    - [Tapping the Power of Visual Perception by Stephen Few](http://www.perceptualedge.com/articles/ie/visual_perception.pdf)
    - [Book: Information Visualization, Perception for Design by Colin Ware](https://www.amazon.com/Information-Visualization-Third-Edition-Technologies/dp/0123814642)
    - [High-Speed Visual Estimation Using Preattentive Processing](https://www.csc2.ncsu.edu/faculty/healey/download/tochi.96.pdf)

- **Negative Space or Encoding Nothingness**

    - [Snow's Cholera Map](https://upload.wikimedia.org/wikipedia/commons/2/27/Snow-cholera-map-1.jpg) - DONE
    - [Designing with White Space: Why 1+1=3](http://designforhackers.com/blog/whitespace-113/)
    - [How Google Uses White Space](http://us1.campaign-archive2.com/?u=836dc9c64862f158af8a31e20&id=fdcffdbf91)
    - [Gay rights in the US, state by state](https://www.theguardian.com/world/interactive/2012/may/08/gay-rights-united-states)

- **Color Encodings**

    - “Indeed, so difficult and subtle that avoiding catastrophe becomes the first principle in bringing color to information: Above all, do no harm.” - Tufte

    - Careful with Color - "First, get it right in black and white."
    - Try not to be redudant with Color Encodings.
    - Consider using less intense colors, medium hues and Pastels.
    - Sometimes, only sometimes, use <span style="color:orangered;">color</span> to highlight
    - [Practical Rules for Using Color in Charts by Stephen Few](http://www.perceptualedge.com/articles/visual_business_intelligence/rules_for_using_color.pdf) - DONE
        1. : If you want different objects of the same color in a table or graph to look the same, make sure that the background — the color that surrounds them — is consistent.
        2. : If you want objects in a table or graph to be easily seen, use a background color that contrasts sufficiently with the object.
        3. : Use color only when needed to serve a particular communication goal.
        4. : Use different colors only when they correspond to differences of meaning in the data.
        5. : Use soft, natural colors to display most information and bright and/or dark colors to highlight information that requires greater attention.
        6. : When using color to encode a sequential range of quantitative values, stick with a single hue (or a small set of closely related hues) and vary intensity from pale colors for low values to increasingly darker and brighter
         colors for high values
        7. : Non-data components of tables and graphs should be displayed just visibly enough to perform their role, but no more so, for excessive salience could cause them to distract attention from the data.
        8. : To guarantee that most people who are colorblind can distinguish groups of data that are color coded, avoid using a combination of red and green in the same display.
        9. : Avoid using visual effects in graphs.

    - **Sequential Palette** - A single set of ordered colors, which progresses in perceptually equal intervals.

    - **Diverging Palette** - This set consists of two sets of sequential colors—one that increases in intensity from the middle of the palette going upwards and one that increases from the middle going downwards. Also known as **dual-ordered palette.**

    - [Rainbow Color Map (Still) Considered Harmful](http://www.rkriz.net/Projects//create_color_table/color_07.pdf)

    - [Why rainbow colors aren’t the best option for data visualization](http://www.poynter.org/2013/why-rainbow-colors-arent-always-the-best-options-for-data-visualizations/224413/)

    - [Choosing colour palettes. Part I: Introduction | R Bloggers](https://www.r-bloggers.com/choosing-colour-palettes-part-i-introduction/)

    - [Choosing colour palettes. Part II: Educated Choices| R Bloggers](https://www.r-bloggers.com/choosing-colour-palettes-part-ii-educated-choices/)

    - [Improving the WSJ Historical U.S. Unemployment Rates heat map | VizWiz](http://www.vizwiz.com/2013/02/improving-wsj-historical-us.html)

    - [Color Blindness Simulator](http://www.color-blindness.com/coblis/coblis.html)

- **Gestalt Principles of Perception**

    - We organize what we see in particular ways to make sense of visual information. There are six principles that influence the ways human see and understand visuals.
        1. Proximity - Objects that are placed close to each other will often be percieved as one group.
        2. Similarity - Objects that look alike, with similar components or attributes, are more likely to be organised together.
        3. Figure and Ground - Viewers will perceive an object (figure) and a surface(ground), even if shapes are grouped together.
        4. Continuity - Objects will be grouped as a whole if they are co-linear, or follow a direction.
        5. Closure - In perception, there is a tendency to complete unfinished objects. We tend to ignore gaps and complete contour lines.
        6. Simplicity - Figures are seen as their simple elements instead of complicated shapes.
    - [The Gestalt Laws of Perception Slides](http://www.slideshare.net/luisaepv/the-gestalt-laws-of-perception) - DONE
    - [Gestalt Principles for Data Visualization](http://emeeks.github.io/gestaltdataviz/section1.html)
    - [The Gestalt Principles](http://graphicdesign.spokanefalls.edu/tutorials/process/gestaltprinciples/gestaltprinc.htm)
    - [Gestalt Design Notes](http://jimsaw.com/design/gestalt.html)

- **Chart Junk**

    - Definition: Anything that is on the chart but visually not necessary to the purpose/aim of the chart.
    - Examples: heavy or dark grid lines, unneccessary text, ornamented chart axes, pictures within graphs, shading or 3D perspective.
    - [Grid Lines in Graphs are Rarely Useful](http://www.perceptualedge.com/articles/dmreview/grid_lines.pdf)
    - Data to Ink Ratio: (Ink used to describe data)/(Ink used to describe everything else)
    - **High Data to Ink Ratio** is better.
    - Lie Factor : (Size of the effect shown in the Graphic)/(Size of the effect shown in the data.)
    - **Lie Factor** of a graphic should be between 0.95 to 1.05.
    - Size of the effect shown in the Graphic = (|2nd val - 1st val| x 100)/1st val

- **Grammar of Graphics**

    - Seprating the Information & Aesthetic Parts of a Data Viz Graphic.
    - Book: The Grammar of Graphics by Leland Wilkinson.
    - Line Charts are good for showing Trends in the data(ie like Google Trends), while tables are good for showing exact dip and heights in the graphic. Also finding a exact data point is  easier on a table.
    - 3 Key Principles:
        1. *Separation of Concerns* - Independently transform data and present data.
        2. *Definition of Common Plot/Chart Elements* - Common composable elements in every graph, e.g. Coordinate System, Scales, Text Annotations, Shapes, Data types.
        3. *Composition of those Common Elements* - for         - Categorical + Continuous x Cartesian = Bar Chart
            - Categorical + Continuous x Polar = Pie Chart
            - Continuous + Continuous x Cartesian = Scatter Chart
    - [A Layered Grammar of Graphics](http://byrneslab.net/classes/biol607/readings/wickham_layered-grammar.pdf)
    - [Introducing the Grammar of Graphics Plotting Concept](http://www.science-craft.com/2014/07/08/introducing-the-grammar-of-graphics-plotting-concept/)
    - [Grammar of Graphics for R & ggplot2](https://ramnathv.github.io/pycon2014-r/visualize/ggplot2.html)

- **Improving Visualizations Case Studies**
    - [Stephen Few Improves many poorly designed visualizations.](http://www.perceptualedge.com/examples.php)
    - [Winner of perceptualedge Dashboard Design Competition 2012](http://www.perceptualedge.com/blog/wp-content/uploads/2012/10/dashboard-competition-winner.png)
    - [Don't end up in Mistaken Data](http://flowingdata.com/category/statistics/mistaken-data/)

- **Common D3 Methods**

    - [d3.selection.append](https://github.com/mbostock/d3/wiki/Selections#append) - inserts HTML or SVG elements into a web page
    - [d3.selection.attr](https://github.com/mbostock/d3/wiki/Selections#attr) - changes a characteristic of an element such as position or fill
    - [d3.json](https://github.com/mbostock/d3/wiki/Requests#d3_json) - loads a data file and returns an array of Javascript objects
    - [d3.layout ](https://github.com/mbostock/d3/wiki/API-Reference#d3layout-layouts) - applies common transformations on predefined chart objects
    - [d3.nest](https://github.com/mbostock/d3/wiki/Arrays#d3_nest) - groups data based on particular keys and returns an array of JSON
    - [d3.scale](https://github.com/mbostock/d3/wiki/API-Reference#d3scale-scales) - converts data to a pixel or color value that can be displayed

- **4 Quadrants of Visualization**
    - [Data Visualization: Clarity or Aesthetics? 3-part Series.](http://dataremixed.com/2012/05/data-visualization-clarity-or-aesthetics/)

## Investigating Dimple.js

- Website - [dimplejs.org](http://dimplejs.org/)

- Why Dimple.js?

    1. Build atop of D3.
    2. Gentle learning curve
    3. exposes native D3 objects.

- Sketching process of a Visualization:

    1. Following an Iterative process of designing a visualization.
    2. Often not a "right answer"
    3. Don't know a priori how data will interact with the aesthetics.

- console.table() - For inspecting data in a tabular format inside the chrome JavaScript console.

    - [Advanced JavaScript Debugging with console.table()](https://blog.mariusschulz.com/2013/11/13/advanced-javascript-debugging-with-consoletable)
    - Be careful with console.data when using on a very big chunk of data.

```javascript
// Drawing a Simple Bar Chart in Dimple.js
// Updated to D3V4 version with Dimple V2.3
const margin = 75;
const width = 1400;
const height = 600;

// Select an SVG element.
var svg = dimple.newSvg("#barchart", width, height);

// Instantiate a dimple chart.
const myChart = new dimple.chart(svg, data);

// Setting boundaries of the chart using margins.
myChart.setBounds(margin, margin, width - 2 * margin, height- 2 * margin);

// Add X-Axis as a Time Axis.
const x = myChart.addTimeAxis("x", "year");

// Sort X-Axis by Date
x.addOrderRule("Date");

// Set Y-Axis as Measurment Axis.
myChart.addMeasureAxis("y", "attendance");

// Add Series Data.
myChart.addSeries(null, dimple.plot.bar);

// Draw the chart on the SVG.
myChart.draw();
```

## Narrative Structures
- FiveThirtyEight's Nate Silver discusses traditional journalism in his Essay [What the Fox knows](http://fivethirtyeight.com/features/what-the-fox-knows/), where he devides news articles into 4 quadrants based on two axes(Qualitative to Qauntative Analysis, Rigourous+Empirical to Anecdotal+Ad-hoc Analysis). For eg, Op-ed comes in Anecdotal+Ad-hoc, Qaulitative Quadrant.

  ![Approaches to Journalism: Nate Silver's 4 Quadrants](https://espnfivethirtyeight.files.wordpress.com/2014/03/538_intro4.png?quality=90&strip=all&w=575)

- **Correlation vs Causation**

    - Correlation - A and B data series are similar.
    - Causation - B data series depends on A data series and vice-versa.
    - Even if a correlation is genuine and meaningful, it does not imply a causal relationship.
    - [More Spurious Correlations](http://www.tylervigen.com/spurious-correlations)

- **Traditional Journalism vs Data Journalism**

    | Traditional Journalism                   | Data Journalism                          |
    | ---------------------------------------- | ---------------------------------------- |
    | Data around Narrative                    | Narrative around Data                    |
    | Data merely exists to Support the Narrative. | Narrative's purpose is to add context to the data. |
    | Delivery: Mostly delivered in a static form/ or even in print/physical form sometimes. | Delivery: Delivered as an interactive visualization on the open web. |

- **Misleading Visualizations**

    - "Not Starting y-axis on a bar graph with 0."
    - "High Lie Factor"
    - [Fox News continues charting excellence (not really)](http://flowingdata.com/2012/08/06/fox-news-continues-charting-excellence/)
    - [Fixing Bad Visualization Examples](http://blog.plot.ly/post/103126614582/four-unclear-graphs-about-healthcare-and)
    - [Save the Pie for Dessert](http://www.perceptualedge.com/articles/visual_business_intelligence/save_the_pies_for_dessert.pdf)
    - [Misleading With Statistics](https://medium.com/i-data/misleading-with-statistics-c63780efa928#.eee9bluif) - How journalists make arguments with distorted data.
    - [Disinformation Visualization: How to lie with datavis](https://visualisingadvocacy.org/blog/disinformation-visualization-how-lie-datavis)

- **Types of Bias in Data Visualizations**

    - Author Bias
        - As the designer/presenter of data visualizations, your design choices should establish trust between the reader and the graphic. Your design choices should facilitate communication. Otherwise as Cole mentioned, you risk the overall credibility of your message among readers.
    - Data Bias
        - Data bias arises from the process of collecting data. Systematic measurement errors or faulty devices can bias raw data values, and selection bias can lead to subgroups that are not representative of the population of interest for a given question.
    - Reader Bias
        - Reader bias encompasses any preconceived notions or assumptions that a reader brings to interpreting a visualization.

- **Types of Narrative Structures**

    - [Narrative Visualization: Telling Stories with Data](http://vis.stanford.edu/files/2010-Narrative-InfoVis.pdf)

        | Author-driven Narratives                 | Viewer-driven Narratives                 |
        | ---------------------------------------- | ---------------------------------------- |
        | Typically have well-defined start and end-points | Well-defined start point but gives Viewers freedom to progress in multiple ways. Different viewers may end up in different end-points. |
        | less exploratory elements                | higher interactions and exploratory elements. |
        | strong ordering, heavy messaging, need for clarity & speed. | Very loose ordering, more freedom to viewers to explore data, ask questions. |
        | [Example 1](http://visual.ly/visualizing-syrian-refugee-crisis?view=true) | [Road to Whitehouse](http://www.nytimes.com/interactive/2012/11/02/us/politics/paths-to-the-white-house.html) |
        | [The Facebook Offering](http://www.nytimes.com/interactive/2012/05/17/business/dealbook/how-the-facebook-offering-compares.html) | [San Francisco Crime Spotting](http://sanfrancisco.crimespotting.org/#dtstart=2017-02-14T11:41:54-07:00&zoom=11&dtend=2017-03-09T23:59:59-07:00&types=AA,Mu,Ro,SA,DP,Na,Al,Pr,Th,VT,Va,Bu,Ar&lat=37.765&hours=0-23&lon=-122.467) |

    - Martini Glass Narrative:

        - First part is more like an author-driven narrative while after the mid point it ends like viewer-driven narrative.
        - Best of both, author-driven as well as viewer-driven narratives.
        - [Gun Death in United States 2013](http://guns.periscopic.com/?year=2013)
        - [Drone Strikes](http://drones.pitchinteractive.com/)
        - TODO: Analyse Narrative Structures: https://classroom.udacity.com/courses/ud507/lessons/3069149263/concepts/30711389660923

- **Annotating Charts**
      - Use clear units, informative labels.

## D3 Joins

- [Thinking with D3 Joins](https://bost.ocks.org/mike/join/)
- Joins, (in db theory), union of two or more tables.
- [The three circles](https://bost.ocks.org/mike/circles/)
- `.enter()` - rows of data.tsv, that are not bound to any SVG/HTML elements.
- `.update()` - rows of data.tsv, that are bound to SVG/HTML elements.
- `.exit()` - SVG/HTML elements, that are not bound to any rows of data.tsv.
- [Setting Scales Domains and Ranges in d3.js](http://www.d3noob.org/2012/12/setting-scales-domains-and-ranges-in.html)
- [D3.js Axes](https://www.dashingd3js.com/d3js-axes)

## Interactivity in Data Visualizations

- [The Jobless Rate for People Like You](http://www.nytimes.com/interactive/2009/11/06/business/economy/unemployment-lines.html?_r=0)

- Add Interactivity & Animations to a static graph to move a author-driven narrative towards a martini glass narrative.

- **Creating a Map** - [Let's make a map](https://bost.ocks.org/mike/map/)

    - Acquire data: Shape files(for drawing regional boundaries etc), TopoJSON, GeoJSON
    - Shapefiles are encoded in binary, while GeoJSON is a valid JSON which is human readable and easily interpreted by JS/Browsers. GeoJSON is more verbose and bigger than a binary Shape file.
    - TopoJSON can encode Topology(adjacency and links between places), while both Shapefiles & GeoJSON can encode Topography.
    - Projection: Some object in 3-dimensions projected in a 2-dimension. Some loss in information is unavoidable in projections.
    - Mercator Projection: Stretch/Distort area near poles, Preserve  equatorial represation. (d3.geo.mercator() converts long,lat values into pixel values.)
    - [Convert to GeoJSON, Convert from GeoJSON](http://ogre.adc4gis.com/)
    - [How to convert Shapefiles to GeoJSON maps for use on GitHub (and why you should)](http://ben.balter.com/2013/06/26/how-to-convert-shapefiles-to-geojson-for-use-on-github/)
    - [GeoJSON Editor](http://geojson.io/#map=6/24.197/79.014)
    - [MapSchool.io](http://mapschool.io/)
    - [Mapschool by Tom Wright](http://www.macwright.org/2014/01/06/mapschool.html)

- **Thematic Maps** - Maps with some data that represent some topic or theme. ex, dot maps, chloropleths, and cartograms. World cup map with attendance levels is part of Graduated Symbols maps.

- **d3.nest()** - used for grouping/aggregating data etc.
    - d3.nest().key - grouping.
    - d3.nest().rollup - aggregation. (Input to rollup is a group of data elements not a single element.)
    - [D3 Nest Tutorial and examples](http://bl.ocks.org/phoebebright/raw/3176159/)

- **D3 Animations & Transitions**

    - [D3.js: animations and transitions](http://www.jeromecukier.net/blog/2012/07/16/animations-and-transitions/)
    - [Learning D3 Part 3: Animation & Interaction](http://synthesis.sbecker.net/articles/2012/07/10/learning-d3-part-3-animation-interaction)
    - [D3 and UI animations](http://blog.andreaskoller.com/2014/02/d3-and-ui-animations/)
    - [D3.js Mouse Events](http://www.stator-afm.com/tutorial/d3-js-mouse-events/)
    - [Adding tooltips to a d3.js graph](http://www.d3noob.org/2013/01/adding-tooltips-to-d3js-graph.html)
    - [Try D3 Now](http://christopheviau.com/d3_tutorial/)

- **Maps**

    - [A simple d3.js map explained](http://www.d3noob.org/2013/03/a-simple-d3js-map-explained.html)
    - [Small multiple maps using d3](http://blog.webkid.io/multiple-maps-d3/)
    - [How to Make Choropleth Maps in D3](http://www.scribblelive.com/blog/2012/02/01/how-to-make-choropleth-maps-in-d3/)
    - [average-daily-surface-air-temperature-anomalies](https://plot.ly/~etpinard/453/average-daily-surface-air-temperature-anomalies-c-in-july-2014-with-respect-to-1/)
    - [The 1000 Most Populous Canadian Cities](https://plot.ly/~MattSundquist/878/the-1000-most-populous-canadian-cities/)

- **Other Links**:

    - [False Visualizations: When Journalists Get Data Viz Wrong](http://www.huffingtonpost.com/randy-krum/false-visualizations-when_b_5736106.html)

    - [This Bubble Chart is Killing Me](http://themendozaline.org/post/95757674381/this-bubble-chart-is-killing-me)

    - [Understand JavaScript’s “this” With Clarity, and Master It](http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/)

    - [Some of 'this'](http://tomhicks.github.io/code/2014/08/11/some-of-this.html)

    - [basemap Python Package](https://pypi.python.org/pypi/basemap/1.0.7)

    - [R 'maps' package](https://cran.r-project.org/web/packages/maps/maps.pdf)

    ​

## Learning Resources

- [Book: Interactive Data Visualization for the Web by Scott Murray](http://chimera.labs.oreilly.com/books/1230000000345)
- [Book: Pocket Guide to Writing SVG](http://svgpocketguide.com/book/)
- [D3 API Reference(v3 version)](https://github.com/d3/d3-3.x-api-reference/blob/master/API-Reference.md)
- [D3 Tutorials Page](https://github.com/d3/d3/wiki/Tutorials)
- [Dimple.js](http://dimplejs.org/index.html)
- [Tributary - experimental environment for rapidly prototyping visualization code](http://tributary.io/)
- [An SVG Primer for Today's Browsers](https://www.w3.org/Graphics/SVG/IG/resources/svgprimer.html)
- [Dashing d3 Tutorial](https://www.dashingd3js.com/table-of-contents)
- [Blog: Flowing Data](http://flowingdata.com/)
- [Blog: The Functional Art by Alberto Cairo](http://www.thefunctionalart.com/)
- [Site: Visualizing Data ](http://www.visualisingdata.com/)
- [Blog: Mike Bostocks](https://bost.ocks.org/mike/)
- [Blog: Story Telling with Data](http://www.storytellingwithdata.com/)
- [Blog: Cartastrophe DataViz Blog](https://cartastrophe.wordpress.com/)
- [Book: Online Stats Book](http://onlinestatbook.com/2/index.html)
- [Book: Data Journalism Handbook](http://datajournalismhandbook.org/1.0/en/index.html)
- [Visual Encoding](https://www.targetprocess.com/articles/visual-encoding/)
- [Graphical perception – learn the fundamentals first](http://flowingdata.com/2010/03/20/graphical-perception-learn-the-fundamentals-first/)
- [Paper: A Tour though Visualization Zoo](http://queue.acm.org/detail.cfm?id=1805128)
- [Chart Chooser in Color](https://apandre.files.wordpress.com/2011/02/chartchooserincolor.jpg)
- [Cole Nussbaumer on the Chart Chooser](http://www.storytellingwithdata.com/blog/2013/04/chart-chooser)
- [Interactive Chart Chooser](http://labs.juiceanalytics.com/chartchooser/index.html)
- [Designing Effective Tables and Graphs by Stephen Few](http://www.perceptualedge.com/images/Effective_Chart_Design.pdf)
- [Selecting the Right Graph for Your Message by Stephen Few](http://www.perceptualedge.com/articles/ie/the_right_graph.pdf)
- [Three charts are all I need](https://signalvnoise.com/posts/3388-three-charts-are-all-i-need)
- [When to use Grouped vs. Stacked Column Charts](http://www.scribblelive.com/blog/2012/08/27/how-groups-stack-up-when-to-use-grouped-vs-stacked-column-charts/)
- [How to Visualize and Compare Distributions](http://flowingdata.com/2012/05/15/how-to-visualize-and-compare-distributions/)
- [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
