---
layout: post
---

In my Spatial Statistics course, we learned how to perform analysis in three primary subfields of spatial statistics: geostatistics, lattice processes, and point processes. For this project, I performed a point process analysis on burglaries in the summer and winter months in Salford, a sub-region in the greater Manchester areas. The following packages were used for this project:

```
library(spatstat)
library(sf)
library(splancs)
```

## Introduction
During the cold winter months, people tend to stay at home more often. However, people tend go outside more often during the summer months and stay away from their homes for longer periods of times. This can possibly increase the likelihood of different types of crime, including burglaries since their are more opportunities to break into an unoccupied house for instance. For this project, it is investigated whether there is a difference in the spatial point patterns of burglaries in the summer and winter months in 2017. The chosen area of interest is Salford which is a sub-region in the greater Manchester area. The months that are used for the summer are June, July, and August. The months that are used for the winter are January, February, and December. There are 696 burglaries reported in the summer in Salford and 235 in the winter. These numbers show that there
are more than twice as many burglaries reported during the summer compared to the winter in Salford. The spatial map below shows the presence of some clusters in the point patterns, especially towards the northeast and northwest of Salford.

```
# Subset December, January, and February for winter months
winter_burglary <- crimes %>% subset(crime_type == "Burglary" & (month == 1 | month == 2 | month == 12))

# Subset June, July, and August for summer months
summer_burglary <- crimes %>% subset(crime_type == "Burglary" & (month == 6 | month == 7 | month == 8))

# Get points from the dataset that are in the right area (Salford)
winter_points <- pip(as.points(winter_burglary$long, winter_burglary$lat), Polypoints, out = FALSE)
colnames(winter_points) <- c("Longitude", "Latitude")
summer_points <- pip(as.points(summer_burglary$long, summer_burglary$lat), Polypoints, out = FALSE)
colnames(summer_points) <- c("Longitude", "Latitude")

# Create map
polymap(Polypoints, xlab = "Longitude", ylab = "Latitude")
pointmap(winter_points, col = "blue", add = TRUE, pch = 18, cex = 1)
pointmap(summer_points, col = "red", add = TRUE, pch = 20, cex = 1)
title("Burglaries in Salford")
legend("bottomright", col = c("blue", "red"), pch = c(18,20), legend = c("Winter", "Summer"))
```

![Burglaries](/img/Burglaries.JPG)

## Assessment of Spatial Randomness
One thing that can be tested is Complete Spatial Randomness (CSR) which tests whether points are scattered randomly or whether clusters are present. In order to assess CSR for burglaries in the summer and winter months, the K and L-functions were used. The estimated K-functions for the summer and winter are both above the theoretical K-function under CSR over all spatial scales. This suggests that the locations of burglaries in the summer and winter are more clustered than a CSR process.

```
kpts_summer <- khat(summer_points, Polypoints, h)
plot(h, kpts_summer, type = "l", main = "K-Function Summer", col = "red", ylab = "K")
lines(h, pi*h^2)
legend("topleft", col = c("black", "red"), lwd = c(1,1), legend = c("True K-Function", "Estimated K-Function"))

h <- seq(0.001,0.01,0.0005)
kpts_winter <- khat(winter_points, Polypoints, h)
plot(h, kpts_winter, type = "l", main = "K-Function Winter", col = "red", ylab = "K")
lines(h, pi*h^2)
legend("topleft", col = c("black", "red"), lwd = c(1,1), legend = c("True K-Function", "Estimated K-Function"))
```

![K_Function_Summer](/img/K_Function_Summer.JPG)

![K_Function_Winter](/img/K_Function_Winter.JPG)

The estimated L-functions for the summer and winter are both above the zero line over all spatial scales. This also suggests that the process is more clustered than a CSR process.

```
lpts_summer <- sqrt(kpts_summer/pi)-h
plot(h, lpts_summer, type = "l", ylim = c(0,0.01), main = "L-Function Summer", col = "red", ylab = "L")
abline(h=0)
legend("topleft", col = c("black", "red"), lwd = c(1,1), legend = c("Zero Line", "Estimated L-Function"))

lpts_winter <- sqrt(kpts_winter/pi)-h
plot(h, lpts_winter, type = "l", ylim = c(0,0.01), main = "L-Function Winter", col = "red", ylab = "L")
abline(h=0)
legend("topleft", col = c("black", "red"), lwd = c(1,1), legend = c("Zero Line", "Estimated L-Function"))
```

![L_Function_Summer](/img/L_Function_Summer.JPG)

![L_Function_Winter](/img/L_Function_Winter.JPG)

## Comparison of the Intensity Burglaries in the Summer and Winter
Before the intensities λ0 and λ1 of burglaries during the winter and summer were compared using the log relative risk, two separate first-order kernel-based intensity plots were created with a bandwidth of 0.05. Both the intensity plots for the summer and winter months show an increase of the intensity the more you move east. Thus, more events (burglaries) are expected the more you move east. When the two intensity plots are compared, it could be said that the plot for the summer months has larger areas with a higher intensity (green and yellow) compared to the plot for the winter months.

```
b <- 0.05
lamnx <- 50
lamny <- 50

# Create kerne based intensity plot
w_lamest <- kernel2d(winter_points, Polypoints, b, lamnx, lamny)
image(w_lamest$x, w_lamest$y, w_lamest$z, asp = 1, col = topo.colors(50), main = "Burglaries Winter Lambda - Bandwidth = 0.05", xlab = "Longitude", ylab = "Latitude")
polymap(Polypoints, add = TRUE)
contour(w_lamest$z, x = w_lamest$x, y = w_lamest$y, add = TRUE)

s_lamest <- kernel2d(summer_points, Polypoints, b, lamnx, lamny)
image(s_lamest$x, s_lamest$y, s_lamest$z, asp = 1, col = topo.colors(50), main = "Burglaries Summer Lambda - Bandwidth = 0.05", xlab = "Longitude", ylab = "Latitude")
polymap(Polypoints, add = TRUE)
contour(s_lamest$z, x = s_lamest$x, y = s_lamest$y, add = TRUE)
```

![Lambda_Summer](/img/Lambda_Summer.JPG)

![Lambda_Winter](/img/Lambda_Winter.JPG)

To compare the intensities of both plots, the log of their ratios was considered giving the log relative risk using the following equation.

r(s) = ln(λ1(s)/λ0(s)) − ln(N1/N0) − ln(q1/q0)

Here, q0 and q1 are assumed to be equal to 1. λ1 is the intensity for the summer months and λ0 is the
intensity for the winter months. N1 is equal to 696 and N0 is equal to 235. The figure below shows the log relative risk plot. It shows similar intensities between summer and winter burglaries around the green areas. The yellow and orange areas suggest more clustering in the summer compared to the winter. The blue areas suggest more clustering in the winter compared to the summer.

```
r <- log(s_lamest$z/w_lamest$z) - log(nrow(summer_points)/nrow(winter_points))
image(s_lamest$x, s_lamest$y, r, asp = 1, col = topo.colors(50), main = "Log Relative Risk - Bandwith = 0.05", xlab = "Longitude", ylab = "Latitude")
polymap(Polypoints, add = TRUE)
contour(r, x = s_lamest$x, y = s_lamest$y, add = TRUE)
```

![Log_Relative_Risk](/img/Log_Relative_Risk.JPG)

The estimated log relative risk plot suggests that there are some areas that are close to zero but that there are also some areas that are significantly different from zero. In order to determine whether the spatial areas have values for the log relative risk that are significantly different from zero, a Monte Carlo test was performed. The figure below shows the locations that exceed the 95 percent Monte Carlo confidence interval. The red area shows the locations where the burglaries in the summer months appear to be more clustered than the winter months while the blue area shows the locations where the events in the winter months appear to be more clustered than the summer months. There significantly appears to be more clustering in the summer in the northwest area of Salford and more clustering in the winter in the northeast area of Salford. The other areas have similar
clustering between the winter and summer months.

```
# 696 summer and 235 winter
r_samp <- array(0, dim = c(50,50,200))
b <- 0.05
lamnx <- 50
lamny <- 50

# Loop to randomly assign burglaries to each location and then calculate r(s)
for (i in 1:200){
  # Randomly assign summer and winter burglaries to one of each location
  samp <- rbind(summer_points, winter_points)
  index <- sample(1:nrow(samp),696,replace = FALSE)
  summer <- samp[index,]
  winter <- samp[-index,]
  
  # Calculate r(s)
  winter_lamest <- kernel2d(winter, Polypoints, b, lamnx, lamny)
  summer_lamest <- kernel2d(summer, Polypoints, b, lamnx, lamny)
  r_samp[,,i] <- log(summer_lamest$z/winter_lamest$z) - log(nrow(summer)/nrow(winter))
}

# Finder lower 2.5 and upper 97.5 quantile
quantiles_rsamp05 <- apply(r_samp, 1:2, quantile, probs = 0.025, na.rm = TRUE)
quantiles_rsamp95 <- apply(r_samp, 1:2, quantile, probs = 0.975, na.rm = TRUE)

# Find which values are less than 2.5 or more than 97.5 quantile
sig1 <- r < quantiles_rsamp05
sig2 <- r > quantiles_rsamp95

# TRUE if value is less than 2.5 or more than 97.5 quantile, else make NA
r_keep1 <- ifelse(sig1 == TRUE,r,NA)
r_keep2 <- ifelse(sig2 == TRUE,r,NA)

# Create plot
image(s_lamest$x, s_lamest$y, r_keep1, asp = 1, col = "blue", main = "Locations Exceeding 95% MC CI", xlab = "Longitude", ylab = "Latitude")
image(s_lamest$x, s_lamest$y, r_keep2, asp = 1, col = "red", main = "Locations Exceeding 95% MC CI", add = TRUE)
polymap(Polypoints, add = TRUE)
legend("bottomright", col = c("red", "blue"), pch = c(20,20), legend = c("Summer more Clustered", "Winter more Clustered"))
```

![Monte_Carlo_Relative_Risk](/img/Monte_Carlo_Relative_Risk.JPG)

## Conclusion
The K and L-functions show that there is evidence of clustering of burglaries in both the summer and winter months. In addition, intensity plots for the summer and winter months show that there are more areas with higher intensities in the summer months compared to the winter months. This suggests that there may be more burglaries in the summer months. Lastly, the plots of the log relative risk and 95 percent Monte Carlo relative risk show that there is significantly more clustering in the summer months in the northwest area of Salford and more clustering in the winter in the northeast area of Salford.
