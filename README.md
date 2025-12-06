# Product Dissection & Schema Design: Zerodha KITE

### 📄 Project Summary
The **Zerodha KITE Capstone Project** demonstrates readiness for Data Analyst roles by reverse-engineering the backend logic of India's largest fintech platform.

The objective of this project was to bridge the gap between business strategy and data engineering. I analyzed the real-world problems Zerodha solves (like high costs and fragmented technology) and translated them into a robust **Relational Database Schema** capable of supporting millions of daily transactions.

* **Domain:** Fintech / Stock Market
* **Focus:** Database Design, System Architecture, Data Modeling
* **Video Presentation:** [Click Here to Watch My Presentation](https://drive.google.com/file/d/1triTuWmyuTMwSnjXy8OvehUG7OQStbVw/view?usp=sharing)

---

### 🧩 Problem Statement
Before Zerodha, the Indian brokerage industry faced three critical issues that limited participation from retail investors:

1.  **High Costs:** Traditional brokers charged percentage-based fees, making trading expensive for small investors.
2.  **Fragmented Tech:** Traders had to use disjointed tools, one for trading, one for charts, and another for reporting.
3.  **Manual Monitoring:** Investors had to watch the screen all day to track prices, often missing opportunities.

**The Solution:**
KITE introduced a "Discount Brokerage" model and a unified web stack. This project maps these features to a normalized database schema that optimizes for speed and data integrity.

---

### 🛠️ Technical Architecture & Logic

My design focuses on two critical architectural decisions to ensure the app is fast and reliable.

#### 1. Core Logic: Separating "History" from "Current State"
The most important decision in this schema is separating the **Order Table** from the **Holding Table**.

* **`Order` Table (The Logbook):** This records every single action (Buy, Sell, Cancel). It acts as an immutable history of the user's activity.
* **`Holding` Table (The Summary):** This stores only what the user *currently* owns. It is a snapshot of the portfolio.

**Why?**
If the app had to calculate a user's portfolio by reading their entire 5-year order history every time they logged in, the system would be incredibly slow. By maintaining a separate `Holding` table, the app can load the portfolio instantly.

#### 2. The "Instrument" Master Table
Instead of storing stock names (like "Reliance Industries Ltd") in every single order, I created a master **Instrument Entity**. This acts as the "Single Source of Truth" for all tradable assets (Stocks, Indices, Futures), preventing data errors and saving storage space.

---

### 🗂️ Schema Structure

The database consists of 6 key entities:

| Entity | Type | Purpose |
| :--- | :--- | :--- |
| **User** | Core | Stores profile details and the unique Demat ID. |
| **Instrument** | Master | Stores details of all tradable assets (Stocks/Indices). |
| **Watchlist** | Feature | Stores user-created lists for tracking stocks. |
| **Watchlist_Item** | Junction | Connects Watchlists to Instruments (Many-to-Many). |
| **Order** | Transaction | Logs every Buy/Sell action (History). |
| **Holding** | Summary | Summarizes current ownership (Portfolio). |

---

### 📊 Entity-Relationship (ER) Diagram

![ER Diagram]([ER diagram.png](https://github.com/gajanan-nawle/Capstone-Project3-Zerodha-Product-Dissection-Schema/blob/main/ER%20diagram.png?raw=true))

*(Note: The diagram visualizes the One-to-Many relationships between Users and Orders, and the Many-to-Many relationship between Watchlists and Instruments.)*

---

### 📝 Conclusion
In this case study, we delved into the design of Zerodha KITE's schema and its Entity-Relationship diagram. Zerodha has revolutionized the Indian financial landscape by solving key user problems like high costs and fragmented technology.
The platform's intricate data model, consisting of entities like User, Instrument, Order, Holding, and Watchlist, forms the foundation for its seamless and high-speed functionality.
By understanding this schema, we gain insight into how KITE effectively manages the complexities of real-time financial transactions, user portfolio management, and data integrity, contributing to its widespread popularity and continued growth in the world of financial technology.

---
