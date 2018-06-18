---
title: "basketball free throws, randomness, and the hot hand"
layout: post
---

For most sports fans the idea that a player is ‘on a roll’, or is ‘due 
to hit a shot’ is almost second nature. However, according to the 
statistics, sports contain much more randomness than most sports fans 
would be comfortable with. A paper published in [1985][hothand-link] claimed the idea a 
player has a hot hand is simply a fallacy. The mind misinterprets these
occurences because our mind is trained to find patterns. When watching sports or going through life, 
it is common for to come up with stories to explain events that are 
inherently random. Claiming that a player ‘is on fire’ seems to just be 
another example of this. Our minds are biased towards looking for 
streaks, and random events can very often appear to show a streak. 

Let me propose an example. Below is the chart of a hypothetical stock coming
from a program randomly simulating stocks. This picture comes from a simulation 
where the stock begins the year at a value of $100 and each day its value 
will go up or down randomly (it is just as likely to go up as it is 
down) between 0 and 2 dollars. Of course some simulations of this will 
show shocks that shoot down, most will stay near $100 but some can seem 
to follow a steep upward trend. Is there any information that one could 
gain from this chart to make an informed decision about whether or not 
to purchase this stock? Absolutely not. The chart is completely 
misleading. This stock is no more likely to increase the following year than another 
simulation under the same conditions which ended up at $50 after one 
year. This is an example of how a trend or a perceived pattern seems 
to give a powerful indication of what will come in the future, and 
oftentimes that judgement is completely anchored in randomness. 
According to the hot hand fallacy, basketball is no exception.

![stock](/assets/randstock.png)

Of course after I say all of
these things about randomness, I am going to admit I wasn't convinced by
the hot hand fallacy. Maybe part of me did not want to 
accept that all of the sports I’ve watched over the years were just a 
mess of randomness, but I wanted to see if I could find any of my own 
evidence for the existence of the hot hand. Sure, maybe sports fans 
blow the idea of the hot hand out of proportion. I could believe that. 
But to not exist at all, no way. I’ve played basketball. I know that 
feeling you get when you’ve hit a couple shots in a row. I thought that 
mental boost, the confidence, whatever it may be, must put you in some 
state of enhanced shot making ability. 

I thought about where to begin and I decided I would settle on an 
analysis of free throw shooting. I decided this is where I would start 
because of the simplicity of the free throw versus the complexity of 
analyzing in game shots. My thinking was a free throw is always taken 
from the same distance with no defence so any given free throw is just about 
the same as any other free throw. The reason this matters is because 
say we have a player who has a field goal percentage of 45%. Say he 
takes 10 shots in a game. Maybe three are layups, one dunk, two three 
pointers, three mid range jump shots, and a half court heave at the end 
of the half. Clearly, each of those shots have different likelihoods of 
going in. There is no way both the dunk and the half court heave have
exactly the same 45% chance of going in or even remotely similar chances
at that. It would be a lot harder to know if a player 
is shooting a better percentage when the degree of difficulty (which changes 
based on shot distance, defense, balance of the shooter etc.) of the 
players' shots are never 
constant. But with free throws, I feel confident in assuming that the 
probability of a free throw going in is always just about what that 
players free throw percentage is. Of course, there are many factors 
that could change the percentage such as injury, fans in the background, 
fatigue, or even if the previous shot was made (if the hot hand fallacy 
is not actually a fallacy). Though these factors do (maybe) matter, they 
seem minor compared to the myriad of other factors that impact a players 
in game shooting. 

For my initial analysis, I found a nice dataset on a website called 
[kaggle][kaggle-site]. Basically kaggle is a website full of freely 
accessible datasets. The dataset I used contained thousands 
and thousands of free throws taken between the 2006 and 2016 NBA season. 
My approach was simple. First I would calculate the average free throw 
percentage in the dataset. Then I would go through each set of two 
free throws and if the first free throw went in, then I would calculate 
the probability of the second going in. If the first free throw did not go in, 
then I’d instead use the data point to calculate the likelihood of the 
second free throw going in. What I hoped is that the free throw 
percentage would be above the average if the first one went in, and 
lower if the first one did not go in.

Here are my findings:

|FT type |Make percentage|Sample size (shots) | 
|--------|--------|---------|
|Avg. FT %| 75.7% | 618,019|
|FT %: shot after make|79.6% | 205,078|
|FT %: shot after miss|73.3% |72,961 |

Clearly, there is some difference here. I know I should check P-values to 
verify that these differences are not random but because of the large
sample sizes I'm confident these results are not random when tested against a reasonable significance level. 
However, that  does not necessarily say much
about the validity of the hot hand. When fans mention the hot hand,
it usually does not have anything to do with free throws. At the very least,
I believe that the findings here show that even free throws, which have 
very few factors influencing the probability the shot goes in, do not have a constant 
make percentage. This variation is very promising because the 
hot hand fallacy assumes there should not be variance due to the 
state of the player ('hot' or 'cold'). In further conclusion, it should be noted
that while there are differences in each free throw percentage, the differences are relatively small. 
They are not large enough for a fan to notice these effects during a game. 
Still, the effects certainly matter and are very encouraging.

I'll soon write a second piece using additional data from in game shots 
and I'll see if I can back up my findings here. 

If you have any questions, comments, or ideas about where to go next,
please email me at the address found at the bottom of this site. 

[hothand-link]: https://en.wikipedia.org/wiki/Hot-hand_fallacy#1985_%22Hot_Hand_in_Basketball%22_paper
[kaggle-site]:  https://www.kaggle.com/

