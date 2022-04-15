# plotly.java
Plotly.java is a third-party Java wrapper for the [Plotly JavaScript open source graphing library](https://plotly.com/javascript/), one of the finest graphing libraries available.  plotly.java lets you generate a wide range of JavaScript/HTML charts.  Please note that Plot.ly (the company) did not develop and does not support plotly.java (the library) in any way, other than to create the beautiful library that we use.  

### Where plotly.java came from

Plotly.java was developed as part of the [Tablesaw Java dataframe library](https://github.com/jtablesaw/tablesaw). Work began in 2018, with the goal of creating a tool for exploratory data analysis in Java that would complement the dataframe itself. It has been used since then in numerous projects. 

Dependencies on Tablesaw have  been removed to make it easier to incorporate visualizations into a broad range of Java applications, but it remains a key part of the Tablesaw data wrangling solution. If you need to plot data from a CSV, Excel file, database, JSON, etc., we strongly recommend you take a look at [Tablesaw](https://github.com/jtablesaw/tablesaw) for data ingestion and transformation support. 

## Plots created with plotly.java

Here are some examples of plots that were created using plotly.java. 


| ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/box1.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/scatter_2_Yaxes.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/tornado.scatter.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/bush_time_series2.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/hist_overlay.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/histogram2.png) |
| ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/histogram2d.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/pie.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/wine_bubble_3d.png) |
| ![](https://jtablesaw.github.io/tablesaw/userguide/images/eda/wine_bubble_with_groups.png) | ![](https://jtablesaw.github.io/tablesaw/userguide/images/eda/robberies_area.png) | ![](https://jtablesaw.github.io/tablesaw/userguide/images/ml/regression/wins%20by%20year.png) |
| ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/bush_heatmap1.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/tornado_bar_groups.png) | ![Tornadoes](https://jtablesaw.github.io/tablesaw/userguide/images/eda/ohlc1.png) |

## An Example:

Here's a simple example that creates an Area Plot. Two data arrays are used to specify the x and y coordinates. 

```java
package tech.tablesaw.examples;

import tech.tablesaw.plotly.Plot;
import tech.tablesaw.plotly.components.Figure;
import tech.tablesaw.plotly.components.Layout;
import tech.tablesaw.plotly.traces.ScatterTrace;

public class AreaPlotExample {

  /** Creates a simple area plot with an index (observation number) x axis */
  public static void main(String[] args) throws Exception {

    String title = "Boston Robberies: 1966-1967";
    double[] observation = {1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0};
    double[] count = {41.0, 39.0, 50.0, 40.0, 43.0, 38.0, 44.0, 35.0, 39.0, 35.0, 29.0, 49.0};

    Layout layout = Layout.builder(title, "Month", "Robberies").build();
    ScatterTrace trace =
            ScatterTrace.builder(observation, count)
                    .mode(ScatterTrace.Mode.LINE)
                    .fill(ScatterTrace.Fill.TO_NEXT_Y)
                    .fillColor("#b987fb")
                    .build();
    Figure figure = new Figure(layout, trace).
    Plot.show(figure);
  }
}
```

As you can see, plotly.java has a builder API, that lets you configure each plot exactly as you want, while retaining Java's type safety. 

A complete plot in Plot.ly is called a Figure. It can have several elements, the most important of which are layouts and traces.

- Layout: Defines the key attributes that determine the appearance of the overall plot, like it's title and it's height and width (if you don't want a responsive plot).
- Trace: Defines the attributes that determine the appearance of a single data series. A line plot for example, may have two traces, where one represents the GDP of Germany, and the other the GDP of France. Similarly, if you want to overlay two histograms on the same plot, each Histogram will be it's own trace. 

Two other elements of Figures are Configs and Events. You can learn about those in the Plot.ly documentation (see below).  From here on, we will use the term plot and figure interchangeably to refer to a single figure. Note, however, that plotly allows you to combine figures in various ways.

## How plots are rendered:

Since Plotly is a JavaScript library, rendering is ultimately handled by a browser. There are several ways:

- Embed a figure in a static web page.
- Send a figure to a browser from a Web app.
- Render a figure in your desktop's default browser from your IDE. 
- Render a figure in a Jupyter Notebook

Each of these is described below. 

#### Embed a plot in a static Web page

To embed a figure in a static web page, you need to get the JavaScript code from your Figure object. Simply construct a figure as show above, get the JavaScript by calling 

````java
String s = figure.asJavascript(); 
````

You can print the contents of s to your console and paste it into your Web page.

#### Send a plot dynamically from a Web app

The details of this will vary depending on which Web framework you use, but the approach is similar to the static approach shown above. You construct the plot in Java, get the JavaScript for the figure by calling 

#### Render a plot in your desktop's default browser

This method is best if you're looking at data interactively in your IDE.  The Plot class used on the last line in the example above shows how. Plot is simply a helper class with several methods called *show()* that write out an HTML file to your local disk, finds your default browser, and tells it to open that HTML page in a new browser tab.  As shown above, the simplest version is 

````java
    Plot.show(figure));
````

See the Plot class for more information on the other varieties.

#### Render a plot in a Jupyter Notebook

There are several ways to use plotly.java in a Jupyter Notebook using one of several Java kernals for Jupyter. Examples for using the older Tablesaw version plotly.java are show on the Tablesaw page. 

- Using the Beaker kernal:
- Using 

## To get started:

Add tablesaw-plotly-java to your project. You can find the version number for the latest release in the [release notes](https://github.com/jtablesaw/tablesaw/releases):


```xml
<dependency>
    <groupId>tech.tablesaw</groupId>
    <artifactId>tablesaw-plotly-java</artifactId>
    <version>VERSION_NUMBER_GOES_HERE</version>
</dependency>
```

## Documentation

The best source of documentation is the Plotly.js library documentation as everything in plotly.java exists solely to generate and render plotly.js code. 

- Examples of many chart types can be found here: https://plotly.com/javascript/. 

- Plotly's figure reference can be found here. https://plotly.com/javascript/reference/index/
- The single-page reference is very useful if you want the details of some plotly component, like an axis, marker, or tick mark.https://plotly.com/javascript/reference/

## License

Plotly.java is free and open source software made available under the [Apache 2 license](https://github.com/jtablesaw/plotly.java/blob/main/LICENSE).

Ploty.js (a required dependency) is licensed under the [MIT license](https://github.com/plotly/plotly.js/blob/master/LICENSE?msclkid=12fac668bcc811ec8739b3ef585e204c).

## If you need help

#### To ask questions:

The best way to ask questions is to use the [Github Discussions](https://github.com/jtablesaw/plotly.java/discussions) feature. 

You are also welcome to try Stack Overflow as well. If you use Stack Overflow, please tag your question with **plotly.java** so we're more likely to see it. 

#### To report an issue or request an enhancement:

Please create an issue [here](https://github.com/jtablesaw/plotly.java/issues). 

## How to contribute

There are SO many ways to contribute. 

**To contribute code**: please see the open issues for any bugs and a list of desired enhancements. We always want to support more plot types. If you are interested in contributing regularly, let us know. We are always looking for additional maintainers.

**To help spread the word:** Let people know about plotly.java through your blog, through twitter, YouTube, Instagram or whatever. If you create a tutorial or some nice examples let us know and we will link from this page. We **LOVE** people who post examples.

If you create any nice plots, please share them in the [Discussions section](https://github.com/jtablesaw/plotly.java/discussions), and tag the with the "Show and Tell" category. 

**To contribute financially**: Please click the support link. If you're working at a company or non-profit that needs additional support, let us know in the Discussions feature. 
