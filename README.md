📊 Global Operations — Backlog, SLA & Throughput Power BI Dashboard

This project recreates a Global Operations performance dashboard using synthetic data, inspired by the backlog/throughput reporting model I used in real-world engineering operations.
It demonstrates end-to-end Power BI capabilities including:
Data modeling (star schema)
Power Query ETL
DAX measures
Row-Level Security (RLS)
Executive dashboards with drill-downs
Python-generated synthetic datasets
All datasets used here are fully synthetic and safe for public demonstration.

🚀 Project Overview

Operational leaders need to track:
How backlog is evolving
Where SLA risk is increasing
Which regions and engineers are over/under-performing
What the daily throughput trend looks like
Whether cycle time is worsening or improving
This Power BI project answers those questions through a clean, enterprise-grade reporting model.

🔧 Tools & Technologies
Power BI
Power Query (M language)
DAX measures & calculated columns
Star schema modeling
Row-Level Security (RLS)
Time intelligence with a Date dimension
Visual design & executive dashboards
Python

Used to generate synthetic operational datasets including backlog, throughput, and work-order lifecycle timelines.

Data Size
The dataset simulates ~1000 work orders across four regions (UK, US, DE, IN), and ~20 engineers, covering one full year.

📈 Dashboard Pages
1️⃣ Executive Overview
Total work orders
Open backlog
SLA Met %
Average cycle time
Backlog trend by region
SLA performance by priority
Throughput by region
Oldest open work orders
📸 Screenshot: (See /screenshots/overview_page.png)

2️⃣ Backlog & SLA Drilldown
Backlog by region
Backlog distribution by priority
SLA by region
SLA trend by month
SLA breach table (late orders only)
📸 Screenshot: (See /screenshots/backlog_page.png)

3️⃣ Throughput & Productivity
Throughput by engineer
Throughput by region
Daily throughput trend
Cycle time vs throughput (scatter plot)
Engineer performance ranking table
📸 Screenshot: (See /screenshots/productivity_page.png)

🧠 Key DAX Measures
Total Work Orders =
COUNTROWS(Fact_WorkOrders)

Open Backlog =
CALCULATE(
    COUNTROWS(Fact_WorkOrders),
    Fact_WorkOrders[Status] <> "Closed"
)

Completed Work Orders =
CALCULATE(
    COUNTROWS(Fact_WorkOrders),
    Fact_WorkOrders[Status] = "Closed"
)

Average Cycle Time (Days) =
AVERAGEX(
    FILTER(Fact_WorkOrders, Fact_WorkOrders[Status] = "Closed"),
    DATEDIFF(Fact_WorkOrders[CreatedDate], Fact_WorkOrders[CompletedDate], DAY)
)

SLA Met % =
VAR TotalClosed =
    [Completed Work Orders]
VAR SlaMet =
    CALCULATE(
        COUNTROWS(Fact_WorkOrders),
        Fact_WorkOrders[Status] = "Closed",
        DATEDIFF(
            Fact_WorkOrders[CreatedDate],
            Fact_WorkOrders[CompletedDate],
            HOUR
        ) <= RELATED(Dim_SLA[SLA_Hours])
    )
RETURN DIVIDE(SlaMet, TotalClosed)

🔐 Row-Level Security (RLS)
Four RLS roles were implemented, allowing region-specific access:
Region_UK → sees only UK data
Region_US → sees only US data
Region_DE → sees only DE data
Region_IN → sees only IN data

🤖 Synthetic Data Generation (Python)
All datasets were created using Python (Pandas & Numpy) by simulating:
Work order creation
SLA assignment
Completion times
Backlog snapshots
Daily throughput per engineer

This ensures:
No confidential data
Realistic operational patterns
Safe for public/portfolio use
Full code is available on request.

📬 Contact
If you'd like to connect, discuss the model, or collaborate:
Shameeh Rahman (Shami)

📝 License
This project is released under the MIT License.
You may use, modify, or build upon it freely
