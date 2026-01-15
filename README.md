# **CUSTOMER FEEDBACK ANALYSIS SYSTEM**


## PROJECT OVERVIEW

This project is a **customer feedback analysis system** that allows users or customers to submit product reviews and have insights through an interactive dashboard.  
It takes feedback for multiple jewellery products, do **sentiment analysis and theme detection**, collect results per product and presents them using pie chart and generated insights.

The system is designed in such a way that it is **transparent and explainable** (no AI), making it easy to understand, debug and extend.  
The frontend UI is styled with a **GIVA-inspired design** to resemble a real e-commerce analytics interface.

---

## TECH STACK

### Frontend
- HTML
- CSS
- JavaScript  
- Chart.js (for sentiment visualization's pie chart)

### Backend
- Node.js  
- Express.js  

### Data Storage
- In-memory storage (JavaScript objects/arrays)  

### Tools
- npm  
- Browser DevTools  
- Postman / browser fetch for API testing  

---

## SYSTEM FLOW AND LOGIC

### 1. Feedback Submission Flow
1. User selects a product, rating (1–5) and writes a review.
2. Frontend sends a `POST /feedback` request.
3. Backend:
   - Analyzes sentiment using pre-defined keyword based rules.
   - Detects themes (appearance, durability, comfort).
   - Stores feedback in memory.
4. Frontend resets the form and updates the dashboard context.

---

### 2. Data Processing Logic

#### Sentiment Analysis
- Rule-based keyword matching.
- Outputs: `positive`, `negative` or `neutral`.

#### Theme Detection
- Keywords mapped to themes:
  - Appearance
  - Durability
  - Comfort
- A single review may belong to **multiple themes**.

#### Theme Aggregation
- Themes are grouped **per product**.
- Counts are computed dynamically to avoid duplicates.

---

### 3. Dashboard Logic
1. Frontend calls `GET /feedback/dashboard/:productId`.
2. Backend returns:
   - Sentiment counts
   - Theme counts
3. Frontend:
   - Renders a pie chart (Positive / Negative / Neutral).
   - Displays explicit counts and totals.
   - Shows theme breakdown.
4. A **dedicated dashboard dropdown** allows switching products independently of the submission form.

---

### 4. Insight Generator Logic
- Insights are generated using rule-based conditions.
- Issues are **only when negative sentiment dominates**.
- Zero review and low data scenarios are handled explicitly.

---

## KEY FEATURES

- Product wise feedback submission  
- Button-based rating system (1–5)  
- Rule based sentiment analysis  
- Theme detection & aggregation  
- Interactive sentiment pie chart  
- Explicit count display  
- Product switchable dashboard  
- Insight generator with rules  
- Handling of edge cases  
- Clean separation of form state and dashboard state  

---

## EDGE CASES, BUGS AND FIXES

### 1. CORS & Fetch Errors
- **Issue:** Browser blocked API requests.
- **Fix:** Added proper CORS middleware in Express.

---

### 2. Pie Chart Showing Incorrect Totals
- **Issue:** Pie chart total didn’t match number of reviews.
- **Cause:** Neutral sentiment was excluded.
- **Fix:** Added neutral category and updated chart logic.

---

### 3. Empty Chart for Zero Reviews
- **Issue:** Chart.js rendered an empty or broken-looking pie chart.
- **Fix:** Detect zero-review case, hide the chart and show a clear message.

---

### 4. Dashboard Always Showing Ring Data
- **Issue:** Dashboard defaulted to `ring_1` after form submission.
- **Fix:** Introduced a dedicated `lastSelectedProduct` dashboard state.

---

### 5. Stale Dashboard Data After Submitting Feedback
- **Issue:** Dashboard title and dropdown updated, but chart stayed on previous product.
- **Root Cause:** Dashboard relied on global state.
- **Fix:** Refactored `loadDashboard(productId)` to accept explicit product context.

---

### 6. Insights Persisting When Switching Products
- **Issue:** Old insights remained visible after product change.
- **Fix:** Cleared insight output whenever dashboard data reloads.

---

### 7. Incorrect Insights for Positive Feedback
- **Issue:** “Issues detected” shown even for positive reviews.
- **Fix:** Insights now trigger **only when negative sentiment dominates**.

---

### 8. Zero-Review Insight Bug
- **Issue:** “Feedback is balanced” displayed even with no reviews.
- **Fix:** Added early return for zero-review scenarios.

---

## HOW TO RUN AND TEST

### 1. Install Node.js (Required)

1. Visit: https://nodejs.org/en
2. Download and install the **latest LTS (Long Term Support)** version.
3. Verify installation:
   ```bash
   node -v
   npm -v
   ```

### 2. Install Project Dependencies

- From the project root directory:
   ```bash
   npm install
   ```

### 3. Start the Backend Server


   ```bash
      node index.js
   ```

- Server will run on:
      ```
      http://localhost:3000
      ```
      
### 4. Open the Frontend

1. Navigate to the frontend/ folder.
2. Open index.html in any modern browser.

### 5. Test the Application

- Submit feedback for different products.
- Observe:
   - Form reset behavior
   - Dashboard auto-switching to submitted product
- Use dashboard dropdown to view other products.
- Click *Generate Insights* to view recommendations.
- Test edge cases:
   - Zero reviews
   - Single review
   - Mixed sentiment

---

## Notes

- All data is stored in memory and resets on server restart.
- The project prioritizes clarity, correctness and explainability.