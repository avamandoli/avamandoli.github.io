---
layout: page
title: Short Form Blogs
description: 
feature_image: 
permalink: /short-form-blogs/
---

## Short Form Blog #2: Many ways to see it

In my continued exploration of the V-Dem dataset, I examined two more variables: the repression of Civil Society Organizations (v2csreprss) and the distribution of political power across socioeconomic groups (v2pepwrses). The first variable was measured by asking country experts the question “Does the government attempt to repress civil society organizations (CSOs)?”. Respondents answered on a scale from 0 to 4, with 0 meaning there is severe governmental repression of CSOs and 4 meaning there is no repression. The second variable was measured by asking country experts the question, “Is political power distributed according to socioeconomic position?” Respondents answered on a scale from 0 to 4, with 0 meaning that wealthy people enjoy a virtual monopoly on political power and average and poorer people have almost no influence, and 4 meaning political power is more or less equally distributed across socioeconomic groups.

For visual clarity, I used the ‘_osp ’ appended version of each variable to map the original measurement scale of zero to four.  


<img src="/images/vis1_grouped_bubble_plot.jpeg" alt = "Visualization 1: CSO freedom across life expectancy quartiles">
Two of the contextual variables I explored these main variables against were life expectancy and population. 
For my first visualization, I used data from 2000 because it was the most recent year with population data for nearly all countries. I sorted each country into quartiles based on life expectancy to see how free civil society organizations (CSOs) were from repression in each quartile. I found that the correlation between life expectancy and CSO freedom increased in countries in the 50-75th percentile and the 75-100th percentile of life expectancy. Below that, it seems like there is not a strong relationship between life expectancy and CSO freedoms. This may indicate that in countries where life expectancy is lower, monitoring or repressing CSO activities are not the top priority for governments. 
I labeled a selection of countries across geo-political regions and mapped the relative size of countries to provide additional context. Interestingly, even some countries with higher life expectancies like China and Cuba rank poorly in terms of CSO freedom. While population size and life expectancy are important factors in comparing countries, CSO freedoms are likely more heavily correlated with variables such as freedom of speech and a strong judicial system.



<img src="/images/vis2_powerdist_byyear.jpeg" alt = "Visualization 2: [Political power distribution trends across time">
Looking across time also helps illuminate historical trends. Almost every geo-political region demonstrated relatively steady increases in the even distribution of political power across economic groups. But there is one exception: Eastern Europe and Central Asia. While the even distribution of political power increased rapidly from around 1915 to 1950, it declined slowly between 1950 and 1990, then dropped rapidly between 1985 and 2010. The middle period of slow decline mirrors the Cold War, which began in 1947 and ended in 1991, indicating that perhaps the Eastern Bloc’s consolidation of power in Russia led to a gradual political disempowerment of average and poor people. 



<img src="/images/vis3_v2pepwrses_barplot.jpeg" alt = "Visualization 3: Political power distributions by life expectancy">
I was inspired by Our World in Data’s interactive visualization of the  <a href="https://ourworldindata.org/democracy">distribution of electoral democracy in 1900 globally</a> to illustrate if life expectancy correlates with the distribution of power by socioeconomic status. I sorted the data by descending order and the color coding showed that many of the countries with very even distributions of political power were within the 75-100th percentile of life expectancy. In countries in the 0-25th percentile of life expectancy, political power was more concentrated among wealthy people. Because wealthy people do not have to focus on simply making ends meet, it follows that they would have more capacity to pursue political goals and power. 



<img src="/images/vis4_CSO_boxplot.jpeg" alt = "Visualization 4: CSO freedoms across regions">
Finally, I wanted to examine the spread of CSO freedom across geo-political regions. I found that Western Europe and North America, Latin America and the Caribbean, and Eastern Europe and Central Asia had the greatest variability of CSO freedom. Visualizations like this help illustrate how consistent trends are across geo-political regions and indicate what outliers we should look more closely at. 


Works cited:
- [VDem](https://www.v-dem.net/data/the-v-dem-dataset/)
- [Our World in Data](https://ourworldindata.org/democracy)
-  <a href="/images/short_form_blog_2_bibliography.pdf">Packages Bibliography</a>