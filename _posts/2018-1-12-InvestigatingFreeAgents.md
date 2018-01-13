---
layout: post
title: Investigating the Return for Major League Baseball Free Agents
---

At the conclusion of the World Series each year, fans of all but one of the 30 major league teams are left disappointed with their team’s finish. The easiest way for teams to try and improve is by signing players on the free agent market. Free agents are players who have accrued at least six years of major league service time and are no longer under contract with any team and, thus, can negotiate terms with any major league franchise. For the teams, free agents represent a significant financial commitment, with some contracts being for tens or even hundreds of millions of dollars. However, there is significant risk involved in signing a free agent as a player’s performance can vary greatly from that of his recent past. I was interested in looking deeper into how often Major League franchises get what they paid for on the free agent market and which organizations are the best at evaluating which players to sign.

I gathered information of every free agent signing in major league baseball starting with the offseason following the 2006 season by scraping performance and salary data from baseball-reference.com and espn.com. For the purposes of this investigation, I am only interested in players that all teams would have had an opportunity to negotiate with and sign as free agents. The reason for this is that I was inspired to investigate this topic after reading a wide variety of media reports calling for teams to make significant commitments through the free agent market. As such, players like Mike Trout and Giancarlo Stanton who signed long term contracts before becoming eligible for free agency or signed extensions while still under contract are not part of this investigation.

Before we can determine a good way to evaluate a contract, we need a metric to measure a player’s performance. For that we use Wins Above Replacement (WAR) as calculated by Baseball Reference. 
***
**A Brief Aside About WAR**
If you are familiar WAR, feel free to skip this section. WAR has become a commonly accepted metric that summarizes all of a player’s contributions at the bat, in the field, or pitching. For reference, the following table taken from Fangraphs provides a breakdown of how to make sense of the WAR awarded to a position player or starting pitcher in a single season:

| Scrub | Role Player | Solid Starter | Good Player | All-Star | Superstar | MVP |
| --- | --- | --- | --- | --- | --- | --- |
| 0-1 WAR | 1-2 WAR | 2-3 WAR | 3-4 WAR | 4-5 WAR | 5-6 WAR | 6+ WAR |

https://www.fangraphs.com/library/misc/war/

More on how Baseball Reference calculates WAR and on how it can be interpreted can be found here: https://www.baseball-reference.com/about/war_explained.shtml
***

WAR gives us a way to evaluate the overall production of a player and compare production between two players, but I am interested in whether or not a free agent signing could be qualified as “successful” from a team’s perspective. It is tempting to try and attempt to assess the monetary value of the production of each player, however due to how rapidly salaries in Major League Baseball have increase from year to year, it would be misleading to compare value based on a player’s salary between two players signed even a few years apart without adjusting for inflation. With that in mind, I will look for a simpler rule to classify whether a free agent signing was a success.

While it might seem obvious to establish a certain WAR level as determining whether or not a signing was a success, teams don’t expect every player they sign to be a star. In fact, a significant proportion on free agent signings are for bench players and pitchers who would not be expected to produce at a star level. On the flip side, when a team does sign a star player, they hope that he will continue to produce at a high level.

My first look into determining whether or not a free agent signing was successful (from the team’s point of view) was whether or not the player continued to produce at the level he did in the seasons leading up to free agency. In order to do this, I compared the WAR per year attributed to each player over the three years immediately preceding filing for free agency with the WAR per year over the life of the contract. In doing so, I found that barely 30% of players signed via free agency matched or exceeded their annual production from the three years before signing their contract. That said, this might be an unreasonable criteria for assessing whether a team got what they expected since every major league front office is familiar with the aging curve: the idea being that, in general, a major league players’ performance will peak some time in their early to late twenties and then decline from there as the player ages.
https://www.fangraphs.com/library/the-beginners-guide-to-aging-curves/

With that in mind, I will be free agents who meet the following criteria:
1.	The player’s Average Annual WAR over the life of the contract is greater than zero and
2.	The player’s Average Annual WAR over the life of the contract was at least half the average annual WAR over the three seasons immediately preceding the player’s free agency.

To my surprise, only 42% of players met even this lower this standard. In fact, it is likely that this percentage will decrease further in the future as some of the long term contracts under consideration have not yet finished their term, and the WAR rate for these players will likely decrease due to aging.

What perhaps is most surprising is that 39% of all players signed in free agency in the past ten years produced zero WAR per year or less over the life of the contract. This is not restricted to short term deals. 10 of the 62 free agents who signed for 4 or 5 years, players who presumably earned those long term deals after producing at levels well above league average, did not result in a positive annual WAR. Looking at the box plots below, which are broken down by the length of the players’ contracts, we see how common it is for players to provide either little, or worse, negative value.

![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/raw/master/images/boxplot_FreeAgents1.png "WAR by Length of Contract"

There is a definite upward trend in the WAR per year for free agents as the number of years on the contract increases from 2 on up. This makes sense as players with a higher performance level leading into free agency can demand more years on their contract. What is noteworthy here is that the median, third quartile and maximum WAR rates on 1 year contracts is higher than those on 2, 3, 4, or 5 year contracts. I suspect that this is because a number of free agents who are not satisfied with the multi-year offers they receive in free agency accept one-year deals hoping for better offers next year.

One might reasonably assume that signing younger players via free agency might lead to better production since their skills are closer to their peak. However, this does not seem to be the case.

![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/raw/master/images/scatterplot_FreeAgents2.png "Scatterplot"

Each color in the above scatterplot corresponds to an age group, where age is determined by the player’s age at midnight, June 30th of the first year of their free agent contract. The age groups are 25-29 years of age (red), 30 - 34 years of age (blue), 35 - 39 (green), 40 - 44 (yellow), and 45+ (the last group consists only of Jamie Moyer’s contract signed in 2008). We see in general that there is definitely a positive correlation between the between a player’s demonstrated production previous to free agency and his performance under his new contract and that correlation appears within each age group. 

But, younger free agents are no better at holding their value than older ones. The table below consists of all players who entered free agency before their age 30 season between 2006 and 2016 with at least 3 WAR per year in the three years leading up to free agency. 

| PLAYER | YEAR | AGE | NEW_TEAM | Length of Contract | WAR per YEAR (3 years preceding free agency) | WAR per YEAR (During Contract) | DOLLARS per YEAR | 
| --- | --- | --- | --- | --- | --- | --- |  | 
| CC Sabathia | 2008 | 28 | Yankees | 7 | 6.10 | 3.20 | $23,000,000.00 | 
| Mark Teixeira | 2008 | 29 | Yankees | 8 | 5.60 | 2.59 | $22,500,000.00 | 
| Jason Heyward | 2015 | 26 | Cubs | 8 | 5.47 | 1.95 | $23,000,000.00 |
| Carl Crawford | 2010 | 29 | Red Sox | 7 | 4.83 | 0.49 | $20,285,710.00 |
| Prince Fielder | 2011 | 28 | Tigers | 9 | 4.13 | 1.15 | $23,777,780.00 | 
| Justin Upton | 2015 | 28 | Tigers | 6 | 3.47 | 3.60 | $22,125,000.00 | 
| Anibal Sanchez | 2012 | 29 | Tigers | 5 | 3.03 | 1.32 | $16,000,000.00 |

All but one of these players even come close to matching their established level of performance throughout their new contract. In fact, only two even meet our looser standard for a successful free agent signing by producing more than half their previous rate of WAR per year throughout their contract.
Identifying the right players to target and sign is hard. With any free agent signing, there is a wide range of potential outcomes. Following the 2018 season, a bumper crop of free agents, some of whom will still be under 30 years old and have already demonstrated an ability to perform at or near MVP levels. They will rightly command huge contracts. However, it is probable that we have already seen them at their highest level of performance and over the course of their next contract, while they may still perform at All-Star levels, there is also a significant risk for each of these signings that the player signed will barely warrant a starting position of the life of the contract.

Before signing off, I wanted to take a look at which organizations have demonstrated the best track record when it comes to signing free agents. It turns out the Blue Jays are head and shoulders above the competition in this area.  

![alt text][logo]

[logo]: https://github.com/t-ricco/t-ricco.github.io/raw/master/images/bar_FreeAgents3.png "Teams"
