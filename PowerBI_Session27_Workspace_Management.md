# Session 27 — Workspace Management
## Module 6: Power BI Service & Capstone | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Demo | Hands-On: Create and Manage Workspaces

---

## Learning Objectives
By the end of this session, you will be able to:
1. Differentiate between My Workspace and shared Workspaces
2. Create and configure a shared Workspace
3. Assign Workspace roles (Admin, Member, Contributor, Viewer)
4. Organize content across Workspaces using a governance strategy
5. Understand Power BI Apps and how to distribute them

---

## 27.1 What is a Workspace?

A **Workspace** is a collaborative container in Power BI Service where teams store and manage reports, dashboards, datasets, and dataflows.

### My Workspace vs Shared Workspace

| Feature | My Workspace | Shared Workspace |
|---------|-------------|-----------------|
| **Owner** | You only | Team/group |
| **Sharing** | Manual share per item | Automatic via workspace membership |
| **Collaboration** | No — single user | Yes — multiple users |
| **Best for** | Personal development, testing | Team reports, production content |
| **Content lifecycle** | Draft/personal | Published/shared |
| **Apps** | Cannot create Apps | Can create and publish Apps |

> **Best Practice:** Use "My Workspace" for **development and testing only**. Use shared Workspaces for anything that others will access.

---

## 27.2 Creating a Workspace

### Step-by-Step

1. In Power BI Service → left navigation → **Workspaces** → **Create a workspace**
2. Enter: **Workspace name** (e.g., "Sales Analytics — Production")
3. Optional: Add a **description** (helps others understand the purpose)
4. Optional: Upload a **workspace image** (logo or icon)
5. **Advanced settings:**
   - **License mode:** Pro, Premium per user, Premium per capacity, Embedded, Fabric
   - **Contact list:** People to contact about this workspace
   - **OneDrive:** Link to a shared OneDrive/SharePoint folder
6. Click **Save**

### Workspace Naming Conventions

| Pattern | Example | Use |
|---------|---------|-----|
| `[Team] - [Environment]` | "Sales Analytics — Production" | Clear ownership and stage |
| `[Department] - [Project]` | "Finance — Budget Reports" | Department-organized |
| `[Region] - [Function]` | "APAC — Operations Dashboard" | Region-based organizations |
| `DEV / UAT / PROD` suffix | "HR Analytics — DEV" | Environment separation |

### Recommended Workspace Strategy

```
Sales Analytics — DEV        ← Developers build and test here
Sales Analytics — UAT        ← Business users validate
Sales Analytics — PROD       ← Published App for all viewers
```

---

## 27.3 Workspace Roles

### Four Roles

| Role | Permissions | Best For |
|------|------------|---------|
| **Admin** | Full control: add/remove users, delete workspace, publish apps, manage all content | Workspace owner, BI team lead |
| **Member** | Create, edit, delete content; publish apps; add Contributors and Viewers | BI developers, report authors |
| **Contributor** | Create and edit content; cannot publish apps or manage access | Analysts who build reports |
| **Viewer** | View content only; cannot edit, create, or share | Business users who consume reports |

### Detailed Permission Matrix

| Action | Admin | Member | Contributor | Viewer |
|--------|-------|--------|-------------|--------|
| View reports and dashboards | ✅ | ✅ | ✅ | ✅ |
| Create/edit reports | ✅ | ✅ | ✅ | ❌ |
| Delete content | ✅ | ✅ | ✅ (own content) | ❌ |
| Publish to workspace | ✅ | ✅ | ✅ | ❌ |
| Create/publish an App | ✅ | ✅ | ❌ | ❌ |
| Add Members/Contributors | ✅ | ✅ | ❌ | ❌ |
| Add Viewers | ✅ | ✅ | ❌ | ❌ |
| Add Admins | ✅ | ❌ | ❌ | ❌ |
| Remove users | ✅ | ❌ | ❌ | ❌ |
| Delete workspace | ✅ | ❌ | ❌ | ❌ |
| Configure dataset refresh | ✅ | ✅ | ✅ | ❌ |
| Manage RLS | ✅ | ✅ | ❌ | ❌ |
| Export data | ✅ | ✅ | ✅ | Depends on setting |

### Adding Users to a Workspace

1. Open the Workspace → click **Access** (top-right, people icon)
2. Enter the user's **email address**
3. Select the **role** (Admin, Member, Contributor, Viewer)
4. Click **Add**
5. User receives an email notification and sees the workspace in their navigation

### Using Security Groups

Instead of adding individual users:
- Create an **Azure AD Security Group** (e.g., "Sales Analysts Group")
- Add the group to the workspace with the appropriate role
- Manage membership in Azure AD — adding/removing users auto-updates access

> **Best Practice:** Use **Security Groups** for workspace access — easier to manage, especially for large teams.

---

## 27.4 Content Organization Within Workspaces

### Content Types in a Workspace

| Content | Icon | Description |
|---------|------|-------------|
| **Report** | 📊 | Published .pbix report pages |
| **Dashboard** | 📋 | Pinned visuals from reports |
| **Dataset** | 🗄️ | Data model behind reports |
| **Dataflow** | 🔄 | Reusable Power Query transformations |
| **Paginated Report** | 📄 | Pixel-perfect, export-ready reports (.rdl) |
| **Scorecard** | 🎯 | Goal tracking with Metrics feature |

### Organization Best Practices

| Practice | Why |
|----------|-----|
| **One workspace per project/team** | Clear ownership and scope |
| **Separate DEV from PROD** | Prevent unfinished work from reaching users |
| **Shared datasets across workspaces** | Build once, use in multiple reports |
| **Naming conventions** | Consistent names help users find content |
| **Workspace description** | Tell users what this workspace is for |
| **Clean up unused content** | Delete old/unused reports regularly |

---

## 27.5 Power BI Apps

### What is an App?

An **App** is a packaged, read-only collection of reports and dashboards published from a Workspace. It's the primary way to distribute content to business users.

### Workspace vs App

| Feature | Workspace | App |
|---------|-----------|-----|
| **Audience** | Developers, report builders | Business users, consumers |
| **Editing** | Full editing for authorized roles | Read-only for all users |
| **Content** | May include draft/WIP items | Curated, production-ready only |
| **Access** | Workspace membership | App installation (no workspace access needed) |
| **Updates** | Instant (any change is live) | Controlled (update App explicitly) |
| **Navigation** | Flat list of all content | Custom navigation with sections |

### Creating and Publishing an App

1. Open the Workspace → click **Create App** (top bar)
2. **Setup tab:**
   - App name (e.g., "Sales Analytics")
   - Description
   - App logo/image
   - Contact information
3. **Navigation tab:**
   - Arrange content into **sections** (like a table of contents)
   - Show/hide specific reports and dashboards
   - Set the **landing page** (first thing users see)
4. **Permissions tab:**
   - **Entire organization** — all Pro/Premium users can install
   - **Specific groups/users** — only listed people can install
   - **Allow copying data** — can users export?
   - **Allow building on datasets** — can users create their own reports on this data?
5. Click **Publish App**

### Updating an App

When you update reports in the Workspace:
1. Changes are **NOT automatically reflected** in the App
2. Go to Workspace → **Update App**
3. Review changes → click **Update App**
4. Users see the updated content on next visit

> **This is a feature, not a bug** — it prevents draft changes from reaching users before they're ready.

### Installing an App (User Perspective)

Users install Apps by:
1. **Direct link** shared by the publisher
2. **Apps** section in Power BI Service → **Get Apps**
3. **AppSource** (Microsoft's marketplace for organizational apps)

---

## 27.6 Shared Datasets (Reusability)

### The Problem
Multiple teams build reports on the same data → each creates their own dataset → inconsistent numbers.

### The Solution: Shared Datasets

1. Create a **certified, well-modeled dataset** in one workspace
2. Other report builders connect to this dataset from their workspaces
3. All reports use the **same data model, same measures, same definitions**

### Connecting to a Shared Dataset

In Power BI Desktop:
1. Home → **Get Data → Power BI datasets**
2. Browse available datasets (from workspaces you have access to)
3. Select the dataset → **Connect**
4. Build your report using the shared model
5. Publish your report to your own workspace

### Dataset Endorsement

| Level | Meaning | Who Can Set |
|-------|---------|-------------|
| **Promoted** | Recommended by the owner | Dataset owner |
| **Certified** | Approved by the organization as a trusted source | BI team / Admin |
| No endorsement | Default — no quality guarantee | — |

**Setting Endorsement:**
- Dataset → ⋯ → **Settings → Endorsement** → choose Promoted or Certified

---

## 27.7 Workspace Governance

### Governance Framework

| Area | Guideline |
|------|-----------|
| **Naming** | Consistent naming: `[Team] - [Environment]` |
| **Ownership** | Every workspace has a designated owner |
| **Access** | Use Security Groups, not individual users |
| **Lifecycle** | DEV → UAT → PROD pipeline |
| **Certification** | Only certified datasets for production reports |
| **Cleanup** | Quarterly review: archive or delete unused content |
| **Documentation** | Maintain a data dictionary and measure definitions |
| **Monitoring** | Use Usage Metrics to track adoption |

---

## 🔧 Hands-On Activity: Workspace Setup

**Duration:** 25 minutes

### Tasks

**Part 1 — Create a Workspace (8 min)**
1. Power BI Service → Workspaces → **Create a workspace**
2. Name: "Sales Analytics — Practice"
3. Add a description: "Practice workspace for Power BI course"
4. Save

**Part 2 — Publish and Organize Content (10 min)**
5. In Power BI Desktop → Publish your report to the new workspace
6. In Service → verify Report and Dataset appear
7. Create a Dashboard in the workspace by pinning visuals
8. Rename items clearly (e.g., "Sales Performance Report — v1")

**Part 3 — Manage Access (7 min)**
9. Workspace → **Access** → Add a colleague as **Viewer**
10. Add yourself as **Admin** (should be default as creator)
11. Review the permission matrix — understand what each role can do
12. (Optional) Create an App from the workspace → configure navigation → publish

---

## Session 27 — Key Takeaways

1. **My Workspace** = personal sandbox; **Shared Workspaces** = team collaboration
2. **Four roles:** Admin (full control), Member (create + manage), Contributor (create), Viewer (read-only)
3. **Apps** are the best way to distribute polished reports to business users
4. **Shared datasets** ensure consistency — build once, report many times
5. Use **Security Groups** for access management — not individual emails

---

## Preparation for Session 28
- Think about: How would you share a report with someone outside your organization?
- Review: What is the difference between sharing a report vs sharing a dashboard?
- Consider: What email alerts would be useful for your dashboard?

---

*Session 27 of 30 | Module 6: Power BI Service & Capstone*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
