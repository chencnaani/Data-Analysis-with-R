## *Lab 2: Visualization Through `ggplot`*  
<br/><br/>  
  

**Contents**:  

* 1. Basic Statistics    
* 2. Scouting Report   
* 3. Model Building 
* 4. Fix Problematic Plots 
* 5. Open Question 


#### Background: 

You've been hired as a data analyst at the football (soccer) club Hapoel London. 
Since this is a small and under-funded club, you will not have access to real-football data, but to data from the football computer game fifa18. Your job is to analyze this dataset and extract meaningful insights from the data in order 
to help your club make better decisions. 

#### Data File: 
You will load and analyze the fifa18 football dataset file called "fifa_data.csv". <br> 
The dataset contains detailed information about each player in the game, including: names, age, nationality, overall ability, estimated potential ability, current club and league, market value, salary (wage), ability at different football skills (also called 'attributes', e.g. Ball.control, Sprint.speed ...), ability to play at different position in the game (CF, CM, ...) and the preferred positions of the player. 


Required Libraries:
```{r, echo=FALSE}
library(ggplot2)
library(dplyr)
library(corrplot)
library(scales)   # needed for formatting y-axis labels to non-scientific type
library(radarchart)
library(tidyr)
library(tidyverse)
library(reshape2) # melt
library(ggthemes)
library(rworldmap) # world map
library(modelr)
library(radarchart) #Spider chart
library(RColorBrewer) #to make it colorful map
```

## 1. Basic Statistics

First, you are requested to load the fifa18 dataset and find and display general information about the players. 

a. Plot showing the age distribution of all players.

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000003.png)


b. Plot comparing the *overall* ability of players in different leagues ('League').

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000004.png)

--It can be seen from the boxplot that leagues which have especially bad players (overall abillity is under 50) are england, france, italy, poland, scotland and "other". Leagues with especially good players (overall ability is over 90) are endland, france and spain. In addition, on average the league with the best players overall abillity is spain. 

c. Plot showing the density of players' salary ('Wage') distribution. <br>
separate plot showing the density distribution of the *log* of players' salary. <br>
 
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000005.png)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000006.png)

--note that the log plot does not include 219 players who don't get paid at all (wage=0, log(wage)=-inf) 

d. Are the top-10 players with the highest value also the top-10 best players in terms of *overall* ability? 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/1.jpg)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/2.jpg)

--Two lists are not identical. 
  M. Neuer is the player with the best overall ability who is also not in the top 10 valued players. 

e. Show a table of the ten *best* and ten *worst* teams in terms of *average* player overall ability.

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/3.5.jpg)


## 2. Scouting Report 

You are in charge of the scouting division. The goal of this division is to follow players' potential and overall ability, and identify undervalued players - that is, players whose current value is lower compared to what would be expected based on their predicted future ability. 

a. Your boss wants to fly abroad to recruit promising players. Use the *rworldmap* package to display the world map and color each country based on the *total number of players* from this nationality. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000007.png)


b. Quantity may not guarantee quality. Repeat the above analysis but this time display a world map where each country is colored by the *average overall quality* of players. Find an under-represented country you'd recommend to travel to (i.e. a country with few players with high overall average quality). 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000008.png)

--we would recommend to travel to Algeria, it looks like they dont have lots of players, but they have high overall average quality 


c. Show the *average overall* ability by *age* of all players, for players 35 years old or younger

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000009.png)

d. Make a graph showing the *average difference* between a player's overall ability to potential ability as a function of age, up to age 35. At what ages should we expect to find players for future development based on this graph?  

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/0000010.png)

-- In order to find players for future development we should look at the ages with the middle diffrence in the graph (around 20), so they have the potential and with enough overall ability, so in the long run the players will get much better then they already are at that age.


e. We are seeking young (age <=21) players with high Overall ability (>70). Show a scatter plot of these players comparing their *Potential* ability (y-axis) and current salary (*Wage*, x-axis). 
Prepare a table showing the 10 most-undervalued players, i.e. currently lowest payed compared to their potential. Calculate for each of them what is a fair salary matching their potential that you would offer to lure them away from their current club and show it in the table. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/0000011.png)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/11.jpg)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/3.jpg)

 

## Q3. Model Building 

a. We are interested in finding out which skills are similar in terms of players' performance at the position. 
Extract the 29 skills for non-goalkeeper players (Acceleration, ..., Volleys, except 'GK.*' skills). 
Calculate the correlation between players' ability in each pair of skills and show a heatmap correlation-plot of the correlations' matrix. What two skills seem least correlated with other skills? 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/0000012.png)

--Jumping & streanght seem to be least correlated with other skills. 

b. Consider the following six major players positions: CAM, CB, CM, RB, RW, ST and in addition the Overall players' performance. Show a correlation-plot of players' skill levels vs. their performance at the six positions + Overall performance. Find the 7 skills mostly correlated for player's Overall performance and list them in a table.

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/0000013.png)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/4.jpg)

c. Build your team by selecting six *different* players, one in each of the above positions in such a way that the players chosen are the best in their individual position. If the same player is the best at multiple positions, try to build the team in such a way that maximize the team's overall average score.

-- we recived that the same player is the best at both RW and ST. 
-- second best at those position is a player who is already taken by other position. 
-- therd best player have same overall abillity. 
-- therd best player in RW has a better score at it then therd best player in ST has in ST, therefor he was chosen for position RW. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/Spider.jpg)

--our best team is : L. Messi in CAM, Sergio Ramos in CB, T. Kroos in CM, Marcelo in RB, Neymar in RW & Cristiano Ronaldo in ST. WINNING TEAM!

d. We are interested in determining how each of the different player's abilities changes with age. 
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/shot.jpg)



e. Your boss suggests that some players may be currently under-performing compared to their skill levels (possibly due to poor fit with their current Club, recent injuries, bad luck, psychological or other reasons), 
and that acquiring them may be beneficial as they will be expected to perform better in the future. 
Fit a multiple regression model predicting player's Overall performance based on their skill level at the 29 different skills. Find the $10$ players with the least Overall performance level compared to what would their set of skills predict, 
and list them in a table. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/5.jpg)



## Q4. Fix Problematic Plots

The previous data-analyst of the club was fired for producing poor plots. 
Below see a code for two bar plots that he made.

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/6.jpg)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/7.jpg)

a. Describe what did your predecessor try to show in each of the two plots. 

--In the first plot our predecessor tried to show the top 10 clubs with the highest number of different nationalities. The closest the club to 1 the least div in their club. we can see that the club with the smallest value is the most diverse club.

--In the second plot our predecessor tried to show football clubs with the highest number of players' nationalities in their team, according to DIV index and plotted the`10 most diverse  clubs according to this DIV measurement.

b. problematic issues with his plot. 

--The first problem is that the first graph is not intuitive, because we expect that the higher the DIV value, the more divese a club should be. Here, it's the opposite.

--The second problem in the graphs are the lack of Headlines.
Healines should be included when presenting a plot.

--The third problem is that people without any club were categorized as people with a club and that all the people without a club were actually categorized in the graphs as one club.That is a problem because these players are not supposed to be included in the diversity of club considurations.

--The fourth problem is that the graph is hard to read, the names of the clubs on the graph. this is why we thought to changed the angle and the size of the text on the x axis.

c. improved plots. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000033.png)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/003303.png)

## Q5. Back to the real world 
Your boss is not convinced that your analysis of the fifa18 dataset is relevant for performance in the real world. To convince her, you need to show her that the fifa18 data can predict actual performance in football. Load the fifa ranking dataset ['fifa_ranking.csv'](https://raw.githubusercontent.com/DataScienceHU/DataAnalysisR_2020/master/data/fifa_ranking.csv) which contains ranking of countries based on their actual performance in international football competitions. 
Use the fifa18 dataset to compare the real vs. game football levels across all countries. 
What is your conclusion regarding the relevancy of the fifa18 game dataset to the real world? 
Use your best judgment to choose the appropriate data, models, analysis and plots to support your conclusions. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/00000d.png)
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/lab%202/000031.png)

--You can see that in both graphs the index goes down and this also shows that the relative score tables are correlated.

--see the cor of the two of the two values, so that it can be seen that the variables explain one another and that the correlation is quite high. We have assumed that each team of state consists of at least 17 players, and will select the best players. So we averaged players' capabilities per country, and this measure seems to explain the score in 2018 by 0.77
