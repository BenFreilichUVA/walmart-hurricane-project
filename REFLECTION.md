# Reflection: Walmart Hurricane Analytics


Each question is answered in at least one full paragraph. The author of each answer is noted under its heading.

---

## 1. Data Quality Impact

*Written by*
Describe a specific data quality issue you encountered in the supplied data. How did your cleaning decision change the outcome of your analysis? What would have happened if you had not caught it?

The most important data quality issue encountered in the supplied data was the same product living under multiple SKUs. Strawberry Pop-Tarts appeared under four seperate SKUs (PT-12, SKU#459812, POPTART-STRAW, and PT_STRAWBERRY, which would have heavily skewed the results on its own, but every other product in the catalog was split across at least two different SKUs as well. We were able to confirm all four Pop-Tart SKUs were the same product because their sales used similar product names, they all sold for the same price, and they were all in the breakfast category. We built a mapping table that helped combined all of the SKUs into an individual product out of 20 different ones, and checked that no transactions were created, duplicated, or deleted as a result of this mapping. Making this decision helped change our answer to which item sold the most before the storm. Looking at the raw data and grouping it by SKUs, the data was off, with the two bottled water SKUs as the top sellers during the surge week, and the best Pop-Tarts SKU ranked third at about 103 units a day. After consolidation, Pop-Tarts sold roughly 377 units a day and took the spot of number one product ahead of water, which ended up at 320 after consolidation. This is still much higher than it was under the individual SKUs, but we now have an accurate picture of which product sold the most. A buyer who didn't see the consolidation and only ordered one of the SKUs numbers of Pop-Tarts would've undershot the total needed by almost three quarters, which would have created large problems. Because we consolidated the SKUs, we are able to accurately tell the managers which products sold the most, and be aware of which ones to stock the most of when the next storm comes around.

---

## 2. ETL Trade-offs

*Written by*

To be written.

---

## 3. Pipeline Trust

*Written by*

To be written.

---

## 4. Business vs. Data

*Written by*

To be written.

---

## 5. Team Collaboration

*Written by both*

To be written.
