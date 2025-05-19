# Power BI Data Professional Survey Project

# data_professional_survey_power_bi

---

Power BI project for cleaning, analyzing, and visualizing data professional survey data.

---

## Author

**Charles Pugh**

Google-certified Data Analyst

Email: [charlespughtech@gmail.com](mailto:charlespughtech@gmail.com)

LinkedIn: [https://www.linkedin.com/in/charlespughtech/](https://www.linkedin.com/in/charlespughtech/)

Date: May 19, 2025

---

## Table of Contents

1. [Dataset](#dataset)
2. [Requirements](#requirements)
3. [Project Structure](#project-structure)
4. [Data Cleaning](#data-cleaning)
5. [Data Analysis](#data-analysis)
6. [Data Visualisation](#data-visualisation)
7. [Usage](#usage)
8. [Contact](#contact)

---

## Dataset

The dataset used in this project is sourced from the `Power BI - Final Project.xlsx` file under the "Data Professional Survey" sheet. The original dataset can be found at:

- **Source URL**: [https://github.com/AlexTheAnalyst/Power-BI/blob/main/Power%20BI%20-%20Final%20Project.xlsx](https://github.com/AlexTheAnalyst/Power-BI/blob/main/Power%20BI%20-%20Final%20Project.xlsx)

For this project, the data is imported into Power BI from the "Data Professional Survey" sheet of `Power BI - Final Project.xlsx`.

---

## Requirements

- Microsoft Power BI Desktop (latest version recommended)
- Access to the `Power BI - Final Project.xlsx` file

---

## Project Structure

```bash
data_professional_survey_power_bi/
├── Power BI - Final Project.xlsx  # Original raw dataset
├── README.md                      # Project overview and instructions
├── data_professional_survey.pbix  # Power BI file containing the cleaned data, analysis, and visualizations
└── screenshot_data_professionals_survey.jpg  # JPG file containing a screenshot of the completed data_professional_survey.pbix Power BI dashboard
```

---

## Data Cleaning

The data cleaning process is implemented in Power BI using the Power Query Editor, with steps applied to the dataset imported from the "Data Professional Survey" sheet. Follow these steps to replicate:

- **Load Data into Power BI**:
  - Open Power BI Desktop and select "Get Data" > "Excel Workbook".
  - Import `Power BI - Final Project.xlsx` and select the "Data Professional Survey" sheet.
  - Load the data into Power Query Editor.
- **Promote Headers**:
  - In Power Query Editor, use "Promote Headers" to set the first row as column headers.
- **Transform Column Types**:
  - Adjust data types for consistency:
    - Set `Unique ID`, `Q1 - Which Title Best Fits your Current Role?`, `Q4 - What Industry do you work in?`, `Q5 - Favorite Programming Language`, `Q7 - How difficult was it for you to break into Data?`, `Q8 - If you were to look for a new job today, what would be the most important thing to you?`, `Q9 - Male/Female?`, `Q11 - Which Country do you live in?`, `Q12 - Highest Level of Education`, and `Q13 - Ethnicity` to Text
    - `Date Taken (America/New_York)` to Text
    - `Time Taken (America/New_York)` and `Time Spent` to Time
    - `Q6 - How Happy are you in your Current Position with the following? (Salary)`, `Q6 - How Happy are you in your Current Position with the following? (Work/Life Balance)`, `Q6 - How Happy are you in your Current Position with the following? (Coworkers)`, `Q6 - How Happy are you in your Current Position with the following? (Management)`, `Q6 - How Happy are you in your Current Position with the following? (Upward Mobility)`, `Q6 - How Happy are you in your Current Position with the following? (Learning New Things)`, and `Q10 - Current Age` to Integer
- **Remove Unnecessary Columns**:
  - Remove columns not needed for analysis: `Email`, `Browser`, `OS`, `City`, `Country`, and `Referrer`.
- **Clean and Split Columns**:
  - Split columns like `Q1 - Which Title Best Fits your Current Role?`, `Q4 - What Industry do you work in?`, `Q5 - Favorite Programming Language`, `Q8 - If you were to look for a new job today, what would be the most important thing to you?`, `Q11 - Which Country do you live in?`, and `Q13 - Ethnicity` by delimiter ` (` to remove parentheses content, keeping only the main text.
  - Further split `Q5 - Favorite Programming Language` by `:` to clean up the values.
- **Transform Salary Column**:
  - Replace `k` with `,000` in `Q3 - Current Yearly Salary (in USD)` (e.g., `50k` becomes `50,000`).
  - Split the salary column by delimiter `-` to separate range values into two columns (e.g., `50,000-75,000` becomes `50,000` and `75,000`).
  - Convert these columns to Integer type.
  - Add a custom column `Average Salary ($)` by calculating the average of the salary range: `([Q3 - Current Yearly Salary (in USD).1] + [Q3 - Current Yearly Salary (in USD).2]) / 2`.
  - Remove the split salary columns (`Q3 - Current Yearly Salary (in USD).1` and `Q3 - Current Yearly Salary (in USD).2`).
- **Reorder and Rename Columns**:
  - Reorder columns for clarity, prioritizing key fields like `Unique ID`, `Date Taken (America/New_York)`, `Q1 - Which Title Best Fits your Current Role?.1`, and `Average Salary ($)`.
  - Rename the custom column to `Average Salary ($)` for clarity.

---

## Data Analysis

Data analysis is performed within Power BI using the cleaned dataset. Follow these steps to replicate:

- **Create Measures and Calculated Columns**:
  - Create a measure for the total number of participants: `Total Participants = COUNTROWS('Data Professional Survey')`.
  - Create a measure for average salary: `Average Salary = AVERAGE('Data Professional Survey'[Average Salary ($)])`.
  - Create a measure for average age: `Average Age = AVERAGE('Data Professional Survey'[Q10 - Current Age])`.
  - Create a measure for average happiness with salary: `Avg Happiness Salary = AVERAGE('Data Professional Survey'[Q6 - How Happy are you in your Current Position with the following? (Salary)])`.
  - Create a measure for average work/life balance: `Avg Work/Life Balance = AVERAGE('Data Professional Survey'[Q6 - How Happy are you in your Current Position with the following? (Work/Life Balance)])`.
- **Analyze Salary by Job Title**:
  - Use a table to group by `Q1 - Which Title Best Fits your Current Role?.1` and calculate the average `Average Salary ($)` for each role.
  - Sort by average salary (descending) to identify top-paying roles (e.g., Data Scientist at $88K, Data Engineer at $77K).
- **Analyze Salary by Gender**:
  - Group by `Q9 - Male/Female?` and calculate the average `Average Salary ($)` for males ($55.19K) and females ($52.7K).
- **Examine Programming Language Preferences**:
  - Group by `Q5 - Favorite Programming Language.1.1` and count the number of participants to identify the most popular language (Python).
- **Analyze Participant Distribution by Country**:
  - Group by `Q11 - Which Country do you live in?.1` and count participants to identify top countries (e.g., United States with 261 participants, India with 224).

### Key Insights

- **Salary Trends**: Data Scientists and Data Engineers have the highest average salaries, while students or those looking for roles have the lowest.
- **Gender Pay Gap**: Males earn slightly more on average ($55.19K) than females ($52.7K), highlighting a potential pay disparity.
- **Programming Language Preference**: Python is the most favored programming language among data professionals, followed by R and SQL.
- **Demographic Patterns**: The United States and India dominate in participant numbers, reflecting the global distribution of data professionals.

These insights guide the report’s design to highlight key trends and disparities.

---

## Data Visualisation

The report is built in Power BI using visuals linked to the analyzed data. Follow these steps to replicate:

- **Create Visuals in the Report View**:
  - **Gauge for Average Happiness with Salary**:
    - Add a Gauge visual, set the value to the `Avg Happiness Salary` measure, with a max value of 10.
    - Set the title to “Average Happiness with Salary Score”.
  - **Gauge for Average Work/Life Balance**:
    - Add a Gauge visual, set the value to the `Avg Work/Life Balance` measure, with a max value of 10.
    - Set the title to “Average Work/Life Balance Score”.
  - **Card for Total Participants**:
    - Add a Card visual, set the value to the `Total Participants` measure.
    - Set the title to “Number of Survey Participants”.
  - **Card for Average Salary**:
    - Add a Card visual, set the value to the `Average Salary` measure.
    - Set the title to “Average Participant Salary ($)”.
  - **Card for Average Age**:
    - Add a Card visual, set the value to the `Average Age` measure.
    - Set the title to “Average Age of Participant”.
  - **Clustered Bar Chart for Average Salary by Job Title**:
    - Add a Clustered Bar Chart, set the axis to `Q1 - Which Title Best Fits your Current Role?.1` and the value to `Average Salary ($)` (average).
    - Set the title to “Average Salary ($) by Job Title”.
  - **Donut Chart for Salary by Gender**:
    - Add a Donut Chart, set the legend to `Q9 - Male/Female?` and the value to `Average Salary ($)` (average).
    - Set the title to “Male vs Female Average Salary ($)”.
  - **Stacked Bar Chart for Programming Language Preference**:
    - Add a Stacked Bar Chart, set the axis to `Q5 - Favorite Programming Language.1.1` and the value to count of `Unique ID`.
    - Set the title to “Favorite Programming Language”.
  - **Treemap for Participants by Country**:
    - Add a Treemap visual, set the group to `Q11 - Which Country do you live in?.1` and the value to count of `Unique ID`.
    - Set the title to “Participants per Country”.
- **Organize Report Layout**:
  - Arrange visuals for clarity:
    - Place the gauges and cards at the top for key metrics.
    - Position the bar charts and treemap below in a 2x2 grid layout.
  - Use consistent colors (e.g., blue for males, orange for females) and fonts (e.g., Segoe UI, size 12).
- **Add Slicers**:
  - Add slicers for `Q1 - Which Title Best Fits your Current Role?.1`, `Q9 - Male/Female?`, `Q11 - Which Country do you live in?.1`, `Q4 - What Industry do you work in?.1`, and `Q5 - Favorite Programming Language.1.1`.
  - Place slicers on the right side of the report for easy access.
  - Enable cross-filtering so slicers dynamically update all visuals.
- **Apply Formatting**:
  - For each visual, ensure clear titles and labels:
    - Format axis titles (e.g., “Job Title” or “Average Salary ($)”).
    - Adjust font sizes for readability (e.g., titles at size 14, labels at size 10).
  - Add a report title: Go to Insert > Text Box, type “Data Professional Survey Report”, format with bold, size 16, and place at the top.
- **Finalize Report**:
  - Ensure the report fits on one page with interactive slicers.
  - Test slicers by filtering (e.g., select “United States” in the country slicer) to confirm visuals update dynamically.

---

## Usage

To explore or replicate the Power BI Data Professional Survey Project, follow these steps:

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/charlespughtech/data_professional_survey_power_bi.git
   cd data_professional_survey_power_bi
   ```

2. **Explore the Project**:

   - Open `data_professional_survey.pbix` in Power BI Desktop.
   - The file contains:
     - **Data Model**: Cleaned dataset with transformed columns and measures.
     - **Report View**: Interactive report with visuals and slicers.
   - Navigate to the Report View to interact with the visuals using slicers (e.g., filter by `Q9 - Male/Female?` or `Q11 - Which Country do you live in?.1`).
   - Review the Data View and Power Query Editor to see the data cleaning and analysis steps.

3. **Replicate the Project from Scratch** (Optional):

   - If you want to rebuild the project:
     - Use the provided `Power BI - Final Project.xlsx` in the repository or download it from the source URL.
     - Create a new Power BI file named `data_professional_survey.pbix`.
     - Import the dataset from the "Data Professional Survey" sheet in `Power BI - Final Project.xlsx`.
     - Follow the steps in Data Cleaning to prepare data in Power Query Editor.
     - Perform analysis as described in Data Analysis by creating measures and analyzing trends.
     - Build the report as outlined in Data Visualisation by adding visuals and slicers.
   - Verify measures in the Data View (e.g., `Total Participants`, `Average Salary`) and transformations in Power Query Editor.

Results are available in `data_professional_survey.pbix`. Check the Power Query Editor for applied steps and the Report View for the final visualizations.

---

## Contact

For inquiries or data analytics services, please contact:

**Charles Pugh**

Google-certified Data Analyst

Email: [charlespughtech@gmail.com](mailto:charlespughtech@gmail.com)

LinkedIn: [https://www.linkedin.com/in/charlespughtech/](https://www.linkedin.com/in/charlespughtech/)
