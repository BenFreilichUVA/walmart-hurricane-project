# Reflection: Walmart Hurricane Analytics


Each question is answered in at least one full paragraph. The author of each answer is noted under its heading.

---

## 1. Data Quality Impact

*Written by Ben Freilich*

Describe a specific data quality issue you encountered in the supplied data. How did your cleaning decision change the outcome of your analysis? What would have happened if you had not caught it?

The most important data quality issue encountered in the supplied data was the same product living under multiple SKUs. Strawberry Pop-Tarts appeared under four seperate SKUs (PT-12, SKU#459812, POPTART-STRAW, and PT_STRAWBERRY, which would have heavily skewed the results on its own, but every other product in the catalog was split across at least two different SKUs as well. We were able to confirm all four Pop-Tart SKUs were the same product because their sales used similar product names, they all sold for the same price, and they were all in the breakfast category. We built a mapping table that helped combined all of the SKUs into an individual product out of 20 different ones, and checked that no transactions were created, duplicated, or deleted as a result of this mapping. Making this decision helped change our answer to which item sold the most before the storm. Looking at the raw data and grouping it by SKUs, the data was off, with the two bottled water SKUs as the top sellers during the surge week, and the best Pop-Tarts SKU ranked third at about 103 units a day. After consolidation, Pop-Tarts sold roughly 377 units a day and took the spot of number one product ahead of water, which ended up at 320 after consolidation. This is still much higher than it was under the individual SKUs, but we now have an accurate picture of which product sold the most. A buyer who didn't see the consolidation and only ordered one of the SKUs numbers of Pop-Tarts would've undershot the total needed by almost three quarters, which would have created large problems. Because we consolidated the SKUs, we are able to accurately tell the managers which products sold the most, and be aware of which ones to stock the most of when the next storm comes around.

---

## 2. ETL Trade-offs

*Written by Ben Freilich*

You made choices about how to standardize SKUs, handle missing timestamps, and join weather data. Pick one decision and explain: what alternative approach could you have taken, and how might it have changed your results?

One decision that we took that an alternative person could have dealt with different was the way we handled transactions without a timestamp. After we removed duplicates, about 3.5% of the transactions had a blank timestamp. We kept the transactions without a timestamp in our main cleaned table but left them out of the dated table used for daily counts, since a sale without a date cannot reliably be placed into the baseline or the surge window. One alternative was to fill in the missing dates. We decided against this because we did not have a defensible argument for what dates should be used while filling it in. The transaction IDs were not placed in time order, so there was not an easily estimate that could be made from the raw data itself. Any date filled in would simply be an invented guess, and it could end up disrupting the actual data trends despite not having any factual basis. The other alternative was to drop the transaction rows without a date entirely from all of the tables. This would have made no difference to our reported results and the recommendations we made to management, as all presented numbers came directly from dated sales. However, it still would have thrown away real sales that could count towrad store or product totals that do not depend on timing. Before excluding them from the daily counts, we checked that the blank timestamps were spread evenly, at between roughly 3 and 4% of sales in all stores and categories. Because no store or category disproportionately lost more transactions that the others, leaving them out lowered the daily counts by about the same share and did not meaningfully change any percentage increases or rankings. We believe our choice made the most sense, as we kept as much data as possible without inserting estimations that could have hurt the accuracy of our results.

---

## 3. Pipeline Trust

*Written by Tommy Snyder*

The Walmart CDO argued that the biggest risk is not the model — it is the pipeline. Based on your experience in this project, do you agree or disagree? What was the most fragile part of your data pipeline?

After immersing ourselves in this project, we do believe the pipeline to be the problem when a few important characteristics are not met. Confirming that all data is clean and correct is the most important factor when determining if the pipeline or the model is the biggest risk. Ben handled all SKU consolidation, but speaking from experience working with the API and weather data, there is many things that could have gone wrong within the pipeline without careful decision making. One important example of this was struggling with the different timezones and confirming them all to be measured the same so there would be no difference in dates and all weather and sales data was combined correctly. If this was done improperly, which it was at first, the sales data would be completely wrong and not give valuable insight to Walmart decision makers. On the other hand, the same thing can be said about the models, with user error, specifically on the first weather correlation graph in our case, posing a massive risk to insightful analysis. However when considering all of these possible human errors and the different problems we ran into, I would agree that the biggest risk is the pipeline. Feeding a model the wrong data can make a graph and calculation look perfectly correct, yet it actually is false due to the wrong data from the pipeline. User error and bad graph decisions are far easier to fix than major data issues that can look deceptively correct. 

---

## 4. Business vs. Data

*Written by Tommy Snyder*

For Question 5 (board games), your team had to make a recommendation with imperfect data. How did you weigh statistical evidence against business risk? Would you have decided differently with more time or more data?

Weighing statistical evidence and business risk is the most prominent issue regarding business decision making, a concept seen throughout business and economics alike. What makes something statistically significant versus economically significant? These decisions come down to judgment and weighing real life risks. When considering making a board game recommendation based on imperfect data, it was incredibly important to consider the effects of the decisions, both positively and negatively, as possibilities. When considering the increased costs of stocking extra board games and the possibility of not being able to fulfill these additional expected purchases, the smart business decision considering all data was to expect a jump due to the evidence of a 250% increase in sales, but also acknowledge the possibility that this data is misleading. Ben came to this conclusion and I fully agree with it as it makes the most sense when considering possible costs and the limited upside that stocking to a 200+% increase truly provides a Walmart in preparation of massive storms. With more storm data from past surges similar to ours, we could have analyzed if this is a common surge in board game sales, easing out fears of a possible drawdown in the next occurrence. It also could have confirmed out concerns that we should hedge against fully expecting that large of a surge every time a massive storm rolls in. More time and data could have provided more insight into either side of our decision, but definitely made us more confident either way.


---

## 5. Team Collaboration

*Written by both*

How did your team divide the work? What would you do differently if you had another week? What was the most valuable skill each team member contributed?

We divided the work by splitting the questions with Ben doing 3 and Tommy doing 2 to best even out the workload. We also split up the big data cleaning/calling processes to ensure that we each had a strong understand of the back ends of our data. Ben working on SKU consolidation and store data while Tommy focused on the API and Weather data. This worked very well together and we had great chemistry and communication throughout the entire project to ensure an even workload and a timely finish to the project. I (Tommy) really enjoyed working with Ben and the only thing I would have changed would have been taking a deeper dive into the SKU consolidation process as I know that was very difficult and believe Ben would have done a great job explaining that to me in depth as it is one aspect of the class I still struggle with. I (Ben) enjoyed working with Tommy and felt we had an even work split with both of us communicating well. The one thing I would have done differently was working a little bit closer on the API weather pulling. This is something that interests me personally and I still haven't fully grasped, and being closer to it during the process may have helped me learn a little bit more.
