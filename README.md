# om621_assignments
# OM 621 — Advanced Visual Analytics
## Assignments 1–3 (Milestone IV) • Repository README

**Student:** Brenda Laime Jalil  
**Course:** OM 621 — Advanced Visual Analytics (Fall 2025)

> This repo is my complete, end‑to‑end story for the **Transportation Cost Estimation & Forecasting** case.  
> It includes: my Assignment 1 story artifacts, a **single cohesive Python notebook** that combines Assignments 2 & 3, clean **plots**, and a **Power BI** area for dashboards. The goal is to make this project easy to understand, reproduce, and extend.

---

## 🎥 3–5 Minute Video Overview (Watch First)
**Video:** `assets/video_overview.mp4` (placeholder)  
In this short video I walk through:
- The **3‑minute story** from Assignment 1 (stakeholders, problem, why it matters)
- A quick tour of the **combined Python notebook** (A2+A3) and the main visuals
- A peek at the **Power BI** dashboard (time‑series patterns by mode & seasonality)
- Key takeaways and **what I’d do next** for better forecasting

> If you’d like to record a similar walkthrough yourself, Zoom’s screen‑recording guide is helpful: https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0063640

---

## 📁 Repository Structure

```
.
├── data/                       # Source datasets (kept lightweight or sampled if needed)
│   └── tr_data_22_24.csv
├── notebooks/                  # Python work (combined notebook for A2+A3)
│   └── OM621_A2_A3_Combined.ipynb
├── plots/                      # Auto‑saved figures from the notebook
│   ├── delay_dist_by_mode.png
│   └── invoice_ts_by_mode.png
├── pbi/                        # Power BI files (PBIX) and exported visuals
│   ├── OM621_Dashboard.pbix           (placeholder)
│   └── exports/                        (optional images/PDFs)
├── assets/
│   └── video_overview.mp4      # 3–5 minute recorded walkthrough (placeholder)
├── README.md                   # You are here
└── LICENSE                     # (optional)
```

**Why this matters:** The folder layout mirrors course expectations. Anyone can open the README, watch the short video, and then dive into notebooks/plots or the PBI file.

---

## 🧭 Fast Start

**To reproduce the Python analysis:**
1. Ensure the dataset exists at `data/tr_data_22_24.csv`.
2. Open and run `notebooks/OM621_A2_A3_Combined.ipynb` **top‑to‑bottom**.
3. Plots will be saved automatically to `plots/`.

**Python deps (tested locally):**
- `pandas`, `numpy`
- `plotnine` (for ggplot‑style charts)
- Python ≥ 3.10 recommended

You can install the basics with:
```bash
pip install pandas numpy plotnine
```

**Power BI:**  
Open `pbi/OM621_Dashboard.pbix` in Power BI Desktop (placeholder, included to host dashboard work for Milestone IV).

---

## 🧩 Assignment 1 — Story Artifacts (Who / What / How & Storyboard)

### 3‑Minute Story (my condensed version)
- **Who (Audience):** Director of Supply Chain (primary), consulting manager, and the director’s analyst team.
- **What (Problem):** Transportation invoices often arrive **weeks to months** after shipments. This delay adds noise to monthly cost reporting and makes forecasts unreliable.
- **Why it matters:** Budgeting and cash planning suffer; late accruals and surprise spikes make stakeholders lose confidence.
- **How (Approach & Value):**  
  1) Build a transparent **delay feature** (Invoice − Ship date) and study it by **mode/region/site**.  
  2) Explore **invoice time‑series** by month and mode to pick up **trend/seasonality**.  
  3) Use **median delay by mode** for accrual timing and **mode‑level seasonal baselines** to stabilize monthly estimates.  
  4) Summarize into simple visuals + an action plan the team can actually use.

### Storyboard (high level)
1. **Context slide:** who/what/why now.  
2. **Delay 101:** define the delay, show the overall shape (skew + long tail).  
3. **Delay by mode:** *Which modes really drive the long tail?* (boxplot, ordered).  
4. **Time series by mode:** lines grouped by year → see seasonality + trend clearly.  
5. **So what:** accrual timing rules by mode + forecasting recipe.  
6. **Next steps:** data hygiene, alerts, and deeper modeling options.

---

## 🐍 Assignments 2 & 3 — Single Combined Notebook (Python)

**Notebook:** `notebooks/OM621_A2_A3_Combined.ipynb`  
What it does, in order:
1. **Data expectation vs reality (A2.Q1):** What I expected (from A1) vs. what’s in the file; risks (missing site/division, label typos) and how I mitigate them.
2. **Basic exploration (A2.Q2):** Non‑null audit and invoice stats (mean/median/IQR/min/max).  
3. **Basic visuals (A2.Q3):** Tasks by site (and by region) + tasks by mode.  
4. **Delay feature (A2.Q4):**  
   - Create `delay = invoice_date − shipping_date` (days).  
   - **Hist/density** by region and **top sites**, with short explanations.  
   - **Delay vs invoice** overall, by region, and for top sites.
5. **Delay by mode (A2.Q5):** Distribution across modes; notes on skew and long tails.
6. **Delay distribution by mode (A3.Q1):**  
   - **Ordered, horizontal boxplot** (largest median delay at the top).  
   - **Human‑readable labels** (LTL, FTL, LCL, FCL, etc.).  
   - Saved to `plots/delay_dist_by_mode.png`.
7. **Invoice time series (A3.Q2):**  
   - Show why a single daily total is noisy.  
   - **Better view:** **Monthly lines grouped by year**, **faceted by mode** to surface trend & seasonality.  
   - Saved to `plots/invoice_ts_by_mode.png`.
8. **Cost estimation & forecasting (A3.Q3):**  
   - **Seasonality:** recurring shape in several modes.  
   - **Trend:** container modes trend up; parcel/air flatter.  
   - **Recipe:** forecast each mode separately (seasonal baseline + recent trend), adjust accruals using **median delay by mode**, add buffers for container modes’ long tails.

---

## 📊 Highlights & Findings

- **Delays are right‑skewed** everywhere; the long tail is where risk hides.  
- **Mode matters:** LCL/FCL show **longer, wider** delay distributions; parcel/air are faster and tighter.  
- **Time‑series patterns differ by mode:** some show **seasonality** and **upward trends** (especially container modes).  
- **Actionable rules:**  
  - Use **median delay per mode** for accrual timing.  
  - Build **mode‑level forecasts** (seasonal baseline + trend) and then sum to a total.  
  - Prioritize data hygiene (label standardization, reduce “missing site”), and set **alerts** for potential long delays.

---

## 🛠️ Reproducibility Notes

- Plots are generated by the notebook and saved into `plots/`.  
- The dataset is used **as‑is**. I standardize a known typo (`parcel_grund` → `parcel_ground`) in‑notebook so results are consistent.  
- If you add more years or fields, the notebook will still run; you’ll just get richer charts.

---

## 📈 Power BI (Dashboard)

The `pbi/` folder hosts my PBIX and any exports. The dashboard mirrors the notebook story so a non‑Python stakeholder can explore:
- Slicers by **mode**, **region**, **site**
- Monthly **invoice trends** with **year‑over‑year** comparison
- A small panel summarizing **median delay by mode** for accrual guidance

---

## 📚 References

- Karimi, M. (2025). *Grammar of Graphics; Visualization Refinement; Advancing Simple Graphics* [Class materials].  
- McKinney, W. (2017). *Python for Data Analysis* (2nd ed.). O’Reilly.   
- Course dataset: `tr_data_22_24.csv` (2022–2024 transportation records).

> I cite plotnine since I’m explicitly using `geom_boxplot`, `facet_wrap`, etc.

---

## 🙌 Acknowledgments

Thanks to my OM 621 cohort and Professor Karimi for the structure and feedback that helped refine the visuals, the writing, and the overall storytelling approach.

---

## 🔜 What I’d Do Next

- Add **carrier** and **contract** features to explain long delays vs. typical.  
- Bring in **holiday calendars** and **port events** to improve forecasting.  
- Productionize a **simple alert** when predicted delay exceeds a threshold (e.g., 45 days).

---

*If you’re reviewing this repo, start with the video, skim the plots, and then open the combined notebook for details.*
