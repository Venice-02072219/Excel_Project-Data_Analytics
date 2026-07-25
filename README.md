# 🌍 World Population & Demographics Analytics Dashboard

## 📋 Project Overview
This project features an interactive **World Population & Demographics Dashboard** built in Microsoft Excel. It leverages **Power Query** to programmatically extract, clean, and transform live web-based global population data. 

By automating the ETL (Extract, Transform, Load) pipeline, this dashboard eliminates manual data collection. It delivers actionable, near-real-time demographic insights that help businesses mitigate expansion risks, optimize supply chains, and execute hyper-targeted marketing campaigns.

## ❓ Core Business Questions Addressed

*   **Market Entry:** Which global regions or countries exhibit the highest population growth velocity for potential market expansion?
*   **Resource Allocation:** How do shifting global age demographics impact long-term labor availability and consumer demand forecasting?
*   **Risk Management:** Which highly populated urban centers face the steepest population density risks or declines?
*   **Targeting Efficiency:** Where are the optimal geographic clusters for localized product marketing based on current population sizes?

### 📸 Dashboard Preview
<img width="1402" height="880" alt="image" src="https://github.com/user-attachments/assets/771b0706-4245-401f-b775-30dd640c5248" />
*Figure 1: Interactive view of the World Population Dashboard built in Excel.*

---

## 🛠️ Excel Skills Used

* The following Excel skills were utilized for analysis:

*   **📊 Pivot Tables
*   **📈 Pivot Charts
*   **🧮 DAX (Data Analysis Expressions)
*   **🔍 Power Query
*   **💪 Power Pivot

---

## 🌍 World Population Dataset

* This dashboard is connected to (https://www.worldometers.info/world-population/) using Power Query ("Get Data > From Web") which allowed me to identify HTML tables, and transform the data before loading. The dataset provides real-time, live-updating data on global population. Utilizing data primarily from the United Nations, it also features comprehensive breakdowns by region and country along with historical trends and future population projections.

---

## 1️⃣ Which global regions or countries exhibit the highest population growth velocity for potential market expansion?

# 🔍 Skill: Power Query (ETL)

*📥 Extract

* Two queries were created:
  * I first used Power Query("Get Data > From Web") to connect to (https://www.worldometers.info/world-population/) which allowed me to identify HTML tables and transform the data before loading.
  * I needed a list of the "Countries" with their corresponding "Region" but there's no table in the current dataset that supports it. So, I connected to https://britannica.com/topic/list-of-countries-1993160. 

# 🔄 Transform

* Then, I transformed each query by changing column types, removing unnecessary columns, cleaning text to eliminate specific words or characters.

* 📊 Population by Country and World Population by Region

* When I was trying to change the data format of the columns in Population by Country and World Population by Region, there were Non-Standard Dash Characters in the Yearly Change, Net Change and Migrants (net) column. Imported text data sometimes uses an en-dash (–) or em-dash (—) instead of a standard hyphen-minus character (-). The thousand separator which is a comma (,) also became a problem. So, I replaced the em-dashes (—) with the standard hyphen-minus character (-) and removed the commas in Yearly Change column and changed the data format to Percentage. I did the same to Net Change and Migrants(net) column and changed the data format to whole number.

  <img width="322" height="540" alt="image" src="https://github.com/user-attachments/assets/141e95d8-225e-41f9-9bc6-1360c9086afa" />

  <img width="322" height="542" alt="image" src="https://github.com/user-attachments/assets/ee0e4a14-5904-46a0-a26f-8a9eee48e9c7" />

* The Urban Pop % column is available in the Population By Country and World Population by Region table. 

* To get the rural population percentage in the Population By Country table, I created the DAX formula below. This is because there were some rows which has 0% or no data in Population by Country'[Urban Pop %]) column.

  =IF (
    AVERAGE ( 'Population by Country'[Urban Pop %] ) > 0,
    1 - AVERAGE ( 'Population by Country'[Urban Pop %] ),
    BLANK ()
  )

* I also added the DAX formula below to World Population by Region table.There were no rows with 0% or no data.

  =1 - AVERAGE('World Population by Region'[Urban Pop %]) 
 
* 📊 Region Lookup

* I want the users to have the capability to filter the countries by Region but there's no column nor tables to support it. To create a list of countries with their corresponding region, I connected to https://www.britannica.com/topic/list-of-countries-1993160. However, the list is alpahabetically separated. Hence, I created a "Region Lookup" by appending the queries to create a single list.

  <img width="1475" height="597" alt="image" src="https://github.com/user-attachments/assets/26dba270-0755-4d6d-8cd9-7a276e99fc20" />

* Then, I used Power Pivot for data modelling. In The Diagram view, I connected the Region Lookup table to Population By Country Table with (Country (or dependency) and (name) relating to one another.

  <img width="311" height="645" alt="image" src="https://github.com/user-attachments/assets/e4748344-8e97-47c3-8a3d-30feb13b3c43" />


* Load
  
* Finally, I loaded the transformed queries into the workbook, setting the foundation for my subsequent analysis.

* I wanted to show the population attributes and compare the exact numbers side-by-side by country but I thought that 234 countries would be too many to show in a bar/column chart, even in a map chart. So created a separate a pivot table on a seperate tab named "By Country" instead and created a pivot table showing all of the countries and their population attributes with slicers to filter by country and By Region.

* <img width="1818" height="416" alt="image" src="https://github.com/user-attachments/assets/c9d4c0ff-3b63-48dc-b7e8-49e07c34ba5d" />


## 💡 Key Analytical Insights
*   **Growth Hotspots:** Identification of specific emerging economies with compounding annual growth rates (CAGR) that signal ripe opportunities for infrastructure investment.
*   **Demographic Divergence:** Visualization of the widening gap between aging populations in developed nations versus expanding youth majorities in developing regions, impacting product-line longevity.
*   **Urbanization Velocity:** Data points showcasing massive population shifts toward mega-cities, forcing logistics companies to pivot toward last-mile delivery solutions.
*   **Saturation Thresholds:** Evidence of historically dominant markets plateauing, proving the financial necessity for immediate international diversification.

---

## 🚀 How to Use the Dashboard
1.  Download the `[Project_1 - Web Scraping Through Microsoft Excel Power Query_Project].xlsx` file from this repository.
2.  Open the file in Microsoft Excel (Ensure macros/data connections are enabled if prompted).
3.  Navigate to the **Data** tab and click **Refresh All** to pull the latest live population data from the web source.
4.  In the "Dashboard" tab, use the interactive drop down menu on the upper left side of the Region scatter plot chart to see the current regional Population, Density (P/Km²) and Land Area (Km²).
5.  In the "By Country" tab, use the interactive slicers on the right side of the pivot table to filter by Country and Region. 

## 🏁 Project Conclusion
This dashboard successfully bridges the gap between raw web-based demographic data and strategic corporate execution. By utilizing Power Query to automate the data pipeline, the project demonstrates a scalable approach to business intelligence. It proves that businesses do not need expensive enterprise software to maintain a reliable, automated data asset. Ultimately, it empowers stakeholders to stop reacting to historical population shifts and start proactively planning for future global demand.

---

## 👤 Author
*   **Venice Ann Santos** - *Software QC Analyst / Business Intelligence Analyst*
*   [LinkedIn Profile Link]([(https://www.linkedin.com/in/venice-ann-santos-032a348a/)])
*   [Portfolio Website Link]([(https://github.com/Venice-02072219)])

