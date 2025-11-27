# Excel Data Cleaning & Dashboard

**Tools:** Excel  
**Focus:** Data cleaning, basic transformations, and building a simple dashboard on top of cleaned data.

This day is split into two mini-tasks:

1. **President Data Cleanup** – practice cleaning and standardizing a messy dataset.
2. **Bike Buyers Dashboard** – clean a customer dataset and build a simple interactive dashboard.

---

## 1. President Data Cleanup (Excel)

**Goal:**  
Practice core Excel data-cleaning steps: removing duplicates, fixing inconsistent text entries, normalizing formats (names, salaries, dates), and preparing the data for later analysis.

### What I Did

1. **Kept original vs cleaned data separate**
    - Created a **new sheet** to work on.
    - Original data stayed untouched on the original sheet.
    - Cleaned/standardized version lives in the new “Cleaned” sheet.
    - This makes it easy to compare before/after and avoid losing raw data.

2. **Removed duplicates**
    - Used **Remove Duplicates** to get rid of repeated rows.
    - Ensured I wasn’t double-counting any records in analysis.

3. **Checked for inconsistent values with filters**
    - Turned on **Filters** for all columns.
    - Scanned dropdowns to spot:
        - Misspellings
        - Inconsistent labels
        - Odd values (e.g., typos, extra spaces, weird capitalization)

4. **Fixed incorrect / inconsistent text values**
    - Corrected obvious typos like:
        - `"Democrtaic"` → `"Democratic"`
    - Standardized category values so each category is spelled and formatted the same way.

5. **Cleaned up names with text functions**
    - Applied `TRIM(PROPER(name))`:
        - `PROPER()` → standardizes name capitalization (e.g., “john smith” → “John Smith”).
        - `TRIM()` → removes leading/trailing double spaces and extra spaces inside.
    - This reduces issues later when:
        - Grouping
        - Matching
        - Using lookups on names

6. **Fixed salary data type**
    - Converted **Salary** from text to **numeric**.
    - This is critical for:
        - Summaries
        - Averages
        - Any future analysis or charts based on salary.

7. **Standardized date formats**
    - Changed dates to a **short date** format.
    - Fixed entries that were:
        - Text pretending to be dates
        - Large serial numbers (e.g., `43021`) without a proper date format
    - Ensured all rows use a consistent, interpretable date format.

### Key Learning

- Even simple cleaning steps (remove duplicates, fix spelling, TRIM/PROPER, correct types) make a huge difference for analysis.
- `TRIM(PROPER())` is a powerful combo to normalize text and avoid hidden whitespace issues.
- Consistent date and numeric formats are essential before moving into any serious reporting or visualization.

---

## 2. Bike Buyers Dashboard (Excel)

**Goal:**  
Take a “bike buyers” dataset from raw form to a cleaned dataset and then build an interactive dashboard using pivot tables and slicers.

### Structure

I organized the workbook into dedicated sheets:

1. `bike_buyers` – original raw data
2. `Working Sheet` – cleaned + transformed data
3. `Pivot Table` – pivot tables used as data source for charts
4. `Dashboard` – final, user-facing dashboard layout

### Data Cleaning & Preparation

1. **Clarified ambiguous single-letter codes**
    - Columns like **gender** and **marital status** used single letters:
        - `M` could mean **Male** or **Married** (ambiguous across different columns).
    - In the **Working Sheet**, I expanded these values so they’re clear to anyone using the dashboard:
        - `M` → `Male` (in Gender column)
        - `F` → `Female`
        - `M` → `Married` (in Marital Status column, where applicable)
        - etc.
    - This improves readability and avoids confusion for end users.

2. **Checked for misspellings / strange values**
    - Applied **Filters** to key columns.
    - Scanned for:
        - Misspellings
        - Weird characters
        - Inconsistent categories
    - Cleaned up any obvious issues.

3. **Removed duplicates**
    - Used **Remove Duplicates** and deleted 26 duplicate records.
    - Ensures counts and summaries (like “how many bought a bike”) are accurate.

4. **Fixed data types**
    - Set **Income** column to a **Currency** type.
    - Makes it easier to interpret and use in pivot tables and charts.

5. **Created an Age Bracket column**
    - On the **Working Sheet**, added a new **Age Bracket** field to group customers:
        - `0–18` → “Children & Teens”
        - `19–30` → “Young Adults”
        - `31–50` → “Middle-Aged Adults”
        - `51–70` → “Older Adults”
        - `71–100` → “Seniors”
    - Formula used (based on age in `L2`):
      ```excel
      =IFS(
        L2<=18,"Children & Teens",
        L2<=30,"Young Adults",
        L2<=50,"Middle-Aged Adults",
        L2<=70,"Older Adults",
        L2<=100,"Seniors",
        TRUE,"Invalid"
      )
      ```
    - This makes it much easier to analyze buying behavior by age group.

6. **Exploratory checks with conditional formatting**
    - On the **Working Sheet**, used conditional formatting to:
        - Highlight the **10 youngest** customers.
        - Highlight all rows from a specific region (e.g., **Pacific**).
    - This helped visually inspect the data and understand distributions.

### Pivot Tables (Analysis Layer)

Built several pivot tables on the **Pivot Table** sheet to explore different questions:

1. **Income vs Bike Purchase by Gender**
    - Pivot: `Gender` vs `Purchased Bike (Yes/No)`
    - Included **Average Income**.
    - Question: Do people with higher or lower income buy more bikes? Does income influence purchase behavior by gender?

2. **Commute Distance vs Bike Purchase**
    - Pivot: `Commute Distance` vs `Purchased Bike (Yes/No)`.
    - Question: Does commute distance affect whether someone buys a bike?

3. **Age Brackets vs Bike Purchase**
    - Pivot: `Age Bracket` vs `Purchased Bike (Yes/No)`.
    - Question: Which **age groups** are most likely to buy a bike?

These pivots are the data source for the dashboard charts.

### Dashboard

On the **Dashboard** sheet:

1. **Presentation cleanup**
    - Removed gridlines.
    - Added a clear **title**.
    - Positioned and aligned charts for a clean layout.

2. **Charts from pivot tables**
    - Created charts based on the three pivot tables above:
        - Bike purchases by gender & income
        - Bike purchases by commute distance
        - Bike purchases by age bracket

3. **Interactive slicers**
    - Added **slicers** for:
        - Marital Status
        - Education
        - Region
    - Connected each slicer to **all three** pivot tables via **Report Connections**.
    - Result: a simple, interactive dashboard where the user can filter everything at once.

### Key Learning

- Separating raw data, working/cleaning area, pivot tables, and dashboard makes the workbook much easier to maintain.
- Cleaning ambiguous codes (`M`, `F`, etc.) increases clarity for any stakeholder who uses the file.
- Creating age brackets (via `IFS`) is a practical way to turn continuous data into categories for analysis.
- Pivot tables + slicers are a quick way to build an interactive dashboard without any VBA or advanced tools.
