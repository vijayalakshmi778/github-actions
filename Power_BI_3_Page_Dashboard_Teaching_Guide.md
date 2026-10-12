# Power BI Training Lab: Build a 3-Page Interactive Sales Dashboard
**Level:** Beginner | **Tool:** Power BI Desktop | **Dataset:** `Power_BI_Cleaned_Sales_Dataset.xlsx`

## What students will build
A consistent, professional **Sales Performance Dashboard** with three report pages:
1. **Overview** — headline KPIs, sales trend, sales by category.
2. **Product & Region** — category/sub-category performance and regional comparison.
3. **Customer Insights** — customer segments, payment methods, and top customers.

### Theme and layout
Use the same design on all three pages so the report feels like one product.

- **Canvas:** 16:9 widescreen.
- **Page background:** very light grey `#F4F6FA`.
- **Primary:** deep navy `#17324D`.
- **Accent:** teal `#16A6A1`.
- **Secondary accent:** sky blue `#4C8BF5`.
- **Highlight:** soft amber `#F4B942`.
- **Text:** dark slate `#243447`.
- **Font:** Segoe UI.
- Keep chart titles short, align visuals to a grid, and leave space between visuals.
- Suggested header on every page: `SALES PERFORMANCE` on the left and page name on the right.
- Add a small footer: `Training Dashboard | Sample Data`.

> Power BI menus can vary slightly by version. If a button name differs, look for the equivalent option in the Format or Visualizations pane.

---

## Part 1 — Get ready

### Step 1: Open Power BI Desktop
1. Launch **Power BI Desktop**.
2. Choose **Blank report**.
3. Save immediately: `Sales_Performance_Dashboard.pbix`.

### Step 2: Import the Excel workbook
1. Select **Home → Get data → Excel workbook**.
2. Choose `Power_BI_Cleaned_Sales_Dataset.xlsx`.
3. In Navigator, select the `SalesData` sheet/table.
4. Click **Transform Data** first, so students can inspect the data in Power Query.

### Step 3: Check the data in Power Query
The supplied dataset is already cleaned for teaching, but show students how to validate it:
1. Confirm `OrderDate` is **Date**.
2. Confirm `Quantity` is **Whole number**.
3. Confirm `UnitPrice`, `DiscountPct`, `SalesAmount`, and `Profit` are **Decimal number** or **Fixed decimal number**.
4. Confirm ID and category fields are **Text**.
5. Check column headers for blanks and look for obvious errors.
6. Select **Home → Close & Apply**.

### Step 4: Create measures
In the Fields/Data pane, right-click `SalesData` → **New measure**. Create these measures one at a time:

```DAX
Total Sales = SUM(SalesData[SalesAmount])
Total Profit = SUM(SalesData[Profit])
Total Orders = DISTINCTCOUNT(SalesData[OrderID])
Units Sold = SUM(SalesData[Quantity])
Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)
Average Order Value = DIVIDE([Total Sales], [Total Orders], 0)
```

After creating `Profit Margin %`, select it and set **Measure tools → Format → Percentage** with 1 decimal place. Format Total Sales, Total Profit, and Average Order Value as currency. If your locale uses a different currency, choose the appropriate symbol.

### Step 5: Apply the theme
1. Open **View → Themes**.
2. Choose **Customize current theme** if available.
3. Set the report/background and visual colors to the palette above, or select a built-in theme and manually apply the palette to visuals.
4. Use a consistent title style: Segoe UI Semibold, 14–18 pt; KPI values around 24–32 pt.
5. Use the **Format page** pane to set the page canvas to 16:9 and background to `#F4F6FA`.

---

## Part 2 — Page 1: Overview

### Page setup
1. Rename the first page tab to **01 Overview**.
2. In Format page, set the canvas to **16:9**.
3. Add a text box at the top: `SALES PERFORMANCE | OVERVIEW`.
4. Style the header with deep navy and a clear font size.

### Add slicers
Add these slicers near the top, below the header:
- `OrderDate` (use Between or Relative date style if available).
- `Region`.
- `Category`.

Make them compact and align them in one row. These slicers should filter the visuals on this page.

### Add KPI cards
Add four **Card** visuals:
- `[Total Sales]`
- `[Total Profit]`
- `[Total Orders]`
- `[Profit Margin %]`

For each card:
1. Drag the measure into the card.
2. Turn on the category label if useful.
3. Use a white visual background, subtle border/shadow if available, and navy/teal accents.
4. Keep all four cards the same size.

### Add charts
**Visual A — Monthly sales trend**
1. Add a **Line chart**.
2. Put `OrderDate` on the X-axis. Use the Date hierarchy and keep **Year** and **Month** (or use the raw date and set the axis to continuous).
3. Put `[Total Sales]` on the Y-axis.
4. Title it `Monthly Sales Trend`.
5. If months from different years are present, use a Year-Month field or date hierarchy so months are not incorrectly combined.

**Visual B — Sales by category**
1. Add a **Clustered bar chart**.
2. Axis: `Category`.
3. Values: `[Total Sales]`.
4. Title: `Sales by Category`.
5. Sort descending by Total Sales.

**Visual C — Sales by region**
1. Add a **Donut chart** or bar chart.
2. Legend/Axis: `Region`.
3. Values: `[Total Sales]`.
4. Title: `Sales Mix by Region`.

### Suggested arrangement
- Header across the top.
- Slicers directly underneath.
- Four KPI cards in one row.
- Monthly trend across the lower left; category and region visuals on the lower right.

### Page 1 validation
- Select a region in the region chart: other visuals should cross-filter.
- Change the date slicer: KPI cards and charts should update.
- Clear slicers and confirm totals return to the overall values.

---

## Part 3 — Page 2: Product & Region

### Create the page
1. Click **+** to add a page.
2. Rename it **02 Product & Region**.
3. Copy the header from Page 1, then change the text to `SALES PERFORMANCE | PRODUCT & REGION`.
4. Keep the same background, font, and palette.

### Add slicers
Add `Region`, `Category`, and `OrderDate` slicers. Align them in the same position as Page 1.

### Add visuals
**Visual A — Sales by sub-category**
- Visual: Clustered bar chart.
- Axis: `SubCategory`.
- Values: `[Total Sales]`.
- Sort by Total Sales descending.
- Title: `Sales by Sub-Category`.

**Visual B — Profit by category**
- Visual: Clustered column chart.
- X-axis: `Category`.
- Y-axis: `[Total Profit]`.
- Title: `Profit by Category`.
- Use teal for positive performance; keep labels readable.

**Visual C — Sales by region and category**
- Visual: Stacked column chart.
- X-axis: `Region`.
- Legend: `Category`.
- Values: `[Total Sales]`.
- Title: `Regional Sales by Category`.

**Visual D — Product performance table**
1. Add a **Table** visual.
2. Add `Product`, `[Total Sales]`, `[Total Profit]`, and `Units Sold`.
3. Sort by Total Sales descending.
4. Turn on a subtle alternating row background if available.
5. Use this to compare product sales and profit at a glance.

### Page 2 validation
- Select one category and confirm the regional chart and product table update.
- Click a sub-category bar and observe cross-filtering.
- Check whether high sales always mean high profit; discuss discounting and cost.

---

## Part 4 — Page 3: Customer Insights

### Create the page
1. Add a new page and rename it **03 Customer Insights**.
2. Reuse the same header and theme.
3. Add `Region`, `Segment`, and `OrderDate` slicers in the consistent slicer row.

### Add visuals
**Visual A — Sales by customer segment**
- Visual: Donut or clustered bar chart.
- Legend/Axis: `Segment`.
- Values: `[Total Sales]`.
- Title: `Sales by Customer Segment`.

**Visual B — Orders by payment method**
- Visual: Clustered bar chart.
- Axis: `PaymentMethod`.
- Values: `[Total Orders]`.
- Title: `Orders by Payment Method`.

**Visual C — Top 10 customers**
1. Add a bar chart.
2. Axis: `CustomerName`.
3. Values: `[Total Sales]`.
4. In the Filters pane, add `CustomerName` to **Filters on this visual**.
5. Change filter type to **Top N**, enter `10`, drag `[Total Sales]` into **By value**, then select **Apply filter**.
6. Sort descending by Total Sales.
7. Title: `Top 10 Customers by Sales`.

**Visual D — Customer detail table**
- Add `CustomerName`, `Segment`, `Region`, `[Total Orders]`, `[Total Sales]`, and `[Total Profit]`.
- Sort by Total Sales descending.
- Optionally apply conditional formatting to Total Sales and Total Profit.

### Page 3 validation
- Select a customer bar and confirm the table reflects that customer.
- Change Segment and observe how top customers change.
- Discuss why the Top 10 chart is useful for account management.

---

## Part 5 — Add navigation between the three pages

Use **Page Navigator** so students can move between pages without clicking tiny tabs.

1. Open **Insert → Buttons → Navigator → Page navigator** (menu labels may vary).
2. Place the navigator near the top of each page, directly below the main header.
3. In Format, set the **Selected** state to deep navy and the **Default** state to white/light grey; use teal as the hover/accent color.
4. Make the navigator wide enough to show:
   - `01 Overview`
   - `02 Product & Region`
   - `03 Customer Insights`
5. If the navigator is not automatically present on every page, copy and paste it to the other pages and check the page destinations.
6. Test every button in **Reading view** or while holding **Ctrl** when selecting buttons in Desktop, depending on the Power BI version.

### Optional: Add a Home button
If you prefer individual buttons:
1. Insert → Buttons → Blank.
2. Set button text to `Overview`.
3. Turn **Action** on and choose **Page navigation**.
4. Set Destination to `01 Overview`.
5. Repeat for the other pages, or use Page Navigator for less maintenance.

---

## Part 6 — Make slicers consistent across pages (Sync slicers)

To make the report feel connected:
1. Select a slicer on Page 1.
2. Open **View → Sync slicers**.
3. In the Sync slicers pane, select the pages where it should sync.
4. Repeat for slicers you want to share, using the same field (for example, Region).
5. Decide whether the slicer should be visible on every page. Sync and visibility are separate settings.
6. Test by selecting a Region on Page 1, then navigating to Page 2 and Page 3.

**Teaching tip:** Syncing is helpful when students expect a selected region or date range to stay active while navigating. If a page should tell a different story, leave that slicer unsynced.

---

## Part 7 — Polish and test

### Design checklist
- [ ] All three pages use the same background, font, and colors.
- [ ] Headers and slicers align in the same positions.
- [ ] KPI cards have equal height and spacing.
- [ ] Chart titles explain what the viewer is seeing.
- [ ] No chart is overcrowded; labels are readable.
- [ ] Currency and percentage formats are correct.
- [ ] Page Navigator works from every page.
- [ ] Synced slicers behave as expected.
- [ ] Clicking a chart filters related visuals appropriately.
- [ ] No visual shows an unexpected blank or error.

### Final test scenario for students
1. Choose **South** in the Region slicer.
2. Choose **Technology** in Category (where available).
3. Set the date range to a smaller period.
4. Record Total Sales, Total Profit, and Profit Margin.
5. Navigate through all three pages and explain which product/sub-category and customer segment contributed most.
6. Clear filters and confirm the full report returns.

---

## Troubleshooting

**A measure says the column cannot be found**
- Confirm the table is named `SalesData` and the column spelling matches exactly.
- Create measures after loading the table.

**Date axis shows a strange hierarchy**
- Use the date hierarchy and keep Year/Month, or use `OrderDate` as a continuous axis. Ensure `OrderDate` is typed as Date.

**Page navigation buttons do not work in Desktop**
- Depending on version, use Ctrl+click to activate buttons, or test in Reading view.

**A slicer does not affect a visual**
- Select the slicer, then use **Format → Edit interactions** to confirm the target visual is set to Filter or Highlight, not None.
- If it should affect other pages, configure Sync slicers.

**Totals change unexpectedly**
- Check active slicers and visual-level filters. Use the eraser/clear filter option to reset selections.

---

## Instructor wrap-up questions
1. What is the difference between Total Sales and Total Profit?
2. Why might a product have high sales but low profit?
3. How do slicers differ from clicking a chart category?
4. Why use a Page Navigator instead of only page tabs?
5. What does Profit Margin % tell a business that Total Profit alone does not?

**Completion outcome:** Students finish with a three-page Power BI report, reusable DAX measures, consistent theme, interactive slicers, and working page navigation.
