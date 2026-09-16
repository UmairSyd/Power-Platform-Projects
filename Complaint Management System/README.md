# 🏢 Customer Complaint Management System

A modern, enterprise-style **Customer Complaint Management System** built using the **Microsoft Power Platform** to streamline complaint intake, employee assignment, complaint tracking, resolution management, notifications, and management oversight.

The solution provides a minimal and role-based user experience where employees only see the controls and information required for their responsibilities, while management gets visibility into complaint status, resolution progress, costs, escalations, and customer satisfaction.

---

## 📌 Project Overview

The Customer Complaint Management System is designed for organizations that receive customer complaints related to services, work orders, billing, property issues, suppliers, warranty claims, safety concerns, and other operational matters.

### Business Problem

Traditional complaint management often involves:

- Complaints received through emails, phone calls, or forms
- Manual assignment to employees
- Lack of visibility into complaint ownership
- Delayed follow-ups
- Difficulty tracking overdue complaints
- Manual notification processes
- No centralized resolution history
- Limited management visibility
- Difficulty measuring customer satisfaction
- Manual reporting and KPI preparation

### Solution

The application provides:

> **Complaint → Assignment → Investigation → Resolution → Customer Acceptance → Closure**

with automated notifications and centralized complaint information.

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Power Apps Canvas App** | Application user interface |
| **SharePoint Online** | Primary data storage |
| **Power Automate** | Notifications and business process automation |
| **Copilot Studio** | AI-powered complaint creation |
| **Power BI** | Reporting and analytics |
| **Microsoft 365 / Office 365** | User identity and organizational integration |
| **SharePoint Attachments** | Complaint documents/photos |
| **Microsoft Entra ID / Office 365 Users** | Employee identity and user information |

---

# 🏗️ Solution Architecture

```text
                         ┌──────────────────────┐
                         │     Customers /      │
                         │   Business Users     │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   Copilot Studio     │
                         │   Complaint Agent     │
                         └──────────┬───────────┘
                                    │
                                    │ Create Complaint
                                    ▼
┌─────────────────────────────────────────────────────────────┐
│                     POWER APPS CANVAS                       │
│                                                             │
│  Employee Assignment Dashboard                              │
│          │                                                  │
│          ▼                                                  │
│  Complaint Details / Management View                        │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
                 ┌──────────────────────┐
                 │   SharePoint Online  │
                 │                      │
                 │  Complaints List     │
                 │  Supporting Data     │
                 │  Attachments         │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │    Power Automate    │
                 │                      │
                 │ Assignment Alerts    │
                 │ Status Notifications │
                 │ Follow-ups           │
                 │ Escalations          │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │      Power BI        │
                 │                      │
                 │ KPIs & Reporting     │
                 │ Complaint Analytics  │
                 └──────────────────────┘
```

---

# 🎯 Key Features

## 1. Complaint Management

The system maintains a centralized complaint record containing:

- Complaint ID
- Work Order Number
- Customer Name
- Customer Phone
- Customer Email
- Date Received
- Complaint Category
- Assigned Employee
- Assigned Manager
- Target Solution Date
- Status
- Escalation Flag
- Proposed Solution
- Resolution Date
- Customer Accepted
- Satisfaction Rating
- Follow-up Required
- Follow-up Date
- Estimated Cost
- Actual Cost
- Warranty Claim
- Supplier Chargeback
- Management Contact Required
- Management Contact Date
- Management Notes
- Complaint Notes / Updates
- Photos and documents

---

# 🆔 Complaint ID Generation

Each complaint receives a unique complaint number.

Example:

```text
CMP-00001
CMP-00002
CMP-00003
...
CMP-00050
```

The Complaint ID provides a simple reference for employees, management, notifications, and customer communication.

---

# 📋 Complaint Status Management

| Status | Purpose |
|---|---|
| 🟢 **Open** | Complaint has been received but work has not started |
| 🔵 **In Progress** | Employee is actively working on the complaint |
| 🟡 **Waiting on Customer** | Additional information/action is required from customer |
| 🟠 **Waiting on Supplier** | Resolution depends on supplier/vendor |
| 🟣 **Resolved** | Complaint resolution has been completed |
| ⚫ **Closed** | Complaint has been completed and formally closed |
| 🔴 **Escalated** | Complaint requires management/escalation attention |

---

# 👥 Role-Based Experience

## Employee / Technician

Employees primarily work with complaints assigned to them.

Example filtering logic:

```powerfx
Filter(
    'Complaints List',
    'Assigned Employee'.Email = User().Email
)
```

The employee can:

- View assigned complaints
- Open complaint details
- Review customer information
- Review complaint description
- Update complaint status
- Add proposed solution
- Add notes/updates
- Upload supporting documents/photos
- Update resolution information
- Complete required follow-up activities

Unnecessary administrative controls are intentionally hidden from the employee experience.

---

## Management

Management receives a broader view of complaints and can monitor:

- Complaint ownership
- Complaint status
- Target solution dates
- Overdue complaints
- Escalated complaints
- Resolution progress
- Customer acceptance
- Satisfaction rating
- Estimated vs actual cost
- Warranty claims
- Supplier chargebacks
- Management contact information
- Complaint history and notes

---

# 🖥️ Application Screens

The application intentionally uses a **minimal two-screen operational experience** rather than a traditional ticket-management interface containing many screens.

---

## Screen 1 — Assignment Dashboard

### Purpose

The Assignment Dashboard is the employee's primary landing page.

It shows only complaints assigned to the currently logged-in employee.

### Header

The header contains:

- Application branding
- Welcome message
- Logged-in employee name
- Notification bell
- Refresh button

Example:

```text
┌─────────────────────────────────────────────────────────────┐
│  Customer Complaints        Welcome, Employee   🔔   ↻       │
└─────────────────────────────────────────────────────────────┘
```

### Dashboard Information

The employee can see relevant complaint information such as:

- Complaint ID
- Work Order Number
- Complaint Category
- Customer
- Status
- Target Solution Date
- Attention indicators where applicable

### KPI Summary

Compact KPI cards can show:

```text
┌───────────┐ ┌──────────────┐ ┌───────────┐
│   OPEN    │ │ IN PROGRESS  │ │  OVERDUE  │
│    12     │ │      7       │ │     2     │
└───────────┘ └──────────────┘ └───────────┘
```

The KPI section is intentionally compact to avoid clutter.

---

# 📄 Screen 2 — Complaint Details / Management View

Selecting a complaint from the Assignment Dashboard opens the Complaint Details screen.

The screen provides the information required to investigate and resolve the complaint.

### Complaint Information

- Complaint ID
- Work Order Number
- Date Received
- Complaint Category
- Complaint Status
- Customer information
- Assigned Employee
- Assigned Manager

### Resolution Information

- Target Solution Date
- Proposed Solution
- Resolution Date
- Customer Accepted
- Satisfaction Rating
- Follow-up Required
- Follow-up Date

### Financial Information

- Estimated Cost
- Actual Cost
- Warranty Claim
- Supplier Chargeback

### Management Information

- Management Contact Required
- Management Contact Date
- Management Notes
- Escalation Flag

### Supporting Information

- Attachments
- Photos
- Documents
- Notes and Updates

---

# 🎨 UI/UX Design Principles

The application was designed around the following principles:

### Minimalistic

Avoid unnecessary screens, controls, cards, and navigation.

### Role-Based

Employees see only the functionality required for their job.

### Responsive

The interface is designed to work across desktop and smaller form factors.

### Enterprise Style

The UI follows a clean Microsoft/Fluent-inspired visual language.

### Information Hierarchy

Important information such as:

- Complaint ID
- Status
- Target Solution Date
- Customer
- Assignment

is displayed prominently.

### Reduced Cognitive Load

Instead of displaying every database field simultaneously, information is grouped logically.

---

# 🗃️ Backend — SharePoint

The primary backend is **SharePoint Online**.

## Main List

### `Complaints List`

The main complaint list stores the complete complaint lifecycle.

### Core Fields

| Field | Type | Description |
|---|---|---|
| Complaint ID | Single line text | Unique complaint number |
| Work Order Number | Single line text | Related work order |
| Customer Name | Single line text | Customer name |
| Customer Phone | Single line text | Customer contact |
| Customer Email | Single line text | Customer email |
| Date Received | Date | Complaint received date |
| Complaint Category | Choice | Complaint classification |
| Assigned Employee | Person | Responsible employee |
| Assigned Manager | Person | Responsible manager |
| Target Solution Date | Date | Target resolution date |
| Status | Choice | Complaint lifecycle status |
| Escalation Flag | Yes/No | Indicates escalation |
| Proposed Solution | Multiple lines | Proposed resolution |
| Resolution Date | Date | Actual resolution date |
| Customer Accepted | Yes/No | Customer acceptance |
| Satisfaction Rating | Choice/Number | Customer satisfaction |
| Follow Up Required | Yes/No | Follow-up requirement |
| Follow Up Date | Date | Scheduled follow-up |
| Estimated Cost | Currency | Expected cost |
| Actual Cost | Currency | Actual cost |
| Warranty Claim | Yes/No | Warranty-related complaint |
| Supplier Chargeback | Yes/No | Supplier cost recovery |
| Management Contact Required | Yes/No | Management involvement |
| Management Contact Date | Date | Management contact date |
| Management Notes | Multiple lines | Management comments |
| Notes / Updates | Multiple lines | Complaint updates |
| Attachments | Attachments | Photos/documents |

---

# 🔐 Security & Access

The solution follows a role-based access model.

### Employee

Employees primarily work with complaints assigned to their account.

```powerfx
'Assigned Employee'.Email = User().Email
```

### Management

Management receives broader visibility into complaint records and operational performance.

### Identity

Logged-in user information can be retrieved through Microsoft 365 / Office 365 user services.

Example:

```powerfx
User().FullName
```

```powerfx
User().Email
```

---

# ⚙️ Power Automate Automation

Power Automate is used to automate operational processes.

---

## Flow 1 — Employee Assignment Notification

### Trigger

A complaint is assigned or the Assigned Employee field is modified.

### Process

```text
Complaint Assigned
       ↓
Identify Assigned Employee
       ↓
Retrieve Employee Email
       ↓
Send Notification
       ↓
Employee Opens Complaint
```

The assigned employee receives a notification when a complaint is assigned to them.

---

# 🔔 Flow 2 — Status Change Notification

When the complaint status changes, Power Automate can notify relevant users.

Example:

```text
Open
  ↓
In Progress
  ↓
Waiting on Supplier
  ↓
In Progress
  ↓
Resolved
  ↓
Closed
```

Notifications can be triggered based on the relevant business condition.

---

# ⏰ Flow 3 — Follow-Up Notification

If:

```text
Follow Up Required = Yes
```

the system can use:

```text
Follow Up Date
```

to trigger a reminder.

Example:

```text
Follow-Up Date Approaching
          ↓
Power Automate
          ↓
Identify Employee / Manager
          ↓
Send Reminder
```

---

# 🚨 Flow 4 — Escalation

Complaints requiring management attention can be escalated.

Example conditions:

```text
Escalation Flag = Yes
```

or:

```text
Target Solution Date < Today()
AND
Status <> Closed
```

The flow can notify the appropriate manager or management team.

---

# 🤖 Copilot Studio Integration

The solution can use **Microsoft Copilot Studio** as an AI-powered entry point for creating complaints.

Instead of requiring a user to manually navigate through the Power Apps interface, a user can interact with the Copilot agent.

### Example

User:

> "I want to report a water leakage issue for work order WO-2026-1001."

The agent can collect the required information:

```text
Customer Name
Customer Contact
Work Order Number
Complaint Category
Complaint Description
```

The agent then passes the information to Power Automate.

---

## Copilot Architecture

```text
User
 ↓
Copilot Studio
 ↓
Collect Complaint Information
 ↓
Power Automate
 ↓
Create SharePoint Item
 ↓
Generate Complaint ID
 ↓
Return Complaint Number
```

Example response:

```text
Your complaint has been created successfully.

Complaint Number: CMP-00026
```

The Copilot experience is designed as an additional entry point and does not replace the operational Power Apps interface.

---

# 📊 Power BI Reporting

Power BI can be connected to the SharePoint complaint data to provide management reporting.

Potential KPIs include:

### Complaint KPIs

- Total Complaints
- Open Complaints
- In Progress
- Waiting on Customer
- Waiting on Supplier
- Resolved
- Closed
- Escalated
- Overdue Complaints

### Operational KPIs

- Complaints by Category
- Complaints by Employee
- Complaints by Manager
- Complaints by Month
- Resolution Trend
- Average Resolution Time
- Follow-Up Requirements

### Financial KPIs

- Estimated Cost
- Actual Cost
- Cost Variance
- Warranty Claims
- Supplier Chargebacks

### Customer KPIs

- Customer Acceptance
- Satisfaction Rating
- Satisfaction Trend

---

# 🧮 Example Business Logic

## Logged-In Employee Filtering

```powerfx
Filter(
    'Complaints List',
    'Assigned Employee'.Email = User().Email
)
```

---

## Overdue Complaint

Conceptually:

```powerfx
'Target Solution Date' < Today()
    &&
Status.Value <> "Closed"
```

This identifies complaints where the target solution date has passed and the complaint is not closed.

---

## Current User

```powerfx
User().Email
```

can be used to identify the logged-in employee.

---

# 🎨 Status Visualization

Status indicators can use different visual treatments to allow users to quickly understand complaint state.

| Status | UI Purpose |
|---|---|
| Open | New/unstarted complaint |
| In Progress | Active work |
| Waiting on Customer | Customer action required |
| Waiting on Supplier | Supplier dependency |
| Resolved | Resolution completed |
| Closed | Process completed |
| Escalated | Management attention |

The exact visual treatment can be implemented through Power Apps conditional formatting.

---

# 📎 Attachments

The complaint record supports supporting documentation such as:

- Customer photos
- Property/service images
- Invoices
- Work order documents
- Supplier documents
- Supporting evidence

These attachments remain associated with the complaint record.

---

# 📝 Complaint Notes & Updates

The application maintains operational notes for documenting complaint progress.

Example:

```text
12-Aug-2026
Technician inspected the reported issue.

14-Aug-2026
Replacement material requested from supplier.

18-Aug-2026
Repair completed.

19-Aug-2026
Customer confirmed resolution.
```

This provides useful context throughout the complaint lifecycle.

---

# 🏢 Example Business Scenario

The solution can be used for organizations such as:

- Real Estate
- Facilities Management
- Property Management
- Construction
- Field Services
- Customer Service
- Manufacturing
- Utilities
- Service Operations

### Example Complaint

```text
Complaint ID: CMP-00026

Work Order: WO-2026-1001

Category: Water Leakage

Customer: Customer Name

Assigned Employee: Technician

Assigned Manager: Operations Manager

Status: In Progress

Target Solution Date: 20-Aug-2026
```

The technician investigates the complaint, updates the proposed solution, uploads photos, and changes the status.

Once the issue is resolved, the customer acceptance and satisfaction information can be captured before the complaint is closed.

---

# 🧩 Solution Components

```text
Customer Complaint Management System
│
├── Power Apps
│   ├── Assignment Dashboard
│   └── Complaint Details
│
├── SharePoint
│   └── Complaints List
│
├── Power Automate
│   ├── Assignment Notification
│   ├── Status Notification
│   ├── Follow-Up Reminder
│   └── Escalation
│
├── Copilot Studio
│   └── Complaint Creation Agent
│
└── Power BI
    └── Complaint Analytics & KPIs
```

---

# 🔄 End-to-End Complaint Lifecycle

```text
                    ┌─────────────┐
                    │   Complaint │
                    │   Received  │
                    └──────┬──────┘
                           ↓
                    ┌─────────────┐
                    │     Open    │
                    └──────┬──────┘
                           ↓
                    ┌─────────────┐
                    │  Assigned   │
                    │  Employee   │
                    └──────┬──────┘
                           ↓
                    ┌─────────────┐
                    │ In Progress │
                    └──────┬──────┘
                           ↓
                ┌──────────┴──────────┐
                ↓                     ↓
       Waiting on Customer    Waiting on Supplier
                │                     │
                └──────────┬──────────┘
                           ↓
                    ┌─────────────┐
                    │   Resolved  │
                    └──────┬──────┘
                           ↓
                  Customer Acceptance
                           ↓
                    ┌─────────────┐
                    │    Closed   │
                    └─────────────┘
```

---

# 🧪 Testing

The application should be tested across the following scenarios.

### Functional Testing

- Create complaint
- Generate Complaint ID
- Assign employee
- Reassign employee
- Update status
- Add notes
- Upload attachment
- Update resolution
- Capture customer acceptance
- Capture satisfaction rating
- Close complaint

### Automation Testing

- Assignment notification
- Status notification
- Follow-up reminder
- Escalation notification

### Security Testing

- Employee sees assigned complaints
- Employee cannot access unnecessary administrative functionality
- Management has appropriate visibility
- User identity is correctly resolved

### Edge Cases

- Missing customer information
- Missing employee assignment
- Past target solution date
- Complaint reassignment
- Supplier dependency
- Customer follow-up
- Escalated complaint
- Complaint reopened after resolution

---

# 🚀 Future Enhancements

Potential future enhancements include:

- Dataverse migration for larger-scale deployments
- Advanced role-based security
- SLA and escalation engine
- Teams notifications
- Microsoft Teams adaptive cards
- Customer-facing Power Pages portal
- AI-generated complaint summaries
- AI-powered complaint categorization
- Sentiment analysis
- Automated priority classification
- Predictive complaint analytics
- Knowledge-based resolution suggestions
- Customer email integration
- Mobile-optimized technician experience
- Azure DevOps CI/CD
- Power Platform ALM
- Environment Variables
- Connection References
- Managed Solutions

---

# 📈 Scalability Considerations

The initial implementation uses SharePoint as the data source, making it suitable for organizations that already operate within Microsoft 365.

For larger enterprise implementations, the data layer can be migrated to **Microsoft Dataverse**.

### Current Architecture

```text
Power Apps
    ↓
SharePoint
    ↓
Power Automate
```

### Enterprise Architecture

```text
Power Apps
    ↓
Dataverse
    ↓
Power Automate
    ↓
Enterprise Integrations
    ↓
Power BI
```

Dataverse would provide additional capabilities around:

- Relational data
- Security roles
- Business units
- Auditing
- Dataverse relationships
- Enterprise-scale application architecture
- ALM

---

# 🔐 ALM & Deployment Considerations

For an enterprise deployment, the solution can be packaged into a Power Platform Solution containing:

```text
Solution
│
├── Canvas App
├── Power Automate Flows
├── Connection References
├── Environment Variables
└── Supporting Components
```

Typical environments:

```text
Development
     ↓
Test / UAT
     ↓
Production
```

This allows changes to be developed and tested before production deployment.

---

# 💼 Business Benefits

The solution helps organizations:

- Centralize complaint information
- Reduce manual complaint tracking
- Improve employee accountability
- Automate notifications
- Improve management visibility
- Track resolution progress
- Monitor overdue complaints
- Capture customer satisfaction
- Track complaint-related costs
- Improve operational reporting
- Reduce dependency on email and spreadsheets

---

# 👨‍💻 Skills Demonstrated

## Power Apps

- Canvas Apps
- Galleries
- Forms
- Data Cards
- Power Fx
- Filtering
- User-based filtering
- Conditional formatting
- Responsive UI
- Role-based UI
- Navigation
- Record selection
- SharePoint integration

## Power Automate

- SharePoint triggers
- Automated cloud flows
- Notifications
- Conditional logic
- Date-based automation
- Assignment workflows
- Escalation workflows
- Dynamic content
- Power Apps integration

## SharePoint

- SharePoint Lists
- Choice columns
- Person columns
- Date fields
- Currency fields
- Yes/No fields
- Attachments
- List-based application architecture

## Copilot Studio

- AI agent
- Topics / conversational flows
- Collecting user information
- Power Automate integration
- Complaint creation
- Returning Complaint IDs

## Power BI

- KPI dashboards
- Complaint analytics
- Operational reporting
- Trend analysis

---

# 📁 Suggested Repository Structure

```text
customer-complaint-management/
│
├── README.md
│
├── docs/
│   ├── architecture.md
│   ├── business-requirements.md
│   ├── data-model.md
│   └── deployment-guide.md
│
├── power-apps/
│   └── screenshots/
│
├── power-automate/
│   └── flow-documentation/
│
├── copilot-studio/
│   └── agent-documentation/
│
├── power-bi/
│   └── dashboard-screenshots/
│
└── screenshots/
    ├── assignment-dashboard.png
    ├── complaint-details.png
    └── management-view.png
```

---

# 📸 Application Screens

### Assignment Dashboard

The primary employee workspace where logged-in employees see their assigned complaints.

### Complaint Details

The operational workspace used to investigate, update, resolve, and close complaints.

### Management View

Provides broader visibility into complaint status, escalation, resolution, costs, customer acceptance, and management information.

---

# 🏁 Project Outcome

The **Customer Complaint Management System** demonstrates how Microsoft Power Platform can be used to build an end-to-end business application using low-code technologies.

The solution combines:

**Power Apps + SharePoint + Power Automate + Copilot Studio + Power BI**

to create a centralized complaint management process covering:

```text
Complaint Intake
       ↓
Complaint Creation
       ↓
Employee Assignment
       ↓
Investigation
       ↓
Status Tracking
       ↓
Follow-Up
       ↓
Escalation
       ↓
Resolution
       ↓
Customer Acceptance
       ↓
Closure
       ↓
Reporting & Analytics
```

The architecture is intentionally modular so the solution can start with Microsoft 365/SharePoint and later evolve toward an enterprise Dataverse-based Power Platform architecture.

---

# ⭐ Project Highlights

- ✅ Canvas Power Apps application
- ✅ Minimalistic enterprise UI
- ✅ Role-based employee experience
- ✅ Employee-specific assignment dashboard
- ✅ Complaint details and management view
- ✅ SharePoint-based backend
- ✅ Complaint lifecycle management
- ✅ Automated employee notifications
- ✅ Status-based automation
- ✅ Follow-up reminders
- ✅ Escalation management
- ✅ Complaint attachments
- ✅ Customer acceptance tracking
- ✅ Satisfaction rating
- ✅ Cost tracking
- ✅ Warranty and supplier chargeback tracking
- ✅ Copilot Studio complaint creation
- ✅ Power Automate integration
- ✅ Power BI reporting architecture
- ✅ Responsive design approach
- ✅ Enterprise scalability considerations
- ✅ ALM-ready architecture

---

## 👨‍💻 Project Type

**Microsoft Power Platform — Business Application / Complaint Management**

**Primary Role:** Power Platform Developer / Solution Developer

**Technologies:**  
`Power Apps` `Power Automate` `SharePoint Online` `Copilot Studio` `Power BI` `Microsoft 365` `Power Fx`

---

## 📌 Disclaimer

This project is a portfolio/demo implementation intended to demonstrate Power Platform application development, automation, AI integration, data management, and reporting capabilities. Business rules, security configuration, and production deployment should be adapted to the organization's specific requirements.
