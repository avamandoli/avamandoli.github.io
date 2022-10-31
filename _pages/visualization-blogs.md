---
layout: page
title: Visualization Blogs
description: 
feature_image: 
permalink: /visualization-blogs/
---


### Visualization Blog #1: Controversial Data

<img src="/images/gun_homicides_developed_countries.jpg">

1) I thought the above graph was uniquely powerful because of one simple aspect: the human icon. When looking at graphs about violent topics like gun violence, I’ve found it can be too easy to forget that the numbers we’re analyzing are real people. While this graph is relatively simple (it just compares one metric across a selection of countries), the use of a human icon instead of a solid bar is a particularly sobering reminder of what the graph is representing. Finding ways to remind people what data really represents is something I definitely want to incorporate into my data visualization practices. 

A couple of lines of code that could produce a similar graphic:

```markdown
gun_homicides_prop_selection <- gun_homicides_prop %>%
	filter (gun_homicides_prop, Development == “Advanced”) 
 
ggplot (gun_homicides_prop_selection, aes(x = Country, y = Prop))+
	 geom_text(aes(label = prop, family = "wmpeople1", size = 5)) +
     scale_x_discrete (“Country”, labels = unique(gun_homicides_prop_selection$Country))
```



<img src="/images/gun_deaths_florida.png">

2) The graph above is really misleading because the Y axis is flipped. It makes it look as if the number of murders committed using firearms decreased after the “Stand Your Ground” law passed. For context, the law “allows those who feel a reasonable threat of death or bodily injury to ‘meet force with force’ rather than retreat.” Gun deaths actually increased significantly after that law was passed. The data itself seems accurate, it’s just the presentation of it that makes it unintuitive and misleading.




<img src="/images/stlprisonadmissions_graph.png">

3) I created this graph to visualize the discrepancy between prison admission rates in St. Louis City and County by filtering data from a national dataset of prison admissions by county. St. Louis City and County have historically been deeply unequal due to the redlining and discriminatory housing policies that determined their borders. This division of resources impacts community health metrics such as prison admissions to this day. This graph was creating using data about prison admissions per 10k residents in selected years they reported data.

```markdown
#Load in packages

library(tidyverse)
library(dplyr)
library(reshape2)

prison_admissions <- read.csv("https://raw.githubusercontent.com/TheUpshot/prison-admissions/master/county-prison-admissions.csv")

#Filter for St. Louis, MO data

stl_prison_admissions <- prison_admissions %>% 
  filter(county == "St. Louis city" | county == "St. Louis County" & state == "MO") %>% 
  select(county, state, admitsPer10k2006, admitsPer10k2013, admitsPer10k2014)

melt(stl_prison_admissions, id.vars = c('county', 'state')) -> melted_stl_prison_admissions

ggplot(melted_stl_prison_admissions, aes(x = variable, y = value, fill = county)) +
  geom_bar(position = "dodge", stat = "identity") +
  scale_fill_discrete(name = "County", labels = c("St. Louis City", "St. Louis County")) +
  scale_x_discrete(labels = c(2006, 2013, 2014)) +
  labs (y = "Admission Number per 10k", x = "Year")
```

**----------**

## Visualization Blog #2: Adding Uncertainty

```markdown
# typical load in of packages 
packages <- c("tidyverse", "reshape2", "fauxnaif", "gganimate", "ggthemes",
              "stringr", "gridExtra", "gifski", "png", "ggrepel", "scales",
              "lubridate", "paletteer", "GGally", "systemfonts", "extrafont", 
              "colorspace", "dplyr", "distributional"
              )

# install.packages("devtools")
# devtools::install_github("vdeminstitute/vdemdata")

lapply(packages, require, character.only = TRUE)
loadfonts(device = "all")

# read in data 
vdemdata <- vdemdata::vdem

# subset the data
election_turnout_usa <- vdemdata %>% 
  filter(country_name == "United States of America", year >= 1970) %>% 
  select(country_name, year, v2eltrnout) %>% 
  filter(!is.na(v2eltrnout)) 
```

```markdown
summary_data <- election_turnout_usa %>% 
  mutate(
    # Create decades categories
    decades = dplyr::case_when(
      year >= 1970 & year <=1979 ~ "1970s",
      year >= 1980 & year <=1989 ~ "1980s",
      year >= 1990 & year <=1999 ~ "1990s",
      year >= 2000 & year <=2009 ~ "2000s",
      year >= 2010 & year <=2019 ~ "2010s",
      year >= 2020 & year <=2029 ~ "2020s"
    ),
    # Convert to factor
    decades = factor(
      decades,
      level = c("1970s", "1980s", "1990s", "2000s", "2010s", "2020s")
    )) %>% 
  # Calculate mean and SD for each decade
  group_by(decades) %>% 
   summarise(
    n=n(),
    mean=mean(v2eltrnout),
    sd=sd(v2eltrnout)
  ) %>%
  # Calculate SE and 95% confidence interval
  mutate(se=sd/sqrt(n))  %>%
  mutate(ci=se * qt((1-0.05)/2 + .5, n-1))

```

```markdown
# Visualization 1: errorbars on line graph 
election_turnout_usa_decades <- ggplot(summary_data, aes(x = decades, y = mean))+ 
  geom_line(group = 1) + 
  ylim(0,100)+
  geom_errorbar(aes(ymin= mean-se, ymax = mean + se), width = 0.2) +
  labs(title = "Election turnout across decades in the United States", y = "Average election turnout (%)", x = "") +
  theme_minimal()

# Could also do confidence interval: ymin = (mean-(se*1.96)), ymax = (mean + (se*1.96))

election_turnout_usa_decades
```
<img src="/images/usa_voting_bydecade_lineplot.png">



```markdown
### Visualization 2: Density + interval plot with boxplot

usa_voting_bydecade <- ggplot(summary_data, aes(xdist = dist_normal(mean, sd), y = as_factor(decades),
             fill = as_factor(decades))) +
  stat_halfeye(
    adjust = .5,
    width = 1, 
    # Interval shows IQR and 95% data range
    .width = c(.5, .95)
  ) + 
  geom_boxplot(
    width = 0.12, 
    outlier.colour = NA, 
    alpha = 0.5
  ) +
  xlim(0, 100)+
  scale_y_discrete(labels = c("1970s", 
                              "1980s", 
                              "1990s", 
                              "2000s", 
                              "2010s",
                              "2020s"))+
  guides(fill = "none")+
  labs(x= "Average election turnout (%)", y = "", title = "U.S. Election turnout across decades")+
  theme_minimal()

usa_voting_bydecade
```
<img src="/images/usa_voting_bydecade_densityplot.png">
