Audit Committee Dashboard Generator;

The interactive dashboard is for audit committee reporting: issue ratings, aging, owner-wise closure and repeat findings. Drop in an Excel or CSV export and get a stakeholder-ready dashboard in seconds, with no server, no install and no data upload.

A single-file web tool (index.html) that reads an audit issue log (or any tabular export), works out what each column means, and builds KPI cards and charts automatically. Charts can then be edited, added or removed, and the result exported to Excel or PowerPoint for the audit committee pack.

1. Problem statement
Internal audit and compliance teams track findings in spreadsheets. Before every audit committee meeting someone has to rebuild the same view by hand: open issues by rating, status split, trend over time, which processes carry the most findings. This is repetitive, error-prone, and the data is often confidential, so pasting it into an online BI tool is not an option.

2. Solution
A browser-based dashboard generator that runs entirely on the user's machine.

Step	What happens
Upload	Drag and drop .xlsx, .xls or .csv. Multi-sheet workbooks get a sheet selector.
Detect	Each column is classified as Date, Number, Status, Risk Rating, Process/Function or Text, using header names and value patterns.
Build	KPI cards plus four starter charts (bar, line, pie, doughnut) are generated from the detected columns.
Refine	Override any column type, edit a chart (dimension, metric, Top-N), add new charts, remove with undo.
Export	Save as Excel (summary plus one sheet per chart) or PowerPoint (title, KPI slide, one native chart per slide).
Audit-aware by design: risk ratings are ordered Critical → Low and coloured consistently; "Very High" and "Moderate" are mapped to Critical and Medium; status values such as Closed, Resolved, Remediated, Cancelled count as closed when computing % Open.

3. Try it in 60 seconds
Open index.html in a browser (or the live demo link above).
Upload sample-data/audit_issues_sample.csv (or the .xlsx).
You should see:
Item	Result on the sample file
Total rows / columns	60 / 10
% Open	45% (27 of 60 not closed)
High / Critical	18
Bar chart	Issues by Process (Fixed Assets and IT General Controls highest, 12 each)
Line chart	Issues raised per month, Nov 2025 to Sep 2026
Pie chart	Risk Rating split: 4 Critical, 14 High, 24 Medium, 18 Low
Doughnut	Status: 33 Closed, 11 Overdue, 9 In Progress, 7 Open
Open the pencil icon on any chart (shown on hover) to change dimension, metric or Top-N, then use Save Dashboard to export.
In the .xlsx sample, switch to the Control_Test_Results sheet using the dropdown at the top to see the tool adapt to a different structure and use Sum of Exceptions by Process.
4. Synthetic data
Everything in sample-data/ is fictional and generated for demonstration. No real client or company data is used.

File	Contents
audit_issues_sample.csv	60 synthetic audit issues: ID, process, description, risk rating, status, dates, owner (role only), days open, repeat-finding flag
audit_issues_sample.xlsx	Same issues on sheet Audit_Issues, plus 22 control-test results on Control_Test_Results
Processes covered: Procure to Pay, Order to Cash, Hire to Retire, Fixed Assets, Financial Close, IT General Controls, Inventory, Treasury.

5. How it works (short version)
Parsing: SheetJS reads the workbook in the browser.
Column typing: header keywords (risk, status, date, process...) combined with value checks on up to 200 non-blank values per column. Dates accept ISO, dd/mm/yyyy, Mon yyyy, dd-Mon-yyyy and Excel serial numbers; day-first versus month-first is inferred from the data.
Aggregation: count, sum or average by any dimension in one pass; dates are grouped by month; long category lists collapse into Top-N plus "Other".
Charts: Chart.js, with dark mode support and keyboard-accessible controls.
Export: SheetJS for Excel, PptxGenJS (loaded on demand) for PowerPoint.
Full detail, including every detection rule: docs/HOW_IT_WORKS.md

6. Privacy
All processing happens in the browser. The file you upload is never sent anywhere. The only network requests are for the open-source libraries listed below.

7. Known limitations
Needs an internet connection on first load, because SheetJS, Chart.js and PptxGenJS come from public CDNs.
Charts are single-series (one dimension, one metric). No cross-filtering or pivoting.
The Excel export contains the chart data tables, not native Excel charts. The PowerPoint export contains native charts.
Exports carry summary numbers only (up to 50 points per chart), not the raw data.
Column detection is heuristic. Where it guesses wrong, use Detected columns to override the type.
The first non-empty row of a sheet is treated as the header row.
8. Tech stack
HTML, CSS and vanilla JavaScript in one file, with SheetJS 0.18.5, Chart.js 4.4.1 and PptxGenJS 3.12.0.

9. Repository structure
.
├── index.html                      # the tool (open directly in a browser)
├── sample-data/
│   ├── audit_issues_sample.csv     # synthetic audit issue log
│   └── audit_issues_sample.xlsx    # same data + control test sheet
├── docs/
│   ├── HOW_IT_WORKS.md             # detection and aggregation rules
│   └── PROMPT_USED.md              # prompt and build approach
├── LICENSE
└── README.md
10. About this project
Built as a portfolio project to show how audit and compliance reporting work can be automated with AI-assisted development. I define the reporting requirement from my experience in risk-based audit and compliance engagements (BFSI, Insurance and Healthcare clients), and the tool was built with AI assistance and checked against that requirement.

A project by,

CA Sweta Mohanty| www.linkedin.com/in/caswetamohanty| caswetamohanty@gmail.com
