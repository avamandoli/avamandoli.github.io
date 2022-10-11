---
layout: page
title: Visualization Blogs
description: 
feature_image: 
permalink: /visualization-blogs/
---
**---
This page will host my visualization blogs. 
---**

# Visualization Blog #1: Controversial Data

<img src="/images/gun_homicides_developed_countries.jpg">

1) I thought this graph was uniquely powerful because of one simple aspect: the human icon. When looking at graphs about violent topics like gun violence, I’ve found it can be too easy to forget that the numbers we’re analyzing are real people. While this graph is relatively simple (it just compares one metric across a selection of countries), the use of a human icon instead of a solid bar is a particularly sobering reminder of what the graph is representing. Finding ways to remind people what data really represents is something I definitely want to incorporate into my data visualization practices. 

A couple of lines of code that could produce a similar graphic:

```markdown
gun_homicides_prop_selection <- gun_homicides_prop %>%
	filter (gun_homicides_prop, Development == “Advanced”) 
 
ggplot (gun_homicides_prop_selection, aes(x = Country, y = Prop))+
	 geom_text(aes(label = prop, family = "wmpeople1", size = 5)) +
     scale_x_discrete (“Country”, labels = unique(gun_homicides_prop_selection$Country))
```

<img src="/images/gun_deaths_florida.png">

2) This graph is really misleading because the Y axis is flipped. It makes it look as if the number of murders committed using firearms decreased after the “Stand Your Ground” law passed. For context, the law “allows those who feel a reasonable threat of death or bodily injury to ‘meet force with force’ rather than retreat.” Gun deaths actually increased significantly after that law was passed. The data itself seems accurate, it’s just the presentation of it that makes it unintuitive and misleading.


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

