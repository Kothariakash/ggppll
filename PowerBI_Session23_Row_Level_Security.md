# Session 23 — Row-Level Security (RLS)
## Module 5: Advanced Reporting | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Implement RLS for Region-Based Data Access

---

## Learning Objectives
By the end of this session, you will be able to:
1. Explain what Row-Level Security is and why it's essential
2. Create static RLS roles with DAX filter expressions
3. Create dynamic RLS using USERPRINCIPALNAME()
4. Test RLS in Power BI Desktop
5. Assign users to RLS roles in Power BI Service

---

## 23.1 What is Row-Level Security?

**Row-Level Security (RLS)** restricts data access at the row level — different users see different data from the same report.

### The Problem RLS Solves

| Without RLS | With RLS |
|-------------|----------|
| All users see all data | Each user sees only their authorized data |
| Create separate reports per region/team | One report, many views — based on login |
| Data leakage risk | Data access controlled and audited |
| Maintenance nightmare (10 regions = 10 reports) | One report, one maintenance point |

### Real-World Examples

| Scenario | RLS Rule |
|----------|----------|
| Regional sales managers | See only their region's data |
| Store managers | See only their store's data |
| Department heads | See only their department's data |
| Account managers | See only their assigned customers |
| Country managers | See only their country's data |

---

## 23.2 How RLS Works

### Architecture

```
User logs into Power BI Service
        │
        ▼
Power BI checks: What ROLE is this user assigned to?
        │
        ▼
Role has a DAX filter: Region = "North"
        │
        ▼
ALL queries are automatically filtered to Region = "North"
        │
        ▼
User sees ONLY North region data in every visual, every page
```

### RLS Components

| Component | Where | Purpose |
|-----------|-------|---------|
| **Role** | Defined in Power BI Desktop | Named security role (e.g., "North Region") |
| **DAX Filter** | Written in Desktop | Filter expression applied to a table |
| **User Assignment** | Done in Power BI Service | Map users to roles |

### Key Concept: RLS Filters Flow Through Relationships

If you apply an RLS filter on the **Regions** dimension table:
- Regions table filtered → only "North" rows
- Filter flows through relationship to **Sales** fact table
- Sales table also filtered → only North sales
- All visuals show only North data

> **This is why Star Schema matters for RLS** — one filter on a dimension cascades to all connected facts.

---

## 23.3 Creating Static RLS Roles

### What is Static RLS?

Each role has a **hardcoded filter** — you create one role per group (region, department, etc.).

### Step-by-Step in Power BI Desktop

1. **Modeling** tab → **Manage Roles**
2. Click **Create** → name the role (e.g., "North Region")
3. Select the table to filter (e.g., "Regions" or "Sales")
4. Write the DAX filter expression:
   ```dax
   [Region] = "North"
   ```
5. Click **Save**
6. Repeat for each role:
   - "South Region": `[Region] = "South"`
   - "East Region": `[Region] = "East"`
   - "West Region": `[Region] = "West"`

### DAX Filter Syntax

| Filter | DAX Expression |
|--------|---------------|
| Single value | `[Region] = "North"` |
| Multiple values | `[Region] IN {"North", "East"}` |
| Starts with | `LEFT([Region], 1) = "N"` |
| Contains | `SEARCH("North", [Region], 1, 0) > 0` |
| Numeric range | `[Revenue] > 50000` |
| Date filter | `[OrderDate] >= DATE(2024, 1, 1)` |

### Where to Apply the Filter

| Apply Filter On | When |
|----------------|------|
| **Dimension table** (recommended) | Filter flows through relationships to all fact tables |
| **Fact table** | Only when no suitable dimension exists |

> **Best Practice:** Always apply RLS filters on **Dimension tables** — they cascade to all related facts through relationships.

---

## 23.4 Creating Dynamic RLS

### What is Dynamic RLS?

Instead of hardcoded values, the filter uses the **logged-in user's identity** to determine what they can see. One role handles all users.

### How It Works

1. A **User-Region mapping table** defines which user can see which region
2. The RLS filter uses `USERPRINCIPALNAME()` to get the current user's email
3. The filter matches the email to the mapping table → shows only authorized data

### Step-by-Step

**Step 1: Create a User-Region Mapping Table**

Import or create (Enter Data):

| UserEmail | Region |
|-----------|--------|
| priya@company.com | North |
| rahul@company.com | South |
| anita@company.com | East |
| vikram@company.com | West |
| manager@company.com | North |
| manager@company.com | South |

> A user can appear multiple times for multi-region access.

**Step 2: Create Relationship**
- UserMapping[Region] → Regions[Region] (or Sales[Region])
- This connects the user mapping to the data model

**Step 3: Create the Dynamic Role**
1. Modeling → Manage Roles → Create → name: "Dynamic RLS"
2. Select the **UserMapping** table
3. DAX filter:
   ```dax
   [UserEmail] = USERPRINCIPALNAME()
   ```
4. Save

**Step 4: How It Works at Runtime**

```
User: priya@company.com logs in
        │
        ▼
RLS filter: UserMapping[UserEmail] = "priya@company.com"
        │
        ▼
UserMapping filtered → Row: priya@company.com, Region = "North"
        │
        ▼
Filter flows: Regions table → Region = "North"
        │
        ▼
Filter flows: Sales table → only North sales
        │
        ▼
All visuals show North data only
```

### USERPRINCIPALNAME() Function

| Function | Returns | Example |
|----------|---------|---------|
| `USERPRINCIPALNAME()` | Current user's email/UPN | "priya@company.com" |
| `USERNAME()` | Current user's domain\username | "DOMAIN\priya" (less common in cloud) |

> **Use `USERPRINCIPALNAME()`** for Power BI Service (cloud). It returns the user's Azure AD email.

---

## 23.5 Testing RLS in Desktop

### How to Test

1. **Modeling** tab → **View as Roles**
2. Check the role you want to test (e.g., "North Region")
3. Optionally check **Other user** and type an email (for dynamic RLS testing)
4. Click **OK**
5. A yellow banner appears: "Now viewing report as: North Region"
6. Verify: All visuals show only North data
7. Click **Stop viewing** to exit

### Testing Checklist

- [ ] Cards show filtered totals (not grand totals)
- [ ] Charts show only authorized categories
- [ ] Tables show only authorized rows
- [ ] Slicers show only authorized values
- [ ] Maps show only authorized locations
- [ ] Drill-through works within authorized data
- [ ] No data leakage in any visual

---

## 23.6 Assigning Users to Roles (Power BI Service)

### After Publishing

1. Publish the report to Power BI Service
2. In the **Workspace** → find the **Dataset** (not the report)
3. Click **... (More options)** → **Security**
4. Select the role (e.g., "North Region")
5. Add members: type email addresses of users who should have this role
6. Click **Add** → **Save**

### Assignment Rules

| Rule | Detail |
|------|--------|
| Users can be in **multiple roles** | They see the UNION of all role data |
| **Admins** are not affected by RLS | Workspace admins/members see all data |
| **Viewers** are affected | Users with Viewer role see RLS-filtered data |
| **Report owner** is not affected | The person who published always sees all data |

### Testing in Service

1. Go to the dataset → Security → select a role
2. Click **Test as role** → opens the report in that role's view
3. Verify the filtered data

---

## 23.7 RLS Best Practices

| Practice | Why |
|----------|-----|
| **Apply filters on Dimension tables** | Cascades through relationships to all facts |
| **Use Dynamic RLS** over Static when possible | Easier to maintain — add users to mapping table, not new roles |
| **Keep the mapping table in the data source** | Not hardcoded in the model — easy to update |
| **Test every role thoroughly** | Data leakage is a security risk |
| **Document role definitions** | Who can see what — for audit and compliance |
| **Don't use RLS for report-level filtering** | Use slicers for user preference; RLS for security |
| **Verify with USERPRINCIPALNAME()** | Test with actual user emails |
| **Inform users** | Let users know they see filtered data (add a note in the report) |

---

## 23.8 RLS Limitations

| Limitation | Detail |
|-----------|--------|
| **Desktop only** | Roles must be created in Power BI Desktop |
| **Assignment only in Service** | Users are assigned to roles in Power BI Service |
| **Not for Power BI Embedded** | Requires different approach (token-based RLS) |
| **Performance** | Complex RLS filters can slow queries |
| **Q&A** | Natural language queries respect RLS |
| **Dashboard tiles** | RLS applies to tiles pinned from reports |
| **Export** | Users can only export data they can see |

---

## 🔧 Hands-On Activity: Implement Row-Level Security

**Duration:** 25 minutes

### Part 1 — Static RLS (10 min)
1. Open your Sales dashboard in Power BI Desktop
2. Modeling → **Manage Roles** → Create role: "North Region"
3. On the Regions (or Sales) table, add filter: `[Region] = "North"`
4. Create another role: "South Region" with filter `[Region] = "South"`
5. Save
6. **Test:** Modeling → View as Roles → select "North Region"
7. Verify: All visuals show only North data
8. Stop viewing

### Part 2 — Dynamic RLS (10 min)
9. Create a **UserMapping** table (Enter Data):
   | UserEmail | Region |
   |-----------|--------|
   | yourname@email.com | North |
   | test@email.com | South |
10. Create relationship: UserMapping[Region] → Regions[Region]
11. Manage Roles → Create: "Dynamic RLS"
12. On UserMapping table: `[UserEmail] = USERPRINCIPALNAME()`
13. Save

### Part 3 — Test Dynamic RLS (5 min)
14. View as Roles → check "Dynamic RLS" + check "Other user" → type your email
15. Verify: Only your assigned region's data appears
16. Stop viewing
17. Save

---

## Session 23 — Key Takeaways

1. **RLS** restricts data access per user — different users see different rows from the same report
2. **Static RLS** = hardcoded filters per role; **Dynamic RLS** = uses `USERPRINCIPALNAME()` + mapping table
3. Apply RLS filters on **Dimension tables** — filters cascade through relationships
4. **Test thoroughly** in Desktop (View as Roles) and in Service (Test as role)
5. Users are **assigned to roles in Power BI Service** after publishing

---

## Preparation for Session 24
- Review: What makes a dashboard "good" vs "bad"?
- Think about: What are the top 5 design mistakes you've seen in dashboards?
- Explore: Look at dashboard examples on the Power BI Community Gallery

---

*Session 23 of 30 | Module 5: Advanced Reporting*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
