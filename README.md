# Vertex Capital Solutions: A Strategic Data Analysis
*(A B2B/FinTech Portfolio Project)*

This repository contains a full-cycle data analysis project. It takes a complex, real-world business problem, breaks it down using Python and machine learning, and delivers a clear, actionable strategic recommendation.

* **Python Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn
* **Analysis:** Feature Engineering, K-Means Clustering, Marketing Channel Attribution, Customer Voice Analysis
* **Jupyter Notebook:** `Vertex_Capital_Analysis.ipynb`

---

## 1. The Problem Statement

**Vertex Capital Solutions** is a mid-sized financial services firm at a strategic crossroads.

Founded as a boutique firm for high-net-worth (HNW) clients, its core **"Vertex Bespoke"** service was praised for high-alpha returns and personalized, "white-glove" service.

In 2023, to scale and compete with FinTech apps, Vertex launched **"Vertex Go"**—a mainstream robo-advisor app. The launch was a commercial disappointment. It failed to gain significant market share, and worse, it created a **"brand fracture."**

**The core business problem:** The "Vertex Go" app is draining the marketing budget, customer acquisition costs (CAC) have soared, and revenue has stalled. The CMO needs to present a data-driven strategy to the board:

> **Should Vertex retreat to its profitable HNW niche, double down on the risky "Vertex Go" app, or is there a way to master both?**

## 2. The Data

The analysis is based on a unified (mock) dataset provided in `vertex_capital_data.xlsx`. This single file contains 7,380 transactions and merges four key data sources:

1.  **Transaction Data:** `service_id`, `annual_management_fee`, `cost_of_service`, `referral_discount`.
2.  **Client Demographics:** `avg_income`, `region_code`.
3.  **Client Behavior:** `service_level_focus` (e.g., 'High-Touch'), `price_sensitivity`, `brand_affinity_score`, `churn_rate`.
4.  **Marketing Attribution:** `experiment_condition` (e.g., 'Fin-Tok Influencer'), `referring_channel` (e.g., 'AdvisorFinda.com', 'Social').
5.  **Client Feedback:** `review_star` and a categorical `review_text` (19 distinct "canned" reviews).

## 3. Analytical Approach

My 5-step process was designed to (1) understand the business, (2) identify the customers, (3) analyse marketing effectiveness, (4) listen to the customer's voice, and (5) deliver a clear strategic recommendation.

1.  **High-Level Analysis:** Is the business profitable, and where?
2.  **Customer Segmentation:** Who are our different customer types? (K-Means Clustering)
3.  **Segment Visualisation:** Create a "Persona Chart" to visualise the segments.
4.  **Marketing Analysis:** Which channels are acquiring our best (and worst) clients?
5.  **Customer Voice Analysis:** What are clients *saying*, and does it confirm the "brand fracture"?

---

## 4. Step-by-Step Analysis & Findings

### Step 1: High-Level Analysis (Niche vs. Mainstream)

First, I engineered a `profit` column for every transaction and a `service_category` ('HNW/Bespoke' vs. 'Mainstream/Go') to compare the two business lines.

**Finding:** The "Mainstream/Go" app is a high-effort, low-profit volume trap.
* **HNW/Bespoke:** Generates **75% of total profit** from only **22% of clients**.
* **Mainstream/Go:** Generates only 25% of profit despite making up **78% of the client base**.
* The "Bespoke" service is **10x more profitable per client** and has a **4.65-star** rating, while the "Go" app is at a mediocre 3.98 stars.

This immediately proved that the company's *profit engine* is its original niche.

<img width="844" height="548" alt="image" src="https://github.com/user-attachments/assets/634fa103-9722-40ba-94df-06dceb8f8554" />

<img width="833" height="548" alt="image" src="https://github.com/user-attachments/assets/dc5f5fc4-9ca4-4c3a-9434-53034ad00eba" />



### Step 2: Customer Segmentation (K-Means Clustering)

I used K-Means clustering on 5 key behavioural features (`avg_income`, `service_level_num`, `price_sensitivity_num`, `brand_affinity_score`, `churn_rate`). The "Elbow Method" showed a clear optimal number of 4 clusters.

<img width="864" height="548" alt="image" src="https://github.com/user-attachments/assets/0e2556ae-cd36-46d3-a9d2-95a9b888a8b0" />


These 4 clusters defined our client "personas":

* **Cluster 2: The "HNW Purist" (Our Golden Segment)**
    * **Profile:** Highest income, highest service demand, lowest price sensitivity, highest brand affinity.
    * **Behavior:** Our most profitable segment (€706 profit/client). They buy 85% "HNW/Bespoke" services.
    * **CRITICAL FINDING:** They have the **highest churn rate (0.22)**. We are actively losing our best clients.

* **Cluster 0: The "App-Only User" (The Volume Trap)**
    * **Profile:** Lowest income, highest price sensitivity, lowest brand affinity.
    * **Behavior:** Our largest segment (3,463 clients) but our *least profitable* (€120 profit/client). They buy 95% "Mainstream/Go."

* **Cluster 1: The "Vertex Fan" (The Loyal Base)**
    * **Profile:** Good income, high brand affinity, and very low churn (0.08).
    * **Behaviour:** Our "upsell" audience. They are profitable (€224/client) and are willing to "buy up," with 20% of their purchases in the HNW category.

* **Cluster 3: The "Aspiring HNW" (The Growth Segment)**
    * **Profile:** Good income and demand high service (like HNW Purists) but are still price-sensitive. Also very loyal (0.08 churn).
    * **Behaviour:** Our most obvious growth path. They *want* the high-end service, even if they're currently on the "Go" app.

### Step 3: Segment Visualisation (The "Persona" Chart)

This single chart visualises the entire business problem. It shows the four segments plotted by their defining traits.

* **X-Axis:** Service Level Demand
* **Y-Axis:** Price Sensitivity
* **Bubble Size:** Number of Clients
* **Color:** Profitability (Yellow=Low, Purple=High)

This chart clearly shows the business is being dragged down by a **massive, low-profit yellow bubble (Cluster 0)**, while its true value comes from a **smaller, high-profit purple bubble (Cluster 2)**.

<img width="1200" height="704" alt="image" src="https://github.com/user-attachments/assets/7d9e2caf-1515-4d6a-946d-4720d5eed684" />


### Step 4: Marketing Analysis (The "Smoking Gun")

This is where the story comes together. I connected our new segments to the marketing channels.

**Finding:** The company's marketing strategy is *inverted*.
* The **`Fin-Tok Influencer`** campaign is a disaster, attracting **50% Cluster 0** (our worst clients) and only **5% Cluster 2** (our best).
* `Social` and `Search` channels are equally broken, attracting 57% and 53% of Cluster 0.
* **`AdvisorFinda.com`** is the **"Golden Channel."** It's our only effective acquisition tool, attracting **43% "HNW Purists" (Cluster 2)**.

Shockingly, the `Control` (no marketing) group was 6x more effective at acquiring Cluster 2 clients than the `Fin-Tok` campaign. We are paying to acquire our worst clients.


<img width="982" height="625" alt="image" src="https://github.com/user-attachments/assets/7e8f7f7b-66ba-4faf-addd-9cec7ba6d424" />


<img width="1137" height="625" alt="image" src="https://github.com/user-attachments/assets/7a1f4716-3691-4a38-86d0-0d3caef6784a" />


### Step 5: Customer Voice Analysis (The "Why")

Finally, I analysed the `review_text` to understand the "why" behind the numbers.

**Finding:** The "brand fracture" is real and is confirmed in the clients' own words.
* **`Go App` Client Reviews (from Fin-Tok):**
    * "The app is very simple; it's **fine for my weekly $50 deposit**."
    * "Good value **for a free app**;... gets the job done."
    * *(The "Fracture"):* "Returns are flat... **below expectations for this brand**."

* **`HNW/Bespoke` Client Reviews (from AdvisorFinda):**
    * "My advisor provides **exceptional alpha** and proactive **tax-loss harvesting**."
    * "**Impressive risk-adjusted returns** and a neutral portfolio."
    * "The **client service is superb**..."

**Conclusion:** The marketing is attracting low-expectation "app" clients (Cluster 0) and disappointing sophisticated clients (Cluster 1 & 3), while the core business (Cluster 2) uses a completely different language.

---

## 5. Final Strategic Recommendations

Based on the 5-step analysis, the "Master of Both" strategy is failing. The data points to a clear, decisive path forward.

1.  **DIVEST:** **Immediately halt all spending** on the `Fin-Tok Influencer` campaign and all paid marketing on `Social` and `Search`. These channels are a net-negative for profitability and brand health.
2.  **REFOCUS:** **Re-allocate 100% of that saved marketing budget** to our proven, high-ROI "golden channel": **`AdvisorFinda.com`**.
3.  **NURTURE & UPSELL:** **Target our "growth" segments** (Cluster 1 "Vertex Fans" and Cluster 3 "Aspiring HNWs") with marketing that creates a clear "upgrade" path from the app to a "Bespoke-Lite" service.
4.  **FIX THE CHURN:** **Treat the high churn of Cluster 2 as a top priority.** Launch a "white-glove" re-engagement campaign to this *specific cluster*, reinforcing our commitment to the "exceptional alpha" and "superb service" they value.

## 6. Tools Used

* **Python 3**
* **Pandas:** For data manipulation, cleaning, and aggregation.
* **Matplotlib & Seaborn:** For all data visualizations.
* **Scikit-learn (sklearn):** For `StandardScaler` and `KMeans` clustering.
* **Jupyter Notebook:** As the coding environment.
