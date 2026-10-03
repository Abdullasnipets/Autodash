AutoDash AI

Upload your data. Get your dashboard.

AutoDash AI is a single-file, browser-based business intelligence tool. Upload a spreadsheet and it inspects your columns, detects your industry, builds a dashboard, and lets you ask questions about your data in plain English — with every number traceable back to a real calculation on your rows.

No backend. No database. No API keys. Your file never leaves the browser tab.

Why

Most people with a sales or operations spreadsheet don't know Power BI, Tableau, pivot tables, or SQL — and don't want to learn them to answer a simple question like "which region is behind target this month?" AutoDash AI reads the file, figures out what the columns mean, and builds the dashboard a business user would have built by hand — automatically, and without ever making up a number.

Features
Upload & inspect
Drag-and-drop or browse for .xlsx, .xls, or .csv
Row/column/file-size/sheet count shown immediately after parsing
Data Health Report — a transparent 0–100 score built from five measured factors (completeness, duplicate rows, date validity, numeric validity, category consistency), with the exact formula shown, not an arbitrary number
Column intelligence
Matches each column to a business concept (Sales, Target, Quantity, Product/SKU, Sales Manager, Distributor, Geography, etc.) with a confidence level (High / Medium / Low)
Every mapping is editable — correcting a column updates industry detection and the dashboard immediately
Industry detection
Scores the dataset against FMCG, Retail, E-commerce, Automotive, Manufacturing, Distribution/Logistics, and General Business templates based on which columns are actually present
Shows its reasoning ("this dataset contains SKU, ASM, Distributor and Target fields, typical of FMCG data") and can be overridden manually
The selected industry changes which dashboard template is used — it never changes or invents the underlying data
Auto-generated dashboard
KPI cards (Total, Target, Achievement %, Growth, Active entities, Record count) — a card only appears if the dataset actually supports it
Trend chart (monthly, from any detected date column) and a top-category bar chart
A ranking table (by ASM, distributor, product, or region — whichever the data supports) with Target vs. Achievement where available
Live filters (date range + up to three category filters) that recompute every KPI and chart from the underlying rows — nothing is cached or faked
An "Explain" button on every KPI shows the exact formula and the numbers used to produce it
Auto-generated business insights (top contributor, under-target flags, period-over-period spikes/drops), each with a "View calculation" link
Ask Your Data
Type a question — "which ASM has the highest achievement?", "top 5 SKUs by revenue", "compare Delhi and Punjab", "what's the growth this period?"
Answers come from a deterministic rule-based parser, not an LLM — every answer is a real calculation over your parsed rows, and the formula + row count used is shown underneath
If a question needs a column the dataset doesn't have, it says so explicitly instead of guessing
Explore & export
Searchable, sortable, paginated data table, plus a full per-column data profile (type, non-null %, unique values, min/max/avg)
Excel export — a multi-sheet workbook (Dashboard, Cleaned Data, Data Profile, Data Quality)
CSV export — filtered view or full dataset
Chart PNG export
Print-to-PDF — a presentation-ready report via the browser's native print dialog
Three themes: Minimal Light, Executive, Dark Analytics
Tech stack

Everything runs client-side in a single HTML file:

Vanilla JavaScript (no framework) for parsing, profiling, semantic detection, filtering, the dashboard, and the Ask Your Data engine
Chart.js for charts
SheetJS (xlsx) for .xlsx / .xls parsing; a hand-written RFC4180-style parser handles .csv
No build step, no dependencies to install, no server
Getting started
bash
git clone https://github.com/<you>/autodash-ai.git
cd autodash-ai
# just open it
open autodash-ai.html     # macOS
# or double-click the file / serve it with any static server
python3 -m http.server 8000

Then open http://localhost:8000/autodash-ai.html and upload a spreadsheet, or click Try Demo to load a synthetic FMCG dataset.

How the calculation engine works

AutoDash AI follows one rule throughout: the AI layer explains, it never calculates.

Question → Intent detection → Column/metric mapping → Aggregation over real rows → Result → Explanation
Numbers are always produced by summing, grouping, or averaging the actual parsed dataset — never estimated or inferred by a language model
If a required column doesn't exist, the app says so instead of answering
Every KPI, chart, and insight carries its formula and the row count behind it, visible on demand
Scope & limitations

This is a client-side demo, not a hosted SaaS product. It intentionally does not include:

User accounts, authentication, or multi-user access
A server or database — so no saved dashboard history or link-sharing between users
A drag/resize dashboard editor (themes are switchable instead)
An actual LLM for "Ask Your Data" — it's a rule-based pattern matcher by design, which is what keeps every answer traceable to a real calculation

These would be natural next steps for a production version (e.g. a FastAPI + Postgres backend for storage/sharing, and an LLM layer constrained to column-mapping and phrasing rather than arithmetic).

Acknowledgements

Built as a demonstration of a calculation-first, no-hallucination approach to AI-assisted analytics: the interface and narrative layer can be flexible, but the numbers are never allowed to be.

some screenshots 👇👇👇

<img width="1920" height="1080" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/306b0d1a-2a84-492a-aa85-4ef3d926dec9" />
<img width="1920" height="1080" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/888082d8-4c6b-42bf-82d0-3c6408234bc7" />
<img width="1920" height="1080" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/96bd7d35-f59f-4c79-b3e3-b98ce27fbe50" />
<img width="1920" height="1080" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/11114517-ae12-4615-a2c6-669f21a9963d" />
<img width="1920" height="1080" alt="Screenshot (13)" src="https://github.com/user-attachments/assets/a0c5c6cf-5a23-4e65-8654-efc408a4e776" />
<img width="1920" height="1080" alt="Screenshot (12)" src="https://github.com/user-attachments/assets/6e4e4f48-5f3c-4a6a-8695-1244dd1b7caf" />
<img width="1920" height="1080" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/308e0aee-81f2-4a41-a13d-096d98b9fa83" />










