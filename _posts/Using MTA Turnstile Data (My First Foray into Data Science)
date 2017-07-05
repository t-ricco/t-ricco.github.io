---
layout: post
title: Using MTA Turnstile Data (My First Foray into Data Science)
---

**The Problem**
 
The Metropolitan Transit Authority provides its turnstile data freely online. At Metis, it’s the ocs of our first data science project. Specifically, we were tasked to use the data to advise a non-profit organization called Women Tech Women Yes (make our WTWY) in how to best deploy street teams to canvass for people to join their email list at New York train stations. Their goal is to promote awareness of their organization and, hopefully, expand their donation base. Those you join the email list are offered tickets to a gala hosted by WTWY in the beginning of the summer.
 
My team and I further framed the problem to thusly: The gala would be held on July 1, 2018 in the area just north of Madison Square Park. WTWY has 4 street teams available, each of which would work two 4-hour shifts canvassing each week. We were comfortable further defining the problem in this way as it would ensure that our conclusions and recommendations would be focused. In the end, our results would be easily adapted to whatever specific needs WTWY might need. Recommending 4-hour shifts for the street teams make sense since MTA data provides turnstile register numbers in 4-hour intervals.
 
Assumptions
 
*What stood out to me from the beginning to the end of the process of my first data science project was the subtle role that assumptions played at every step of the way. Throughout the investigation into MTA data, the team’s work was based on a set of assumptions. Without making assumptions about the way the world in general work, even a simple analysis would become impractically complicated. For instance, the work throughout is based on the assumption that any large group of randomly selected MTA riders would be have roughly the same proportion of men and women. With that in mind, our process was guided by the idea that the easiest way to engage more women (Who would, presumably, more interested in receiving informational emails from a group promoting women in the tech industry - another assumption) would be to engage the largest number of people in general.*
 
**The Data**
 
We decided to look at data from the month of May and June for the years 2017, 2016, and 2015. We figured that these would be most representative of the time of year that WTWY’s street teams would be canvassing. After importing the MTA data into a pandas dataframe certain anomalies became evident:
Some register data was reported at irregular time intervals, as opposed to every four hours of the day starting at midnight as most of the data was.
Some of the changes in register number seemed impossibly high, even when accounting for the possibility of a register counter resetting through 0000000000.
Some register counts decreased over time, rather than increased as most did.
In order to deal with these anomalies, we made the following decisions:
+ Ignore stations reports that were an extremely short or extremely long time interval apart. We felt comfortable doing so since stations that reported in this way were eventually “corrected” to report in the regular 4-hour schedule most others were. This indicated that data from these reports was not reliable. By looking at 3 years worth of data, we were able to make reasonable projections about what each station’s expected ridership would be on any particular day of the week.
+ We ignored extremely large changes in register counts. We defined “extremely large” to mean indicating more than one person passing through an individual turnstile each second over a 4-hour interval. We also assumed register counts that were descending were counting accurately and, thus, still providing usable data.
 
 
*Again, in order to make progress, the team made assumptions about how the world worked in order to determine which data was reliable. I am confident that establishing what data was reliable based on our reason and understanding of the world lead to more accurate results than if we had included all of the data in our analysis. However, there was a trade-off: Register differences reported at PATH train stations were much larger than at other MTA turnstiles. I hypothesize that this means that hardware at those stations differ significantly than those used at New York City Subway stations. Regardless, the team decided at this point that we should only focus on NYC subway lines as we had a better understanding of how to interpret the data from these machines and could make conclusions we were confident in.*
 
*We also made the decision at this point to make our decisions based on the total number of riders both entering and exiting a subway station rather than one or the other. From my point of view, it is reasonable that most people entering a subway station between 8am and 12 noon are on their way to work, that those entering between 4 pm and 8 pm were leaving work, etc. However, there was no good way of determining what percentage of people using the subway were commuting or were doing so for some other reason. With that in mind, we decided to not make any assumption in that regard and simply determine when and where ridership was at its peak.*
 
**The Analysis**

With much of the “dirty work” or organizing and cleaning our data out of the way, we could start examining the data and making observations we could use to formulate or recommendations to WTWY. Firstly we looked at the overall volume of riders and saw right away that: Ridership was much higher Monday through Friday than it was on Saturday and Sunday, with Wednesday being the busiest day of the week. When looking at the busiest stations, from Monday to Friday, ridership hit a small peak in the morning between 8am and noon, dropped somewhat from noon to 4 pm, than hit a higher peak in the afternoon to early evening from 4 pm to 8. 
Below, the average number of persons passing through a turnstile versus time at Herald Square and Penn Stations are graphed over the course of a week as examples.
![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/blob/master/_images/MTA_post_1.png "Herald Square"

![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/blob/master/_images/MTA_post_2.png "Penn Station"

We noted that our numbers correlated as much with the size of the strain station as anything and at this point decided to look at the traffic at each station through the lens of computing the average number of riders per turnstile. We reasoned that with a limited number of street teams deployed, we needed to be able to predict where the highest density of people would be to maximize the potential for the street teams to engage people. We found that many of the largest stations were still near the top of our list of potential time-location recommendations, but other noted:
1 - Certain other stations had a higher traffic density than those with the highest overall volume of riders and, additionally,
2 - There was relatively little difference in the traffic density among the busiest time-location combinations.

![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/blob/master/_images/MTA_post_3.png "Avg Persons per turnstile"

With that in mind we further filtered our recommendations by comparing our list of potential recommended time-locations for WTWY to a map of the locations of the largest tech employers in New York. We found the region between 14th street and 34th street in Manhattan to be particularly dense with tech companies*. With that in mind we were ables to make our recommendation for where WTWY’s street teams should be deployed with the following in mind:

1 - The stations should be in Manhattan between 14th street and 34th street.
2 - Clearly, a single street team could not operate at more than one location at the same time.
3 - Our recommended times at locations would maximize ridership traffic density.

![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/blob/master/_images/MTA_post_4.png "Avg Persons per turnstile - revised"

Our final recommendations to WTWY based on the problem criteria and our analysis
|Team number|Station|Time|
|----------:|-------:|:--|
|1| 23 St and 6 Ave  |Wednesday 4pm to 8pm
| |                  |Thursday 4pm to 8pm
|2|  34 St - Herald Square |Wednesday 4pm to 8pm
| |  14 St - Union Square | Tuesday 4pm to 8pm
|3| 23 St and 6 Ave |Tuesday 4pm to 8pm
| |                 |Friday 4pm to 8pm
|4| 14 St - Union Square |Tuesday 4pm to 8pm
| |                      |Wednesday 5pm to 9pm

*Throughout the process, the assumptions the team made framed our investigation and guided our reasoning to the results. There were times where we debated whether recommending to position street teams when most people on their way home from work would be the best thing to do. Again, we need to be careful about what we are assuming: Is it fair to assume almost everyone is commuting home? If that were so, the evening peak should more closely match the morning peak. Is it even fair to assume that people commuting to or from work are more or less likely to engage a volunteer canvasser? Maybe, but without any actual evidence one way or another I am uncomfortable jumping to a conclusion that might bias my conclusion towards whatever preconceived notions I might hold at the start of my investigation. Without questioning every assumption we bring to bear, we risk undermining our objectivity.* 
 
*Perhaps I am being too rigid in this stance and further experience with applying the tools of data science will teach me otherwise. Perhaps even the assumptions I and my team allowed to guide our process were already too limiting. I look forward to learning which of these hypotheses holds bears out once I’ve gained more experience as a data scientist.* 
