# 🔧 Jira API → Project Management Dashboard

![Dashboard Preview](screenshots/overview.png)

**🔥 This is a FULLY AUTOMATED solution — data refreshes itself daily with zero manual exports.**

---

## 📋 Project Overview

**Industry:** Software Development / Project Management  
**Dashboard Type:** Agile Sprint Tracking & Team Performance  
**Pages:** 4 (Overview, Sprint Velocity, Ticket Aging, Team Workload)  
**Data Source:** Jira Cloud REST API  
**Automation:** C# Script + SQL Server + Power BI Scheduled Refresh  
**Tools Used:** C#, Jira API, SQL Server, Power BI, Windows Task Scheduler

---

## 🎯 Business Problem

Project management teams using Jira face these challenges:

❌ Jira's native reports are rigid and don't support custom KPIs  
❌ Teams spend 5+ hours/week manually exporting Jira data to Excel  
❌ No unified view of sprint velocity trends over time  
❌ Difficult to identify aging tickets and bottlenecks  
❌ Manual effort to track team workload distribution  

**The ask:** "Can we get a live dashboard that updates itself?"

---

## ✅ Solution Architecture

Built an **end-to-end automated pipeline:**

```
┌─────────────┐       ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
│ Jira Cloud  │  -->  │  C# Script  │  -->  │ SQL Server  │  -->  │  Power BI   │
│  REST API   │       │ (Auth, Pull)│       │  (Staging)  │       │  Dashboard  │
└──────────��──┘       └─────────────┘       └─────────────┘       └─────────────┘
                             ↓
                  ┌─────────────────────┐
                  │ Windows Task        │
                  │ Scheduler           │
                  │ (Runs Daily 8 AM)   │
                  └─────────────────────┘
```

**Key Benefits:**
✔️ **Zero Manual Work** — Data pulls and refreshes automatically  
✔️ **Real-Time Insights** — Dashboard always shows yesterday's data  
✔️ **Custom KPIs** — Track metrics Jira reports can't show  
✔️ **Historical Trends** — SQL Server stores historical data for trend analysis  

---

## 📊 Dashboard Pages

### Page 1: Executive Overview
![Overview](screenshots/overview.png)

**KPIs:**
- Total Active Tickets
- Sprint Velocity (avg story points completed per sprint)
- Average Cycle Time (days)
- Tickets Aging > 14 Days

**Visuals:**
- KPI cards with trend indicators
- Sprint velocity trend (line chart)
- Tickets by status (donut chart)
- Upcoming sprint capacity

---

### Page 2: Sprint Velocity Analysis
![Sprint Velocity](screenshots/sprint-velocity.png)

**Analysis:**
- Sprint-by-sprint story points completed (bar chart)
- Velocity trend line
- Burndown chart for current sprint
- Sprint completion rate (planned vs completed)

---

### Page 3: Ticket Aging & Cycle Time
![Ticket Aging](screenshots/ticket-aging.png)

**Features:**
- Aging tickets table (> 14 days without updates)
- Average cycle time by ticket type (Bug, Story, Task)
- Bottleneck identification (tickets stuck in specific statuses)
- Drill-through to individual ticket details

---

### Page 4: Team Workload Distribution
![Team Workload](screenshots/team-workload.png)

**Analysis:**
- Active tickets per team member (bar chart)
- Story points per assignee
- Workload balance matrix
- Unassigned tickets alert

---

## 🧮 Key DAX Measures

### 1. Average Cycle Time
```dax
Avg Cycle Time (Days) = 
AVERAGE(
    DATEDIFF(
        'Jira Tickets'[Created Date],
        'Jira Tickets'[Resolved Date],
        DAY
    )
)
```

### 2. Sprint Velocity
```dax
Sprint Velocity = 
CALCULATE(
    SUM('Jira Tickets'[Story Points]),
    'Jira Tickets'[Status] = "Done"
)
```

### 3. Aging Tickets (> 14 Days)
```dax
Aging Tickets = 
CALCULATE(
    COUNTROWS('Jira Tickets'),
    'Jira Tickets'[Days Open] > 14,
    'Jira Tickets'[Status] <> "Done"
)
```

### 4. Days Open (Calculated Column)
```dax
Days Open = 
IF(
    'Jira Tickets'[Status] = "Done",
    DATEDIFF('Jira Tickets'[Created Date], 'Jira Tickets'[Resolved Date], DAY),
    DATEDIFF('Jira Tickets'[Created Date], TODAY(), DAY)
)
```

---

## 🤖 Automation Script (C#)

### Overview
The C# script handles:
1. **Authentication** with Jira Cloud (Basic Auth or OAuth)
2. **API Calls** to fetch tickets (issues) using JQL queries
3. **Pagination** to handle large datasets (>100 tickets)
4. **Data Transformation** (flatten nested JSON)
5. **SQL Insert/Update** to stage data in SQL Server

### Key Script Features
- Error handling and logging
- Incremental load (only fetch updated tickets)
- Retry logic for API failures
- Configurable via `appsettings.json`

**Script Location:** `scripts/jira-api-integration.cs`

### How to Run the Script

**Prerequisites:**
- .NET 6.0 or later
- SQL Server (local or Azure)
- Jira API token (from Jira Cloud settings)

**Setup:**
1. Clone this repository
2. Navigate to `scripts/` folder
3. Update `appsettings.json` with your Jira credentials and SQL connection string
4. Run: `dotnet run`

**Scheduling:**
- Set up Windows Task Scheduler (Windows) or Cron Job (Linux)
- Run daily at 8 AM (or your preferred time)

**Full documentation:** See `scripts/README.md`

---

## 🗄️ Data Model

**SQL Server Tables:**

1. **JiraTickets** (Fact Table)
   - TicketID (Primary Key)
   - TicketKey (e.g., PROJ-123)
   - Summary
   - Status
   - Priority
   - Assignee
   - Reporter
   - CreatedDate
   - UpdatedDate
   - ResolvedDate
   - StoryPoints
   - TicketType (Bug, Story, Task)
   - SprintID

2. **Sprints** (Dimension Table)
   - SprintID (Primary Key)
   - SprintName
   - StartDate
   - EndDate
   - Goal

3. **DateDim** (Calendar Table)
   - Date, Year, Quarter, Month, Week

**Power BI Relationships:**
- JiraTickets[CreatedDate] → DateDim[Date]
- JiraTickets[SprintID] → Sprints[SprintID]

---

## 📥 Data Flow

### Step 1: Jira API Call (C# Script)
```csharp
// Pseudo-code (simplified)
var jql = "project = MYPROJECT AND updated >= -1d";
var response = await JiraClient.SearchIssuesAsync(jql);
foreach (var issue in response.issues)
{
    SaveToSQLServer(issue);
}
```

### Step 2: SQL Server Staging
Data is inserted/updated in `JiraTickets` table with timestamp.

### Step 3: Power BI Refresh
- Power BI connects to SQL Server via DirectQuery or Import mode
- Scheduled refresh runs daily at 9 AM (1 hour after data pull)

---

## 🚀 How to Implement This for Your Team

### Option 1: Use This Exact Setup
1. Get Jira API credentials (Settings → Security → API Tokens)
2. Set up SQL Server (local or Azure SQL)
3. Configure and run the C# script
4. Download the .pbix file and connect to your SQL Server
5. Schedule script + Power BI refresh

### Option 2: Adapt to Your Jira Instance
- Modify the JQL query in the script to match your project keys
- Adjust the data model if your Jira uses custom fields
- Customize dashboard pages to your team's KPIs

### Option 3: Hire Me to Build It for You
If you want this implemented for your team (customized to your Jira setup), I can build it end-to-end in 7–10 days.

📧 Contact: [YOUR_EMAIL]  
💼 Fiverr: [YOUR_FIVERR_URL]

---

## 💡 Business Impact

**Before:**
- 5+ hours/week manually exporting Jira data to Excel
- No historical sprint velocity data
- Difficult to spot aging tickets
- Manual effort to track team workload

**After:**
- **Zero manual work** — dashboard updates itself
- Historical trends visible instantly
- Aging tickets flagged automatically
- Leadership has real-time visibility

**Time Saved:** ~20 hours/month for a 5-person PM team

---

## 🔧 Technical Details

**Script:**
- Language: C# (.NET 6)
- Jira API Version: v3
- Authentication: Basic Auth (email + API token)
- Error Handling: Retry logic with exponential backoff

**Database:**
- SQL Server 2019 or later
- Tables: JiraTickets (fact), Sprints (dim), DateDim (dim)
- Performance: Indexed on TicketID, CreatedDate

**Power BI:**
- Connection: Import Mode (faster performance for this use case)
- Refresh: Scheduled daily at 9 AM via Power BI Service
- File Size: ~12 MB

---

## 📸 Architecture Diagram

```
┌───────────────────────────────────────────────────────────────┐
│                      JIRA CLOUD                               │
│  (Issues, Sprints, Custom Fields)                             │
└───────────────────┬───────────────────────────────────────────┘
                    │
                    │ REST API (HTTPS)
                    │
┌───────────────────▼───────────────────────────────────────────┐
│               C# AUTOMATION SCRIPT                            │
│  - Authenticate with API token                                │
│  - Fetch tickets via JQL                                      │
│  - Transform JSON → Relational                                │
│  - Insert/Update SQL Server                                   │
└───────────────────┬───────────────────────────────────────────┘
                    │
                    │ SQL Server Connection
                    │
┌───────────────────▼───────────────────────────────────────────┐
│                   SQL SERVER (Staging)                        │
│  Tables: JiraTickets, Sprints, DateDim                        │
│  Stores historical data for trend analysis                    │
└───────────────────┬───────────────────────────────────────────┘
                    │
                    │ Power BI Connection (Import/DirectQuery)
                    │
┌───────────────────▼───────────────────────────────────────────┐
│                  POWER BI DASHBOARD                           │
│  - DAX measures for KPIs                                      │
│  - Interactive visuals                                        │
│  - Scheduled refresh (daily 9 AM)                             │
└───────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Technologies Used

- **C#** (.NET 6): API integration and data pipeline
- **Jira REST API v3**: Data source
- **SQL Server 2019**: Data staging and storage
- **T-SQL**: Stored procedures for data transformation
- **Power BI Desktop**: Dashboard development
- **Power BI Service**: Scheduled refresh hosting
- **Windows Task Scheduler**: Script automation

---

## 📬 Want This for Your Team?

I can build a custom Jira (or Salesforce, Monday.com, Asana, etc.) → Power BI pipeline for your team in 7–10 days.

**What you get:**
✅ API integration script (C# or Python — your choice)  
✅ SQL database setup (or CSV/Excel staging if you prefer)  
✅ Custom Power BI dashboard with your KPIs  
✅ Scheduled automation setup  
✅ Full documentation  
✅ 2 weeks post-delivery support  

**Pricing:** $100–220 / ₹8,000–18,000 (depending on complexity)

📧 Email: [YOUR_EMAIL]  
🟢 Fiverr: [YOUR_FIVERR_URL]  
💼 LinkedIn: [YOUR_LINKEDIN_URL]

---

## ⭐ If you found this useful, please star the main repository!

[← Back to Portfolio](../)
