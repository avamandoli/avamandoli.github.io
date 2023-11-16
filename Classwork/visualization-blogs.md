---
layout: page
title: Visualization Blogs
description: 
feature_image: 
permalink: /visualization-blogs/
---


## Visualization Blog #1
# STAT 301: Political Data Visualization


<img src="/images/stlprisonadmissions_graph.png">

I created this graph to visualize the discrepancy between prison admission rates in St. Louis City and County by filtering data from a national dataset of prison admissions by county. St. Louis City and County have historically been deeply unequal due to the redlining and discriminatory housing policies that determined their borders. This division of resources impacts community health metrics such as prison admissions to this day. This graph was creating using data about prison admissions per 10k residents in selected years they reported data. While St. Louis City prision admissions have decreased since 2006, they continue to be disproportionately larger than St. Louis County prison admissions.

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

#Create visualization
ggplot(melted_stl_prison_admissions, aes(x = variable, y = value, fill = county)) +
  geom_bar(position = "dodge", stat = "identity") +
  scale_fill_brewer(name = "County", labels = c("St. Louis City", "St. Louis County")) +
  scale_x_discrete(labels = c(2006, 2013, 2014)) +
  labs (title = "Prison Admissions per 10k Citizens in \n St. Louis City versus St. Louis County", y = "Admission Number per 10k", x = "Year")+
  theme_pander()+
  theme(axis.title.x = element_text(family = "Avenir", vjust = -2),
        axis.title.y = element_text(family = "Avenir", vjust = 3),
        axis.text = element_text(family = "Avenir"),
        legend.text = element_text(family = "Avenir"),
        legend.title = element_text(family = "Avenir"),
        plot.margin = margin(1, 1, 1, 1, "cm"))
```



<hr>

## Visualization Blog #2: Adding Uncertainty

<img src="/images/usa_voting_bydecade_lineplot.jpg">

I created this visualization to show the trend of election turnout in the United States since 1970. Today, we often hear that less and less people are voting. Whether it's door-knocking or "get out the vote" campaigns, politicians and community leaders alike are attempting to reverse this trend. But when did this trend of low voter turnout actually start, and it it as bad as people say? Looking at data from the Varieties of Democracy dataset, we see that this trend started around the 1970s or 1980s. However, adding error bars reveals something else: the downward trend from the 1970s to the 2000s may not be as dramatic as it looks because the error bars overlab significantly with each other. We can definiitely see a drop in the 2010s, but before that, the error bars show we should not be too quick to say election turnout has dropped precipitously in the last few decades. 

<img src="/images/usa_voting_bydecade_densityplot.jpg">

This second visualization is another way to represent the uncertainty surrounding U.S. election turnout across decades that highlights the spread across each year. For example, it shows that in the 2000s, there was a very wide range in election turnouts, while in the 2010s the turnout was more consistently around 55%. 



<hr>


## Visualization Blog #3: Final Project Proposal


Studying global history has taught me to think a lot about big-picture trends. One common question that we examine is what role individual leaders play in shaping these trends and the development of a country or movement. While it is impossible to entirely disentangle one individual’s impact from the complex web of circumstances that influence a movement, we can look for patterns between the characteristics of leaders and their environments. Looking at leaders of rebel organizations can be useful in this search because such organizations arise out of opposition to the status quo. This can provide insight into what people want – and what lengths they are willing to go to in order to get it – under different political conditions. 

I’m interested in answering the question, “How do rebel leaders look and act in countries with different levels of political participation/freedom?” 

<a href="https://www.rebelleaders.org/">The Rebel Organization Leaders (ROLE) Database</a> , compiled by investigators Benjamin Acosta, Reyko Huang and Daniel Silverman, seeks to uncover how rebel leaders “shape the dynamics of armed conflicts, and contemporary world politics more broadly.” This data will be particularly useful in investigating how individual leaders impact the development of a movement because it provides biographical information about rebel, insurgent, and terrorist leaders who were active in civil wars between 1980 and 2011. 

To address my research question, I plan to visualize the relationship between how elite or democratic a country’s leadership is and how democratic/elite rebel movements are. I’d also like to visualize how politically active women are in the country versus how active they are in rebel movements. To understand if there are patterns among rebel leaders, I’d like to visualize what traits rebel leaders most commonly share by mapping size to a bubble graph. 