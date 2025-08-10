# PnP Clarity — Mini Studio (No‑Build HTML App)
_Last updated: August 10, 2025_

This repo contains:
- **index.html** – a no‑build, single‑file web app that reads Google Apps Script JSON endpoints (from your Sheets) and renders:
  - Waterfalls (placeholders ready for Chart.js hookup)
  - Production Plan table (sortable, alternating rows)
  - Purchasing Plan table (sortable, alternating rows)
- This README – context, endpoints, what’s working, and next steps.

---

## Live JSON Endpoints

**Base deployment**  
`https://script.google.com/macros/s/AKfycbzURBxvHmhXdptzjJNGO01INhZxDqLt2XIRJG_ofLVoqLEk9uQEB6M9UYNWS5H1_eiBDw/exec`

**Feeds** (append `?sheet=`):
- inventoryFlow  
  `https://script.google.com/macros/s/AKfycbzURBxvHmhXdptzjJNGO01INhZxDqLt2XIRJG_ofLVoqLEk9uQEB6M9UYNWS5H1_eiBDw/exec?sheet=inventoryFlow`
- ProductionPlan  
  `https://script.google.com/macros/s/AKfycbzURBxvHmhXdptzjJNGO01INhZxDqLt2XIRJG_ofLVoqLEk9uQEB6M9UYNWS5H1_eiBDw/exec?sheet=ProductionPlan`
- purchasingPlan  
  `https://script.google.com/macros/s/AKfycbzURBxvHmhXdptzjJNGO01INhZxDqLt2XIRJG_ofLVoqLEk9uQEB6M9UYNWS5H1_eiBDw/exec?sheet=purchasingPlan`
- openPOs (optional)  
  `https://script.google.com/macros/s/AKfycbzURBxvHmhXdptzjJNGO01INhZxDqLt2XIRJG_ofLVoqLEk9uQEB6M9UYNWS5H1_eiBDw/exec?sheet=openPOs`
- ProposedProduction (optional)  
  `https://script.google.com/macros/s/AKfycbzURBxvHmhXdptzjJNGO01INhZxDqLt2XIRJG_ofLVoqLEk9uQEB6M9UYNWS5H1_eiBDw/exec?sheet=ProposedProduction`

> If your deployment URL changes, update `ENDPOINTS` inside **index.html**.

---

## Data expectations (inventoryFlow)
Monthly columns repeat as:
- `<Mon-YY> Start`
- `<Mon-YY> Forecast`
- `<Mon-YY> Component Usage`
- `<Mon-YY> Purchases`
- `<Mon-YY> Production`
- `<Mon-YY> End`

Example: `Aug-25 Start … Aug-25 End`, `Sep-25 Start … Sep-25 End`, etc.

---

## What works now
- Page tabs (Waterfalls / Production / Purchasing).
- Production & Purchasing tables:
  - Sortable headers (client‑side).
  - Alternating row shading.

## What still needs wiring
- Waterfalls:
  - Populate **Description / Product Line / Component Level** dropdowns from `inventoryFlow`.
  - Aggregate month deltas and render **chained waterfall** (Chart.js stacked bars).
  - Separate FG (ExpenseType=Production) vs Components (ExpenseType≠Production).
- Production:
  - Visual group bands by **Build Group ID**, while globally sorting by **Target Completion Date**.
- Purchasing:
  - Sections by **PO Status**; highlight rows with **PO Placed Date** within 30 days.

---

## Run it
- Open **index.html** in a browser.
- You should see tables populate if endpoints return `{ data: [...] }`. If not, open DevTools → Console to inspect payload shape and adjust mapping in **index.html**.

---

## Next steps (recommended)
- Confirm exact JSON keys (e.g., `Description`, `Product Line`, `Component Level`, `ExpenseType`, `Category`) and adjust the mapping in **index.html**.
- Implement the waterfall math and Chart.js rendering.
- Add dependent (cascading) dropdown logic for the four waterfall blocks.

-–
