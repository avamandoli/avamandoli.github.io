---
layout: page
title: Short Form Blogs
description: 
feature_image: 
permalink: /short-form-blogs/
---

Short Form Blog #1: Motivating a Point 

While the internet can be a democratic platform for free expression and a powerful tool for community organizing, it can also be leveraged by governments to surveil and suppress citizens’ sentiments. It can be a double-edged sword that has very different impacts depending on who wields power over it. 
Recent protests in Iran over the death of a 22-year-old woman, Mahsa Amini, in the custody of the country’s “morality police” have reignited dialogue about the role of the internet in civic life. The Iranian government has shut off the internet in parts of Tehran and Kurdistan and blocked social media platforms such as Instagram and WhatsApp, “in an attempt to curb a growing protest movement that has relied on social media to document dissent” (Strzyżyńska, “Iran blocks capital’s internet access as Amini protests grow,” The Guardian). Investigating the relationship between internet access and variables like civil liberties is crucial to understanding how crises like these play out.
While internet access is widespread, it is still not available to all. First, I want to examine what factors influence various countries’ access to the internet. Is GDP or GDP per capita a strong influence on the level of internet access a country has? How is internet access distributed globally and which areas have the lowest rates of engagement?  After establishing the outline of the issue, I then want to investigate the internet’s impact on individuals’ freedoms. Does increased internet access generally lead to increased civil liberties? Are there cases where the opposite is true because the state uses the internet as a weapon against its citizens? Do other factors such as natural resource wealth have a stronger impact on civil liberties than internet access? By exploring these questions, we can better understand how internet access influences the social and political atmosphere of countries. 


```markdown
# Loading packages and organizing data

#install.packages("devtools")
#devtools::install_github("vdeminstitute/vdemdata")
library(vdemdata)
library(tidyverse)
library(patchwork)
vdemdata <- vdemdata::vdem
```
I obtained this data from the Varieties of Democracy (V-Dem) Research Project, which can be found at https://www.v-dem.net/. 
The organization collects data in an attempt to address the “uncertainty [that] persists over why some countries become and remain democratic and others do not.”
Democracies are multifaceted systems and V-Dem attempts to accurately quantify democratization by breaking it down into a few core principles: electoral, liberal, majoritarian, consensual, participatory, deliberative, and egalitarian. Each principle includes hundreds of specific indicators to create a more nuanced analysis. 
The V-Dem Institute is based out of the University of Gothenburg, Sweden, and has worked with many other reputable institutions, such as the University of Notre Dame. Its global network includes over 3,500 Country Experts who complete surveys to help V-Dem “obtain detailed, local knowledge from qualified experts familiar with political developments in a given country.”

Because the majority of the world has access to the internet, comparing data between countries with internet and without internet was not very illuminating as the sample sizes were very different. Instead, I compared countries based on the level of internet censorship they experienced by their government. This better illustrates trends between internet access and socio-political liberties such as freedom of speech, access to justice, and educational equality. 

```markdown
vdemdata_post1960 <- vdemdata %>% 
  filter(year >= 1960)

vdemdata_middleeast <- vdemdata %>% 
  filter(e_regionpol_6C == 3)

vdemdata$internet_binary_def <- if_else(vdemdata$v2mecenefibin_osp >= 0.95, 1, 0)

vdemdata$internet_censorship_levels <- if_else(vdemdata$v2mecenefi_osp >= 2, 1, 0)
```

```markdown
# Visualization 1: Executive oversight and Freedom of the press, grouped by level of internet censorship by government 

exec_oversight_freepress_byinternet <- ggplot(vdemdata_no_nas, aes(x = v2lgotovst_osp, y = v2mecenefm_osp, color = as_factor(internet_censorship_levels)))+
  geom_point(alpha = 0.05, se = FALSE, )+
  geom_smooth(method = "lm")+
  scale_color_discrete(name = "Internet censorship by government",
    labels = c("High", "Low"))+
  labs(x= "Executive oversight", y = "Freedom of the press")+
  theme_clean()

exec_oversight_freepress_byinternet
```
![Visualization 1: Executive oversight and Freedom of the press]<img src="/images/exec_oversight_freepress_byinternet.jpeg">
For this project, I focused on understanding the impact of the internet and media on both social and political indicators of democracy. The internet and the more traditional press both represent spaces for public opinion to be shared. Whether citizens are able to utilize these media in a way that accurately reflects their sentiments is a strong indicator of the level of civil liberties they have. The media is often called “the Fourth Estate,” as it theoretically has the ability to hold other positions of power to account. To see if this is truly the case, I graphed the level of executive oversight in relation to the freedom of the press in countries with high and low levels of internet censorship. According to VDem, “Executive oversight” is a measure of how likely it would be that a body other than the legislature would investigate executive branch officials if they were engaged in unconstitutional, illegal, or unethical activity. That likelihood does increase as freedom of the press increases in all countries, regardless of internet censorship. However, in countries with high levels of internet censorship, the rate of that increase is lower than in countries with low levels of internet censorship. Additionally, freedom of the press is much lower in countries with high levels of internet censorship. This indicates that the traditional press has become intertwined with the internet, so censorship of the internet is also censorship of much of the press. 



```markdown
# Visualization 2: Government censorship efforts / Freedom of discussion for women

censorship_fos_w <- ggplot(vdemdata_middleeast, aes(x = v2mecenefm, y = v2cldiscw,, size = (e_gdppc)))+
  geom_point(alpha = 0.2)+
  geom_smooth(method = lm)+
  labs(x = "Government censorship of print and broadcast media", y = "Freedom of discussion for women", size = "GDP per capita")+
  theme_clean()

censorship_fos_w
```
![Visualization 2: Government censorship efforts / Freedom of discussion for women]<img src="/images/censorship_fos_w.jpeg">
Looking at more direct measures of freedom of speech for both women and men mirror graphs of freedom of the press. In the above visualization, an increase in the x-axis represents a decrease in government censorship of print and broadcast media. The freedom of print and broadcast media to share their unfiltered thoughts correlates with the freedom of discussion for women in civil society. To see if this trend changes depending on a country’s affluence, I also plotted the GDP per capita for each country. However, it appears that countries with higher GDP per capita do not necessarily have higher levels of freedom of discussion for women, and their governments censor media in rates on par with governments of less affluent countries. 


```markdown
# Visualization 3: Freedom of discussion for women by politico-geographic region

gdppc_regional <- ggplot(vdemdata_post1960, aes(x = v2cldiscw, col = as_factor(e_regionpol_6C))) +
  geom_density()+
  scale_color_brewer(name = "Politico-Geographic Region",
                     palette = "Set1",
                       labels = c("Eastern Europe and Central Asia", "Latin America and the Caribbean", 
                                      "The Middle East and North Africa", "Sub-Saharan Africa",
                                      "Western Europe and North America", "Asia and Pacific"))+
  labs(x = "Freedom of discussion for women", y = "Density")
  
gdppc_regional 
```
![# Visualization 3: Freedom of discussion for women by politico-geographic region]<img src="/images/freedomofspeech_women_regional.jpeg">
While the relative affluence of countries does not seem to have a strong impact on womens’ freedom of speech, countries’ politico-geographic location does. Western Europe and North America have the highest levels of freedom of speech for women by far. The Middle East and North Africa have the lowest levels. Sub-Saharan Africa and Asia and the Pacific have medium-low levels; Latin America and the Caribbean and Eastern Europe and Central Asia have medium-high levels. 



```markdown
# Visualization 4: Internet censorship levels across regions
vdemdata_2021 <- vdemdata_no_nas %>% 
  filter(year == 2021)

regions_internet_censorship <- ggplot(vdemdata_2021, aes(x=e_regionpol_6C, fill = as_factor(internet_censorship_levels)))+
  geom_bar(position = "dodge")+
  scale_fill_discrete (name = "Internet censorship levels", labels = c("High", "Low"))+
  scale_x_discrete(name = "Politico-geographic region", limits = c("Eastern Europe \n & Central Asia", "Latin America \n & the Caribbean", "The Middle East \n & North Africa", "Sub-Saharan\nAfrica", "Western Europe \n & North America", "Asia & Pacific"))+
  labs(y = "Count")+
  theme_clean()+
  theme(axis.text.x = element_text(angle = 45),
        axis.text.x.bottom = element_text(hjust = 1))

regions_internet_censorship
```

![# Visualization 4: Internet censorship levels across regions]<img src="/images/regions_by_internetcensorship_lvls.jpeg">
I continued to look for other trends on a global scale using these six politico-geographic regions. While there are different amounts of countries in each region, looking at the proportion of high to low internet censorship levels helps us compare regions by internet freedom. These relationships somewhat mirror the previous visualization. Latin America and the Caribbean and Eastern Europe and Central Asia have similar proportions of countries with high internet censorship levels, just as they had similar levels of freedom of speech for women. Western Europe and North America have the most freedom from internet censorship by far. The Middle East and North Africa is the only region where there are more countries with high internet censorship than not. 


```markdown
# Visualization 5: Acccess to justice for women vs. internet censorship in the Middle East

vdemdata_middleeast_subset <- vdemdata %>% 
  filter(country_name %in% c("Iran", "Saudi Arabia", "Syria", "Tunisia"), year >= 1900)

me_justicef <- ggplot(vdemdata_middleeast_subset, aes(x = year, y= v2clacjstw_osp, col = as_factor(country_name))) +
  geom_line()+
  scale_color_discrete(limits = c("Tunisia", "Iran", "Saudi Arabia", "Syria"), name = "Country")+
  labs(x = "Year", y = "Access to justice for women")+
  xlim(1990,2025)+
  theme_minimal()
  
me_internet <- ggplot(vdemdata_middleeast_subset, aes(x = year, y= v2mecenefi_osp, col = as_factor(country_name))) +
  geom_line()+
  scale_color_discrete(limits = c("Tunisia", "Iran", "Saudi Arabia", "Syria"), name = "Country")+
  labs(x = "Year", y = "Internet censorship by government \n (0 = Complete, 3 = None)")+
  xlim(1990,2025)+
  theme_minimal()

me_justicef + me_internet +
  plot_layout(guides = 'collect')
```
![# Visualization 5: Acccess to justice for women vs. internet censorship in the Middle East]<img src="/images/me_justice4women_patchwork.jpeg">
Because the Middle East and North Africa had both the lowest levels of freedom of speech for women and the highest proportion of countries with highly censored internet, I decided to take a closer look at the region. Given the recent protests in Iran over the death of Mahsa Amini and the Iranian government’s subsequent internet shutdowns, I decided to compare VDem’s data on access to justice for women and government censorship of internet. I created a subset of countries with relatively different socio-political environments and attempted to see if there was a relationship between access to justice for women and government internet censorship in each country. There appears to be some correlation in countries like Tunisia. In 2010, there was a sharp increase in internet freedom; since then, access to justice for women has steadily increased as well. Saudi Arabia shows a similar trend, although the level of internet freedom and access to justice for women are both significantly lower than in Tunisia. Iran and Syria, on the other hand, do not show such a strong correlation between the two variables. This may be because there are other variables such as the economy or civil unrest that have a stronger impact on the levels of these variables. 



```markdown
# Visualization 6: Relationship between political power distributed by gender and educational equality, compared in countries with and without internet access

vdemdata_no_nas <- vdemdata %>%
     filter(!is.na(internet_binary_def)) 
     
internet_binary_named <- c("0" = "Countries without internet access",
                           "1" = "Countries with internet access")

internet_censorship_levels_named <- c("0" = "High levels of Internet censorship",
                           "1" = "Low levels of Internet censorship")

 genderedpower_eduequality_byinternet <- ggplot(vdemdata_no_nas, aes(x = v2pepwrgen_osp, y = v2peedueq_osp))+
  geom_jitter(alpha = 0.1)+
  facet_wrap(~internet_censorship_levels, labeller = as_labeller(internet_censorship_levels_named))+
  geom_smooth(method = "lm")+
  labs(x= "Political power distributed by gender", y = "Educational equality")+
  theme_grey()

genderedpower_eduequality_byinternet
```

![# Visualization 6: Relationship between political power distributed by gender and educational equality, compared in countries with and without internet access] <img src="/images/genderedpower_eduequality_byinternet.jpeg">
Looking at internet censorship also helps us understand other socio-political factors such as educational equality and how positions of power are distributed by gender. In the above graph, we see that equality in both spheres have a positive relationship with each other. However, the positive relationship is significantly stronger in countries with low levels of internet censorship. Ultimately, while internet access is certainly not the only thing impacting measures of democracy, it is one factor that can help explain global trends.

Works cited:
- [Iran blocks capital’s internet access as Amini protests grow](https://www.theguardian.com/world/2022/sep/22/iran-blocks-capitals-internet-access-as-amini-protests-grow) 
- [VDem](https://www.v-dem.net/data/the-v-dem-dataset/)