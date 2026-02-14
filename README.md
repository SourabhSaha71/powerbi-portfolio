# 💼 Power BI Portfolio — Sourabh Saha

**Senior Power BI Developer @ HCL Technologies** | 3.5+ Years Enterprise BI Experience  
**Specialties:** Power BI · DAX · SQL · API Integration · Automation · C#

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](http://www.linkedin.com/in/sahasourabh)
[![Email](https://img.shields.io/badge/Email-Contact-red)](mailto:sahasourabh71@gmail.com)
[![Fiverr](https://img.shields.io/badge/Fiverr-Hire_Me-green)](YOUR_FIVERR_URL)

---

## 👋 About Me

I'm a **Senior Power BI Developer** at HCL Technologies with **3.5+ years** building enterprise-grade business intelligence solutions for clients across e-commerce, finance, HR, operations, and project management.

I specialize in:
- 📊 Interactive Power BI dashboards with advanced DAX
- 🔄 **API integration + automation** (Jira, Salesforce, Google Analytics, custom APIs)
- 🗄️ SQL data modeling and optimization
- 🤖 C# and Python automation scripts
- 📈 Excel-to-Power BI migrations

**What makes me different:** I don't just build dashboards — I build the **entire data pipeline** so your dashboards update themselves automatically.

---

## 🎯 Services Offered

| Service | Starting Price | Delivery Time |
|---------|----------------|---------------|
| **1-page Power BI Dashboard** | $40 / ₹3,500 | 2–3 days |
| **Multi-page Dashboard (3–5 pages)** | $70–110 / ₹6,000–9,000 | 5–7 days |
| **Full Dashboard Suite (5+ pages)** | $140–240 / ₹12,000–20,000 | 7–10 days |
| **Excel → Power BI Migration** | $60–110 / ₹5,000–9,000 | 3–7 days |
| **API Integration + Dashboard** 🔥 | $100–220 / ₹8,000–18,000 | 7–10 days |
| **Jira/Salesforce → Power BI Pipeline** | $100–180 / ₹8,000–15,000 | 7–10 days |
| **Monthly Maintenance Retainer** | $35–55/mo / ₹3,000–4,500/mo | Ongoing |

💡 **All projects include:** Source files (.pbix), documentation, and post-delivery support.

---

## 📂 Featured Projects

### 1. 🛒 E-Commerce Sales Performance Dashboard

![E-Commerce Dashboard Preview](ecommerce-dashboard/screenshots/overview.png)

**Business Problem:**  
E-commerce businesses track sales across multiple channels (Amazon, Flipkart, website) using disconnected spreadsheets, making it impossible to get unified performance insights.

**Solution:**  
Built a comprehensive sales analytics dashboard with:
- Revenue trends and YoY/MoM growth analysis
- Regional sales breakdown with drill-through capabilities
- Product category performance ranking
- Customer segmentation analysis
- Interactive date slicers and dynamic filtering

**Key DAX Measures:**
- YoY Revenue Growth: `DIVIDE([Revenue] - [Revenue PY], [Revenue PY])`
- Running Total: `CALCULATE([Revenue], FILTER(ALL('Date'), 'Date'[Date] <= MAX('Date'[Date])))`
- Top N Products with dynamic filtering

**Tech Stack:** Power BI, DAX, Power Query, Excel

[📁 View Full Project →](ecommerce-dashboard/)

---

### 2. 👥 HR Analytics & Attrition Dashboard

![HR Dashboard Preview](hr-analytics-dashboard/screenshots/overview.png)

**Business Problem:**  
HR teams manually calculate attrition rates in Excel and struggle to identify patterns in employee turnover across departments, tenure, and salary bands.

**Solution:**  
Built an interactive HR analytics dashboard featuring:
- Overall attrition rate with trend analysis
- Department-wise and role-wise attrition breakdown
- Tenure band and salary range analysis
- Demographics insights (age, gender, education)
- Drill-through from department summary to individual employee details

**Key DAX Measures:**
- Attrition Rate: `DIVIDE(CALCULATE(COUNTROWS(HR), HR[Attrition]="Yes"), COUNTROWS(HR))`
- Average Tenure by Department
- Conditional formatting for high-risk attrition segments

**Tech Stack:** Power BI, DAX, Power Query, Kaggle IBM HR Dataset

[📁 View Full Project →](hr-analytics-dashboard/)

---

### 3. 💰 Financial P&L — Budget vs Actuals Dashboard

![Finance Dashboard Preview](financial-dashboard/screenshots/overview.png)

**Business Problem:**  
Finance teams spend hours every month creating P&L reports in Excel, manually comparing budget vs actual figures line by line.

**Solution:**  
Built an automated financial dashboard with:
- P&L statement with budget vs actual comparison
- Variance analysis (absolute and percentage)
- YTD, QTD, MTD views with dynamic time period selection
- Cost center and department drill-downs
- Executive KPI cards (gross margin %, EBITDA, variance %)

**Key DAX Measures:**
- Variance %: `DIVIDE([Actual] - [Budget], [Budget])`
- YTD Actual: `TOTALYTD([Actual], 'Date'[Date])`
- Dynamic time intelligence with SAMEPERIODLASTYEAR
- Conditional formatting for over/under budget indicators

**Tech Stack:** Power BI, DAX, Power Query, SQL Server

[📁 View Full Project →](financial-dashboard/)

---

### 4. 🔧 Jira API → Project Management Dashboard 🔥

![Jira Dashboard Preview](jira-automation-dashboard/screenshots/overview.png)

**Business Problem:**  
Project teams waste 5+ hours weekly manually exporting Jira data to Excel to track sprint velocity, ticket aging, and team workload. Jira's native reports are inflexible and don't support custom KPIs.

**Solution:**  
Built a **fully automated pipeline** that:
- Pulls data from Jira REST API using C# script
- Stages data in SQL Server
- Refreshes Power BI dashboard daily via scheduled task
- **Zero manual data exports** — completely hands-free

**Dashboard Features:**
- Sprint velocity trends and burndown charts
- Ticket cycle time and aging analysis
- Team workload distribution (active tickets per assignee)
- Epic progress tracking with drill-through to story details
- Blocker identification and dependencies visualization

**Technical Architecture:**
```
Jira REST API → C# Script → SQL Server → Power BI (Scheduled Refresh)
                    ↓
            Windows Task Scheduler (Daily 8 AM)
```

**Key DAX Measures:**
- Average Cycle Time: `AVERAGE(DATEDIFF([Created Date], [Resolved Date], DAY))`
- Sprint Velocity: `CALCULATE(SUM([Story Points]), [Status]="Done")`
- Aging Tickets (conditional): `IF([Days Open] > 14, "Aging", "Active")`

**Tech Stack:** C#, Jira REST API, SQL Server, Power BI, Windows Task Scheduler, T-SQL

**Impact:** Eliminated 5+ hours/week of manual reporting for project management team.

[📁 View Full Project →](jira-automation-dashboard/)

---

## 🛠️ Technical Skills

### Power BI Ecosystem
- Power BI Desktop & Service
- DAX (Advanced)
- Power Query (M Language)
- Power BI Gateway
- Row-level Security (RLS)
- Paginated Reports

### Data & Databases
- SQL Server
- T-SQL (Complex Queries, Stored Procedures, Views)
- Star Schema Data Modeling
- ETL Pipelines
- Data Warehousing Concepts

### Programming & Automation
- **C#** (API Integration, Automation Scripts)
- **Python** (Pandas, NumPy, API requests)
- **REST APIs** (Jira, Salesforce, Google Analytics, Custom)
- ASP.NET MVC
- Git & Version Control

### Business Intelligence
- Dashboard Design Best Practices
- KPI Development
- Data Storytelling
- Stakeholder Requirement Gathering
- Performance Optimization

---

## 📈 Professional Experience

**Senior Executive — HCL Technologies** (Jan 2025 - Present)
- Leading enterprise Power BI dashboard development for multiple client projects
- Built 10+ production dashboards across sales, finance, HR, and operations
- Reduced client reporting time by 60%+ through Excel-to-Power BI migrations
- Designed complex DAX measures including time intelligence, variance analysis, and dynamic calculations

**Graduate Engineer Trainee — HCL Technologies** (Aug 2022 - Dec 2024)
- Developed business intelligence solutions and automation scripts
- Built Jira API integration with C# → automated project tracking dashboard
- Created data models and wrote T-SQL queries for data extraction and transformation
- Collaborated with cross-functional teams to deliver analytical solutions

---

## 📫 Let's Work Together

I'm available for:
✅ One-off dashboard projects  
✅ Excel-to-Power BI migrations  
✅ API integration + automation solutions  
✅ Monthly retainer (dashboard maintenance)  
✅ Consulting & training

**Contact Me:**
- 📧 Email: [YOUR_EMAIL]
- 💼 LinkedIn: [YOUR_LINKEDIN_URL]
- 🟢 Fiverr: [YOUR_FIVERR_URL]
- 🔵 Upwork: [YOUR_UPWORK_URL]

**Typical Response Time:** Within 2–4 hours during business hours (IST)

---

## 💬 What Clients Say

> *"Sourabh delivered a complex Jira dashboard with API integration in just 8 days. The automation saved our team hours every week. Highly recommend!"*  
> — [Client Name], Project Manager

> *"Fast, professional, and really understood our business needs. The financial dashboard he built is now used by our entire leadership team."*  
> — [Client Name], CFO

*(Add real testimonials as you complete projects)*

---

## 📊 GitHub Stats

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=ssahaoctafx&show_icons=true&theme=radical)

---

## 📝 Recent Blog Posts & Tips

*(Optional — add links to LinkedIn posts, Medium articles, or tips as you create content)*

- [5 DAX Measures Every Sales Dashboard Needs](#)
- [How to Migrate from Excel to Power BI Without Breaking Your Workflow](#)
- [Building a Jira API Integration: Step-by-Step Guide](#)

---

## 🏆 Certifications & Training

- **Microsoft Power BI Data Analyst Associate** (if you have it — if not, skip or plan to get it)
- HCL Internal Training: Advanced Power BI, DAX, SQL Server
- *(Add any relevant certifications)*

---

## ⚖️ License

All dashboard samples in this repository are available under MIT License for educational purposes. If you use these as templates, please provide attribution.

---

**⭐ If you find these projects useful, please star this repository!**

**📩 For project inquiries:** sahasourabh71@gmail.com
