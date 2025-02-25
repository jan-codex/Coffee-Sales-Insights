<header>

<!--
  <<< Author notes: Course header >>>
  Include a 1280×640 image, course title in sentence case, and a concise description in emphasis.
  In your repository settings: enable template repository, add your 1280×640 social image, auto delete head branches.
  Add your open source license, GitHub uses MIT license.
-->

# Coffee Sales Project


</header>

<!--
  <<< Author notes: Step 1 >>>
  Choose 3-5 steps for your course.
  The first step is always the hardest, so pick something easy!
  Link to docs.github.com for further explanations.
  Encourage users to open new tabs for steps!
-->

## Problem Statement

This dataset provides detailed records of coffee sales from a vending machine, created by the dataset author to support open data initiatives. It is designed for analyzing purchasing patterns, sales trends, and customer preferences for coffee products. This dashboard visualizes sales patterns by month, time, and percentage, offering valuable insights into trends and customer behavior.

In this project, we imported data from https://www.kaggle.com/datasets/ihelon/coffee-sales a CSV file into Power BI for analysis and visualization.

**Objectives**
This project aims to:
1. Analyze coffee sales patterns by month.
2. Identify coffee sales trends by hour.
3. Determine coffee sales distribution by coffee type.


**Step 1**: 
1. Load the csv file in the Power BI.
2. Steps to create a BaseMeasure table: Home --> Enter Data --> Type the table name here and click on create.
3. ## Creating a New Measure in Power BI

## Creating a New Measure in Power BI  

To create a new measure in the **BaseMeasure** table, follow these steps:

i. Go to the **BaseMeasure** table.  
ii. Click on **"New Measure"** in the ribbon.  
iii. Copy and paste the following DAX code:

```DAX
Total Coffee Sale = SUM('Coffee Sales'[money])
```

Now, you can use this measure to calculate the total coffee sales in your Power BI reports.

