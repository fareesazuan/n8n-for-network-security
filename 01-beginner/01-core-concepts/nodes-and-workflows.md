# Module 3: Nodes and Workflows

## 🎯 What You'll Learn (1 hour)

- What are nodes and how they work
- Core node types: Trigger, Action, Logic
- Connecting nodes and data mapping
- Workflow execution rules
- Reading and modifying workflow JSON

---

## 🔧 What are Nodes?

### Definition

A **node** is a single reusable component that performs one task:

```
Node = Single Task
├─ Receives input data
├─ Processes or transforms it
├─ Outputs result
└─ Passes to next node
```

### Node Anatomy

```
┌────────────────────────────────────────┐
│          HTTP Request Node             │
├────────────────────────────────────────┤
│                                        │
│  INPUT HANDLE (top)                    │
│    ↑ (receives data from previous)     │
│    │                                   │
│  ┌──────────────────────────────────┐  │
│  │  Node Configuration Panel        │  │
│  │  ├─ Method: GET                  │  │
│  │  ├─ URL: https://api.github.com  │  │
│  │  └─ Headers: {...}               │  │
│  └──────────────────────────────────┘  │
│    │                                   │
│    ↓ (sends data to next)              │
│  OUTPUT HANDLE (bottom)                │
│                                        │
└────────────────────────────────────────┘
```

### Node Properties

| Property | Meaning | Example |
|----------|---------|---------|
| **Name** | Display name | "Query SIEM" |
| **Type** | Category of task | "HTTP Request" |
| **Configuration** | Node-specific settings | URL, method, auth |
| **Input** | Data from previous node | JSON from trigger |
| **Output** | Data to next node | API response |

---

## 🎯 Core Node Types

### Type 1: Trigger Nodes (Start Workflows)

**Purpose:** Start the workflow execution

**Examples:**
```
Manual Trigger      - Click Execute button
Webhook            - External system sends HTTP request
Schedule/Cron      - Run at specific times
Interval           - Run every X minutes
On App Event       - n8n app events
```

**Characteristics:**
- ✅ No input (starts the workflow)
- ✅ Always green entry point
- ✅ Produces initial data for workflow
- ❌ Only ONE trigger per workflow

**Trigger Node Anatomy:**
```
┌─────────────────────────┐
│  Manual Trigger         │
├─────────────────────────┤
│                         │
│  ☰ Manual Trigger       │
│                         │
│  (No input connection)  │
│         ↓               │
│    [Execute]            │
│         ↓               │
│   OUTPUT HANDLE         │
│   { "success": true }   │
│                         │
└─────────────────────────┘
```

**Real Security Example:**
```
Trigger: Webhook (receives SIEM alert)
Input: 
{
  "alert_id": "SIEM-12345",
  "severity": "HIGH",
  "source_ip": "192.168.1.100"
}
Output: Same data passed to next node
```

### Type 2: Action Nodes (Do Things)

**Purpose:** Perform actions (API calls, send messages, store data, etc.)

**Examples:**
```
HTTP Request        - Call any API
Send Email          - Send email via SMTP
Slack               - Send Slack message
Webhook             - Send HTTP POST to external system
SQL Database        - Query or update database
File System         - Read/write files
Wait                - Pause workflow for duration
```

**Characteristics:**
- ✅ Requires input (from previous node)
- ✅ Performs real action
- ✅ Returns results as output
- ✅ Usually requires configuration

**Action Node Anatomy:**
```
┌────────────────────────────────┐
│  HTTP Request                  │
├────────────────────────────────┤
│                                │
│   INPUT HANDLE (from trigger)  │
│         ↑                       │
│    [GET request]               │
│    URL: api.example.com/...    │
│    Auth: API Key xyz...        │
│         ↓                       │
│   OUTPUT HANDLE                │
│   { "status": 200, "data": {} }│
│                                │
└────────────────────────────────┘
```

**Real Security Example:**
```
Action: HTTP Request (Block IP on Firewall)
Input: { "source_ip": "192.168.1.100" }
Configuration:
  Method: POST
  URL: https://firewall.internal/api/block
  Body: { "ip": "192.168.1.100" }
Output: { "status": "success", "blocked_ip": "192.168.1.100" }
```

### Type 3: Logic Nodes (Make Decisions)

**Purpose:** Control workflow flow based on conditions

**Examples:**
```
If / Then            - Conditional routing
Switch               - Multiple conditions
Function             - Custom logic
Code                 - JavaScript code execution
Merge                - Combine multiple flows
Split                - Duplicate data
```

**Characteristics:**
- ✅ Takes input and evaluates
- ✅ Routes to different paths
- ✅ Doesn't modify external systems
- ✅ Controls workflow logic

**Logic Node Anatomy:**
```
┌─────────────────────────────┐
│  If / Then                  │
├─────────────────────────────┤
│                             │
│   INPUT HANDLE              │
│         ↑                   │
│   Condition:                │
│   IF severity == "HIGH"     │
│         ↓                   │
│   ┌──TRUE──┬──FALSE──┐     │
│   ↓        ↓                │
│ [Route A] [Route B]        │
│   ↓        ↓                │
│  OUTPUT HANDLES             │
│                             │
└─────────────────────────────┘
```

**Real Security Example:**
```
Logic: If / Then (Threat Check)
Input: { "severity": "HIGH", "source_ip": "..." }
Condition: IF severity == "HIGH"
  TRUE → Route to "Immediate Response" (block IP)
  FALSE → Route to "Log Only" (continue monitoring)
```

---

## 🔗 Connecting Nodes and Data Mapping

### Creating Connections

**Visual Connection:**
```
┌──────────┐        ┌──────────┐
│  Node 1  │        │  Node 2  │
│          │        │          │
│ OUTPUT ●─────────→ INPUT    │
└──────────┘        └──────────┘
  (blue circle)      (blue circle)
```

**How to Connect:**
1. Click output circle (●) on Node 1
2. Drag to input circle (●) on Node 2
3. Release to connect

### Data Mapping (Passing Variables)

**Concept:** Map output fields from previous node to input fields of next node

**Example Scenario:**
```
Node 1 Output (SIEM Alert):
{
  "alert_id": "ALR-123",
  "severity": "HIGH",
  "source_ip": "192.168.1.100"
}

Node 2 Input (HTTP Request to Firewall):
{
  "ip_to_block": ???         ← Where does this come from?
}
```

**Solution - Data Mapping:**
```
In Node 2 configuration:
Field: "ip_to_block"
Map from: Node 1 → source_ip

Result:
{
  "ip_to_block": "192.168.1.100"  ← Automatically filled!
}
```

### Data Mapping in n8n UI

```
When editing a field in Node 2:
┌─────────────────────────────────────┐
│ Field: "ip_to_block"                │
├─────────────────────────────────────┤
│ [Type: Text or Expression]          │
│                                     │
│ Choose "Expression" mode:           │
│ >> Click "{ }" icon                 │
│                                     │
│ Then type:                          │
│ {{ $node["Node 1"].json.source_ip}}│
│                                     │
│ n8n autocompletes available fields! │
└─────────────────────────────────────┘
```

### Common Data Mapping Patterns

#### Pattern 1: Simple Field Mapping

```
Expression: {{ $node["HTTP Request"].json.login }}

From previous node:
{ "login": "alice", "id": 123 }

Result: "alice"
```

#### Pattern 2: Array Iteration

```
Expression: {{ $node["Query API"].json.results[0].name }}

From previous node:
{ "results": [ {"name": "Alice"}, {"name": "Bob"} ] }

Result: "Alice" (first item)
```

#### Pattern 3: String Interpolation

```
Expression: User {{ $node["LDAP"].json.username }} created

Result: "User alice created"
```

#### Pattern 4: Conditional Mapping

```
Expression: 
{{ $node["SIEM"].json.severity === "HIGH" ? "URGENT" : "NORMAL" }}

If severity is HIGH → "URGENT"
If severity is not HIGH → "NORMAL"
```

---

## ⚙️ Workflow Execution Rules

### Rule 1: Sequential Execution

```
Workflows execute TOP to BOTTOM through connections:

Node 1
  ↓ (only starts when connection fires)
Node 2
  ↓ (only starts when Node 2 completes)
Node 3
  ↓
Node 4
```

**Rule:** A node only starts executing when:
1. Previous node completes successfully
2. Connection is established
3. Input data is available

### Rule 2: Data Flows Forward

```
Node 1 Output → Node 2 Input
Node 2 Output → Node 3 Input
(Cannot go backwards)
```

**Rule:** Data only flows in the direction of connections

### Rule 3: One Execution at a Time (per workflow)

```
Execution 1 completes
    ↓
Execution 2 starts
(Cannot overlap)
```

**Exception:** Multiple instances can run in parallel (different servers)

### Rule 4: Error Stops Workflow (by default)

```
Node 1: ✓ Success
Node 2: ✗ Error
Node 3: Not executed (stopped)
Node 4: Not executed (stopped)
```

**Exception:** Use error handlers to continue on error

### Rule 5: No Loops (by design)

```
NOT ALLOWED:
Node 1 → Node 2 → Node 1 (creates infinite loop)

WORKAROUND:
Use Schedule trigger to re-run periodically
Or use Split nodes with parallel execution
```

---

## 📄 Reading and Modifying Workflow JSON

### Understanding Workflow JSON

Each n8n workflow is stored as JSON:

**Simple Example:**
```json
{
  "name": "Alert Response",
  "active": true,
  "nodes": [
    {
      "id": "trigger",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "id": "http",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.7,
      "position": [450, 300],
      "parameters": {
        "method": "GET",
        "url": "https://api.example.com/check"
      }
    }
  ],
  "connections": {
    "trigger": {
      "main": [[
        { "node": "http", "type": "main", "index": 0 }
      ]]
    }
  }
}
```

### Workflow JSON Structure

```
{
  "name": "Workflow Name",
  "active": true/false,
  
  "nodes": [
    {
      "id": "node_identifier",
      "type": "n8n-nodes-base.nodeType",
      "typeVersion": 1,
      "position": [x, y],
      "parameters": { /* node configuration */ }
    }
  ],
  
  "connections": {
    "source_node": {
      "main": [[
        { "node": "target_node", "type": "main", "index": 0 }
      ]]
    }
  }
}
```

### Finding Node IDs

```
In n8n UI:
1. Click on node
2. Top left shows: "Node name"
3. In JSON: "id": matches this

Finding connections:
1. Look at visual connections in UI
2. In JSON: "connections" section shows links
```

### Exporting Workflow JSON

**In n8n UI:**
1. Click workflow name (top)
2. Click ⋮ (menu)
3. Click "Download"
4. Saves as `workflow.json`

### Importing Workflow JSON

**In n8n UI:**
1. Click "New Workflow"
2. Click ⋮ (menu)
3. Click "Import from JSON"
4. Select file or paste JSON

---

## 🎬 Hands-On Task 1: Build Multi-Step Workflow

### Objective
Create a workflow that uses Trigger → Action → Logic → Action

### Steps

#### Step 1: Create New Workflow

1. Click "New Workflow"
2. Name: **"Multi-Step Demo"**

#### Step 2: Add Manual Trigger

1. Click "+" to add node
2. Search: **"Manual Trigger"**
3. Position it on canvas

#### Step 3: Add HTTP Request (Get User Data)

1. Click "+" to add node
2. Search: **"HTTP Request"**
3. Click to add
4. Connect to Manual Trigger

Configure:
```
Method: GET
URL: https://randomuser.me/api/
```

#### Step 4: Add If/Then Logic

1. Add **"If"** node
2. Connect to HTTP Request
3. Configure condition:
   ```
   Condition: gender == "male"
   ```

#### Step 5: Add Action for True Branch

1. Add **"Code"** node
2. Connect from If node (TRUE path)
3. Add JavaScript:
   ```javascript
   return {
     name: items[0].json.results[0].name.first,
     gender: "M",
     status: "processed"
   };
   ```

#### Step 6: Execute

1. Click **"Execute"** button
2. Watch execution flow
3. Check node states (GREEN/YELLOW)
4. Inspect debug panel output

#### Step 7: Save

1. Click "Save"
2. Note: Workflow is saved locally

---

## 🎬 Hands-On Task 2: Export and Inspect JSON

### Objective
Export workflow and understand JSON structure

### Steps

#### Step 1: Export Workflow

1. Click workflow name (top)
2. Click ⋮ (three dots)
3. Click "Download"
4. Save file as `multi-step-demo.json`

#### Step 2: Open JSON File

1. Open in text editor (VS Code recommended)
2. Format JSON nicely (most editors auto-format)
3. Look for key sections:
   ```
   - "name": your workflow name
   - "nodes": array of all nodes
   - "connections": how nodes link
   ```

#### Step 3: Identify Nodes

In the JSON, find:
```json
"nodes": [
  {
    "id": "Manual Trigger",      ← This is Node 1
    "type": "n8n-nodes-base.manualTrigger"
  },
  {
    "id": "HTTP Request",        ← This is Node 2
    "type": "n8n-nodes-base.httpRequest"
  }
]
```

#### Step 4: Find Connections

Look for:
```json
"connections": {
  "Manual Trigger": {
    "main": [[
      { "node": "HTTP Request", ... }  ← Connection to Node 2
    ]]
  },
  "HTTP Request": {
    "main": [[
      { "node": "If", ... }  ← Connection to If node
    ]]
  }
}
```

#### Step 5: Document

Write notes on:
- [ ] How many nodes in workflow?
- [ ] What is first node ID?
- [ ] What is the connection pattern?
- [ ] Find the HTTP Request URL in parameters

---

## ✅ Summary

### Node Types

✅ **Trigger:** Start workflows (Manual, Webhook, Schedule)  
✅ **Action:** Do things (HTTP, Email, Slack, Database)  
✅ **Logic:** Make decisions (If/Then, Switch, Code)  

### Connections

✅ **Data mapping:** Connect previous node outputs to next node inputs  
✅ **Sequential flow:** Top to bottom through connections  
✅ **JSON structure:** Nodes and connections stored as JSON  

### Key Takeaway

> **Workflows are built by connecting nodes.**  
> **Each node type performs a specific task.**  
> **Data flows from one node to the next.**

---

## 🚀 Next Steps

1. ✅ Complete both hands-on tasks
2. ✅ Export and review workflow JSON
3. ⬜ Move to **Module 4: Hello World Workflow**

---

**Module Author:** Network Security Learning Team  
**Last Updated:** December 2025  
**License:** MIT
