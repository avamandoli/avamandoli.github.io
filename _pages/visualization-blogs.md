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

1. I thought this graph was uniquely powerful because of one simple aspect: the human icon. When looking at graphs about violent topics like gun violence, I’ve found it can be too easy to forget that the numbers we’re analyzing are real people. While this graph is relatively simple (it just compares one metric across a selection of countries), the use of a human icon instead of a solid bar is a particularly sobering reminder of what the graph is representing. Finding ways to remind people what data really represents is something I definitely want to incorporate into my data visualization practices. 

A couple of lines of code that could produce a similar graphic:

```markdown
gun_homicides_prop_selection <- gun_homicides_prop %>%
	filter (gun_homicides_prop, Development == “Advanced”) 
 
ggplot (gun_homicides_prop_selection, aes(x = Country, y = Prop))+
	 geom_text(aes(label = prop, family = "wmpeople1", size = 5)) +
     scale_x_discrete (“Country”, labels = unique(gun_homicides_prop_selection$Country))
```

<img src="/images/gun_deaths_florida.png">

2. This graph is really misleading because the Y axis is flipped. It makes it look as if the number of murders committed using firearms decreased after the “Stand Your Ground” law passed. For context, the law “allows those who feel a reasonable threat of death or bodily injury to ‘meet force with force’ rather than retreat.” Gun deaths actually increased significantly after that law was passed. The data itself seems accurate, it’s just the presentation of it that makes it unintuitive and misleading.

3. 

