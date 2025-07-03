# 🎯 SC-200 Study Reflection Summary

## 🟢 Microsoft Sentinel

### Sentinel Workspaces
**What is it?**  
A Log Analytics workspace + Sentinel solution layered on top.

**Needed to deploy Sentinel:**
- Azure subscription
- Microsoft Entra tenant (Azure AD)
- Log Analytics workspace

✅ **First step when deploying Sentinel:**  
_Create a Log Analytics workspace._

---

### Livestream Queries
- **Livestream = Real-time streaming view of incoming events.**
- **Rule:**  
  Livestream queries cannot have time filters (e.g., `TimeGenerated > ago(7d)`).
- If you see `ago()` or any fixed time range—**remove it**.

---

### Bookmarks vs. Watchlists
- **Bookmark:** Save query results as evidence for investigations.
  - Shows in the **investigation graph**.
- **Watchlist:** Static list of values (usernames, IPs) you reference in queries.
  - **Does NOT** store query results.

✅ **Quick Tip:**  
_Need evidence? Bookmark._  
_Need lookup list? Watchlist._

---

### Entity Mapping in Hunting Queries
Some fields can be mapped to entities in Sentinel:

| Column              | Entity Mapping        |
|---------------------|------------------------|
| `UserPrincipalName` | ✅ Account entity       |
| `IPAddress`         | ✅ IP entity            |
| `AppDisplayName`    | ✅ Cloud app entity     |
| `Reason`            | ❌ No entity mapping    |

✅ **Quick Tip:**  
_Descriptive fields (e.g., Reason) can’t map to entities._

---

### Roles
- **Sentinel Responder:** Manage incidents (assign, close).
- **Logic App Operator:** Run (but not edit) playbooks.
- **Contributor:** Full edit permissions—**too much for Tier 1 analysts.**

✅ **Quick Tip:**  
_Need least privilege to manage incidents and run playbooks? Responder + Logic App Operator._

---

### Data Connectors
- **Collect SharePoint/Teams logs:** Microsoft 365 connector.
- **Collect Defender for Office 365 alerts:** Defender for Office 365 connector.

✅ **Quick Tip:**  
_SharePoint activity = Microsoft 365 connector._

---

### KQL Basics
- `render`: Displays results as a chart.
- `print`: Outputs a single row with scalar values.
- `project`: Selects and orders columns.
- `extend`: Adds calculated columns.
- `summarize`: Groups rows and aggregates.

✅ **Quick Tip:**  
_render = chart_  
_project = select columns_  
_extend = new column_  
_summarize = group + aggregate_  
_print = single row_

---

## 🟢 Microsoft Defender

### Custom Detection Rules in Hunting
- Must return **ReportId** and **Timestamp** columns.
- `AlertId` is invalid here.

✅ **Quick Tip:**  
_Hunting detection? Always ReportId and Timestamp._

---

### Notification Rules
- **Threat analytics email notification rule:** Alerts about new threat intelligence content.
- **Advanced Hunting detection rule:** Alerts on query matches.
- **Alert email notification rule:** Emails you on already-generated alerts (not new threat analytics).

✅ **Quick Tip:**  
_New threat intelligence? Use Threat Analytics Email Notification._

---

### Attack Surface Reduction
- Blocks unsigned executables from USB.
- Blocks executable content from email.

✅ **Quick Tip:**  
_Blocking risky behavior? Attack Surface Reduction._

---

### Custom Network Indicators
- Allow/block specific IPs and URLs.
- Different from web content filtering (category-based).

✅ **Quick Tip:**  
_Need to block a specific IP or domain? Custom network indicators._

---

### Suppression Rules
- Automatically close alerts from known benign sources (e.g., lab environments).

✅ **Quick Tip:**  
_Auto-close alerts from specific IP ranges? Suppression rule._

---

## 🟢 Defender for Servers (AWS context)

### To onboard AWS EC2 instances:
- Defender for Servers plan **enabled in Azure.**
- Azure Arc-enabled servers **installed on EC2 instances.**
- Log Analytics agent connected.

✅ **Quick Tip:**  
_AWS Defender? Arc + Defender Plan + Log Analytics Agent._

---

### Azure Pipelines Agent
- Used only for Azure DevOps pipelines.
- **Does not** provide Defender connectivity.

---

## 🟢 How to Use This Summary

✅ Review these Quick Tips regularly.  
✅ Rephrase them in your own words weekly to reinforce memory.  
✅ Practice identifying scenarios (e.g., “Which connector do I use?” “Which role do I assign?”).

---

This will be updated continuously... > A$AP RAF
