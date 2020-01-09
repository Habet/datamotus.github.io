---
layout: post
mathjax: true
title:  Changes in air pollution
excerpt: It is hard to eliminate the health effects of the toxic contaminators on health. Air pollutants can be the cause of death from stroke, lung cancer, childhood cancer, and another heart disease. Apart from affecting our health, a decrease in the level of air quality is causing long-term environmental damage by driving climate change, which is itself a danger for people and their health. In the article, changes in the quality of air are detected using historical data of four types of air pollutants: carbon dioxide, sulphur dioxide, particulate matter and concentration of ozone in the air. 
keywords: air quality, air pollutants, world map, changes
---


Introduction
------------

Even without visible smog, air pollution is all around us, and thus it
is hard to eliminate the health effects of the toxic contaminators on
health. The harmful effect of air pollutants is widely investigated in
different researches conducted in many regions of the world. Air
pollutants can be the cause of death from stroke, lung cancer, and
another heart disease. Air pollution has a pernicious effect on children
and it trigger childhood cancer. All over the world, up to 14% of 5 --
18 years-old children have asthma relating to factors including air
pollution (see [World Health
Organisation](https://www.who.int/airpollution/news-and-events/how-air-pollution-is-destroying-our-health)
for details). Besides, air pollution drives **climate change** (the main
driver of climate change is fossil fuel combustion), which itself can be
the problem for well-being.

An assessment by WHO concluded that, in 2016, 91% of the world
population was living in places where the WHO air quality guidelines
levels were not met. In order to protect public health, WHO created air
quality standards, which suggest limits for four main air pollutants.
According to [WHO Air quality
guidelines](https://apps.who.int/iris/bitstream/handle/10665/69477/WHO_SDE_PHE_OEH_06.02_eng.pdf?sequence=1)
estimates, air pollution is the cause of 3 million deaths per year. The
evaluation of WHO shows, that the death caused by air pollution can be
decreased by around 15% as a result of reduction in particulate matter
(PM10) pollution from 70 to 20 micrograms per cubic meter.

Many countries fail to monitor pollutant concentrations in the air.
However, now a combination of satellite data, air transport models and
local meteorological conditions can provide a good evaluation of air
quality. Outdoor air pollution can be defined as the emission of harmful
substances into the atmosphere. This broad definition, encapsulates a
number of pollutants, including:

-   sulphur dioxide ($SO_2$),
-   nitrogen oxides ($NO_x$),
-   ozone ($O_3$),
-   particulate matter,
-   carbon monoxide ($CO$)
-   carbon dioxide ($CO_2$)
-   and volatile organic compounds ($VOC_s$).

Data description
================

We took the historical data of emissions of the following four types of
pollutants: [carbon
dioxide](https://ourworldindata.org/co2-and-other-greenhouse-gas-emissions),
[sulphur
dioxide](https://ourworldindata.org/grapher/so-emissions-per-capita-tonnes-per-year)
per person, [particulate
matter](https://ourworldindata.org/air-pollution) measuring less than
2.5µm (micrometers) in diameter,
[ozone](https://ourworldindata.org/grapher/ozone-o3-concentration-in-ppb?country=CHN+JPN+SAU+SWE+USA+ZWE)
based on territorial emissions derived by [Our World in
Data](https://ourworldindata.org/).

``` {.r}
# load the required libraries used in the article
if (!require("pacman")) install.packages("pacman")
pacman::p_load(ggplot2, dplyr, kableExtra, tidyverse, magrittr, ggmap, ggpubr, stringr, RColorBrewer, reshape2)
```

The variables `Entity` and `Code` show the country and/ or area and its
code, where the level of a particular pollutant was measured.

### Carbon dioxide (CO2)

``` {.r}
co <- read.csv("co.csv")
range(unique(co$Year))
```

    ## [1] 1800 2017

The number of observations in the initial data is 16739 and the covered
time span is 1800-2017. Data contains 194 countries.

The variable `Co2` shows the tonnes of measured carbon dioxide data has
been converted from tonnes of carbon to tonnes of carbon dioxide
($CO_2$) using a conversion factor of 3.664). Carbon Dioxide commonly
enters the body through breathing indoor and outdoor air, vehicle
exhaust, and fumes from heating or cooking and via skin contact -
touching dry ice. Carbon dioxide can cause suffocation, incapacitation
and unconsciousness, vertigo and double vision, headaches, inability to
concentrate, tinnitus and seizures. The long-term exposure of $CO_2$ can
cause changes in bone calcium and body metabolism. When levels of CO2
rise and there is less fresh air, it [can
cause](https://www.airthings.com/es/what-is-carbon-dioxide)
restlessness, drowsiness and more. High levels are directly correlated
to low productivity, high sick leave and infectious disease
transmission.

The acceptable level of $CO_2$ in the air is 400ppm (ppm is parts per
million). The level of 2000ppm can cause symptoms like sweating,
increased heart rate and difficulty during breathing will occur.

The summary of carbon dioxide emissions is represented below:

``` {.r}
summary(co$Co2)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   0.000   0.201   1.071   3.555   4.503 252.645

### Sulphur dioxide (SO2)

``` {.r}
so <- read.csv("so.csv")
```

The number of observations in the initial data is 2079 and the covered
time span is 1850-2000 (represented by decades). Data contains 130
countries.

``` {.r}
range(unique(so$Year))
```

    ## [1] 1850 2000

The variable `So2` shows the tonnes of measured emissions per capita
(1850-2000). One of the main causes of $SO_2$ emissions is the use of
coal as a source of energy. $SO_2$ emissions sharply rise after
industrialisation: the increase in emission is as a result of
large-scale burning of sulphur-containing fuels and industrial
processing.

Sulfure dioxide can be the cause of health problems like asthma,
bronchial symptoms, lung inflammation, reduced lung function and causes
irritation of the eyes. Sulfuric acid (combination of $SO2$ and water)
is the main component of acid rain which is the cause of deforestation.
The guideline values for sulfure dioxide is 20 $\frac{mg}{m^3}$ 24-hour
mean.

The summary of sulphur dioxide emissions is represented below:

``` {.r}
summary(so$So2)
```

    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ## 0.0000167 0.0002001 0.0015000 0.0178443 0.0162977 0.4250609

### Particulate matter (PM)

``` {.r}
pm <- read.csv("pm.csv")
```

The number of observations in the initial data is 2090 and the covered
time span is 1990-2016 (the frequency of the data is not regular). Data
contains 189 countries.

``` {.r}
range(unique(pm$Year))
```

    ## [1] 1990 2016

The variable `PM` shows the average level of exposure of a nation's
population to concentrations of suspended particles measuring less than
2.5 microns in aerodynamic diameter. The calculations had been done by
using weighting mean annual concentrations of PM2.5 by population.
Actually, one of the most harmful air pollutant is a particulate matter,
which is capable of penetrating deep into the respiratory tract and
increases the risk of heart, respiratory diseases and lung cancer. This
pollutant can originate from natural or man-made sources, mainly from
fuel combustion and road traffic. According to the WHO Air Quality
Guideline the limits for PM is 10 $\frac{mg}{m^3}$ annual mean.

The summary of this variable is represented below:

``` {.r}
summary(pm$PM)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   3.291  15.199  21.950  30.160  37.624 203.744

### Ozone (O3)

``` {.r}
oz <- read.csv("oz.csv")
```

The number of observations in the initial data is 1316 and the covered
time span is 1990-2015 (the frequency of the data is not regular). Data
contains 188 countries.

``` {.r}
range(unique(oz$Year))
```

    ## [1] 1990 2015

The variable `OZ` shows population-weighted ozone ($O_3$) concentration
by country (1990-2015) in parts per billion (ppb). As source states,
data is gathered based on a combination of air quality observations from
satellites combined with information from global chemical transport
models, and available ground measurements. A global chemical transport
model was used to calculate a seasonal (summer, when temperatures are
highest) average concentration. Taking into account the population in
each block within a country, this data is then aggregated as estimated
exposure concentrations to national-level population-weighted averages
for a given year.

Ozone is can be the cause of asthma or the cause of making it worse.
Ozone is mainly caused by the reaction of sunlight with pollutants from
vehicle emissions. Ozone is major constituents of photochemical smog.
The highest levels of ozone pollution occur during periods of sunny
weather. According to the WHO Air Quality Guideline the limits for ozone
is 100 $\frac{mg}{m^3}$ 8-hour mean.

The summary of the level of ozone concentration is represented below:

``` {.r}
summary(oz$OZ)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    5.00   45.00   54.00   54.55   63.00  116.00

Categorization/Grouping
-----------------------

In order to see the changes in air pollution worldwide, let us
categorize pollutants, by using unequal-size groups. As in the equal
categorization groups with extreme values contain only a few
observations, the extremal values are included in the same group (the
last or the first). See the code below for grouping four above-mentioned
pollutant types; the new variable `group` for each data will be created.

``` {.r}
# Creating groups
co$group <- cut(co$Co2, breaks = c(0, 1.5, 3, 6, 12.5, 25, 37.5, max(co$Co2)))
so$group <- cut(so$So2, breaks = c(0, 0.001, 0.017, 0.034, 0.07, 0.2, max(so$So2)))
pm$group <- cut(pm$PM, breaks = c(min(pm$PM), 12, 24, 44.7, 65.4, 86.1, max(pm$PM)))
oz$group <- cut(oz$OZ, breaks = c(min(oz$OZ), 34.9, 45.7, 56.6, 67.4, 78.3, max(oz$OZ)))
gr <- data.frame(table(co$group), rbind(data.frame(table(so$group)), c(NA, NA)), 
  rbind(data.frame(table(pm$group)), c(NA, NA)), rbind(data.frame(table(oz$group)), c(NA, NA)))
colnames(gr) <- c("CO2", "Freq CO2", "SO2", "Freq SO2", "PM", "Freq PM", "OZ", "Freq OZ")
options(knitr.kable.NA = "")
knitr::kable(gr, digits = 2) %>% kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
CO2
</th>
<th style="text-align:right;">
Freq CO2
</th>
<th style="text-align:left;">
SO2
</th>
<th style="text-align:right;">
Freq SO2
</th>
<th style="text-align:left;">
PM
</th>
<th style="text-align:right;">
Freq PM
</th>
<th style="text-align:left;">
OZ
</th>
<th style="text-align:right;">
Freq OZ
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:right;">
8936
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:right;">
970
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:right;">
330
</td>
<td style="text-align:left;">
(5,34.9\]
</td>
<td style="text-align:right;">
67
</td>
</tr>
<tr>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:right;">
1970
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:right;">
598
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:right;">
803
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
<td style="text-align:right;">
276
</td>
</tr>
<tr>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:right;">
2106
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:right;">
186
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:right;">
527
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:right;">
377
</td>
</tr>
<tr>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:right;">
2365
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:right;">
176
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:right;">
265
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:right;">
391
</td>
</tr>
<tr>
<td style="text-align:left;">
(12.5,25\]
</td>
<td style="text-align:right;">
698
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:right;">
128
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:right;">
93
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:right;">
161
</td>
</tr>
<tr>
<td style="text-align:left;">
(25,37.5\]
</td>
<td style="text-align:right;">
146
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
<td style="text-align:right;">
71
</td>
<td style="text-align:left;">
(78.3,116\]
</td>
<td style="text-align:right;">
41
</td>
</tr>
<tr>
<td style="text-align:left;">
(37.5,253\]
</td>
<td style="text-align:right;">
94
</td>
<td style="text-align:left;">
</td>
<td style="text-align:right;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:right;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:right;">
</td>
</tr>
</tbody>
</table>

Maps
----

When the groups are created, the results can be shown using the world
map. We are going to use the function `map_data()` which contains the
data to create a world map.

``` {.r}
map.world <- map_data("world")
```

### Co2

In order to use the information from the built-in data (especially data
about the longitude and latitude of locations to plot countries as
polygons) the names of countries must be exactly the same, thus the
names in our data should be changed. As there were dissimilarities
between country names in the data world and our data, the changes had
been inspected. The code below shows the difference between country
names in both data. As data is cleaned, there is no difference between
the countries names. The detection of dissimilarities for further 3 data
will be done in the same way.

``` {.r}
# Detect dissimilarities
unique(na.omit(co$Entity))[c(which(!unique(na.omit(co$Entity)) %in% unique(na.omit(map.world$region))))]
```

    ## factor(0)
    ## 193 Levels: Afghanistan Albania Algeria Andorra Angola ... Zimbabwe

Then, these two separate datasets should be joined together.

``` {.r}
map.world_joined <- left_join(co, map.world, by = c('Entity'='region'))
```

Now, we are going to plot the changes in the data. The reference year
for Co2 is chosen as 2011. In the remaining three plots only the
countries with changes are shown (with respect to the base year).

``` {.r}
themeplot <- theme(text = element_text(family = "Gill Sans", size = 8), legend.key.size = unit(0.5, 
    "lines"), panel.grid = element_blank(), plot.title = element_text(size = 30), 
    plot.subtitle = element_text(size = 10), axis.text = element_blank(), axis.title = element_blank(), 
    axis.ticks = element_blank(), legend.position = c(0, 0), legend.justification = c(0, 
        0), legend.title = element_blank())
finalplot <- function(base = 2011, current = 2014, var = Co2, data = map.world_joined, 
    initialdata = co) {
    var = enquo(var)
    
    if (base == current) {
        data %>% filter(!is.na(!!var)) %>% filter(Year == base) %>% ggplot() + geom_polygon(aes(x = long, 
            y = lat, group = group.y, fill = group.x)) + scale_fill_brewer(palette = "Set1") + 
            themeplot + labs(subtitle = paste(base)) + geom_path(color = "black", 
            aes(x = long, y = lat, group = group.y))
        
    } else {
        
        save <- initialdata %>% filter(Year == base | Year == current) %>% filter(Entity == 
            lag(Entity), group != lag(group)) %>% left_join(., map.world, by = c(Entity = "region"))
        save %>% ggplot() + geom_polygon(data = map.world, aes(x = long, y = lat, 
            group = group), fill = "gray81") + geom_polygon(aes(x = long, y = lat, 
            group = group.y, fill = group.x)) + scale_fill_manual(values = brewer.pal(n = 7, 
            name = "Set1")[as.numeric(sort(unique(save %>% select(group.x) %>% pull())))]) + 
            themeplot + labs(subtitle = paste(current)) + geom_path(color = "black", 
            aes(x = long, y = lat, group = group.y))
    }
}
```

To see the changes in two directions (increase *or* decrease), we need
to create functions that extract from the initial data the name of the
country which experienced increase or decrease, the year of change and
the group:

``` {.r}
returndataup <- function(data, base, current) {
    
    data %>% filter(Year == base | Year == current) %>% 
    filter(Entity == lag(Entity), as.numeric(group) > as.numeric(lag(group))) %>% 
    left_join(., map.world, by = c(Entity = "region")) %>% 
    distinct(Entity, .keep_all = TRUE) %>% select(Entity, Year, group.x)
}
returndatadown <- function(data, base, current) {
    
    data %>% filter(Year == base | Year == current) %>% 
    filter(Entity == lag(Entity), as.numeric(group) < as.numeric(lag(group))) %>% 
    left_join(., map.world, by = c(Entity = "region")) %>% 
    distinct(Entity, .keep_all = TRUE) %>% select(Entity, Year, group.x)
}
```

And, finally, using the function above the changes can be detected on
the created map:

``` {.r}
annotate_figure(ggarrange(finalplot(2011, 2011), finalplot(2011, 2013), 
  finalplot(2011, 2015), finalplot(2011, 2017), ncol = 2, nrow = 2, common.legend = F),
  top = text_grob("Carbon dioxide emissions in 2011, 2013, 2015 and 2017", 
  face = "bold", size = 12))
```

![](2020-01-09-Changes-in-air-pollution_files/figure-markdown/cogr-1.png)

Countries that experienced an increase in the level of carbon dioxide
emissions:

``` {.r}
coup <- rbind(co%>%select(Entity, Year, group)%>%filter(Year == 2011)%>%
  rename(group.x = group), returndataup(co, 2011, 2013),
  returndataup(co, 2011, 2015),
  returndataup(co, 2011, 2017))%>%
  arrange(Entity)%>% rename(Group = group.x) 
options(knitr.kable.NA = '')
knitr::kable(dcast(coup%>%filter(Entity %in% names(which(table(coup$Entity) > 1))), Entity~Year))%>% 
kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
2011
</th>
<th style="text-align:left;">
2013
</th>
<th style="text-align:left;">
2015
</th>
<th style="text-align:left;">
2017
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Andorra
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bahamas
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Botswana
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
India
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Kyrgyzstan
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Maldives
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Mongolia
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(12.5,25\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Namibia
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Palau
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12.5,25\]
</td>
<td style="text-align:left;">
(12.5,25\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Seychelles
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Turkmenistan
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12.5,25\]
</td>
<td style="text-align:left;">
(12.5,25\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Venezuela
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
</tbody>
</table>

Countries that experienced a decrease in the level of carbon dioxide
emissions:

``` {.r}
codown <- rbind(co%>%select(Entity, Year, group)%>%filter(Year == 2011)%>%
  rename(group.x = group), returndatadown(co, 2011, 2013),
  returndatadown(co, 2011, 2015),
  returndatadown(co, 2011, 2017))%>%
  arrange(Entity)%>% rename(Group = group.x)
options(knitr.kable.NA = '')
knitr::kable(dcast(codown%>%filter(Entity %in% names(which(table(codown$Entity) > 1))), Entity~Year))%>% 
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
2011
</th>
<th style="text-align:left;">
2013
</th>
<th style="text-align:left;">
2015
</th>
<th style="text-align:left;">
2017
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Belize
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bulgaria
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Cyprus
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Equatorial Guinea
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Estonia
</td>
<td style="text-align:left;">
(12.5,25\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Italy
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Malta
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
North Korea
</td>
<td style="text-align:left;">
(1.5,3\]
</td>
<td style="text-align:left;">
(0,1.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Qatar
</td>
<td style="text-align:left;">
(37.5,253\]
</td>
<td style="text-align:left;">
(25,37.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Spain
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Ukraine
</td>
<td style="text-align:left;">
(6,12.5\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(3,6\]
</td>
<td style="text-align:left;">
(3,6\]
</td>
</tr>
</tbody>
</table>

### SO2

To see the changes onthe map the data for sulphur dioxide is created:

``` {.r}
map.world_joined2 <- left_join(so, map.world, by = c('Entity'='region' ))
```

``` {.r}
annotate_figure(ggarrange(finalplot(1970, 1970, So2, map.world_joined2, so), 
  finalplot(1970, 1980, So2, map.world_joined2, so), finalplot(1970, 1990, So2, map.world_joined2, 
  so), finalplot(1970, 2000, So2, map.world_joined2, so), ncol = 2, nrow = 2, common.legend = F),
  top = text_grob("Sulphur dioxide emissions in 1970, 1980, 1990 and 2000", 
  face = "bold", size = 12))
```

![](2020-01-09-Changes-in-air-pollution_files/figure-markdown/sogr-1.png)

Countries that experienced an increase in the level of sulfur dioxide
emissions:

``` {.r}
soup <- rbind(so %>% select(Entity, Year, group) %>% filter(Year == 1970) %>% 
    rename(group.x = group), returndataup(so, 1970, 1980), returndataup(so, 1970, 1990),
    returndataup(so, 1970, 2000)) %>% arrange(Entity) %>% rename(Group = group.x)
options(knitr.kable.NA = "")
knitr::kable(dcast(soup %>% filter(Entity %in% names(which(table(soup$Entity) > 1))), Entity ~ Year)) %>%
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
1970
</th>
<th style="text-align:left;">
1980
</th>
<th style="text-align:left;">
1990
</th>
<th style="text-align:left;">
2000
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Azerbaijan
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Bahrain
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Benin
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bosnia and Herzegovina
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Botswana
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Brunei
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bulgaria
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Cameroon
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
China
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Croatia
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Eritrea
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Estonia
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Gabon
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Greece
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Haiti
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Iceland
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Indonesia
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Iraq
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Israel
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Jamaica
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Lebanon
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Lithuania
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Macedonia
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Malta
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Moldova
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Mongolia
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Namibia
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Nepal
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
North Korea
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Oman
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Panama
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Portugal
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Republic of Congo
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Russia
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Saudi Arabia
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Singapore
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
South Korea
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Spain
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Syria
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Trinidad
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Tunisia
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Turkey
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Turkmenistan
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
United Arab Emirates
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Yemen
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
</tbody>
</table>

Countries that experienced a decrease in the level of sulfur dioxide
emissions:

``` {.r}
soup <- rbind(so %>% select(Entity, Year, group) %>% filter(Year == 1970) %>% 
    rename(group.x = group), returndataup(so, 1970, 1980), returndataup(so, 1970, 1990),
    returndataup(so, 1970, 2000)) %>% arrange(Entity) %>% rename(Group = group.x)
options(knitr.kable.NA = "")
knitr::kable(dcast(soup %>% filter(Entity %in% names(which(table(soup$Entity) > 1))), Entity ~ Year)) %>% 
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
1970
</th>
<th style="text-align:left;">
1980
</th>
<th style="text-align:left;">
1990
</th>
<th style="text-align:left;">
2000
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Azerbaijan
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Bahrain
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Benin
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bosnia and Herzegovina
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Botswana
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Brunei
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bulgaria
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Cameroon
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
China
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Croatia
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Eritrea
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Estonia
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.2,0.425\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Gabon
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Greece
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Haiti
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Iceland
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Indonesia
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Iraq
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Israel
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Jamaica
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Lebanon
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Lithuania
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Macedonia
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Malta
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Moldova
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Mongolia
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Namibia
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Nepal
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
North Korea
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Oman
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Panama
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Portugal
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Republic of Congo
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Russia
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Saudi Arabia
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Singapore
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
</tr>
<tr>
<td style="text-align:left;">
South Korea
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Spain
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Syria
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Trinidad
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Tunisia
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Turkey
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Turkmenistan
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
United Arab Emirates
</td>
<td style="text-align:left;">
(0.034,0.07\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
(0.07,0.2\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Yemen
</td>
<td style="text-align:left;">
(0,0.001\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.001,0.017\]
</td>
<td style="text-align:left;">
(0.017,0.034\]
</td>
</tr>
</tbody>
</table>

### PM

To see the changes on the map the data for particulate matter is
created:

``` {.r}
map.world_joined3 <- left_join(pm, map.world, by = c('Entity'='region'))
```

``` {.r}
annotate_figure(ggarrange(finalplot(2010,2010, PM, map.world_joined3, pm),
  finalplot(2010,2012, PM, map.world_joined3, pm), finalplot(2010,2014, PM, map.world_joined3, pm),
  finalplot(2010,2016, PM, map.world_joined3, pm), ncol = 2, nrow = 2, common.legend = F),
  top = text_grob("Particulate matter esmissions in 2010, 2012, 2014, 2016", face = "bold", size = 12))
```

![](2020-01-09-Changes-in-air-pollution_files/figure-markdown/pmgr-1.png)

The main changes of particulate matter concentration refer to African
countries. In the table below, the groups of chosen countries show that
the amount of the most harmful pollutant type (particulate matter) was
high and became higher in comparison with the reference year 2010.

Here is the list of countries which experienced changes in 2012, 2014
and 2016 (reference year is 2010), correspondingly. Countries which
experienced an increase in the level of particulate matter:

``` {.r}
pmup <- rbind(pm %>% select(Entity, Year, group) %>% filter(Year == 2011) %>%
    rename(group.x = group), returndataup(pm, 2010, 2012), returndataup(pm, 2010, 2014), 
    returndataup(pm, 2010, 2016)) %>% arrange(Entity) %>% rename(Group = group.x)
options(knitr.kable.NA = "")
knitr::kable(dcast(pmup %>% filter(Entity %in% names(which(table(pmup$Entity) > 1))), Entity ~ Year)) %>% 
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
2011
</th>
<th style="text-align:left;">
2012
</th>
<th style="text-align:left;">
2014
</th>
<th style="text-align:left;">
2016
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Bangladesh
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Belize
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Benin
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Brazil
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Burkina Faso
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Burundi
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Cameroon
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Cape Verde
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Central African Republic
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Chad
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Democratic Republic of the Congo
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Djibouti
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Equatorial Guinea
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Eritrea
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Ethiopia
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Gabon
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Gambia
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Ghana
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Greece
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Guinea
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Guinea-Bissau
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Haiti
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Hungary
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
India
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Lesotho
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Liberia
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Mali
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Mauritania
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Mongolia
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Morocco
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Namibia
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Nepal
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Nicaragua
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Nigeria
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Oman
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Pakistan
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Panama
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(12,24\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Papua New Guinea
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(12,24\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Rwanda
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Senegal
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Singapore
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
South Sudan
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Sudan
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Swaziland
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Switzerland
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Thailand
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Togo
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Uganda
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
UK
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
United Arab Emirates
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Uzbekistan
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Venezuela
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Yemen
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Zimbabwe
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
</tr>
</tbody>
</table>

Countries which experienced a decrease in the level of particulate
matter:

``` {.r}
pmdown <- rbind(pm %>% select(Entity, Year, group) %>% filter(Year == 2011) %>% 
    rename(group.x = group), returndatadown(pm, 2010, 2012), returndatadown(pm, 2010, 2014), 
    returndatadown(pm, 2010, 2016)) %>% arrange(Entity) %>% rename(Group = group.x)
options(knitr.kable.NA = "")
knitr::kable(dcast(pmdown %>% filter(Entity %in% names(which(table(pmdown$Entity) > 1))), Entity ~ Year)) %>% 
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
2011
</th>
<th style="text-align:left;">
2012
</th>
<th style="text-align:left;">
2014
</th>
<th style="text-align:left;">
2016
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Bahrain
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Bolivia
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Burkina Faso
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
France
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Iran
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Iraq
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Japan
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
(3.29,12\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Kuwait
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Libya
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Niger
</td>
<td style="text-align:left;">
(86.1,204\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(65.4,86.1\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Nigeria
</td>
<td style="text-align:left;">
(44.7,65.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Sierra Leone
</td>
<td style="text-align:left;">
(24,44.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(12,24\]
</td>
<td style="text-align:left;">
</td>
</tr>
</tbody>
</table>

### OZ

To see the changes on the map the data for ozone is created:

``` {.r}
map.world_joined4 <- left_join(oz,map.world, by = c('Entity'='region' ))
```

``` {.r}
annotate_figure(ggarrange(finalplot(2005, 2005, OZ, map.world_joined4, oz), 
   finalplot(2005, 2010, OZ, map.world_joined4, oz), finalplot(2005, 2013, OZ, map.world_joined4, oz), 
   finalplot(2005, 2015, OZ, map.world_joined4, oz), ncol = 2, nrow = 2, common.legend = F), 
   top = text_grob("Concentration of ozone in 2005, 2010, 2013, 2015", face = "bold", size = 12))
```

![](2020-01-09-Changes-in-air-pollution_files/figure-markdown/ozgr-1.png)

Countries which experienced an increase in the level of ozone
concentration:

``` {.r}
ozup <- rbind(oz %>% select(Entity, Year, group) %>% filter(Year == 2005) %>% 
    rename(group.x = group), returndataup(oz, 2005, 2010), returndataup(oz, 2005, 2013), 
    returndataup(oz, 2005, 2015)) %>% arrange(Entity) %>% rename(Group = group.x)
options(knitr.kable.NA = "")
knitr::kable(dcast(ozup %>% filter(Entity %in% names(which(table(ozup$Entity) > 1))), Entity ~ Year)) %>% 
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
2005
</th>
<th style="text-align:left;">
2010
</th>
<th style="text-align:left;">
2013
</th>
<th style="text-align:left;">
2015
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Bangladesh
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bhutan
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Bolivia
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Cambodia
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Colombia
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
El Salvador
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Laos
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Malaysia
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Maldives
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Myanmar
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(78.3,116\]
</td>
</tr>
<tr>
<td style="text-align:left;">
North Korea
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Pakistan
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Paraguay
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Saudi Arabia
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
South Korea
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Taiwan
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Thailand
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Venezuela
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Zimbabwe
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
</tbody>
</table>

Countries which experienced a decrease in the level of ozone
concentration:

``` {.r}
ozdown <- rbind(oz %>% select(Entity, Year, group) %>% filter(Year == 2005) %>% 
    rename(group.x = group), returndatadown(oz, 2005, 2010), returndatadown(oz, 2005, 2013), 
    returndatadown(oz, 2005, 2015)) %>% arrange(Entity) %>% rename(Group = group.x)
options(knitr.kable.NA = "")
knitr::kable(dcast(ozdown %>% filter(Entity %in% names(which(table(ozdown$Entity) > 1))), Entity ~ Year)) %>% 
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Entity
</th>
<th style="text-align:left;">
2005
</th>
<th style="text-align:left;">
2010
</th>
<th style="text-align:left;">
2013
</th>
<th style="text-align:left;">
2015
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Central African Republic
</td>
<td style="text-align:left;">
(78.3,116\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Nigeria
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Norway
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
<td style="text-align:left;">
(34.9,45.7\]
</td>
</tr>
<tr>
<td style="text-align:left;">
Portugal
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
<td style="text-align:left;">
(45.7,56.6\]
</td>
</tr>
<tr>
<td style="text-align:left;">
USA
</td>
<td style="text-align:left;">
(67.4,78.3\]
</td>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
<td style="text-align:left;">
(56.6,67.4\]
</td>
</tr>
</tbody>
</table>

Conclusion
----------

Apart from affecting our health, a decrease in the level of air quality
is causing long-term environmental damage by driving climate change,
which is itself a danger for people and their health. Thus the air
pollution level should be well monitored by countries, analyzed and the
appropriate action should be taken into consideration.

The analysis of the data shows that in both high-income countries with
well-developed air quality monitoring networks and low- and
middle-income countries with poor data coverage, the condition of
outdoor air pollution becomes worse. To sum up, by considering certain
reference year for each pollution type, we can point out the following
facts:

-   CO2 (Reference year is 2011)

In recent years, the changes in carbon dioxide emissions are not sharp.
For example, in 2013, 3% of counties experienced an increase and 4% of
them experienced a decrease in the level of carbon dioxide emissions.
Similarly, in 2015, 5% of countries and 4% of countries; in 2017, 5% and
3% of countries experienced an increase and a decrease correspondingly
in the level of carbon dioxide emissions.

-   SO2 (Reference year is 1970)

In 1980, 22% of counties experienced an increase and 9% of them
experienced a decrease in the level of sulphur dioxide emissions.
Similarly, in 1990, 25% of countries and 22% of countries; in 2000, 22%
and 35% of countries experienced an increase and a decrease
correspondingly in the level of sulphur dioxide emissions.

-   PM (Reference year is 2010)

In 2012, 7% and 2% of countries show the increase and decrease in the
amount of particulate matter in the air, accordingly. In 2014, 8% and 4%
of countries show the increase and decrease in the amount of particulate
matter in the air, accordingly. In 2016, 25% and 2% of countries show
the increase and decrease in the amount of particulate matter in the
air, accordingly.

-   OZ (Reference year is 2005)

In 2010, 5% and 2% of countries show an increase and decrease in the
level of ozone concentration in the air, accordingly. In 2013, 8% and 3%
of countries show an increase and decrease in the level of ozone
concentration in the air, accordingly. In 2015, 10% and 3% of countries
show an increase and decrease in the level of ozone concentration in the
air, accordingly.
