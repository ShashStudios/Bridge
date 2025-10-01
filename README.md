# 🏨 Hotel Pro Forma Builder (MVP)

**Live Demo:** https://bridge-proforma.vercel.app/  
**Stack:** Next.js · TypeScript · Tailwind CSS · shadcn/ui · Recharts

A streamlined, browser-based tool for hotel developers to model a **simple 5–20 year pro forma** and instantly visualize **Revenue, Expenses, RevPAR, Occupancy, and NOI**. Inputs update outputs in real time; charts and tables are exportable.

---

## ✨ Highlights

- **Interactive Inputs** (sliders + numeric fields) with instant recalculation
- **Key Metrics Cards**: RevPAR, Occupancy, Total Revenue, NOI (+ margin)
- **Tabbed Dashboards**: Overview · Revenue · Expenses · Profitability
- **Charts**: Trends with hover tooltips; toggle between multiple views
- **Tables**: Year-by-year summary for 5–20 years
- **Exports**: CSV export (PDF report generation WIP); AI “Generate Report” summary

---

## 🔗 Quick Links

- **Live:** https://bridge-proforma.vercel.app/
- **Status:** MVP focused on clarity and speed; assumptions are intentionally simple
- **License:** MIT (example—adjust as needed)

---

## 🧮 Financial Model (MVP)

> The MVP uses standard hotel math with minimal assumptions for speed and clarity. Values recalc automatically on input change.

**Inputs**
- Rooms (integer)
- Base Occupancy (%)
- Base ADR ($)
- ADR Growth (%/yr) _(slider)_
- Occupancy Growth (%/yr) _(slider)_
- Expense Growth (%/yr)
- Projection Horizon (5-20 years)

**Derived Metrics**
- **RevPAR** (per year `y`):  
  `RevPAR_y = ADR_y × Occ_y`
- **Occupied Room-Nights**:  
  `OccRooms_y = Rooms × 365 × Occ_y`
- **Rooms Revenue**:  
  `RoomsRev_y = OccRooms_y × ADR_y`
- **Other Revenue** (MVP assumption):  
  `OtherRev_y = RoomsRev_y × k`  _(k ≈ 10–15% in the current model)_
- **Total Revenue**:  
  `TotalRev_y = RoomsRev_y + OtherRev_y`
- **Expenses** (MVP global growth):  
  `Expenses_y = Expenses_(y-1) × (1 + ExpenseGrowth)`  
  _(Year-1 is seeded from a base; future versions support fixed vs. variable)_
- **NOI**:  
  `NOI_y = TotalRev_y − Expenses_y`  
  `NOI Margin_y = NOI_y / TotalRev_y`

**Growth Curves**
- `ADR_y = ADR_(y-1) × (1 + ADRGrowth)`
- `Occ_y = min(1.0, Occ_(y-1) × (1 + OccGrowth))`  _(capped at 100%)_

> ℹ️ **Transparency:** The app surfaces all displayed figures. Future iterations will expose “Other Revenue %” and expense category seeds so power users can tune assumptions directly.

---

## 🖥️ UI/UX Notes

- **Top KPI cards** for instant read: NOI (and margin), Total Revenue, RevPAR, Occupancy
- **Tabbed workspace** separates concerns and reduces cognitive load
- **Graph toggle** to switch among Revenue, Expenses, NOI, and RevPAR trends
- **Expense Analysis** pie + trend chart (Payroll, Utilities, Marketing, Maintenance, Other)

**Validation & Guardrails**
- Occupancy capped at **100%**
- Basic input validation for negative/invalid values
- Visual cues for unusually high expense ratios (future—warning badges)

---

## 🧰 Tech Stack

- **Framework:** Next.js (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **UI Library:** shadcn/ui (Radix primitives; accessible components)
- **Charts:** Recharts
- **Build/Deploy:** Vercel
- **AI (optional):** “Generate Report” uses an LLM summary of the computed table/charts (no private data persisted)

---

## 🚀 Getting Started (Local)

```bash
# 1) Clone
git clone https://github.com/ShashStudios/Bridge.git hotel-pro-forma
cd hotel-pro-forma

# 2) Install
pnpm install        # or npm install / yarn

# 3) Run
pnpm dev            # or npm run dev / yarn dev

# 4) Open
# http://localhost:3000
