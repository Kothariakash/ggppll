# Session 28 — Sharing & Collaboration
## Module 6: Power BI Service & Capstone | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Demo | Hands-On: Share Reports, Set Alerts, Subscribe to Reports

---

## Learning Objectives
By the end of this session, you will be able to:
1. Share reports and dashboards using multiple methods
2. Set up data-driven alerts on dashboard tiles
3. Create email subscriptions for automated report delivery
4. Embed reports in Teams, SharePoint, and PowerPoint
5. Understand sharing permissions and security implications

---

## 28.1 Sharing Methods Overview

| Method | Best For | License Required |
|--------|----------|-----------------|
| **Direct Share (link)** | Quick sharing with specific people | Sender + Recipient: Pro or Premium |
| **Workspace Access** | Team collaboration on content | All members: Pro or Premium workspace |
| **App** | Distributing polished reports to many users | Publisher: Pro; Viewers: Pro or Premium capacity |
| **Embed in Teams** | Teams-native access | Microsoft 365 + Power BI Pro |
| **Embed in SharePoint** | SharePoint page integration | SharePoint + Power BI Pro |
| **Embed in PowerPoint** | Live data in presentations | PowerPoint + Power BI Pro |
| **Publish to Web** | Public internet (anyone can view) | Free — but NO security |
| **Email Subscription** | Scheduled PDF/image delivery | Pro or Premium |
| **Export** | Static file sharing (PDF, PPT, Excel) | Pro for Service export |

---

## 28.2 Direct Sharing (Share Link)

### How to Share a Report

1. Open the Report in Power BI Service
2. Click **Share** button (top bar)
3. Choose link type:
   - **People in your organization** — anyone with a Pro license
   - **People with existing access** — only current viewers
   - **Specific people** — named users/groups only
4. Enter email addresses
5. Options:
   - **Allow recipients to share** — they can re-share
   - **Allow recipients to build on dataset** — they can build their own reports
   - **Send an email notification** — sends email with link
6. Click **Send** or **Copy link**

### Sharing Permissions

| Setting | Effect |
|---------|--------|
| **Read** (default) | View the report — cannot edit |
| **Allow resharing** | Recipient can share with others |
| **Allow building** | Recipient can create reports on the dataset |
| **Allow export** | Depends on admin settings |

### Sharing a Dashboard

Same process as reports. Additionally:
- Shared dashboards show all pinned tiles
- Clicking a tile navigates to the source report — user needs report access too
- **RLS applies** — users see data based on their RLS role

### Sharing Limitations

| Limitation | Detail |
|-----------|--------|
| Both users need **Pro license** | Unless content is in Premium capacity |
| Cannot share from **My Workspace** directly to external users | Use workspaces or apps |
| **RLS is enforced** on shared content | Viewer sees only their authorized data |
| Cannot share **individual pages** | Share entire report — use bookmarks for specific views |
| **External sharing** | Requires Azure AD B2B and admin approval |

---

## 28.3 Data-Driven Alerts

### What Are Alerts?

**Alerts** notify you via email and notification center when a data value on a **Dashboard tile** crosses a threshold you define.

### Setting Up an Alert

1. Open a **Dashboard** in Power BI Service
2. Hover over a **Card or KPI tile** → click **⋯ (More options)** → **Manage alerts**
3. Click **+ Add alert rule**
4. Configure:
   - **Title:** e.g., "Revenue Below Target"
   - **Condition:** Above / Below / Equal to
   - **Threshold value:** e.g., 500000
   - **Notification frequency:** At most once an hour / At most once a day / At most once a week
5. Toggle **Email notification** → On
6. Click **Save and Close**

### Alert Behavior

| Setting | Detail |
|---------|--------|
| **Trigger** | Fires when data refreshes and condition is met |
| **Frequency** | Won't fire more often than the selected frequency |
| **Reset** | Alert fires again only after the value goes back below threshold and crosses again |
| **Where notifications appear** | Notification bell in Power BI Service + optional email |
| **Mobile** | Push notifications on Power BI Mobile app |

### Alert Limitations

| Limitation | Detail |
|-----------|--------|
| **Only on Dashboard tiles** | Not on report visuals directly |
| **Only on Card, KPI, and Gauge tiles** | Not on charts or tables |
| **Based on data refresh** | Not real-time streaming (unless using streaming datasets) |
| **Max 250 alerts** per user | Across all dashboards |

---

## 28.4 Email Subscriptions

### What Are Subscriptions?

**Subscriptions** automatically send a snapshot (PDF or image) of a report page or dashboard to specified email addresses on a schedule.

### Creating a Subscription

1. Open a **Report** or **Dashboard** in Power BI Service
2. Click **Subscribe** (top bar, envelope icon)
3. Configure:
   - **Subject:** Custom email subject
   - **Message:** Optional body text
   - **Frequency:** Daily, Weekly (pick day), After data refresh
   - **Start date / End date:** Schedule window
   - **Time:** When to send
   - **Format:** Full report (attached) or Link only
   - **Include page / Include preview image**
4. **Add recipients:** Your email or other users' emails
5. Click **Save and close**

### Subscription Options

| Setting | Options |
|---------|---------|
| **Frequency** | Daily, Weekly (Mon–Sun), After data refresh |
| **Time** | Any time in your time zone |
| **Attachment** | PDF attachment, Link to report, or Both |
| **Include** | Current page, All pages, or Specific pages |
| **Conditions** | Send only when data changes (optional) |
| **Recipients** | You + up to 24 other email addresses |

### Subscription Best Practices

| Practice | Why |
|----------|-----|
| **Use "After data refresh"** trigger | Ensures recipient gets the latest data |
| **Set end dates** | Avoid forgotten subscriptions running forever |
| **PDF attachment for executives** | They can read without logging in |
| **Link for analysts** | They want to interact with the report |
| **Conditional send** | Avoid sending when nothing changed |
| **Clean up** | Review subscriptions quarterly |

---

## 28.5 Embedding in Microsoft 365

### Embed in Microsoft Teams

**Method 1: Power BI Tab**
1. In a Teams channel → click **+** (Add a tab)
2. Choose **Power BI**
3. Select the report or dashboard
4. Click **Save**
5. Report is now a tab in the channel — interactive, respects RLS

**Method 2: Teams Chat**
1. Paste a Power BI report link in a Teams chat
2. Teams auto-renders a preview card
3. Click to open in full interactive view

### Embed in SharePoint Online

1. Open the report in Power BI Service
2. **File → Embed report → SharePoint Online**
3. Copy the embed URL
4. In SharePoint → Edit page → Add **Power BI web part**
5. Paste the URL → Publish the page

### Embed in PowerPoint (Live)

1. Open **PowerPoint** (desktop or web)
2. **Insert** tab → **Power BI** (or Add-ins → Power BI)
3. Paste the report URL
4. The report appears as a **live, interactive visual** in the slide
5. During presentation → full interactivity (slicers, drill-through)

> **Note:** Viewers need Power BI access to see live embedded content. For audiences without access, export as static images or PDF.

---

## 28.6 Export Options

### Exporting from Power BI Service

| Format | How | Use Case |
|--------|-----|----------|
| **PDF** | File → Export → PDF | Static document sharing, email attachment |
| **PowerPoint** | File → Export → PowerPoint | Presentation slides (static images) |
| **Excel (data)** | Visual → ⋯ → Export Data | Underlying data for analysis |
| **CSV** | Visual → ⋯ → Export Data → CSV | Raw data extract |
| **Analyze in Excel** | Dataset → Analyze in Excel | Build Excel pivot tables on Power BI data |
| **Print** | File → Print | Hard copy |

### Export Permissions

Admin settings control whether users can:
- Export data from visuals
- Download .pbix files
- Print reports
- Export to PDF/PowerPoint

> **RLS is respected** in exports — users can only export data they're authorized to see.

---

## 28.7 Publish to Web (Public Embedding)

### What Is Publish to Web?

Generates a **public embed code** (iframe) that anyone on the internet can view — no login required.

### When to Use
- **Public websites** — company blog, public dashboard
- **Kiosk displays** — lobby screens, conference rooms
- **Educational content** — embedded in articles or tutorials

### When NOT to Use
- Any report with **sensitive or confidential data**
- Internal business reports
- Reports with **RLS** (RLS is NOT enforced in Publish to Web)

### How to Publish to Web

1. Open report in Service → **File → Embed report → Publish to Web**
2. Read the warning about public access → click **Create embed code**
3. Copy the **iframe** code or **direct link**
4. Paste into your website HTML

> ⚠️ **Security Warning:** Publish to Web makes data visible to **anyone on the internet**. There is no authentication. Never use for confidential data.

---

## 28.8 Usage Metrics

### Tracking Report Usage

1. Open a report or dashboard in Power BI Service
2. Click **⋯ (More options)** → **View usage metrics report**
3. View:
   - **Views per day** — who's looking and when
   - **Unique viewers** — how many people are using it
   - **Views by platform** — Desktop, Web, Mobile
   - **Most viewed pages** — which pages are popular
   - **Performance** — average render time

### Why Monitor Usage

| Insight | Action |
|---------|--------|
| Report has zero views in 30 days | Consider archiving or deleting |
| One page gets 80% of views | Promote that page as the landing page |
| Mobile usage is high | Optimize mobile layout |
| Specific users view frequently | Engage them for feedback |
| Slow render times | Optimize DAX, reduce visuals, check data model |

---

## 🔧 Hands-On Activity: Share and Collaborate

**Duration:** 25 minutes

### Tasks

**Part 1 — Share a Report (7 min)**
1. Open your published report in Power BI Service
2. Click **Share** → create a link for "People with existing access"
3. Copy the link → paste in a chat or email to yourself
4. (Optional) Share with a colleague as Viewer with read-only access

**Part 2 — Set an Alert (5 min)**
5. Open your Dashboard
6. On the Total Revenue card tile → ⋯ → **Manage alerts**
7. Add alert: "Revenue Below ₹30 Lakhs" → Condition: Below → Value: 3000000
8. Enable email notification → Save

**Part 3 — Create a Subscription (8 min)**
9. Open your report → click **Subscribe**
10. Set: Daily at 8:00 AM, PDF attachment, your email
11. Add a custom subject: "Daily Sales Dashboard — [Date]"
12. Save

**Part 4 — Embed (5 min)**
13. (If Teams available) Add your report as a **tab in a Teams channel**
14. (If SharePoint available) Copy the embed URL for SharePoint
15. (If PowerPoint available) Insert the report in a PowerPoint slide
16. View **Usage Metrics** for your report

---

## Session 28 — Key Takeaways

1. **Multiple sharing methods:** Direct link, Workspace access, Apps, Teams, SharePoint, email
2. **Alerts** notify you when dashboard card values cross thresholds — proactive monitoring
3. **Subscriptions** deliver report snapshots via email on a schedule — great for executives
4. **Embed in Teams/SharePoint/PowerPoint** for seamless Microsoft 365 integration
5. **Publish to Web** is public and unsecured — never use for confidential data
6. **Usage Metrics** help you understand adoption and optimize your reports

---

## Preparation for Session 29
- **Choose a Capstone project topic** — a business scenario you want to build an end-to-end BI solution for
- Gather or prepare a **dataset** (real or simulated) for your project
- Review all skills learned across Sessions 1–28
- Think about: What business question will your capstone dashboard answer?

---

*Session 28 of 30 | Module 6: Power BI Service & Capstone*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
