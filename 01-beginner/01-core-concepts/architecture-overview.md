# Module 2: Architecture Overview

## 🎯 What You'll Learn (45 minutes)

- How n8n executes workflows internally
- Different execution models (triggers vs manual)
- Data flow through workflows
- Node lifecycle and states
- Error handling fundamentals

---

## 🏗️ n8n Architecture Fundamentals

### The Big Picture: Execution Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    n8n Workflow Execution                   │
└─────────────────────────────────────────────────────────────┘

1. TRIGGER EVENT
   └─→ Something starts the workflow
       (webhook, schedule, manual click, etc.)

2. WORKFLOW EXECUTION STARTS
   └─→ n8n creates execution context
       (isolated environment)

3. NODES EXECUTE IN SEQUENCE
   └─→ Each node processes data:
       Input → Process → Output

4. DATA FLOWS FORWARD
   └─→ Each node's output becomes next node's input

5. EXECUTION COMPLETES
   └─→ Last node outputs result
       (success or error)

6. LOGGING & PERSISTENCE
   └─→ Execution recorded in database
       (for auditing and debugging)
```

### Key Principle: Data Pipeline

n8n workflows are **data pipelines**:

```
Node 1          Node 2          Node 3
┌──────┐        ┌──────┐        ┌──────┐
│ Data │ ──→ │ Data │ ──→ │ Data │
│Input │  Transform  │ Transform  │Output│
└──────┘        └──────┘        └──────┘
   ↓               ↓               ↓
 {id:1}         {id:1,           {id:1,
  name:         name:            name:
  "Alice"}      "Alice",         "Alice",
               status:          status:
               "active"}        "active",
                               email:
                              "..."}
```

**Important:** Each node receives data from previous node and passes it to the next.

---

## 🎯 Execution Models

### Model 1: Manual Execution

**How:** Click the "Execute" button in n8n

```
Developer/Admin
       ↓
[Execute Button Click]
       ↓
Workflow starts immediately
       ↓
Runs once, completes
```

**Use Cases:**
- Testing workflows
- One-time jobs
- Debugging

**Security Example:**
```
Manual: "Run compliance audit now"
→ Admin clicks Execute
→ n8n connects to systems
→ Generates report
→ Saves to database
```

### Model 2: Webhook Trigger (Event-Driven)

**How:** External system sends data to n8n via HTTP

```
External System (Alert, Event, Data)
       ↓
HTTP POST to n8n Webhook URL
       ↓
n8n receives webhook payload
       ↓
Workflow executes immediately with webhook data
       ↓
Response sent back to caller
```

**Flow Diagram:**
```
┌──────────────────┐
│  SIEM System     │
│  Detects Alert   │
└────────┬─────────┘
         │
         │ POST /webhook/siem-alert
         │ Content: {alert_id, severity, ...}
         ↓
┌──────────────────────────┐
│    n8n Webhook Node      │
│  (Listens on port 5678)  │
└────────┬─────────────────┘
         │
         │ Trigger fires
         │ (workflow starts)
         ↓
    [Workflow Executes]
         ↓
┌──────────────────────────┐
│  Response Sent Back      │
│  HTTP 200 OK             │
└──────────────────────────┘
```

**Use Cases:**
- Real-time alerts
- Incident response
- Event-driven automation

**Security Example:**
```
Real-Time Threat Response:
SIEM Alert → Webhook → n8n executes → Block IP → Done (2 sec)
```

### Model 3: Scheduled/Cron Trigger

**How:** Workflow runs on a schedule (hourly, daily, weekly, etc.)

```
Scheduler (cron job)
    ↓
[Time Matches Schedule]
    ↓
Workflow executes automatically
    ↓
No input data (or default data)
    ↓
Continues to next node
```

**Example Timing:**
```
Daily at 2 AM:
- Run compliance audit
- Generate reports
- Check for new vulnerabilities

Every Hour:
- Monitor system health
- Check for policy violations

Every 5 minutes:
- Poll API for new data
```

**Use Cases:**
- Reports generation
- Periodic checks
- Batch processing

**Security Example:**
```
Nightly Compliance Report:
Schedule: Every day at 2 AM
    ↓
Query all security logs
    ↓
Analyze for violations
    ↓
Generate report PDF
    ↓
Email to management
```

### Model 4: External Trigger (Polling)

**How:** n8n checks external system regularly for changes

```
n8n Timer (every 5 min)
    ↓
[Check]
    ↓
Call external API: "Any new data?"
    ↓
If YES: Execute workflow with data
If NO: Wait for next check
```

**Use Cases:**
- Monitoring APIs without webhooks
- Legacy systems
- Systems that don't support webhooks

---

## 🔄 Data Flow Through Workflows

### Understanding the Data Pipeline

**Real Example: Security Alert Processing**

```
┌─────────────────────────────────────────────────────────────┐
│                    Workflow: Process Security Alert          │
└─────────────────────────────────────────────────────────────┘

INPUT: Webhook triggers with this data:
{
  "alert_id": "ALR-12345",
  "severity": "HIGH",
  "source_ip": "192.168.1.100",
  "target_system": "Exchange-Server",
  "timestamp": "2025-12-17T15:30:00Z"
}

                        ↓ PASSES TO NODE 1

┌───────────────────────────────────┐
│ Node 1: Webhook (Trigger)         │
│ Input: Raw HTTP POST data         │
│ Output: Parsed JSON               │
└──────────────────┬────────────────┘
                   │
                   ↓ PASSES TO NODE 2

┌──────────────────────────────────────────┐
│ Node 2: Query Threat Intelligence        │
│ Input: {alert_id, severity, source_ip}  │
│ Action: Query threat intel API           │
│ Output: {ip_reputation: "malicious",     │
│          confidence: 95,                 │
│          threat_type: "botnet"}          │
└──────────────────┬───────────────────────┘
                   │
                   ↓ PASSES TO NODE 3

┌──────────────────────────────────────────┐
│ Node 3: Decision (If/Then)               │
│ Input: Previous node output              │
│ Logic: Is ip_reputation == "malicious"?  │
│ YES → Route to Node 4                    │
│ NO  → Skip to Node 6                     │
└──────────────────┬───────────────────────┘
                   │
        ┌──────────┴──────────┐
        ↓                     ↓
    MALICIOUS            CLEAN
        │                   │
        ↓                   ↓
   ┌─────────────┐     ┌──────────────┐
   │ Node 4:     │     │ Node 6:      │
   │ Block IP    │     │ Log Event    │
   │ on Firewall │     │ Store Report │
   └────┬────────┘     └──────┬───────┘
        │                     │
        ↓                     ↓
   ┌─────────────┐     ┌──────────────┐
   │ Node 5:     │     │ Node 7:      │
   │ Send Alert  │     │ Complete     │
   │ to SOC      │     │              │
   └────┬────────┘     └──────┬───────┘
        │                     │
        └──────────┬──────────┘
                   ↓
            EXECUTION COMPLETE
            Result saved in database
```

### Key Data Flow Rules

```
Rule 1: Sequential Execution
────────────────────────────
Nodes execute TOP to BOTTOM in connection order
You control the sequence by connecting nodes

Rule 2: Data Transformation
──────────────────────────
Each node can:
  - Accept input from previous node
  - Transform/process the data
  - Pass output to next node
  - Add new fields to data

Rule 3: Branching
───────────────
Use "If" nodes to:
  - Take different paths based on conditions
  - Skip certain nodes
  - Run parallel branches

Rule 4: Data Isolation
─────────────────────
Each workflow execution is isolated:
  - Separate memory space
  - No interference between executions
  - Variables don't persist between runs
```

---

## 🔄 Node Lifecycle and States

### Node States During Execution

```
┌─────────────────────────────────────────┐
│           Node Lifecycle                │
└─────────────────────────────────────────┘

   IDLE (waiting to execute)
      ↓
   EXECUTING (processing)
      ↓
   ┌─────────────┬──────────────────┐
   ↓             ↓
SUCCESS      ERROR/FAILURE
   │             │
   ├─ Output sent to next node
   │
   └─ Workflow continues or stops
      depending on error handling
```

### Node States in UI

```
┌──────────────────────────────────┐
│  Node Visual States in n8n UI    │
├──────────────────────────────────┤
│                                  │
│  🟢 GREEN: Executed successfully │
│  🔴 RED: Error occurred          │
│  🟡 YELLOW: Executing...         │
│  ⚪ GREY: Not yet executed       │
│  ⏸️  Blue: Disabled              │
│                                  │
└──────────────────────────────────┘
```

### Example: Node States During Execution

```
Workflow: "Process Alert"

Initial State:
┌─────────────┐  ┌──────────┐  ┌──────────┐
│   Webhook   │  │  Query   │  │  Block   │
│   (Grey)    │  │   API    │  │   IP     │
│             │  │  (Grey)  │  │  (Grey)  │
└─────────────┘  └──────────┘  └──────────┘

Step 1: Webhook fires
┌─────────────┐  ┌──────────┐  ┌──────────┐
│   Webhook   │  │  Query   │  │  Block   │
│  (GREEN)    │  │   API    │  │   IP     │
│ ✓Done       │  │  (Grey)  │  │  (Grey)  │
└─────────────┘  └──────────┘  └──────────┘

Step 2: Query API executing
┌─────────────┐  ┌──────────┐  ┌──────────┐
│   Webhook   │  │  Query   │  │  Block   │
│  (GREEN)    │  │   API    │  │   IP     │
│ ✓Done       │  │ (YELLOW) │  │  (Grey)  │
│             │  │ ⏳Loading│  │          │
└─────────────┘  └──────────┘  └──────────┘

Step 3: All complete
┌─────────────┐  ┌──────────┐  ┌──────────┐
│   Webhook   │  │  Query   │  │  Block   │
│  (GREEN)    │  │   API    │  │   IP     │
│ ✓Done       │  │  (GREEN) │  │  (GREEN) │
│             │  │ ✓Done    │  │ ✓Done    │
└─────────────┘  └──────────┘  └──────────┘
```

---

## ⚠️ Error Handling Fundamentals

### Error Types

```
1. CONNECTION ERRORS
   Problem: Can't reach external API
   Example: "Connection timeout to firewall"
   Fix: Retry, fallback, alert

2. DATA VALIDATION ERRORS
   Problem: Data format wrong
   Example: "Invalid JSON in webhook payload"
   Fix: Validate input, transform, alert

3. AUTHENTICATION ERRORS
   Problem: API key expired or invalid
   Example: "401 Unauthorized from SIEM API"
   Fix: Refresh credentials, alert

4. BUSINESS LOGIC ERRORS
   Problem: Condition fails or data missing
   Example: "IP address not found in threat intel"
   Fix: Handle gracefully, log, continue

5. WORKFLOW ERRORS
   Problem: Node configuration wrong
   Example: "Required field not mapped"
   Fix: Verify node configuration
```

### Error Handling Strategies

#### Strategy 1: Continue on Error

```
Node Setup:
  Click Node → "On Error" → "Continue"

Result:
  If error: Skip this node, continue to next
  Use: Non-critical actions

Example:
  Optional enrichment fails?
  → Continue with alert anyway
```

#### Strategy 2: Stop on Error

```
Node Setup:
  Click Node → "On Error" → "Stop Workflow"

Result:
  If error: Halt entire workflow
  Use: Critical operations

Example:
  Can't block IP on firewall?
  → Stop, alert admin, don't proceed
```

#### Strategy 3: Use Error Handling Node

```
┌─────────────────────────────────────┐
│ Main Node (might fail)              │
└────────┬──────────────┬─────────────┘
         │              │
         ↓              ↓
     SUCCESS         ERROR
         │              │
         ↓              ↓
    [Node 2]    [Error Handler]
                  (retry, alert, log)
```

---

## 🎬 Hands-On Task 1: Simple 3-Node Workflow

### Objective
Build a workflow that demonstrates data flow and node execution

### Steps

#### Step 1: Create New Workflow

1. Open n8n
2. Click **"New Workflow"**
3. Name it: **"Data Flow Demo"**

#### Step 2: Add Trigger Node

1. Click on the canvas (center)
2. Click "+" button to add a node
3. Search: **"Manual Trigger"**
4. Click to add it

**Node 1 Result:**
```
Node: Manual Trigger
Purpose: Start workflow manually (for testing)
Output: { "message": "trigger" }
```

#### Step 3: Add HTTP Request Node

1. Click "+" to add another node
2. Search: **"HTTP Request"**
3. Click to add it
4. Connect it to Manual Trigger node:
   - Drag circle from Manual Trigger → to HTTP Request

**Node 2 Configuration:**
```
HTTP Request Settings:
- Method: GET
- URL: https://api.github.com/users/github
- Leave other settings default
```

#### Step 4: Add Code Node (Transform Data)

1. Click "+" to add another node
2. Search: **"Code"**
3. Click to add it
4. Connect to HTTP Request

**Node 3 Configuration:**
```
Code Node:
  Add this JavaScript code:
  
  return {
    username: items[0].json.login,
    followers: items[0].json.followers,
    profile_url: items[0].json.html_url,
    timestamp: new Date().toISOString()
  };
```

#### Step 5: Execute and Observe

1. Click green **"Execute"** button (top right)
2. Watch nodes execute:
   - Manual Trigger turns GREEN ✓
   - HTTP Request turns YELLOW (loading)
   - HTTP Request turns GREEN ✓
   - Code node turns YELLOW
   - Code node turns GREEN ✓

3. Look at the **Debug Panel** (bottom):
   - Click each node to see its output
   - Trace data flowing through workflow

#### Step 6: Examine Data Flow

In Debug Panel:
```
Manual Trigger Output:
{ "message": "trigger" }
    ↓ (passed to next node)
HTTP Request Output:
{ "login": "github", "followers": 1234, ... }
    ↓ (passed to next node)
Code Node Output:
{
  "username": "github",
  "followers": 1234,
  "profile_url": "https://github.com/github",
  "timestamp": "2025-12-17T15:30:00Z"
}
```

#### Step 7: Save Workflow

1. Click **"Save"** (top right)
2. Keep name: **"Data Flow Demo"**

---

## 🎬 Hands-On Task 2: Node States Observation

### Objective
Understand node states by watching execution

### Steps

#### Step 1: Create "Error Handling Demo" Workflow

1. Click "New Workflow"
2. Name: **"Error Handling Demo"**

#### Step 2: Add Trigger

- Add **Manual Trigger** node

#### Step 3: Add HTTP Request That Will Fail

1. Add **HTTP Request** node
2. Connect to Manual Trigger
3. Configure:
   ```
   Method: GET
   URL: https://httpbin.org/status/500
   (This will return an error)
   ```

#### Step 4: Add Decision Node After

1. Add **If/Then** node
2. Connect to HTTP Request
3. Don't configure it yet

#### Step 5: Execute and Watch States

1. Click Execute
2. Watch what happens:
   - Manual Trigger: GREEN ✓
   - HTTP Request: RED ✗ (error!)
   - If/Then: GREY (not executed, because error occurred)

#### Step 6: Add Error Handler

1. Right-click HTTP Request node
2. Select "On Error"
3. Choose "Continue"

#### Step 7: Re-execute

1. Click Execute
2. Now HTTP Request shows error but:
   - If/Then node: YELLOW (executing now!)
   - If/Then node: GREEN (executed despite error)

**Key Learning:** With error handling, workflow continues!

---

## ✅ Summary

### Architecture Principles

✅ **Sequential Execution:** Nodes run top to bottom  
✅ **Data Pipeline:** Each node transforms data  
✅ **Multiple Triggers:** Manual, webhook, scheduled  
✅ **Error Handling:** Strategies to handle failures  
✅ **Node States:** Visual feedback during execution  

### Key Takeaway

> **n8n workflows are data pipelines.**  
> **Data flows from one node to the next,**  
> **transforming at each step.**

---

## 🚀 Next Steps

1. ✅ Complete both hands-on tasks
2. ✅ Save screenshots of node states
3. ⬜ Move to **Module 3: Nodes and Workflows**

---

**Module Author:** Network Security Learning Team  
**Last Updated:** December 2025  
**License:** MIT
