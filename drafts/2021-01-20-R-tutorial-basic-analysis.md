---
layout: post
---

R is a statistical language that I have used a lot in my undergraduate and graduate classes. This post will be a tutorial that walks you through some basic analysis that can be done in R. For this tutorial, I will be using the dataset mtcars that is already built into R. If you would like to learn more about the dataset, you can access information in R Help. To do this, you can enter the following into your R command:

```
?mtcars
```

![rhelp](/img/rhelp.JPG)

R Help can also be used to learn about new functions. I find it extremely helpful and use it all the time when I'm not sure how to use a function in my code.

## Structure of the Dataset
One of the first things I like to do when I have a new dataset, is taking a look at its structure. This can be done with the following command:

```
str(mtcars)
```

![str](/img/str.JPG)

You can see that this command shows us that our dataset is a dataframe. We can also see that there are 32 observations in the dataset and 11 variables. The output shows you a short preview of that variables and tells you what type of variables we have. In this dataset, we have 11 numeric variables. This is a fairly small dataset, but you can imagine that this output can be helpful if you have a large dataset.

Next, I often like to take a look at the dataset itself. This can be challenging with a large dataset, so instead of looking at all of it, I often like to look at just a small part of the dataset. We can take a look at the first 6 observations using this command line:

```
head(mtcars)
```

![head](/img/head.JPG)

If we want to look at the last 6 observations in the dataset instead, we can use this command:

```
tail(mtcars)
```

![tail](/img/tail.JPG)

You may want to look at more or less than 6 observations. You can do this by adding one more part to the command:

```
head(mtcars, 10)
```

Instead of the first 6 observations, we will now be shown the first 10 observations in the dataset.

## Basic Exploratory Analysis
Now it's time to take a closer look at the data. One thing I often like to do, is creating a summary output of my dataset. I can do this using the summary command:

```
summary(mtcars)
```

![summary](/img/summary.JPG)

You can see that R gives us the minimum value, 1st quantile, median, mean, 3rd quantile, and maximum value of all numeric variables. If any missing data is present, the summary command will show you this as well as NA. There are a few variables for which the summary statistics don't make as much sense. An example is the variable cyl that can only have 3 possible values: 4, 6, and 8. For these types of variables, we can create a contingency table:

```
table(mtcars$cyl)
```

![table](/img/table.JPG)

In my code, you can see that I used the dollar sign to specifiy I only want to use the cyl column in my dataset to make a table. 
