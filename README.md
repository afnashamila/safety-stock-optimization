Safety Stock Optimization — King's Formula vs. Weighted Average Method
Supply Chain Analytics | Excel | Inventory Management
> Internship Project — Footwear Manufacturing Company (Supply Chain Management Division)
---
Problem Statement
In footwear manufacturing supply chains, demand is seasonal, promotional, and uncertain. The company's existing safety stock method — a weighted average formula — relied on simplified assumptions and failed to account for:
Demand variability across product grades (fast-moving, top models, new launches, etc.)
Lead time uncertainty arising from manufacturing cycle time (2–3 days) and transit time (7–10 days nationally)
No reorder point system, meaning restocking decisions were reactive rather than planned
This led to two chronic outcomes: excess inventory during off-peak periods, and stockouts during peak sales windows — costing the company both capital and customer service levels.
---
Objective
To evaluate an alternative, statistically grounded approach (King's Formula) against the company's existing weighted average method, assign the most appropriate formula to each product grade based on the nature of its demand and lead time variability, and generate reorder points to trigger timely restocking.
---
Methodology
Dataset
~105 unique articles (SKUs) across 8 product grades
Sales data for 3 months (February, March, April) at national level, later extended to depot-level analysis for two states
Lead time data collected across 10 orders: average lead time = 8.8 days, standard deviation = 1.03 days
Existing Method (Baseline)
The company used a weighted average formula called NOM (normalized order measure):
```
NOM = Weighted Average Sales + (Transit Day Sale / 26) × 10

Transit Day Sale = Per Day Sale × 12
```
Weights assigned: 50% to the highest-sales month, and 20%, 15%, 15% to the remaining months. This method ignores demand variability and has no probabilistic service level target.
Alternative Method — King's Formula
Four variants of King's Formula were applied depending on the source of variability for each product grade:
Formula	When Applied	Equation
Method 1	Demand + Lead Time uncertainty (independent)	`SS = z × √(LT_avg × σ_demand² + avg_sales² × σ_LT²)`
Method 2	Demand uncertainty only	`SS = z × σ_demand × √LT_avg`
Method 3	Lead time uncertainty only	`SS = z × avg_sales × σ_LT`
Method 4	Demand + Lead Time uncertainty (dependent)	`SS = z × σ_demand × √LT_avg + z × avg_sales × σ_LT`
Service level target: 90% → z-score = 1.28
Average demand was calculated as total 3-month sales ÷ 78 working days (26 days/month).
Formula Assignment by Product Grade
Each of the 8 product grades was analysed and assigned the most appropriate formula:
Grade	Method Assigned	Rationale
Top Models	Method 1	High, consistent sales; lead time and demand variabilities are independent
Competition Similar	Method 4 (Method 1 for one high-volume article)	Lead time changes affect demand; maximum stock needed
Fast Moving	Method 1	High sales volume, continuous demand
Running	Method 1	High sales, always in demand
PT Fast Moving	Method 1	High sales volume
PT Running	Method 1 (Method 1 or 2 for 3 articles)	Some articles have identical Method 1 and 2 outputs
PT Top Models	Method 1	High, consistent demand
PT New Models	Method 2	New to market; demand still building; only demand-side uncertainty expected
Reorder Point
For each article:
```
Reorder Point = Safety Stock + (Average Daily Sales × Lead Time)
```
An intimation threshold was also built: if total stock on hand falls within 10% of the reorder point, a restocking alert is triggered.
For very high-demand articles where the formula-derived reorder point exceeded practical depot storage capacity, a 90% reorder point was applied instead.
---
Results
King's Formula produced significantly different safety stock levels compared to the weighted average method for several articles — particularly those with high demand variability
For some articles, results were similar, validating the existing method in stable-demand categories
The analysis revealed that the company's primary inventory problem was not the safety stock quantity itself, but the failure to deliver safety stock to depots in the first place during peak periods
Depot-level breakdowns were completed for Kerala and Tamil Nadu
---
Business Impact
Provided a statistically grounded alternative to an ad hoc weighted average formula, incorporating a target service level (90%) for the first time
Introduced a reorder point system — the company previously had no formal trigger for restocking
Identified the root cause of stockouts: distribution failure to depots, not formula design — a finding with direct strategic implications
Delivered grade-wise formula assignments for all 105 SKUs, making the model operationally actionable without requiring one-size-fits-all assumptions
Recommended a depot-first stocking strategy: fill each depot to its safety stock level before applying reorder logic — directly addressing the peak-season shortage problem
---
Tools Used
Microsoft Excel — safety stock calculations, reorder point modelling, grade-wise analysis, depot-level breakdowns
King's Formula (P.L. King, 2011) — academic framework for safety stock under uncertainty
Z-score / Normal distribution — for service level to safety factor conversion
---
Project Structure
```
safety-stock-optimization/
│
├── data/
│   └── analysis_grade_method_assignment.xlsx.    # 
├── analysis/
│   └── analysis_kings_formula_analysis.xlsx  # Full workings: all 105 articles, 4 methods
├── README.md
```
> Note: Full dataset is proprietary to the company. Only anonymized sample data is shared here.
---
Key Learnings
Applying a single formula to all SKUs ignores meaningful differences in demand behaviour across product grades — grade-wise assignment is more accurate
A probabilistic safety stock model (with explicit service level) is more defensible and adjustable than a weighted average with arbitrary month weights
Operational constraints (depot capacity, distribution reliability) can render even a well-designed formula ineffective — inventory optimization must account for the full supply chain, not just the formula
Reorder points are as important as safety stock levels; without a trigger, safety stock is a static buffer rather than a dynamic system
---
Reference
King, P.L. (2011). Crack the Code: Understanding Safety Stock and Mastering its Equations. APICS Magazine. Available at: MIT Reading List
---
About
Afna | BA Economics | Supply Chain & Data Analytics  
Azim Premji University 
