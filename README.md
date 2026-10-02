# 🎫 Customer Support Ticket Priority Prediction and Automated Assignment System

DEMO VIDEO:https://drive.google.com/file/d/1YDJtAjkI6D1kwpgYVtr1iUQyjoPeoxvN/view?usp=drivesdk
DOCUMENT:https://drive.google.com/file/d/1QSJqZnM8nKMY4wmpNCgRLxcP985z3fiB/view?usp=drivesdk

![Salesforce](https://img.shields.io/badge/Platform-Salesforce-blue)
![Agentforce](https://img.shields.io/badge/AI-Agentforce-purple)
![Automation](https://img.shields.io/badge/Automation-Auto--Launched%20Flow-orange)
![Team](https://img.shields.io/badge/Team-SWTID--2026--3135-green)

## 📌 Project Overview

The **Customer Support Ticket Priority Prediction and Automated Assignment System** is a Salesforce-based solution designed to automate customer support ticket triage.

The system uses a **Salesforce Custom Object**, **Auto-Launched Flow**, and **Agentforce** to analyze the latest support ticket associated with a customer Account, determine its priority as **High, Medium, or Low**, and automatically assign the appropriate support level.

For High-priority tickets, the system creates an **Urgent Ticket Handling** task and routes the ticket to a senior support agent.

The solution provides support users with a conversational way to trigger ticket analysis through Agentforce.

---

## 👥 Team Details

| Detail           | Information                                        |
| ---------------- | -------------------------------------------------- |
| **Team ID**      | `SWTID-2026-3135`                                  |
| **Team Size**    | 3                                                  |
| **Institution**  | St. Joseph’s College of Engineering and Technology |
| **Location**     | Thanjavur                                          |
| **College Code** | 8219                                               |

### 👨‍💻 Team Members

| Role            | Name                   | NMID                               |
| --------------- | ---------------------- | ---------------------------------- |
| **Team Leader** | **Caroline Hansika L** | `EE5AF944F977849BC0A4A2FFC4E39260` |
| **Team Member** | **Sindhuja S**         | `A3F31935BF29E039D9D4E9886B6D1818` |
| **Team Member** | **Preethi S**          | `B1D9E1B2FE56650A8594BCAE726AD349` |

Team information is taken directly from the project documentation.

---

## 🎯 Problem Statement

Customer support teams receive a large number of tickets, making manual prioritization and assignment time-consuming.

Common problems include:

* Manual ticket prioritization
* Critical issues being overlooked
* Delayed assignment to appropriate support agents
* Repetitive ticket analysis
* Difficulty identifying urgency from ticket descriptions
* SLA-related risks

The project addresses these issues through automated ticket analysis, priority classification, task creation, and assignment.

---

## 💡 Proposed Solution

The proposed solution combines **Salesforce CRM, Auto-Launched Flow, and Agentforce**.

### Workflow

```text
Customer / Support User
          │
          ▼
     Account Name
          │
          ▼
      Agentforce
          │
          ▼
 Auto-Launched Flow
          │
          ├── Find Account
          │
          ├── Find Latest Ticket
          │
          ├── Analyze Description
          │
          ▼
    Priority Decision
     ┌────┼────┐
     ▼    ▼    ▼
   HIGH MEDIUM LOW
     │    │    │
     │    │    └── Queue for Processing
     │    └────── Handle Shortly
     │
     ├── Create Urgent Task
     │
     └── Assign Senior Support Agent
          │
          ▼
    Response to User
```

The documented architecture consists of four main layers: **Users, AI, Automation, and Data**.

---

## ✨ Key Features

### 🔹 Automatic Priority Classification

Tickets are classified into:

* 🔴 **High**
* 🟡 **Medium**
* 🟢 **Low**

The current Flow uses configured keywords from the ticket description.

### 🔹 High-Priority Automation

When a ticket is classified as High:

* An urgent task is automatically created.
* The task is named **“Urgent Ticket Handling”**.
* The ticket is assigned to the **Senior Support Agent**.
* An action message is returned to the user.

### 🔹 Agentforce Integration

Support users can provide an **Account Name** to Agentforce.

Agentforce:

1. Retrieves the latest support ticket.
2. Reads the ticket description.
3. Determines its priority.
4. Triggers the Flow.
5. Returns the ticket and assignment information.

### 🔹 SLA Risk Checking

The system includes an optional SLA-risk decision that flags tickets older than two days.

### 🔹 Conversational Support

Users can interact with the system through Agentforce instead of manually navigating through multiple records.

---

## 🧠 Priority Classification Logic

The current implementation uses keyword-based classification.

| Priority      | Trigger Keywords                   | Action                                   |
| ------------- | ---------------------------------- | ---------------------------------------- |
| 🔴 **High**   | `urgent`, `not working`, `failure` | Create urgent task + assign senior agent |
| 🟡 **Medium** | `issue`, `slow`, `delay`           | Handle shortly                           |
| 🟢 **Low**    | No configured priority keywords    | Queue for processing                     |

This classification logic is documented in the Auto-Launched Flow and Agentforce instructions.

---

## 🗃️ Data Model

The main custom Salesforce object is:

```text
Support Ticket Intelligence
API Name: Support_Ticket_Intelligence__c
```

### Fields

| Field           | API Name             | Type             |
| --------------- | -------------------- | ---------------- |
| Ticket Number   | `Ticket_Number__c`   | Auto Number      |
| Customer        | `Customer__c`        | Lookup (Account) |
| Contact         | `Contact__c`         | Lookup (Contact) |
| Issue Type      | `Issue_Type__c`      | Picklist         |
| Description     | `Description__c`     | Long Text Area   |
| Priority Level  | `Priority_Level__c`  | Picklist         |
| Status          | `Status__c`          | Picklist         |
| Created Date    | `Created_Date__c`    | Date             |
| Assigned To     | `Assigned_To__c`     | Lookup (User)    |
| SLA Breach Risk | `SLA_Breach_Risk__c` | Checkbox         |
| Resolution Time | `Resolution_Time__c` | Number           |

The documented Issue Type values are **Technical, Billing, and General**, while Priority Level supports **Low, Medium, and High**.

---

## 🛠️ Technology Stack

| Layer                   | Technology                                          |
| ----------------------- | --------------------------------------------------- |
| CRM Platform            | Salesforce                                          |
| AI                      | Agentforce                                          |
| Automation              | Salesforce Auto-Launched Flow                       |
| Data                    | Salesforce Custom Object                            |
| Records                 | Account, Contact, User, Task                        |
| Agent                   | Support Ticket Priority Analysis                    |
| Development Environment | Salesforce Developer Edition / Trailhead Playground |

The project documentation identifies Salesforce Developer Edition and Trailhead Playground as the development environments.

---

## 🤖 Agentforce Configuration

### Subagent

**Name:** `Support Ticket Priority Analysis`

**API Name:**

```text
Support_Ticket_Priority_Analysis
```

### Responsibilities

The Agentforce subagent:

* Requests the Account Name when required.
* Retrieves the latest associated support ticket.
* Analyzes the ticket description.
* Determines High, Medium, or Low priority.
* Triggers the Auto-Launched Flow for High-priority cases.
* Assigns the appropriate support level.
* Returns a clear action message.

The subagent is intentionally scoped to ticket priority and support prioritization rather than unrelated billing, subscription, or account-update requests.

---

## 🔄 Auto-Launched Flow

### Flow Name

```text
Support Ticket Intelligence
```

### Flow Type

```text
Auto-Launched Flow
```

### Main Flow Steps

1. Get Account
2. Store Account ID
3. Get Latest Support Ticket
4. Store Ticket ID
5. Analyze Description
6. Determine Priority
7. Create Task for High Priority
8. Assign Support Agent
9. Check SLA Risk
10. Generate Final Response

The Flow is designed without a trigger so that Agentforce can invoke it as an action.

---

## 📊 Data Flow

```text
Account Name
     │
     ▼
Agentforce Subagent
     │
     ▼
Auto-Launched Flow
     │
     ▼
Find Account
     │
     ▼
Find Latest Ticket
     │
     ▼
Read Ticket Description
     │
     ▼
Analyze Priority
     │
     ├───────────────┐
     ▼               ▼
High / Medium / Low
     │
     ▼
Assignment & Actions
     │
     ▼
Agentforce Response
```

---

## 🧪 Testing

The system was tested using Agentforce Conversation Preview.

### Test Cases

| Test Case | Input                                                 | Expected Result                     |
| --------- | ----------------------------------------------------- | ----------------------------------- |
| TC-01     | `hi`                                                  | Agent introduces itself             |
| TC-02     | `let me know about TKT-0002`                          | Ticket summary returned             |
| TC-03     | Ticket contains `urgent`, `not working`, or `failure` | High priority + task + senior agent |
| TC-04     | Ticket contains `issue`, `slow`, or `delay`           | Medium priority                     |
| TC-05     | No configured keywords                                | Low priority                        |

The documented test cases verify the Agentforce interaction and Flow priority logic.

---

## 📅 Project Planning

The project followed an **Agile, sprint-based approach**.

### Sprint Structure

| Sprint   | Story Points | Duration |
| -------- | -----------: | -------- |
| Sprint 1 |            3 | 3 days   |
| Sprint 2 |            8 | 3 days   |
| Sprint 3 |           10 | 3 days   |
| Sprint 4 |           13 | 3 days   |
| Sprint 5 |            5 | 3 days   |
| Sprint 6 |            5 | 3 days   |

**Total Story Points:** 44

The project documentation records six sprints and a calculated average velocity of approximately **2.44 points per day**.

---

## 👥 Team Responsibilities

The documented product backlog assigns work across the three team members.

### Caroline Hansika L

* Salesforce environment setup
* Auto-Launched Flow
* Agentforce and automation

### Sindhuja S

* Data modeling
* Priority classification
* SLA management

### Preethi S

* Account/Contact relationships
* Task and assignment
* Conversational support

The responsibilities above are based on the owners listed in the project backlog.

---

## ✅ Advantages

* Automatic ticket prioritization
* Faster identification of critical cases
* Reduced manual triage effort
* Automatic urgent-task creation
* Support-level assignment
* Agentforce conversational access
* SLA-risk awareness
* Scalable Salesforce automation
* Reduced repetitive support work

---

## ⚠️ Current Limitations

The current implementation has several documented limitations:

* Keyword-based priority detection
* Limited understanding of contextual urgency
* Dependency on accurate Account, Contact, and ticket data
* Flow and Agentforce configuration requires maintenance
* Billing and subscription requests are outside the agent's scope
* SLA monitoring is currently limited
* Assignment rules need expansion for additional teams
* Advanced analytics are not currently implemented

---

## 🚀 Future Scope

Planned improvements include:

* Add additional priority indicators and business rules
* Return more ticket information through Agentforce
* Implement comprehensive SLA monitoring
* Add escalation mechanisms
* Support additional teams and assignment rules
* Add analytics for priority trends
* Analyze resolution performance
* Add additional Flow variables for richer Agentforce responses

---

## 📁 Suggested Repository Structure

```text
Customer-Support-Ticket-Priority/
│
├── README.md
│
├── documentation/
│   └── Customer_Support_Ticket_Priority_Documentation.pdf
│
├── salesforce/
│   ├── objects/
│   ├── flows/
│   ├── agentforce/
│   └── screenshots/
│
└── assets/
    └── project-images/
```

> **Note:** The exact Salesforce metadata folder structure can be adjusted depending on how the Salesforce configuration is exported and maintained.

---

## 🎓 Institution

**St. Joseph’s College of Engineering and Technology**
Thanjavur, Tamil Nadu, India

**College Code:** `8219`

**Team ID:** `SWTID-2026-3135`

---

## 📜 Conclusion...


The **Customer Support Ticket Priority Prediction and Automated Assignment System** demonstrates how Salesforce Flow and Agentforce can automate customer-support ticket triage.

By providing an Account Name, the system retrieves the latest ticket, analyzes its description, determines its priority, creates an urgent task for High-priority cases, assigns an appropriate support level, and provides a conversational response.

The project demonstrates the integration of **CRM data, workflow automation, and AI-assisted interaction** within Salesforce.

---

## 👨‍💻 Team

**Team ID:** `SWTID-2026-3135`

**Team Leader:** Caroline Hansika L
**Team Members:** Sindhuja S, Preethi S

**St. Joseph’s College of Engineering and Technology, Thanjavur**

---

### ⭐ Project Status

```text
Project Type : Salesforce + Agentforce
Status       : Completed / Prototype
Team ID      : SWTID-2026-3135
Team Size    : 3
```

---

## 📄 Documentation

The complete project documentation is included in this repository as:

```text
Customer_Support_Ticket_Priority_Documentation.pdf
```

For the complete implementation details, Flow configuration, Agentforce configuration, testing evidence, and project planning, refer to the project documentation.
