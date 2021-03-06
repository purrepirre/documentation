---
title: geom_abline| Examples | Plotly
name: geom_abline
permalink: ggplot2/geom_abline/
description: How to use the abline geom in ggplot2 to add a line with specified slope and intercept to the plot.
layout: base
thumbnail: thumbnail/ipython_graph_email.jpg
language: ggplot2
page_type: example_index
has_thumbnail: true
display_as: basic
order: 1
redirect_from: ggplot2/line-shapes/
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.


```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.5.6.9000'
```

### Line
add line for mean using <code>geom_vline</code>


```r
library(plotly)

set.seed(1234)
dat <- data.frame(cond = factor(rep(c("A","B"), each=200)),
                   rating = c(rnorm(200),rnorm(200, mean=.8)))

p <- ggplot(dat, aes(x=rating)) +
    geom_histogram(binwidth=.5, colour="black", fill="white") +
    geom_vline(aes(xintercept=mean(rating, na.rm=T)),   # Ignore NA values for mean
               color="red", linetype="dashed", size=1)

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/vline")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/3997.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Histogram
overlaid histograms with <code>geom_vline</code>


```r
library(plotly)
library(plyr)
cdat <- ddply(dat, "cond", summarise, rating.mean=mean(rating))

# Overlaid histograms with means
p <- ggplot(dat, aes(x=rating, fill=cond)) +
    geom_histogram(binwidth=.5, alpha=.5, position="identity") +
    geom_vline(data=cdat, aes(xintercept=rating.mean),
               linetype="dashed", size=1)

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/histogram-overlay")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/3999.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Histogram Means
histograms with <code>geom_vline</code> means


```r
library(plotly)
library(plyr)
cdat <- ddply(dat, "cond", summarise, rating.mean=mean(rating))

# With mean lines
p <- ggplot(dat, aes(x=rating)) + geom_histogram(binwidth=.5, colour="black", fill="white") +
    facet_grid(cond ~ .) +
    geom_vline(data=cdat, aes(xintercept=rating.mean),
               linetype="dashed", size=1, colour="red")

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/histogram-means")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4001.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Density Plots
density plots with <code>geom_vline</code> means


```r
library(plotly)
library(plyr)
cdat <- ddply(dat, "cond", summarise, rating.mean=mean(rating))

# Density plots with means
p <- ggplot(dat, aes(x=rating, colour=cond)) +
    geom_density() +
    geom_vline(data=cdat, aes(xintercept=rating.mean),
               linetype="dashed", size=1)


p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/density")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4003.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Horizontal Line
add horizontal line with <code>geom_hline</code>


```r
library(plotly)

dat <- read.table(header=TRUE, text='
      cond xval yval
   control 11.5 10.8
   control  9.3 12.9
   control  8.0  9.9
   control 11.5 10.1
   control  8.6  8.3
   control  9.9  9.5
   control  8.8  8.7
   control 11.7 10.1
   control  9.7  9.3
   control  9.8 12.0
 treatment 10.4 10.6
 treatment 12.1  8.6
 treatment 11.2 11.0
 treatment 10.0  8.8
 treatment 12.9  9.5
 treatment  9.1 10.0
 treatment 13.4  9.6
 treatment 11.6  9.8
 treatment 11.5  9.8
 treatment 12.0 10.6
')

# The basic scatterplot
p <- ggplot(dat, aes(x=xval, y=yval, colour=cond)) + 
  geom_point()

# Add a horizontal line
p <- p + geom_hline(aes(yintercept=10))

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/line-horizontal")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4005.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Mean Line
add mean line with <code>geom_hline</code>


```r
library(plotly)

dat <- read.table(header=TRUE, text='
      cond xval yval
   control 11.5 10.8
   control  9.3 12.9
   control  8.0  9.9
   control 11.5 10.1
   control  8.6  8.3
   control  9.9  9.5
   control  8.8  8.7
   control 11.7 10.1
   control  9.7  9.3
   control  9.8 12.0
 treatment 10.4 10.6
 treatment 12.1  8.6
 treatment 11.2 11.0
 treatment 10.0  8.8
 treatment 12.9  9.5
 treatment  9.1 10.0
 treatment 13.4  9.6
 treatment 11.6  9.8
 treatment 11.5  9.8
 treatment 12.0 10.6
')

# The basic scatterplot
p <- ggplot(dat, aes(x=xval, y=yval, colour=cond)) + 
  geom_point()

# Add colored lines for the mean xval of each group
p <- p + 
  geom_hline(aes(yintercept=10)) + 
  geom_line(stat="vline", xintercept="mean")
```

```
## Error: Found object is not a stat.
```

```r
p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/line-mean")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4272.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Geom_vline & Geom_hline
use <code>geom_vline</code> with <code>geom_hline</code>


```r
library(plotly)

dat <- read.table(header=TRUE, text='
      cond xval yval
   control 11.5 10.8
   control  9.3 12.9
   control  8.0  9.9
   control 11.5 10.1
   control  8.6  8.3
   control  9.9  9.5
   control  8.8  8.7
   control 11.7 10.1
   control  9.7  9.3
   control  9.8 12.0
 treatment 10.4 10.6
 treatment 12.1  8.6
 treatment 11.2 11.0
 treatment 10.0  8.8
 treatment 12.9  9.5
 treatment  9.1 10.0
 treatment 13.4  9.6
 treatment 11.6  9.8
 treatment 11.5  9.8
 treatment 12.0 10.6
')

# The basic scatterplot
p <- ggplot(dat, aes(x=xval, y=yval, colour=cond)) + geom_point()

# Add a red dashed vertical line
p <- p + geom_hline(aes(yintercept=10)) +
    geom_vline(aes(xintercept=11.5), colour="#BB0000", linetype="dashed")

p <- ggplotly(p)



# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_abline/vline-hline")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4274.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

These ggplot2 examples were inspired by <a href="http://www.cookbook-r.com/Graphs/Lines_(ggplot2)/">the Cookbook for R</a>.
