---
layout: post
---

Let's say you're interested in finding out the currencies for a few cities you would like to visit. You put the cities in an Excel Sheet with the countries next to it. Of course you could Google the currencies one by one but this is time consuming, especially since it cane be done a lot quicker with a function in Excel.

![Cities](/img/Cities.JPG)

In this post, I am going to show you how to use the function Vlookup in Excel to find the currencies for each of the cities above. Before we can use the Vlookup function, we need to have some kind of look-up table that we can use to find the currencies for all countries. I found a table online on this [website]( https://www.downloadexcelfiles.com/wo_en/download-excel-file-list-currencies-native-languages-countries#.YRlTWIhKhaQ) that has the currencies listed for each country in an Excel Sheet. 

![Currencies](/img/Currencies.JPG)

Our goal is to use that table to fill in the currencies for our cities which can be done using Vlookup. The description that Excel gives for what the Vlookup function does is that it looks for a value in the most left column of your table and then returns a value in the same row from a column you specify. The table must be sorted in ascending order. So in our example, the function is going to look for the country name (the most left column of our table) and it will then return the value of the same row that we specify, which will be the name of the currency.

So, how can we actually use this function? There are 3 things the function needs to know from us: the value we want to look up, the table where we want to look for the value, and the column number in the table that contains the value that we want to return. In our example, the first city listed is Rio de Janeiro, a city in Brazil. Thus, we want our function to look up "Brazil", which is cell B2. We specifically want the table to look it up in our Currencies tab which has 2 columns - A and B. Then, the last thing Excel wants to know from us is which column to return from that table. We want the column with the currencies to be returned, which is column 2. Our function looks as follows:

![Brazil](/img/Brazil.JPG)

When we fill in this function for all our cities, our table look as follows. The currencies are filled in for all our cities. This took me less than a minute which is a lot quicker than looking up the currencies for the cities one by one!

![Cities_Currencies](/img/Cities_Currencies.JPG)
