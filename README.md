# Team DannyTuran
Course: DS2002, Fall 2026
Project notebook: [`notebooks/2026_10_30_—_Midterm_Progress_—_Lab.ipynb`]

Project overview
This project examines how purchasing patterns changed across Walmart stores in Florida before Hurricane Helene in September 2024. We cleaned inconsistent transaction records, standardized product identifiers, joined daily sales with historical weather observations, and assessed whether unusual pre-hurricane demand was a real signal or a data artifact. The goal is to inform inventory decisions without overstating what one storm can prove.

How to run
1. Clone or download this repository and open the repository root in VS Code or Jupyter.
2. Use Python 3 with pandas, numpy, matplotlib, requests, ipykernel, and IPython installed.
3. Open the completed notebook. Keep the data folder in the repository root because the notebook reads files using paths
4. Read the displayed cleaning log, tables, charts, and written interpretations in Q1–Q5.

ETL and Data Cleaning
The source contained 25,562 rows. After cleaning, 25,372 rows remained, a reduction of 190 rows. The pipeline standardized store IDs and category labels, parsed five timestamp formats, converted prices and quantities to numeric values, removed exact and selected near-duplicate transactions, and excluded negative-quantity rows from the purchase-demand analysis. Product codes were mapped from 45 distinct SKUs to 20 product families using the supplied product catalog. The total remained 49,535 units before and after consolidation.

Reflection
1. Data Quality - The biggest data-quality issue the missing store locations. Of the 12 Walmart stores in our dataset, one store, Tallahassee (FL-619), did not have usable latitude and longitude information. As a result, our geographic analysis only included 11 stores instead of all 12. This mattered because we were trying to determine whether stores closer to Hurricane Helene experienced larger increases in demand. Our analysis found a correlation of 0.426 between distance from the hurricane and demand increases, which is somewhat unexpected because we initially assumed that the stores closer to the storm would experience larger surges in comparison. Since one store was excluded, we cannot be certain whether including it would have strengthened or weakened that relationship. For the capstone, I would make sure to check for missing geographic information earlier and investigate whether missing values can be recovered before excluding observations. This would strengthen our conclsions significantly as we account for all known information. 

2. ETL Trade-offs - One cleaning decision where we could have taken a different approach was combining different SKUs into the same product family. Our dataset originally contained 45 SKUs, which we consolidated into 20 product families. An alternative would have been to keep each SKU separate, since different identifiers could represent different product variations or package sizes. This would not have changed our total of 49,535 units sold, but it would have spread those sales across 45 categories instead of 20, making demand for individual products appear smaller. For example, Pop-Tarts Strawberry appeared under four different SKUs, which could have made us underestimate its overall demand. I would make the same decision again because our goal was to understand which products experienced increased demand before the hurricane, and combining equivalent SKUs gave us a clearer picture of customer purchasing behavior.

3. Pipeline Trust - We would first check whether the weather data and sales data were matched to the correct dates. Since we used an external weather API and combined it with our transaction data, a mistake in the date alignment could significantly change our results. Our same-day correlation was 0.39, while the two-day lead correlation was 0.82, showing how much the timing matters. We already checked that the datasets joined successfully, but for the capstone I would add a more detailed check to verify that the dates and time zones were aligned correctly before calculating correlations.

4. Business vs Data - One area where our recommendation went beyond what the data strictly proved was suggesting that Walmart increase inventory before future hurricanes. Our analysis showed that demand for certain products increased significantly, including a 3.59-fold increase for Monopoly Board Games and a 2.53-fold increase for Playing Cards. However, increased demand does not necessarily mean that stocking more of these products would be profitable. We did not analyze the costs of holding additional inventory, profit margins, or the potential losses from unsold products. While our findings suggest an opportunity to increase sales during hurricane preparation periods, we cannot determine the ideal amount of additional inventory from our data alone. I would recommend testing a smaller inventory increase first and evaluating the financial results before making a larger investment.

5. Team Process - One challenge outside the data itself was coordinating our work through a shared GitHub repository and notebook. Working on the same project required us to keep track of which version contained the latest changes and make sure that new analysis did not interfere with existing code. For the capstone, I would establish clearer ownership of individual sections and make sure changes are committed and pushed regularly. I would also have the team run the complete notebook before combining our work, so problems with execution order are caught earlier.

6. Carry Forward List - Improve team process and organizagtion. Create more reusable functions to streamline repetitive processes. Be more careful when interpreting correlations.

