In my Spatial Statistics course, we learned how to perform analysis in three primary subfields of spatial statistics: geostatistics, lattice processes, and point processes. For this project, I performed a point process analysis on crime area in Manchester, a city in Greater Manchester, England.

## Introduction
During the cold winter months, people tend to stay at home more often. However, people tend go outside more often during the summer months and stay away from their homes for longer periods of times. This can possibly increase the likelihood of different types of crime, including burglaries since their are more opportunities to break into an unoccupied house for instance. For this project, it is investigated whether there is a difference in the spatial point patterns of burglaries in the summer and winter months in 2017. The chosen area of interest is Salford which is a sub-region in the greater Manchester area. The months that are used for the summer are June, July, and August. The months that are used for the winter are January, February, and December. There are 696 burglaries reported in the summer in Salford and 235 in the winter. These numbers show that there
are more than twice as many burglaries reported during the summer compared to the winter in Salford. The spatial map below shows the presence of some clusters in the point patterns, especially towards the northeast and northwest of Salford.

![Burglaries](/img/Burglaries.JPG)

## Assessment of Spatial Randomness
In order to assess Complete Spatial Randomness (CSR) for burglaries in the summer and winter months, the K and L-functions were used. The estimated K-functions for the summer and winter are both above the theoretical K-function under CSR over all spatial scales. This suggests that the locations of burglaries in the summer and winter are more clustered than a CSR process.

![K_Function_Summer](/img/K_Function_Summer.JPG)

![K_Function_Winter](/img/K_Function_Winter.JPG)

The estimated L-functions for the summer (figure 4) and winter (figure 5) are both above the zero line over all spatial scales. This also suggests that the process is more clustered than a CSR process.

![L_Function_Summer](/img/L_Function_Summer.JPG)

![L_Function_Winter](/img/L_Function_Winter.JPG)

## Comparison of Burglaries in the Summer and Winter
Before the intensities λ0 and λ1 of burglaries during the winter and summer were compared using the log relative risk, two separate first-order kernel-based intensity plots were created with a bandwidth of 0.05. Both the intensity plots for the summer and winter months show an increase of the intensity the more you move east. Thus, more events (burglaries) are expected the more you move east. When the two intensity plots are compared, it could be said that the plot for the summer months has larger areas with a higher intensity (green and yellow) compared to the plot for the winter months.

![Lambda_Summer](/img/Lambda_Summer.JPG)

![Lambda_Winter](/img/Lambda_Winter.JPG)

To compare the intensities of both plots, the log of their ratios was considered giving the log relative risk
using the following equation.

r(s) = ln(λ1(s)/λ0(s)) − ln(N1/N0) − ln(q1/q0)

Here, q0 and q1 are assumed to be equal to 1. λ1 is the intensity for the summer months and λ0 is the
intensity for the winter months. N1 is equal to 696 and N0 is equal to 235. The figure below shows the log relative risk
plot. It shows similar intensities between summer and winter burglaries around the green areas. The yellow
and orange areas suggest more clustering in the summer compared to the winter. The blue areas suggest more
clustering in the winter compared to the summer.

![Log_Relative_Risk](/img/Log_Relative_Risk.JPG)

The estimated log relative risk plot suggests that there are some areas that are close to zero but that there are also some areas that are significantly different from zero. In order to determine whether the spatial areas have values for the log relative risk that are significantly different from zero, a Monte Carlo test was performed. The figure below shows the locations that exceed the 95 percent Monte Carlo confidence interval. The red area shows the locations where the burglaries in the summer months appear to be more clustered than the winter months while the blue area shows the locations where the events in the winter months appear to be more clustered than the summer months. There significantly appears to be more clustering in the summer in the northwest area of Salford and more clustering in the winter in the northeast area of Salford. The other areas have similar
clustering between the winter and summer months.

![Monte_Carlo_Relative_Risk](/img/Monte_Carlo_Relative_Risk.JPG)

## Conclusion
The K and L-functions show that there is evidence of clustering of burglaries in both the summer and winter months. In addition, intensity plots for the summer and winter months show that there are more areas with higher intensities in the summer months compared to the winter months. This suggests that there may be more burglaries in the summer months. Lastly, the plots of the log relative risk and 95 percent Monte Carlo relative risk show that there is significantly more clustering in the summer months in the northwest area of Salford and more clustering in the winter in the northeast area of Salford.
