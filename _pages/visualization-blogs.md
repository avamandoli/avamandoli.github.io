---
layout: page
title: Visualization Blogs
description: 
feature_image: 
permalink: /visualization-blogs/
---


### Visualization Blog #1: Controversial Data

<img src="/images/gun_homicides_developed_countries.jpg">

1) I thought the <a href="https://www.vox.com/policy-and-politics/2015/12/4/9850572/gun-control-us-japan-switzerland-uk-canada"> above graph </a >was uniquely powerful because of one simple aspect: the human icon. When looking at graphs about violent topics like gun violence, I’ve found it can be too easy to forget that the numbers we’re analyzing are real people. While this graph is relatively simple (it just compares one metric across a selection of countries), the use of a human icon instead of a solid bar is a particularly sobering reminder of what the graph is representing. Finding ways to remind people what data really represents is something I definitely want to incorporate into my data visualization practices. 

A couple of lines of code that could produce a similar graphic:

```markdown
gun_homicides_prop_selection <- gun_homicides_prop %>%
	filter (gun_homicides_prop, Development == “Advanced”) 
 
ggplot (gun_homicides_prop_selection, aes(x = Country, y = Prop))+
	 geom_text(aes(label = prop, family = "wmpeople1", size = 5)) +
     scale_x_discrete (“Country”, labels = unique(gun_homicides_prop_selection$Country))
```



<img src="/images/gun_deaths_florida.png">

2) <a href="https://www.businessinsider.com/gun-deaths-in-florida-increased-with-stand-your-ground-2014-2"> The graph above </a> is really misleading because the Y axis is flipped. It makes it look as if the number of murders committed using firearms decreased after the “Stand Your Ground” law passed. For context, the law “allows those who feel a reasonable threat of death or bodily injury to ‘meet force with force’ rather than retreat.” Gun deaths actually increased significantly after that law was passed. The data itself seems accurate, it’s just the presentation of it that makes it unintuitive and misleading.




<img src="/images/stlprisonadmissions_graph.png">

3) I created this graph to visualize the discrepancy between prison admission rates in St. Louis City and County by filtering data from a national dataset of prison admissions by county. St. Louis City and County have historically been deeply unequal due to the redlining and discriminatory housing policies that determined their borders. This division of resources impacts community health metrics such as prison admissions to this day. This graph was creating using data about prison admissions per 10k residents in selected years they reported data. While St. Louis City prision admissions have decreased since 2006, they continue to be disproportionately larger than St. Louis County prison admissions.

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

**----------**

<hr>

## Visualization Blog #2: Adding Uncertainty

<img src="/images/usa_voting_bydecade_lineplot.jpg">

1) I created this visualization to show the trend of election turnout in the United States since 1970. Today, we often hear that less and less people are voting. Whether it's door-knocking or "get out the vote" campaigns, politicians and community leaders alike are attempting to reverse this trend. But when did this trend of low voter turnout actually start, and it it as bad as people say? Looking at data from the Varieties of Democracy dataset, we see that this trend started around the 1970s or 1980s. However, adding error bars reveals something else: the downward trend from the 1970s to the 2000s may not be as dramatic as it looks because the error bars overlab significantly with each other. We can definiitely see a drop in the 2010s, but before that, the error bars show we should not be too quick to say election turnout has dropped precipitously in the last few decades. 

<img src="/images/usa_voting_bydecade_densityplot.jpg">

2) This second visualization is another way to represent the uncertainty surrounding U.S. election turnout across decades that highlights the spread across each year. For example, it shows that in the 2000s, there was a very wide range in election turnouts, while in the 2010s the turnout was more consistently around 55%. 


**----------**

<hr>


## Visualization Blog #3: Final Project Proposal



Studying global history has taught me to think a lot about big-picture trends. One common question that we examine is what role individual leaders play in shaping these trends and the development of a country or movement. While it is impossible to entirely disentangle one individual’s impact from the complex web of circumstances that influence a movement, we can look for patterns between the characteristics of leaders and their environments. Looking at leaders of rebel organizations can be useful in this search because such organizations arise out of opposition to the status quo. This can provide insight into what people want – and what lengths they are willing to go to in order to get it – under different political conditions. 

I’m interested in answering the question, “How do rebel leaders look and act in countries with different levels of political participation/freedom?” 

<a href="https://www.rebelleaders.org/">The Rebel Organization Leaders (ROLE) Database</a> , compiled by investigators Benjamin Acosta, Reyko Huang and Daniel Silverman, seeks to uncover how rebel leaders “shape the dynamics of armed conflicts, and contemporary world politics more broadly.” This data will be particularly useful in investigating how individual leaders impact the development of a movement because it provides biographical information about rebel, insurgent, and terrorist leaders who were active in civil wars between 1980 and 2011. 
 
I may also use the <a href="https://www.waarproject.com/">Women’s Activities in Armed Rebellion (WAAR) Project dataset</a>, depending on if they have overlapping data. This could help me understand what role women have played in different rebel movements. I’d be interested to see if women are more or less involved in rebel movements in countries where women are not granted a high level of political participation. 

To address my research question, I plan to visualize the relationship between how elite or democratic a country’s leadership is and how democratic/elite rebel movements are. I’d also like to visualize how politically active women are in the country versus how active they are in rebel movements. To understand if there are patterns among rebel leaders, I’d like to visualize what traits rebel leaders most commonly share by mapping size to a bubble graph. 

Some visualizations that are inspiring me are <a href="https://www.pewresearch.org/fact-tank/2019/04/18/a-look-at-how-people-around-the-world-view-climate-change/ft_19-04-18_climatechangeglobal_since2013concerns/">this one by Pew Research</a>  and <a href="https://twitter.com/spren9er/status/1195826547724374018">this one by Dr. Torsten Sprenger</a>.  I want to make something like the Pew Research graph to illustrate the number of rebel leaders in different countries over time. I also want to emulate the visualization by Dr. Sprenger to show what the most common attributes rebel leaders have in common are. 




