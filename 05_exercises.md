---
title: 'Weekly Exercises #5'
author: "Alison Lange"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## -- Attaching packages ------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.2     v purrr   0.3.4
## v tibble  3.0.3     v dplyr   1.0.2
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.3.1     v forcats 0.5.0
```

```
## -- Conflicts ---------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(googlesheets4) # for reading googlesheet data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.8.0, GDAL 3.0.4, PROJ 6.3.1
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(shiny)         # for creating interactive apps
gs4_deauth()           # To not have to authorize each time you knit.
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## Parsed with column specification:
## cols(
##   year = col_double(),
##   month = col_double(),
##   service = col_character(),
##   departure_station = col_character(),
##   arrival_station = col_character(),
##   journey_time_avg = col_double(),
##   total_num_trips = col_double(),
##   avg_delay_all_departing = col_double(),
##   avg_delay_all_arriving = col_double(),
##   num_late_at_departure = col_double(),
##   num_arriving_late = col_double(),
##   delay_cause = col_character(),
##   delayed_number = col_double()
## )
```

```r
# Lisa's garden data
garden_harvest <- read_sheet("https://docs.google.com/spreadsheets/d/1DekSazCzKqPS2jnGhKue7tLxRU3GVL1oxi-4bEM5IWw/edit?usp=sharing") %>% 
  mutate(date = ymd(date))
```

```
## Reading from "2020_harvest"
```

```
## Range "Sheet1"
```

```r
# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## Parsed with column specification:
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele.num = col_double(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = ""),
##   time_hr = col_double(),
##   dist_km = col_double(),
##   speed = col_double()
## )
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## Parsed with column specification:
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele = col_logical(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## Parsed with column specification:
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## Parsed with column specification:
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## Parsed with column specification:
## cols(
##   date = col_date(format = ""),
##   state = col_character(),
##   fips = col_character(),
##   cases = col_double(),
##   deaths = col_double()
## )
```

```r
#scholar strike data
firsts <- read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-06-09/firsts.csv')
```

```
## Parsed with column specification:
## cols(
##   year = col_double(),
##   accomplishment = col_character(),
##   person = col_character(),
##   gender = col_character(),
##   category = col_character()
## )
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  
  Graph from exercise 3: total harvest in pounds for each variety of tomato.

```r
tomato_harvest_graph <- garden_harvest %>%
  filter(vegetable %in% c("tomatoes")) %>%
  mutate(variety2 = fct_reorder(variety, date,
                                .desc = TRUE)) %>%
  group_by(variety2) %>% 
  summarize(tot_harvest_lbs = 
              sum(weight*0.00220462), 
            first_day_harvest = min(date)) %>%
  ggplot(aes(x = tot_harvest_lbs, y = variety2)) +
  geom_col()
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

```r
ggplotly(tomato_harvest_graph)
```

<!--html_preserve--><div id="htmlwidget-331b113059e3791b8801" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-331b113059e3791b8801">{"x":{"data":[{"orientation":"v","width":[40.19463184,22.24020656,22.87072788,14.72465698,21.95360596,52.29799564,14.9803929,14.26168678,27.86419218,30.3355712,24.07224578,15.22951496],"base":[0.55,1.55,2.55,3.55,4.55,5.55,6.55,7.55,8.55,9.55,10.55,11.55],"x":[20.09731592,11.12010328,11.43536394,7.36232849,10.97680298,26.14899782,7.49019645,7.13084339,13.93209609,15.1677856,12.03612289,7.61475748],"y":[0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999],"text":["tot_harvest_lbs: 40.19463<br />variety2: volunteers","tot_harvest_lbs: 22.24021<br />variety2: Mortgage Lifter","tot_harvest_lbs: 22.87073<br />variety2: Old German","tot_harvest_lbs: 14.72466<br />variety2: Brandywine","tot_harvest_lbs: 21.95361<br />variety2: Big Beef","tot_harvest_lbs: 52.29800<br />variety2: Amish Paste","tot_harvest_lbs: 14.98039<br />variety2: Black Krim","tot_harvest_lbs: 14.26169<br />variety2: Jet Star","tot_harvest_lbs: 27.86419<br />variety2: grape","tot_harvest_lbs: 30.33557<br />variety2: Better Boy","tot_harvest_lbs: 24.07225<br />variety2: Bonny Best","tot_harvest_lbs: 15.22951<br />variety2: Cherokee Purple"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(89,89,89,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":113.24200913242},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-2.614899782,54.912895422],"tickmode":"array","ticktext":["0","10","20","30","40","50"],"tickvals":[0,10,20,30,40,50],"categoryorder":"array","categoryarray":["0","10","20","30","40","50"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"tot_harvest_lbs","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,12.6],"tickmode":"array","ticktext":["volunteers","Mortgage Lifter","Old German","Brandywine","Big Beef","Amish Paste","Black Krim","Jet Star","grape","Better Boy","Bonny Best","Cherokee Purple"],"tickvals":[1,2,3,4,5,6,7,8,9,10,11,12],"categoryorder":"array","categoryarray":["volunteers","Mortgage Lifter","Old German","Brandywine","Big Beef","Amish Paste","Black Krim","Jet Star","grape","Better Boy","Bonny Best","Cherokee Purple"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"variety2","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"1c8c7b2efb1":{"x":{},"y":{},"type":"bar"}},"cur_data":"1c8c7b2efb1","visdat":{"1c8c7b2efb1":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
  
  Tidy tuesday #1
  

```r
firsts_in_science <- firsts%>%
  select(year, accomplishment, category, gender)%>%
  filter(category %in% c("Education & Science")) %>%
  ggplot(aes(x=year, fill=gender))+
  geom_histogram(bins=20)+
  scale_fill_manual(values = c("dodgerblue4",
                               "maroon3"))+
  theme_minimal()+
  labs(title="First African Men and Women in
       Education and Science", 
       x="Year", 
       y="Number of Firsts")+
  theme(legend.position="bottom", legend.text = 
          element_text(size=8), legend.title = 
          element_text(size=8))+
  labs(fill = "")

ggplotly(firsts_in_science)
```

<!--html_preserve--><div id="htmlwidget-d3781159693993af16e5" style="width:576px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-d3781159693993af16e5">{"x":{"data":[{"orientation":"v","width":[12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367],"base":[0,0,0,0,0,0,1,4,1,2,0,0,1,0,1,2,2,2,3,1],"x":[1778.15789473684,1790.42105263158,1802.68421052632,1814.94736842105,1827.21052631579,1839.47368421053,1851.73684210526,1864,1876.26315789474,1888.52631578947,1900.78947368421,1913.05263157895,1925.31578947368,1937.57894736842,1949.84210526316,1962.1052631579,1974.36842105263,1986.63157894737,1998.89473684211,2011.15789473684],"y":[1,0,0,1,1,1,2,3,3,3,3,2,1,0,13,13,8,5,4,3],"text":["count:  1<br />year: 1778.158<br />gender: African-American Firsts","count:  0<br />year: 1790.421<br />gender: African-American Firsts","count:  0<br />year: 1802.684<br />gender: African-American Firsts","count:  1<br />year: 1814.947<br />gender: African-American Firsts","count:  1<br />year: 1827.211<br />gender: African-American Firsts","count:  1<br />year: 1839.474<br />gender: African-American Firsts","count:  2<br />year: 1851.737<br />gender: African-American Firsts","count:  3<br />year: 1864.000<br />gender: African-American Firsts","count:  3<br />year: 1876.263<br />gender: African-American Firsts","count:  3<br />year: 1888.526<br />gender: African-American Firsts","count:  3<br />year: 1900.789<br />gender: African-American Firsts","count:  2<br />year: 1913.053<br />gender: African-American Firsts","count:  1<br />year: 1925.316<br />gender: African-American Firsts","count:  0<br />year: 1937.579<br />gender: African-American Firsts","count: 13<br />year: 1949.842<br />gender: African-American Firsts","count: 13<br />year: 1962.105<br />gender: African-American Firsts","count:  8<br />year: 1974.368<br />gender: African-American Firsts","count:  5<br />year: 1986.632<br />gender: African-American Firsts","count:  4<br />year: 1998.895<br />gender: African-American Firsts","count:  3<br />year: 2011.158<br />gender: African-American Firsts"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(16,78,139,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"African-American Firsts","legendgroup":"African-American Firsts","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367,12.2631578947367],"base":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"x":[1778.15789473684,1790.42105263158,1802.68421052632,1814.94736842105,1827.21052631579,1839.47368421053,1851.73684210526,1864,1876.26315789474,1888.52631578947,1900.78947368421,1913.05263157895,1925.31578947368,1937.57894736842,1949.84210526316,1962.1052631579,1974.36842105263,1986.63157894737,1998.89473684211,2011.15789473684],"y":[0,0,0,0,0,0,1,4,1,2,0,0,1,0,1,2,2,2,3,1],"text":["count:  0<br />year: 1778.158<br />gender: Female African American Firsts","count:  0<br />year: 1790.421<br />gender: Female African American Firsts","count:  0<br />year: 1802.684<br />gender: Female African American Firsts","count:  0<br />year: 1814.947<br />gender: Female African American Firsts","count:  0<br />year: 1827.211<br />gender: Female African American Firsts","count:  0<br />year: 1839.474<br />gender: Female African American Firsts","count:  1<br />year: 1851.737<br />gender: Female African American Firsts","count:  4<br />year: 1864.000<br />gender: Female African American Firsts","count:  1<br />year: 1876.263<br />gender: Female African American Firsts","count:  2<br />year: 1888.526<br />gender: Female African American Firsts","count:  0<br />year: 1900.789<br />gender: Female African American Firsts","count:  0<br />year: 1913.053<br />gender: Female African American Firsts","count:  1<br />year: 1925.316<br />gender: Female African American Firsts","count:  0<br />year: 1937.579<br />gender: Female African American Firsts","count:  1<br />year: 1949.842<br />gender: Female African American Firsts","count:  2<br />year: 1962.105<br />gender: Female African American Firsts","count:  2<br />year: 1974.368<br />gender: Female African American Firsts","count:  2<br />year: 1986.632<br />gender: Female African American Firsts","count:  3<br />year: 1998.895<br />gender: Female African American Firsts","count:  1<br />year: 2011.158<br />gender: Female African American Firsts"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(205,41,144,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"Female African American Firsts","legendgroup":"Female African American Firsts","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":42.3013698630137,"r":7.30593607305936,"b":38.7214611872146,"l":37.2602739726027},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"First African Men and Women in<br />       Education and Science","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1759.76315789474,2029.55263157895],"tickmode":"array","ticktext":["1800","1850","1900","1950","2000"],"tickvals":[1800,1850,1900,1950,2000],"categoryorder":"array","categoryarray":["1800","1850","1900","1950","2000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Year","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.75,15.75],"tickmode":"array","ticktext":["0","5","10","15"],"tickvals":[0,5,10,15],"categoryorder":"array","categoryarray":["0","5","10","15"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Number of Firsts","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":10.6268161062682},"y":0.952755905511811},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"1c8c154b55f1":{"x":{},"fill":{},"type":"bar"}},"cur_data":"1c8c154b55f1","visdat":{"1c8c154b55f1":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
  
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
small_train_delays <- small_trains %>%
  group_by(month, year) %>%
  summarize(tot_delays = (sum(num_late_at_departure)+
                           sum(num_arriving_late))
           /sum(total_num_trips)) %>%
  ggplot(aes(x = month, y = tot_delays)) +
  geom_col() +
  labs(title = "Percentage of Train Delays",
       x = "Month",
       y = "") +
  transition_states(year,
                    transition_length = 2, 
                    state_length = 1)
```

```
## `summarise()` regrouping output by 'month' (override with `.groups` argument)
```

```r
small_train_delays
```

```
## Warning: Removed 5 rows containing missing values (position_stack).
```

![](05_exercises_files/figure-html/unnamed-chunk-3-1.gif)<!-- -->



## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 
  

```r
tomato_daily_harvest <- garden_harvest %>%
  filter(vegetable == "tomatoes") %>% 
  group_by(variety, date) %>% 
  summarize(daily_harvest = sum(weight)*0.00220462) %>% 
  mutate(cum_harvest = cumsum(daily_harvest),
         day_of_week = wday(date, label = TRUE)) %>% 
  ungroup() %>% 
  mutate(variety = fct_reorder(variety, daily_harvest, sum, .desc = TRUE)) 
```

```
## `summarise()` regrouping output by 'variety' (override with `.groups` argument)
```

```r
  ggplot(data = tomato_daily_harvest, aes(y = variety, x = cum_harvest, fill = variety)) +
  geom_col()+
  transition_time(date)
```

![](05_exercises_files/figure-html/unnamed-chunk-5-1.gif)<!-- -->


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

  
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the x-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  
  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. Put date in the subtitle. Comment on what you see.

## Your first `shiny` app

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
