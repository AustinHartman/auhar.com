---
title: "More on the hot hand"
layout: post
---


In the initial article for this project I tried to find any evidence for 
or against the hot hand fallacy by analyzing free throws. Those findings 
indicated some evidence for the hot hand. The analysis showed that after 
making the first free throw, the following free throw had a 
significantly better than average chance of going in. The first article 
can be read [here][first-article].

After the free throw analysis I have decided to consider an analysis of 
in game shots.

The first approach I thought of was very simple. I wanted to see how a players shooting 
percentage composed of shots after a make differed from their overall 
shooting percentage (similar to FT approach). Essentially, if a player makes a shot, could the 
player now ‘be on a roll.’ Of course, not every time a player makes a 
shot would fans consider them to be on fire, but this approach still 
seems that it could detect hot streaks if they really do exist. However, 
I also have to consider how a players' approach could change after making 
a shot. It is certainly possible that after a player makes a shot, their 
heightened confidence would lead to them taking more difficult shots 
that they otherwise would be less likely to take. So this makes 
calculations a whole lot more difficult. With free throws, I could just 
look at shooting percentages before and after a make because the 
distance and the defence (because there is none) for the shot remain constant. If 
the shooting percentage after a make is higher, that gives a pretty good 
indication there is some sort of effect going on. However, with in game 
shots it is possible that a player has a higher shot making ability 
after making a shot, but his shooting percentage after a make is lower 
than his overall shooting percentage because the shots he attempted 
after the make were more difficult. This is why free throws were nice.


So, to detect the hot hand for in game shots,  I will have to determine 
the difficulty of each shot taken. If the player performs better than 
the predicted difficulty after a make than when he typically shoots, 
then that would be very convincing evidence for the hot hand. The thing 
is, the only attribute in my dataset that would help indicate the shot 
difficulty is the distance of the shot. Typically, a longer shot is more 
difficult. To demonstrate this, I graphed the shooting percentages of 
all the shots in an NBA season from different distances below. 

![stock](/assets/13-14.png)

As expected, there is a downward trend as the distance increases. To my 
surprise, shooting percentage essentially plateaus at 40% from 5 to 20 
feet. If I had more data I might be able to decide why that is. Perhaps 
defenders defend more closely at 5 feet than they do at 20 feet which 
balances out the difficulty due to higher distance. I also created 
graphs for many other seasons as well, and the shape of the graph was 
approximately the same each season. The other charts can be found 
[here][chart-link].

So at the very least I could test this as an indicator of shot 
difficulty. Unfortunately, the lack of other information really makes it 
difficult to estimate the difficulty of a given shot. It would be 
helpful to know where the nearest defender was when the shot was taken. 
Was the shooter fully contested or wide open? It’d also be helpful to 
know the time on the shot clock. It is common to see a player throw up 
a prayer in the last few seconds of the shot clock, so knowing a shot 
was taken at the end of the shot clock often means it was a shot with a 
very low chance of going in. Obviously, there are plenty of factors that 
determine the difficulty of a shot but some of the factors are difficult 
to quantify and/or I have not found them.

Because I do not have the detailed data I feel would be necessary to 
find significant statistical evidence for or against the hot hand, I 
will perform an analysis similar to what I did with free throws. 
However, this time I am going to do the analysis on a player by player 
basis. The reason for this is I only want to choose players who are 
taking shots regularly throughout the game. In other words, I would 
rather do this analysis on Lebron James than a role player like Cedi 
Osman. If a player shoots once in the first quarter and makes it and 
then takes his second shot of the game in the third quarter and makes 
it, nobody will assume his ability to make the shot was enhanced by his 
hot hand due to his shot made over an hour earlier. The idea is that the 
hot hand is temporary and that is why I want to only analyze players who 
will regularly be attempting shots.

Below I graphed residuals of many top offensive players during the 
2014-2015 NBA season (I chose this season simply because this was the 
data I had available). Each residual point on the graph represents the 
difference between overall shooting percentage and shooting percentage when the 
previous shot was made.

![stock](/assets/residuals.png)

The graph shows that top players typically shoot a lower percentage 
after a make. The best explanation I have for this is top players 
attempt more ambitious shots after making a shot. So in the end, based 
on this data, I do not have enough evidence to comment specifically on 
the hot hand fallacy. However, I can say that many high volume shooters 
see a drop in shooting percentage after a make, but that does not mean 
their shot making ability drops after a make. Most 
likely this drop is due to players attempting more difficult shots after 
a make. 

[chart-link]: https://github.com/AustinHartman/stats_scraper/tree/master/charts/shooting%20percentage%20vs%20dist
[first-article]: http://www.auhar.com/2018/05/31/free-throws-and-randomness.html

