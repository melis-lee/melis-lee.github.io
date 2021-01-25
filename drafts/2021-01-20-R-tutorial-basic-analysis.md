---
layout: post
---

## Overview

R is a language that is used for statistical computing. This post will be a tutorial that walks you through some basic analysis that can be done in R. I will show you how to look at the structure of your dataset, do some basic exploratory data analysis, and subset you data. For this tutorial, I will be using the dataset mtcars that is already built into R. If you would like to learn more about the dataset, you can access information in R Help. To do this, you can enter the following into R:

```
?mtcars
```

![rhelp](/img/rhelp.JPG)

R Help can also be used to learn about functions. I find R Help extremely helpful and I use it all the time when I'm not sure how to use a function in my code.

## Structure of the Dataset

One of the first things I like to do when I have a new dataset, is taking a look at its structure. This can be done with the following command:

```
str(mtcars)
```

![str](/img/str.JPG)

You can see that this command shows us that our dataset is a dataframe. We can also see that there are 32 observations in the dataset and 11 variables. The output shows you a short preview of the variables and tells you what type of variables we have. In this dataset, we have 11 numeric variables. This is a fairly small dataset, but you can imagine that this output can be helpful if you have a large dataset.

Next, I often like to take a look at the dataset itself. This can be challenging with a large dataset, so instead of looking at all of it, I often like to look at just a small part of the dataset. We can take a look at the first 6 observations using this command:

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

Now it's time to take a closer look at the data. One thing I often like to do, is creating a summary output of my dataset. I can do this using the summary function:

```
summary(mtcars)
```

![summary](/img/summary.JPG)

You can see that R gives us the minimum value, 1st quantile, median, mean, 3rd quantile, and maximum value of all numeric variables. If any missing data is present, the summary command will show you this as well. R calls missing values NA. There are a few variables for which the summary statistics don't make much sense. An example is the variable cyl that can only have 3 possible values: 4, 6, and 8. For these types of variables, we can create a contingency table:

```
table(mtcars$cyl)
```

![table](/img/table.JPG)

In my code, you can see that I used the dollar sign to specifiy I only want to use the cyl column in my dataset to make a table. We can make our table even more specific by adding another variable:

```
table(mtcars$cyl, mtcars$gear)
```

![table2](/img/table2.JPG)

In this table, the rows correspond to the options for cyl and the columns correspond to the options for gear. So we can say that 12 cars have cyl = 8 and gear = 3. We can add a third dimension to the table by adding one more variable:

```
table(mtcars$cyl, mtcars$gear, mtcars$vs)
```

![table3](/img/table3.JPG)

The table is now split into two parts: vs = 0 and vs = 1. There is a separate contingency table for the two parts. Here we can say that 2 cars have vs = 0, cyl = 6, and gear = 4.

We have seen that we can get some basic summary statistics and create tables to learn more about the variables. However, there are many more statistics you may be interested in calculating such as the standard deviation. It's pretty easy to calculate the standard deviation for a variable:

```
sd(mtcars$mpg)
```

If you would like to round the values to a certain number of decimals, you can do this using the round function. I'm rounding to 3 decimals in the example below:

```
round(sd(mtcars$mpg), 3)
```

If you want to calculate the standard deviation of all variables in the dataset, you could do this one by one using the command above. However, this can be tedious to do for all 11 variables in this dataset. Imagine how long it could take if you have an even large dataset. Luckily, there is a function in R that can do this for you called sapply. To use this function, you need to include the name of the dataset, and what function you would like to apply it to. We used sd as the function, but there are many other functions you could use such as range, mean, and median.

```
sapply(mtcars, sd)
```

![sapply](/img/sapply.JPG)

## Subsetting Data

Sometimes, I like to subset my dataset if I only want to look at specific parts of the data. There are multiple ways to do this in R, but in this tutorial I will show you how to subset using brackets. In the brackets you're able to specifiy the indices of the rows and columns you would like to keep or remove. The first index is for rows, and the second index is for columns. The code below only takes the first row of the dataset:

```
mtcars[1,]
```

![subset1](/img/subset1.JPG)

If you only want the first column, you can do this in two different ways. You can use "1" to specifiy we want to first column. However, since we know the name of the column, we could also use "mpg" to specify we want to include that column. This could especially be helpful if you have a lot of columns in your dataset and don't want to count which column you want to keep.

```
mtcars[,1]
mtcars[,"mpg"]
```

In some cases, you may want to keep all variables in your dataset except one. In this example, let's say we want to keep all variables except the first one. There are two ways we could code this:

```
mtcars[,-1]
mtcars[,2:11]
```

The first line tells R to remove the first variable. The second line tells R to keep the second till the eleventh variable. One important thing to keep in mind when you subset data, is that it won't change anthing in your original dataset. If you would like to save your subset as a new dataset, you need to assign it a name which you can do as follows:

```
new_data <- mtcars[,2:11]
```

When you assign a name to a variable, or a new dataset in this case, the rule is that it has to start with a letter. After that you can have letters, nummbers, an underscore, or period. R is case sensitive so you need to keep that in mind when you assign names. Lastly, special characters are not allowed in variable names. In the example above, we wanted to keep variables 2 to 11. But what if we don't want to keep consecutive variables? Fortunately, this can be done pretty easily as follows:

```
mtcars[1:15 ,c(1,3,5)]
```

This code tells R that we want to keep the first, third, and fifth variable for the first 15 observations in the dataset. 

## Subsetting with Logical Operators

The last topic I would like to talk about in this post combines what we learned about subsetting with logical operators. In the previous section, all subsetting was done based on certain rows or columns we wanted to keep. But in many cases, we want to subset based on certain conditions. For example, for the variables cyl, we may only be interested in cars that have cyl = 6. We could code that as follows:

```
mtcars[mtcars$cyl == 6,]
```

This line tells R that we want to keep all rows that have the value 6 for cyl. Another thing that we may be interested in, is all cars that have an mpg greater than 20. We use the > symbol for greater than:

```
mtcars[mtcars$mpg > 20, ]
```

We can also combine logical operators. For example, we may be interested in keeping all cars that have hp less than or equal to 100, and am equal to 1:

```
mtcars[mtcars$hp <= 100 & mtcars$am == 1,]
```

R will only return the cars for which both conditions are true. If one of the conditions is false, R won't return that observation. What if we want R to return the observations if either condition is true? We can tell R to do this as follows:

```
mtcars[mtcars$hp <= 100 | mtcars$am == 1, ]
```

Now, if either or both conditions are true, R will return the observation. The last type of logical operator I would like to show you is used when you want to tell R you want to include observations that do not have a certain value.

```
mtcars[mtcars$carb != 4,]
```

This line tells R to keep all observations that do not have a value of 4 for carb.

In this tutorial, I showed you how to do some very basic data analysis on your dataset. We created summaries, tables, and also learned how to create different subsets. I hope that this helped you get started with your dataset, even if you have never worked with R before.
