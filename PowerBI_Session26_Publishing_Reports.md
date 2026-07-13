# Session 26 — Publishing Reports to Power BI Service
## Module 6: Power BI Service & Capstone | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Demo | Hands-On: Publish a Report and Configure Data Refresh

---

## Learning Objectives
By the end of this session, you will be able to:
1. Publish reports from Power BI Desktop to Power BI Service
2. Navigate the Power BI Service interface (app.powerbi.com)
3. Understand the difference between Reports, Dashboards, and Datasets in the Service
4. Pin visuals to create a Dashboard
5. Configure scheduled data refresh

---

## 26.1 Power BI Desktop vs Power BI Service

| Feature | Power BI Desktop | Power BI Service |
|---------|-----------------|-----------------|
| **Purpose** | Build reports and data models | Share, collaborate, consume |
| **Platform** | Windows desktop application | Web browser (app.powerbi.com) |
| **Cost** | Free | Pro ($10/user/month) or Premium |
| **Data modeling** | Full (Power Query, DAX, relationships) | Limited (measures only, no Power Query) |
| **Report building** | Full visual creation and editing | Edit in browser (limited) |
| **Sharing** | Cannot share directly | Share via links, apps, workspaces |
| **Scheduled refresh** | Manual only | Automated (up to 8x/day Pro, 48x Premium) |
| **RLS assignment** | Create roles | Assign users to roles |
| **Collaboration** | Single user | Multi-user workspaces |
| **Mobile access** | No | Yes (Power BI Mobile app) |

### The Workflow

```
Power BI Desktop                     Power BI Service
┌────────────────┐                   ┌────────────────────────┐
│ Build Report   │                   │ View Reports           │
│ (.pbix file)   │───── Publish ────►│ Create Dashboards      │
│                │                   │ Share with Users        │
│ Data Model     │                   │ Schedule Refresh        │
│ DAX Measures   │                   │ Manage Security (RLS)   │
│ Visuals        │                   │ Mobile Access           │
└────────────────┘                   └────────────────────────┘
```

---

## 26.2 Publishing a Report

### Prerequisites
- Power BI Pro license (or PPU/Premium workspace)
- Organizational email (work/school account — not personal Gmail/Outlook)
- Report saved as `.pbix` file

### Step-by-Step

1. Open your report in **Power BI Desktop**
2. Click **Home** tab → **Publish**
3. Sign in with your organizational account (if not already signed in)
4. Select the **destination workspace** (e.g., "My Workspace" or a shared workspace)
5. Click **Select**
6. Wait for publish to complete → click **Open in Power BI** link

### What Gets Published

| Item | Published? | Name in Service |
|------|-----------|----------------|
| **Report** | ✅ | Same name as .pbix file |
| **Dataset** | ✅ | Same name as .pbix file |
| **Dashboard** | ❌ | Must be created manually in Service |

### Re-Publishing (Updates)

When you modify the `.pbix` and publish again:
- **Report** is overwritten (new visuals, layouts, pages)
- **Dataset** is overwritten (new data model, queries, measures)
- **Dashboard** pins are NOT affected (existing pins stay)
- **RLS assignments** are preserved
- **Scheduled refresh settings** are preserved

---

## 26.3 Power BI Service Interface

### Navigation

```
┌──────────────────────────────────────────────────────────────┐
│  ☰ Power BI  │  Home  │  Create  │  Browse  │  [Search]     │
├──────────────┼──────────────────────────────────────────────────┤
│              │                                                │
│  Home        │     CONTENT AREA                              │
│  Browse      │                                                │
│  Data Hub    │     Reports, Dashboards, Datasets              │
│  Metrics     │     displayed here based on selection          │
│  Apps        │                                                │
│  Learn       │                                                │
│              │                                                │
│  Workspaces  │                                                │
│  ├ My        │                                                │
│  ├ Sales     │                                                │
│  └ Finance   │                                                │
└──────────────┴────────────────────────────────────────────────┘
```

### Key Areas

| Area | Purpose |
|------|---------|
| **Home** | Recently viewed, favorites, quick access |
| **Browse** | Find all content across workspaces |
| **Data Hub** | Discover shared datasets, dataflows, datamarts |
| **Metrics** | Scorecards and goal tracking |
| **Apps** | Installed Power BI Apps from the organization |
| **Workspaces** | Collaborative spaces for teams (Session 27) |

---

## 26.4 Reports vs Dashboards vs Datasets

### Three Content Types in Power BI Service

| Content Type | What It Is | Created Where | Interactive? |
|-------------|-----------|---------------|-------------|
| **Report** | Multi-page interactive visualizations (.pbix) | Power BI Desktop | Yes — full interactivity |
| **Dashboard** | Single-page collection of pinned visuals | Power BI Service only | Limited — click to open source report |
| **Dataset** | The underlying data model (tables, relationships, measures) | Power BI Desktop | Not directly — powers reports |

### Report vs Dashboard

| Feature | Report | Dashboard |
|---------|--------|-----------|
| **Pages** | Multiple pages | Single page only |
| **Created in** | Desktop (published) | Service (pin visuals) |
| **Interactivity** | Full: slicers, cross-filter, drill-through | Click-to-navigate to report |
| **Data source** | One dataset | Multiple reports/datasets |
| **Visuals** | Built from scratch | Pinned from reports, Q&A, Excel |
| **Best for** | Detailed analysis | At-a-glance executive overview |
| **Sharing** | Share the report link | Share the dashboard link |
| **Alerts** | Not supported | Data-driven alerts on cards |

---

## 26.5 Creating a Dashboard (Pinning Visuals)

### Step-by-Step

1. Open a **Report** in Power BI Service
2. Hover over a visual → click the **📌 Pin** icon
3. Choose: **New Dashboard** or **Existing Dashboard**
4. Name the dashboard → click **Pin**
5. Repeat for other visuals you want on the dashboard
6. Navigate to the Dashboard to view all pinned tiles

### What You Can Pin

| Source | How to Pin |
|--------|-----------|
| **Report visual** | Hover → Pin icon |
| **Entire report page** | Pin → "Pin Live Page" (real-time interactive tile) |
| **Q&A result** | Ask a question → Pin the answer visual |
| **Excel range** | From Excel Online → Pin to dashboard |
| **Image / Web content** | Dashboard → Add Tile → Image, Web Content, Video |
| **Text box** | Dashboard → Add Tile → Text Box (for annotations) |

### Dashboard Tiles

Each pinned item becomes a **tile** on the dashboard:
- **Click a tile** → navigates to the source report (filtered to context)
- **Resize tiles** by dragging corners
- **Rearrange** by dragging
- **Edit details** → custom title, subtitle, link

---

## 26.6 Data Refresh in Power BI Service

### Refresh Types

| Type | How | When |
|------|-----|------|
| **Manual Refresh** | Dataset → ⟲ Refresh Now | On-demand, one-time |
| **Scheduled Refresh** | Dataset → Settings → Schedule | Automatic, recurring |
| **On-demand via API** | Power BI REST API | Programmatic trigger |
| **Dataflow Refresh** | Dataflow settings | For dataflow-based sources |

### Configuring Scheduled Refresh

1. Go to the **Workspace** → find the **Dataset** (not the report)
2. Click **⋯ (More options)** → **Settings**
3. Expand **Scheduled Refresh**
4. Toggle **Keep your data up to date** → On
5. Set **Refresh frequency:** Daily or Weekly
6. Set **Time zone** and **Time(s)** to refresh
7. Add up to 8 time slots per day (Pro) or 48 (Premium)
8. **Failure notifications:** Add email addresses to be notified on refresh failure
9. Click **Apply**

### Data Gateway Requirements

| Data Source Location | Gateway Needed? |
|--------------------|----------------|
| **Cloud sources** (SharePoint, Azure SQL, Dataverse) | ❌ No |
| **OneDrive / SharePoint files** | ❌ No (auto-refresh available) |
| **Local files** (C:\Data\Sales.xlsx) | ✅ Yes — Personal or Enterprise Gateway |
| **On-premises SQL Server** | ✅ Yes — Enterprise Gateway |
| **Network file shares** | ✅ Yes — Enterprise Gateway |

### Installing a Gateway

1. Download from [gateway.powerbi.com](https://gateway.powerbi.com)
2. Install on a machine with access to the data sources
3. Register with your Power BI account
4. Configure data source credentials in Power BI Service → Manage Gateways

---

## 26.7 Data Source Credentials

### Setting Credentials in Service

After publishing, Power BI Service needs credentials to access your data sources:

1. Dataset → Settings → **Data Source Credentials**
2. Click **Edit Credentials** for each source
3. Enter authentication details:
   - **OAuth2** — for Microsoft services (sign in)
   - **Basic** — username/password
   - **Key** — API key
   - **Windows** — Windows authentication (via gateway)
4. Set **Privacy Level:** Organizational, Private, or Public

### Common Credential Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| "Data source credentials are missing" | First publish — no credentials set | Edit credentials in Dataset Settings |
| "Gateway required" | On-premises source | Install and configure a gateway |
| "This dataset includes a data source that requires an On-premises data gateway" | Local file path in query | Move file to cloud (OneDrive/SharePoint) or install gateway |
| Refresh fails with authentication error | Credentials expired | Re-enter credentials |

---

## 26.8 OneDrive / SharePoint Auto-Refresh

### Automatic Refresh for Cloud-Stored Files

If your Excel/CSV source is in **OneDrive for Business** or **SharePoint**:
- Power BI auto-detects changes (approximately every hour)
- No gateway needed
- No manual scheduled refresh needed

### Setup
1. Store your Excel/CSV in OneDrive for Business or a SharePoint document library
2. In Power BI Desktop: connect using the **SharePoint** or **OneDrive** connector (not local file path)
3. Publish → auto-refresh enabled

---

## 🔧 Hands-On Activity: Publish and Configure

**Duration:** 25 minutes

### Tasks

**Part 1 — Publish (8 min)**
1. Open your Executive Dashboard in Power BI Desktop
2. Home → **Publish**
3. Sign in with your organizational account
4. Select **My Workspace** as destination
5. Wait for completion → click **Open in Power BI**
6. Verify: Report and Dataset appear in My Workspace

**Part 2 — Create a Dashboard (10 min)**
7. Open the published report in Power BI Service
8. Pin the following to a **new Dashboard** called "Sales Executive Dashboard":
   - Total Revenue Card
   - Monthly Revenue Trend (Line Chart)
   - Revenue by Category (Bar Chart)
   - Map visual
9. Navigate to the Dashboard → verify all tiles appear
10. Resize and rearrange tiles for a clean layout
11. Click a tile → verify it navigates to the source report

**Part 3 — Scheduled Refresh (7 min)**
12. In the Workspace → find the Dataset → ⋯ → **Settings**
13. Check: Are there any credential warnings? If so, edit credentials
14. Set up **Scheduled Refresh:** Daily at 7:00 AM
15. Add your email for failure notifications
16. Apply → verify status shows "Scheduled"

---

## Session 26 — Key Takeaways

1. **Publish** sends your .pbix from Desktop to Service — creates a Report + Dataset
2. **Reports** are multi-page interactive visuals; **Dashboards** are single-page collections of pinned tiles
3. **Pin visuals** from reports to create dashboards — click tiles to drill into reports
4. **Scheduled Refresh** keeps data current — requires gateway for on-premises sources
5. **Credentials** must be set in Service for refresh to work — check Dataset Settings

---

## Preparation for Session 27
- Explore your Workspace in Power BI Service
- Think about: How would you organize reports for Sales, Finance, and HR teams?
- Review: What is the difference between "My Workspace" and a shared Workspace?

---

*Session 26 of 30 | Module 6: Power BI Service & Capstone*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
