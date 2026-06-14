# Driving the Transition: An Analysis of Electric Vehicle Adoption Across the United States

![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Power BI](https://img.shields.io/badge/PowerBI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![GitHub](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

- [Project Introduction](#project-introduction)
- [:bulb: Key Takeaways at a Glance](#bulb-key-takeaways-at-a-glance)
- [:dart: Project Goals](#dart-project-goals)
- [:question: Questions to Answer](#question-questions-to-answer)
- [:information\_source: Data Source](#information_source-data-source)
- [:hammer: Tech Stack](#hammer-tech-stack)
- [:broom: Data Cleaning \& Preparation](#broom-data-cleaning--preparation)
- [:microscope: Analysis \& Key Findings](#microscope-analysis--key-findings)
  - [Fuel Mix](#fuel-mix)
  - [EV Adoption Leaders \& Laggards](#ev-adoption-leaders--laggards)
  - [Alternative Fuels — Significant vs. Niche](#alternative-fuels--significant-vs-niche)
  - [Infrastructure Investment Gaps](#infrastructure-investment-gaps)
- [:bulb: Recommendations](#bulb-recommendations)
- [:warning: Limitations](#warning-limitations)

## Project Introduction

Faced with the ongoing oil crisis, Electric Vehicles (EVs) shine bright as a solution that is both independent of global supply chain blockages and environmentally sustainable. 

The question is no longer **IF ELECTRIC VEHICLES WILL REPLACE 
GASOLINE**. Rather, it is **WHO WILL BE LEADING THE CHARGE AND 
WHO WILL BE LEFT BEHIND**.

This project analyzes electric and traditional vehicle registrations across all 50 U.S. states to answer that question and to provide data-driven insights and recommendations to policymakers and automakers.


**Stakeholder:** Transportation Research Group

## :bulb: Key Takeaways at a Glance

| | Finding |
|---|---|
| :trophy: | California and DC lead EV adoption at 9%+ |
| :warning: | Florida and Texas have 480,000+ EVs but adoption below 1.5% |
| :battery: | 95% of U.S. vehicles still run on Gasoline |

## :dart: Project Goals
  
- Determine lagging and leading states in EV adoption
  
- Compare EV adoption against traditional fuel vehicle market
  
- Provide actionable recommendations for infrastructure investment for policymakers and automakers. 

## :question: Questions to Answer

- What percentage of vehicles in each state are EVs, PHEVs, HEVs, and gasoline?
  
- Which states have the highest EV adoption rates, and which states lag behind?

- Which alternative fuels (biodiesel, ethanol, hydrogen) are significant vs. niche?

- Where should policymakers prioritize EV infrastructure investment based on adoption trends and gaps in support?

## :information_source: Data Source

[:link:Raw Data](Data/Raw_Data/vehicle_data_raw.csv)

[:link:Processed Data](Data/Processed_Data/vehicle_data_final.xlsx)

> **Note:** On GitHub, click the link above then click the :arrow_down: **Download** 
> button (or press the download icon) on the top right of the page to save the file.

## :hammer: Tech Stack

- Excel & Power Query - Data preparation & cleaning
  
- Power BI - Data visualization and dashboards

## :broom: Data Cleaning & Preparation

The provided raw data was cleaned and prepared for visualization through Power Query and afterwards connected to Power BI for visualization.

Full list of issues/observations and actions taken for cleaning can be found in the table below.

| # | Issue/Observation | Action Taken |
|---|---|---|
| 1.|Data is in wide format with one row per each state and fuel type, interfering with filtering and aggregation during visualization in Power BI | Un-pivoted the fuel type column and to convert the data to long format |
|2.| A separate column required to categorize "EV" and "Non-EV" fuel sources| Created a separate reference table containing "EV" or "Non-EV" for each fuel type and merged it with the data to create EV_Non_EV column|
|3. |A separate column was necessary to categorize fuel sources as "Mainstream" or "Alternative" | Updated the reference table to include the required categories and made the required changes in the Query|
|4. | State column did not have any duplicates or data quality issues| No action required. Data is available for all 50 U.S. states. **Discussion with the stakeholder may be required to gauge if the scope should expand to U.S. territories**  |
|5. | Hydrogen registration count was available for California only.|  Since we do not know if this lack of data for other states is due to issues in the data collection, the data was not removed. **The stakeholder must validate the accuracy of this approach**|
|6. | Methanol has no data for any state. | Since the column is not useful in the analysis, we removed it to reduce processing time. **The stakeholder must validate the accuracy of this approach**|
|7.|"Unknown Fuel" registrations were available |"Unknown Fuel" registrations were retained and categorized as equivalent to Gasoline for the scope of this analysis. **The stakeholder must validate the accuracy of this approach**.|


## :microscope: Analysis & Key Findings

### Fuel Mix

- Across all states, Gasoline is leading at 95% of all registrations

- Within the EV market, HEVs claim more than half the market at 60% while the rest is filled by EVs and PHEVs.

![Gasoline & EV](<Exports/Images/01. Gasoline_&_EV.jpeg>)

- The chart below shows the EV/PHEV/HEV breakdown for the top 5 states by adoption rate. Gasoline is excluded for readability given its 95% national dominance.

![Large States EV Adoption](<Exports/Images/02._Large_States_EV_Adoption.jpeg>)

- [Click here](<Exports/PDF/EV_Adoption_Dashboard.pdf>) to view the breakdown of the EV market for all states.

- The key takeaway is that while the Gasoline is the current fuel of choice, the market is in the early stages of adopting EVs.

### EV Adoption Leaders & Laggards

- Large states such as California, District of Columbia and Washington are leading in EV adoption.
  
- However, smaller states such as Hawaii are making inroads as well.

- States such as North Dakota, Mississippi and Wyoming are lagging in EV adoption.

![EV Adoption Top and Bottom 5](<Exports/Images/03._EV_Adoption_Top_and_Bottom_5.jpeg>)

- In general, states located in the West Coast are embracing EVs while midwestern and southern states are lagging behind.

![EV Adoption Heatmap](<Exports/Images/04._EV_Adoption_Heatmap.jpeg>)

-  Possible reasons might include
   -  lack of EV infrastructure
   -  limited state-level policy initiatives
   -  cultural affinity towards internal combustion engines

### Alternative Fuels — Significant vs. Niche

- Alternative fuels (Ethanol, Biodiesel,Compressed Natural Gas (CNG), Hydrogen & Propane) account for only 8% of all registrations with EVs being classified as mainstream fuel for the purpose of this analysis.

- Out of all alternative fuel registrations, Ethanol (88%) & Biodiesel (12%) show significant adoption.
  
- Compressed Natural Gas (CNG), Hydrogen & Propane  collectively represent less than 1% of all alternative fuel registrations.

![Alternative Sources](<Exports/Images/05._Alternative_Sources.jpeg>)

- A possible cause is that internal combustion engines have greater compatibility with Ethanol and Biodiesel, making the transition to them more convenient and cost-effective

- Based on these observations, it is recommended to prioritize spending on charging infrastructure and incentive programs and allocate minimal spending for alternative fuels until adoption rates justify increased spending.


### Infrastructure Investment Gaps

Using the lower right quadrant of the scatter plot analysis, we have identified states with high EV registrations but low adoption rates, marking them as ideal candidates for EV infrastructure spending and consumer rebate initiatives.

![EV Count vs Adoption Rate](<Exports/Images/06._EV_Count_vs_Adoption_Rate.jpeg>)

| State | Pure EV Registrations (approx.) | Adoption Rate | Priority Reason
|---|---|---|---|
| Florida | 250,000 | 1.4% |Highest EV registrations outside of California with a massive infrastructure gap to the tune of just 1.4% adoption |
| Texas | 230,000 | 0.9% | Just below Florida when it comes to EV registrations and yet an adoption rate of below 1% makes this an untapped reservoir|
| New York | 100,000 | 1.1%  | A dense urban population with a particularly high potential of possible EV growth in metropolitan areas |

Prioritizing these states will maximize the impact of the infrastructure investment and consumer incentive programs.

## :bulb: Recommendations

Based on the analysis, the following recommendations are made 
for the Transportation Research Group:

**1. Prioritize EV Charging Infrastructure in Florida, Texas and New York**

Expand EV charging network and establish repair and maintenance points at high traffic areas.

**2. Introduce or Expand Consumer EV Incentive Programs**

Establish state-level rebates and tax incentives for EV adoption, modelling the adoption strategies of leaders in the EV space such as California and Washington. 

**3. De-prioritize Alternative Fuel Infrastructure Spending**

- National alternative fuel adoption rate is less than 1%, making increased spending inviable.

- Investment should be de-prioritized at this stage.

- However, alternative fuel adoption should be measured as an ongoing concern.

- Should the adoption rates continue to grow and surpass 20%, an increase in spending would be viable, barring any unforeseen circumstances.


## :warning: Limitations

- Data for U.S. Territories & Minor Outlying Islands were not provided.

- Since the data collection timeframe was not included, wider economic trends were not taken into account. 

- Hydrogen had only data collected for California while Methanol had no data at all. This may be indicative of gaps in the data collection process.

-   "Unknown Fuel" was assumed to be Gasoline for the scope of this analysis. A detailed breakdown of this category may cause slight changes to the results.