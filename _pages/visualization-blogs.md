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

I thought this graph was uniquely powerful because of one simple aspect: the human icon. When looking at graphs about violent topics like gun violence, I’ve found it can be too easy to forget that the numbers we’re analyzing are real people. While this graph is relatively simple (it just compares one metric across a selection of countries), the use of a human icon instead of a solid bar is a particularly sobering reminder of what the graph is representing. Finding ways to remind people what data really represents is something I definitely want to incorporate into my data visualization practices. 

‘Gun_homicides_prop_selection <- Gun_homicides_prop %>%
	Filter (Gun_homicides_prop, Development == “Advanced”) 
 
Ggplot (Gun_homicides_prop_selection, aes(x = Country, y = Prop))+
	 geom_text(aes(label = prop, family = "wmpeople1", size = 5)) +
	Scale_x_discrete (“Country”, labels = unique(Gun_homicides_prop_selection$Country))’
