
Red & White SkillPower BI Practical Report 1: Badha Tasks (1 thi 13) Education · Superstore Sales Dataset · Power BI Desktop
Aa doc ma badha 13 tasks ek j jagya e chhe: shu karvanu, kya karvu, ane check karva mate sacha numbers. Task 1 thi 10 tame karI lidha chhe. Task 11, 12, 13 baki chhe.
Dataset
• Name: Sample Superstore Sales Dataset
• File: C:\Power Bi\archive\Sample - Superstore.csv
• Rows: 9,994 (cleaning pachhi 8,211)
• Report file: Superstore Report.pbix
Task 1 · Data source connect karo ✅
1.  Home → Get Data → Text/CSV.
2.  Sample - Superstore.csv select karo.
3.  Navigator ma preview juo.
4.  Transform Data par click karo.
Task 2 · Power Query interface ✅
1.  Queries pane (left), Data preview (center), Applied Steps (right) ne oLakho.
2.  View tab ma Column Quality, Column Distribution, Column Profile tick karo.
3.  Formula bar ma M code juo.
Task 3 · Table transformations ✅
Advanced Editor ma aa code paste karyo hato (3.1 thi 3.6 automatic):
let
    Source = Csv.Document(File.Contents("C:\Power Bi\archive\Sample - Superstore.csv"),[Delimiter=",", Encoding=1252, QuoteStyle=QuoteStyle.Csv]),
    Headers = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    Typed = Table.TransformColumnTypes(Headers,{
        {"Order Date", type date}, {"Ship Date", type date},
        {"Sales", type number}, {"Quantity", Int64.Type},
        {"Discount", type number}, {"Profit", type number}}, "en-US"),
    Renamed = Table.RenameColumns(Typed,{
        {"Sub-Category","Sub Category"}, {"Product Name","Product"},
        {"Customer Name","Customer"}, {"Ship Mode","Ship Mode Type"}}),
    NoNulls = Table.SelectRows(Renamed, each [Sales] <> null and [Profit] <> null),
    Filtered = Table.SelectRows(NoNulls, each [Segment] = "Consumer" or [Segment] = "Corporate"),
    Dup = Table.DuplicateColumn(Filtered, "Order ID", "Order ID - Copy"),
    Split = Table.SplitColumn(Dup, "Order ID - Copy",
        Splitter.SplitTextByDelimiter("-", QuoteStyle.Csv),
        {"Order Region Code","Order Year","Order Number"}),
    Removed = Table.RemoveColumns(Split, {"Row ID","Country","Postal Code"})
in
    Removed
Step
Kaam
3.1
4 columns rename (Sub Category, Product, Customer, Ship Mode Type)
3.2
Data types: date, decimal, whole number
3.3
Sales ane Profit ma null hoy to rows remove
3.4
Fakt Consumer ane Corporate rakhya
3.5
Order ID ne - thi split karyo (Order Region Code)
3.6
Row ID, Country, Postal Code remove
3.7
Home → Close & Apply
Task 4 · Fields pane ✅
1.  Report View ma Data pane ma tables ane columns juo.
2.  Σ vala numeric: Sales, Quantity, Discount, Profit. Bija text.
3.  Sales ne canvas par drag karine auto visual juo, pachhi delete karo.
Task 5 · Visualizations pane ✅
1.  Build/Visualizations pane ma icons par hover karo (Card, Bar, Table, Slicer, Pie).
2.  Khali canvas par click karo, Card icon dabavo.
Task 6 · KPI cards ✅
Pehla Card icon dabavo, pachhi field tick karo.
Card
Field
Title
1
Sales (Sum)
Total Sales
2
Profit (Sum)
Total Profit
3
Quantity (Sum)
Total Quantity
4
Discount (Average)
Average Discount
Chare cards page ni upar ek row ma.
Task 7 · Bar charts ✅
Pehla Clustered bar chart icon (pehli row, trijo icon) dabavo, pachhi fields tick karo.
• Chart 1: Y-axis = Category, X-axis = Sum of Sales
• Chart 2: Y-axis = Region, X-axis = Sum of Profit
• Data labels On
• ... → Sort axis → Sort descending
Task 8 · Visuals formatting ✅
Step
Setting
8.1
Titles: Total Sales by Product Category, Total Profit by Region
8.2
Bars: Chart 1 red #CC0000, Chart 2 charcoal #4A4A4A
8.3
Data labels: font 10, Display units Thousands
8.4
KPI values: font 28, Bold, Color #4A4A4A
8.5
Subtitle: FY 2014–2017 · Consumer & Corporate Segments
8.6
Gridlines Off (X-axis ane Y-axis)
Format pane ni Search ma title, callout, gridlines lakhi ne sidhu section male.
Task 9 · Slicers ✅
• Slicer 1: Region, Style = Tile ya Dropdown
• Slicer 2: Category, Style = List ya Dropdown
• Banne cards ni upar horizontal row ma
• Test: Region ma West select karo, badhu filter thavu joiye, pachhi All
Slicer icon Table icon ni barobar dabi baju chhe. Hover karine "Slicer" naam check karo.
Task 10 · Filters ✅
• 10.1 Page-level: Filters on this page ma Ship Mode Type = Standard Class ane Second Class.
• 10.2 Visual-level: Navo bar chart (Sub Category, Sales). Filters on this visual ma Sub Category → Top N → Top 5 → By value Sum of Sales → Apply filter.
• 10.3 Verify: Slicers sathe koi conflict nathi.
Check karva mate numbers (Ship Mode filter pachhi): Total Sales ≈ 1.50M, Profit ≈ 178.57K, Quantity ≈ 25K, Avg Discount ≈ 0.16. Top 5: Chairs, Phones, Storage, Tables, Binders.
Task 11 · Report page formatting ⏳
Khali jagya par click karo (kai select na hoy), pachhi:
1.  11.1: Format pane → Canvas settings → Type = 16:9 (1280 × 720).
2.  11.2: Format pane → Canvas background → Color → Custom color → F5F5F5, Transparency 0%.
3.  11.3: View tab → Snap to grid ✓, Gridlines ✓.
4.  11.4: Visuals ne goothvo. Upar slicers, tenaa niche 4 cards, tenaa niche 3 charts. Ctrl + click thi select karo, Format tab → Align → Align top, pachhi Distribute horizontally.
5.  11.5: Niche + thi navo page, Table visual, fields: Order ID, Order Date, Customer, Segment, Category, Sub Category, Sales, Quantity, Discount, Profit. Page naam: Order Details.
Task 12 · Theme ⏳
1.  12.1: View tab → Themes → koi professional theme (jemke Executive ya Classic).
2.  12.2: Check karo ke colours ane fonts badha visuals ma badlai gaya. Jo bars no red/charcoal badlai jay to Task 8.2 pharithi karo.
Task 13 · Visual interactions ⏳
1.  13.1: Sales by Category bar chart select karo (source visual).
2.  13.2: Format tab → Edit interactions. Bija visuals par icons aavshe.
3.  13.3: Profit by Region par Filter (funnel) icon.
4.  13.4: KPI cards par Highlight ya None icon.
5.  13.5: Test: Technology bar par click karo, bija visuals filter/highlight thavi joiye.
6.  13.6: Aaj rite ochha ma ochha 2 vadhu source visuals mate karo (jemke Profit by Region, Top 5 chart). Kul 3+ visual pairs hovi joiye.
7.  Pachhi Edit interactions band karo (Format tab ma pharithi click).
Final checklist
[ ] Task 1 thi 3: Data load ane clean (8,211 rows)
[ ] Task 4 thi 5: Fields ane Visualizations pane explore
[ ] Task 6: 4 KPI cards
[ ] Task 7: 2 bar charts, labels, sorted
[ ] Task 8: Titles, red/charcoal, font, subtitle, gridlines off
[ ] Task 9: Region ane Category slicers
[ ] Task 10: Page filter ane Top 5 visual filter
[ ] Task 11: 16:9, #F5F5F5, snap to grid, aligned, bijo page
[ ] Task 12: Theme
[ ] Task 13: 3+ visual interactions
[ ] File save: Superstore Report.pbix
