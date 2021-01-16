---
layout: post
---

# Basketball Analytics Using R

Last semester, I attended the UConn Sports Analytics Symposium. It was an all-day symposium with speakers, poster presentations and workshops. I really enjoyed learning more about sports analytics and all the types of analysis that can be done. In the afternoon, I attended a workshop about basketball analytics with R. I learned about some cool visualizations you can do with the package BasketballAnalyzeR. I will illustrate some of them in this blog post.

The package includes datasets that have statistics from the 2017-2018 NBA season. The Houston Rockets did well that season so I decided to use that team to illustrate some things that can be done with this package.

```{r }
# install the package and load package to the library
install.packages('BasketballAnalyzeR')
library('BasketballAnalyzeR')

# Prepare the dataset
PbP <- PbPmanipulation(PbP.BDB) 
```
  
## Creating a Shot Chart

The first thing I would like to show that you can do is creating a shot chart:

```{r }
subdata <- subset(PbP, team=="HOU")
subdata$xx <- subdata$original_x/10
subdata$yy <- subdata$original_y/10-41.75

shotchart(data=subdata, x="xx", y="yy", z="playlength",
          num.sect=5, type="sectors", scatter=FALSE,
          result = "result")
```

This shot chart does not only tells us where the shots are taken and the shot percentages, it also tells us when the shot was taken. In the NBA, there is a 24 seconds shot clock and the team needs to shoot the ball before the 24 seconds are over.  The red and orange shots areas were taken closer to the end of the 24 seconds shot clock compared to the more green and yellow colored shots. It is interesting to see that the Houston Rockets like to take a lot of three pointers or shots very close to the basket when they are not in a time rush. The midrange shots that they take are often shot when they are close to reaching the end of the 24 seconds shot clock.

## Expected Points by Shot Distance

Another statistic that a team may be interested in is the expected points of shots that players take. This can be plotted as a function of the distance to the basket:

```{r }
PbP.HOU.sd <- subset(PbP.HOU, shot_distance < 40)
Pbox.HOU <- subset(Pbox, PTS>=500 &
                     Team=="Houston Rockets")
pl.HOU <- c("James Harden", "Chris Paul", "Eric Gordon")

mypal.HOU <- colorRampPalette(c("red","green"))
expectedpts(data=PbP.HOU.sd, players=pl.HOU,
            col.team="gray", palette=mypal.HOU,
            col.hline="gray")
```

The dashed horizontal line represents the expected points for all the shots in the data. We can see that when the shot distance is low, Chris Paul and James Harden have expected points that are lower than the expected points for all the shots in the data and lower than the team as well. On the other hand, Eric Gordon has higher expected points compared to the others for close shots. However, we can see that when we go further away from the basket and get towards the three point line (around 24 feet), Eric Gordon's expected points drop significantly while Chris Paul's and James Harden's expected points increase. We can see that this plot helps explain what shots have higher expected values for the different players. The far two pointers seem to have an overall lower expected value and can be seen as less desirable shots to take compared to close two pointers and three pointers.

## Assists

The last plot I would like to show illustrates the network of assist-shots:

```{r }
PbP.HOU <- subset(PbP, team == "HOU")
netdata.hou <- assistnet(PbP.HOU)
plot(netdata.hou, layout="circle")
```

This plot shows us the assists made by the team. The arrow shows the direction of the assist and the color shows how many assists the player made to the other player. For example, we can see that Chris Paul made a lot of assists to his teammates. He made most assists to Clint Capela shown by the dark red arrow.

There are other functions in the package, but these are the ones I wanted to share with you today. I think that these plots can be helpful for teams and opponents to learn about the team and trends in the way they play. I hope you find this as cool as I think it is, be on the lookout for more stuff soon!
