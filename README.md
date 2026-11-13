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
1. Data Quality - The biggest data-quality issue was inconsistent SKU identifiers. Our dataset contained 45 different SKUs, but after standardization, those represented only 20 actual product families. If we had not caught this, we would have treated different identifiers for the same product as separate products, which could have understated demand for individual items. For example, Pop-Tarts Strawberry appeared under four different SKUs. Although the total number of units remained 49,535 before and after consolidation, the way those sales were distributed across products changed. This mattered because our goal was to identify which products Walmart should stock before a hurricane. Without consolidating the SKUs, we could have underestimated demand for certain products and made weaker inventory recommendations.

2. ETL Trade-offs - One cleaning decision that could reasonably have gone the other way was removing duplicate and near-duplicate transactions. We chose to remove rows that appeared to represent repeated records, but some near-duplicates could have been legitimate purchases made at the same store and time. Keeping them would have avoided the risk of deleting real transactions, although it could also have inflated demand. Our Q5 comparison showed that cleaning had very little effect on the results. Monopoly's surge multiple changed from 3.584 to 3.592, while Playing Cards changed from 2.520 to 2.530. These comparisons reflect the overall cleaning process, not just duplicate removal. I would make the same decision again because the potential duplicate records were a small part of the dataset, and removing them did not materially change our conclusions.

3. Pipeline Trust - If someone handed me our notebook and asked whether the numbers were accurate, I would first check whether cleaning and merging the datasets changed the number of transactions or units unexpectedly. This is especially important because we standardized product identifiers, removed duplicates, and combined sales data with weather information. We already included a check showing that SKU consolidation preserved all 49,535 units, as well as a check that the weather join did not lose any dates.

4. Business vs Data - Our analysis showed that demand for several products increased significantly before Hurricane Helene. Monopoly sales increased 3.59 times, Playing Cards increased 2.53 times, and Roku Streaming Sticks increased 2.98 times relative to our baseline period. These findings support the idea that customers purchased more entertainment products before the storm. However, they do not prove that Walmart should permanently increase inventory or that the same pattern will occur during every hurricane. Our recommendation goes beyond the data because we are using one storm to suggest a future inventory strategy.

5. Team Process - One challenge outside the data itself was coordinating our work through a shared GitHub repository and notebook. Working on the same project required us to keep track of which version contained the latest changes and make sure that new analysis did not interfere with existing code. For the capstone, I would establish clearer ownership of individual sections and make sure changes are committed and pushed regularly. I would also have the team run the complete notebook before combining our work, so problems with execution order are caught earlier.

6. Carry Forward List - Improve team process and organizagtion. Create more reusable functions to streamline repetitive processes. Be more careful when interpreting correlations.

