<header>
  <h1>Coffee Sales Project</h1>
  <p><em>Power BI dashboard to analyze coffee sales trends, patterns, and product performance.</em></p>
</header>

<h2>Problem Statement</h2>
<p>
  This dataset provides detailed records of coffee sales from a vending machine, created to support open data initiatives. 
  It helps analyze purchasing patterns, sales trends, and customer preferences for coffee products. 
  The dashboard visualizes sales patterns by month, time, and percentage, offering valuable insights into trends and behavior.
</p>
<p>
  In this project, we imported data from 
  <a href="https://www.kaggle.com/datasets/ihelon/coffee-sales" target="_blank">this Kaggle dataset</a> 
  into Power BI for analysis and visualization.
</p>

<h2>Objectives</h2>
<ul>
  <li>Analyze coffee sales patterns by month.</li>
  <li>Identify coffee sales <strong>trends by hour</strong>.</li>
  <li>Analyze the <strong>percentage distribution</strong> of coffee sales by <strong>coffee type</strong>.</li>
</ul>

<h3>Step 1: Load Data and Create Base Measure Table</h3>
<ol>
  <li>Load the CSV file into Power BI.</li>
  <li>Create a table named <code>BaseMeasure</code>: Home → Enter Data → Name → Create.</li>
  <li>Create a new measure using this DAX formula:</li>
</ol>

<pre><code>Total Coffee Sale = SUM('Coffee Sales'[money])</code></pre>

<p>Use this measure in a Card visual to show total coffee sales.</p>

<h3>Step 2: Create New Columns</h3>
<ol>
  <li>Create a <strong>Month</strong> column:</li>
</ol>

<pre><code>Month = FORMAT('Coffee Sales'[date], "MMMM")</code></pre>

<ol start="2">
  <li>Create an <strong>Hour</strong> column:</li>
</ol>

<pre><code>Hour = HOUR('Coffee Sales'[datetime])</code></pre>

<p>Use these in bar charts to display monthly sales trends.</p>

<h3>Step 3: Create Time Table</h3>
<ol>
  <li>Go to Modeling → New Table and use the following DAX formula:</li>
</ol>

<pre><code>Time = 
ADDCOLUMNS(
    CROSSJOIN(
        GENERATESERIES(1, 12, 1),
        DATATABLE("AM_PM", STRING, { {"AM"}, {"PM"} })
    ),
    "Hour", [Value],
    "Time Slot", 
        SWITCH(
            TRUE(),
            [Value] = 12 && [AM_PM] = "AM", "Midnight",
            [Value] >= 1 && [Value] < 6 && [AM_PM] = "AM", "Midnight - 6 AM",
            [Value] >= 6 && [Value] < 12 && [AM_PM] = "AM", "Morning",
            [Value] = 12 && [AM_PM] = "PM", "Noon",
            [Value] >= 1 && [Value] < 6 && [AM_PM] = "PM", "Afternoon",
            [Value] >= 6 && [Value] < 12 && [AM_PM] = "PM", "Evening"
        )
)</code></pre>

<p>This creates a Time table with four columns: AM_PM, Hour, Time Slot, and Value.</p>

<h3>Step 4: Create Relationships and Visuals</h3>
<ol>
  <li>In Model View, relate <code>Hour</code> in the Coffee Sales table to <code>Hour</code> in the Time table.</li>
  <li>Use a line chart: X-axis → Time Slot and Hour, Y-axis → money.</li>
</ol>

<h3>Step 5: Create Percentage Measure</h3>
<ol>
  <li>Create a new measure in BaseMeasure:</li>
</ol>

<pre><code>Coffee Sale % = 
DIVIDE(
    [Total Coffee Sale], 
    CALCULATE([Total Coffee Sale], ALL('Coffee Sales'[coffee_name]))
)</code></pre>

<ol start="2">
  <li>Use a bar chart with coffee_name on Y-axis and Coffee Sale % on X-axis.</li>
</ol>

<h3>Step 6: Add Slicers</h3>
<p>Add slicers for Total Coffee Sales, Date Interval, Cash Type, Date, and Month for better interactivity.</p>

<h2>End Results</h2>

<p align="center">
  <img src="images/coffee%20insight1.png" alt="Coffee Sales Overview" width="700">
  <br>
  <em>Figure 1: Power BI Dashboard Overview (no slicers applied)</em>
</p>

<p>
  Figure 1 shows total coffee sales of <strong>$97.8K</strong>. Top contributing products include <strong>Latte</strong>, 
  <strong>Americano with Milk</strong>, and <strong>Cappuccino</strong>, contributing <strong>25.3%</strong>, 
  <strong>22.7%</strong>, and <strong>15.7%</strong>, respectively. <strong>Espresso</strong> had the lowest contribution, 
  with a modest growth of <strong>2.4%</strong>.
</p>

<p>
  Sales peaked during the <strong>afternoon to evening hours (2:00 PM to 10:00 PM)</strong>, indicating high customer activity 
  in those time slots.
</p>

<p align="center">
  <img src="images/coffee%20insight2.png" alt="Month Wise Coffee Sales Trend" width="700">
  <br>
  <em>Figure 2: Coffee Sale Trend by Month</em>
</p>

<p>
  Figure 2 highlights a <strong>declining trend in sales</strong>, with a notable drop in <strong>February</strong>, 
  where sales decreased to approximately <strong>$2.8K</strong>.
</p>

<p>
  <h2>Key Decisions and Recommendations</h2>
<ul>Promote Bestsellers: Focus on Latte, Americano with Milk, and Cappuccino as they drive the majority of sales.</ul>

<ul>Improve Espresso Sales: Investigate reasons for low performance and consider promotions or recipe adjustments.</ul>

Target Peak Hours: Boost marketing and staffing between 2 PM and 10 PM, when sales are highest.</ul>

Address February Drop: Analyze and respond to the sales decline in February with targeted offers or campaigns.</ul>
</p>
