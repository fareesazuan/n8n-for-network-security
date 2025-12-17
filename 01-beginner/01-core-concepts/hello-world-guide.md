# Module 4: Hello World Workflow

## 🎯 What You'll Learn (30 minutes)

- Building your first complete workflow
- Testing and debugging workflows
- Understanding workflow execution monitoring
- Best practices for workflow design

---

## 📖 Your First Workflow: "Hello Security World"

### Workflow Overview

```
Purpose: Query threat intelligence and log results
Security Use Case: Check if an IP is malicious

Flow:
1. Start (Manual trigger)
2. Get sample IP address
3. Query threat intelligence API
4. Check if malicious
5. Log result

Estimated Execution Time: 2-3 seconds
```

### What We'll Build

```
┌────────────────────────────────────────────────┐
│         Hello Security World Workflow           │
└────────────────────────────────────────────────┘

[1. Manual Trigger]
       ↓
[2. Set IP Address (Code)]
       ↓
[3. Query Threat Intel (HTTP)]
       ↓
[4. Check Result (If)]
       ├─→ [5a. Format Result - Malicious]
       └─→ [5b. Format Result - Clean]
       ↓
[6. Log Output]
```

---

## 🔨 Step-by-Step: Build the Workflow

### Step 1: Create New Workflow

1. Open n8n dashboard
2. Click **"New Workflow"** button
3. Name: **"Hello Security World"**
4. Click "Save"

### Step 2: Add Manual Trigger

**Purpose:** Starts the workflow (for testing)

1. Click "+" button on canvas
2. Search: **"Manual"**
3. Select **"Manual Trigger"**
4. Click to add

**Node is now on canvas!**

### Step 3: Add Code Node (Set IP)

**Purpose:** Create a sample IP address to check

1. Click "+" to add another node
2. Search: **"Code"**
3. Select **"Code (JavaScript)"**
4. Connect to Manual Trigger (drag from output → input)

**Configure the Code Node:**

Click on the Code node to edit:

```javascript
// Set a sample IP to check against threat intelligence
return {
  ip_to_check: "192.168.1.100",
  timestamp: new Date().toISOString(),
  workflow: "Hello Security World"
};
```

**What this does:**
- Creates a sample IP address
- Adds timestamp
- Adds workflow name as metadata
- Outputs this data to next node

### Step 4: Add HTTP Request (Query Threat Intel)

**Purpose:** Call a real threat intelligence API

1. Click "+" to add node
2. Search: **"HTTP"**
3. Select **"HTTP Request"**
4. Connect to Code node

**Configure HTTP Request:**

```
Method: POST
URL: https://jsonplaceholder.typicode.com/posts

Body:
{
  "title": "IP Check: {{ $node["Set IP"].json.ip_to_check }}",
  "body": "Checking threat intelligence at {{ $node["Set IP"].json.timestamp }}",
  "userId": 1
}
```

**Note:** We use a fake API for testing. In production, use:
- AbuseIPDB API
- VirusTotal API
- AlienVault OTX
- Other threat intel services

### Step 5: Add If/Then Node (Check if Malicious)

**Purpose:** Make a decision based on API response

1. Click "+" to add node
2. Search: **"If"**
3. Select **"If"**
4. Connect to HTTP Request

**Configure the If Condition:**

```
Condition: Condition 1

Field: {{ $node["HTTP Request"].json.id }}
Operator: Greater than or equal to
Value: 1

(This means: if API returned an ID >= 1, consider it valid)
```

**What this creates:**
```
IF condition true  → goes to TRUE branch
IF condition false → goes to FALSE branch
```

### Step 6a: Add Code Node (True Branch - Malicious)

**Purpose:** Format result if threat detected

1. Click "+" to add node
2. Search: **"Code"**
3. Select **"Code"**
4. Connect from If node TRUE output

**Configure:**

```javascript
// IP is considered suspicious (in real workflow)
return {
  ip: "{{ $node['Set IP'].json.ip_to_check }}",
  status: "SUSPICIOUS",
  severity: "HIGH",
  action_required: true,
  recommended_action: "Block IP on firewall",
  threat_level: "HIGH"
};
```

### Step 6b: Add Code Node (False Branch - Clean)

**Purpose:** Format result if IP is clean

1. Click "+" to add node
2. Search: **"Code"**
3. Select **"Code"**
4. Connect from If node FALSE output

**Configure:**

```javascript
// IP is clean
return {
  ip: "{{ $node['Set IP'].json.ip_to_check }}",
  status: "CLEAN",
  severity: "LOW",
  action_required: false,
  recommended_action: "No action needed",
  threat_level: "LOW"
};
```

### Step 7: Test Execution

**Execute the workflow:**

1. Click green **"Execute"** button (top right)
2. Watch nodes execute:
   - Manual Trigger → GREEN ✓
   - Set IP (Code) → GREEN ✓
   - Query Threat Intel (HTTP) → YELLOW ⏳ → GREEN ✓
   - Check Result (If) → GREEN ✓
   - Format Result → GREEN ✓

### Step 8: Review Results

**In Debug Panel (bottom):**

1. Click **"Manual Trigger"** node
   - Output: `{ "success": true }`

2. Click **"Set IP"** node
   - Output: `{ "ip_to_check": "192.168.1.100", ... }`

3. Click **"Query Threat Intel"** node
   - Output: `{ "id": 1, "title": "...", ... }`

4. Click **"Check Result"** node
   - Output: Shows which branch was taken (TRUE or FALSE)

5. Click **"Format Result"** node
   - Output: Final structured result
   - Example: `{ "status": "CLEAN", "ip": "192.168.1.100", ... }`

---

## 🧪 Testing and Debugging

### Method 1: Using Debug Panel

**What it shows:**
```
├─ Input to node: Data received from previous node
├─ Output from node: Data sent to next node
└─ Execution time: How long node took
```

**How to use:**
1. Execute workflow
2. Bottom panel shows all node executions
3. Click node name to see I/O
4. Inspect JSON structure

### Method 2: Testing with Different Data

**Change the IP address:**

1. Click "Set IP" node
2. Change `"192.168.1.100"` to different IP
3. Execute again
4. See results change

**Example IPs to test:**
```
8.8.8.8           - Google DNS (should be clean)
192.168.1.1       - Private IP
10.0.0.1          - Private IP
192.168.0.1       - Router IP
```

### Method 3: Adding Logs for Debugging

**Add a Log node:**

1. Click "+" to add node
2. Search: **"Log"**
3. Position at end
4. Connect from Format Result nodes

**Configure:**
```
Log Level: Info
Message: Threat check result: {{ $node["Format Result"].json.status }}
```

**This logs to n8n dashboard for monitoring!**

### Common Issues and Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| Node stays YELLOW | Taking too long | Check network/API |
| Node turns RED | Error occurred | Click node, read error |
| No data in output | Mapping wrong | Check previous node output |
| Can't connect nodes | Wrong type | Both nodes must have I/O handles |

---

## 📊 Workflow Execution Monitoring

### Where to Find Execution History

**In n8n Dashboard:**
1. Click "Executions" (left sidebar)
2. See all past executions
3. Click one to inspect

**Execution Info Shows:**
```
├─ Status: SUCCESS or FAILED
├─ Duration: How long it took
├─ Started: When it started
├─ Nodes: Which nodes ran
└─ Output: Final result
```

### Reading Execution Logs

**Each execution shows:**

```json
{
  "executionId": "abc123def456",
  "status": "success",
  "startTime": "2025-12-17T15:30:00Z",
  "endTime": "2025-12-17T15:30:02Z",
  "duration": "2.543 seconds",
  "nodes": [
    "Manual Trigger",
    "Set IP",
    "Query Threat Intel",
    "Check Result",
    "Format Result"
  ],
  "output": { "status": "CLEAN", "ip": "192.168.1.100" }
}
```

### Monitoring Best Practices

```
✅ Enable logging for critical workflows
✅ Save execution results for audit
✅ Set up alerts for failures
✅ Archive old executions for compliance
✅ Monitor execution times (watch for slowdowns)
```

---

## 🔒 Security Best Practices for This Workflow

### 1. Credential Security

```
❌ WRONG: Hardcode API key
✅ RIGHT: Use n8n Credentials

In HTTP Request:
  Authentication: OAuth2 or API Key
  (stores encrypted, not in workflow)
```

### 2. Data Validation

```
Add validation for IPs:

return {
  ip: $node["Set IP"].json.ip_to_check,
  is_valid_ip: /^(\d{1,3}\.){3}\d{1,3}$/.test(ip),
  ...
};
```

### 3. Error Handling

```
Set each node:
  On Error: Continue (or Stop if critical)
  This prevents cascading failures
```

### 4. Audit Logging

```
Log all threat checks:
├─ IP checked
├─ Timestamp
├─ Result
├─ Action taken
└─ User/system that initiated
```

### 5. Rate Limiting

```
Add Wait node if hitting API limits:
  Wait X seconds between requests
  Or check API rate limit headers
```

---

## 🎬 Hands-On: Complete the Workflow

### Your Tasks

#### Task 1: Build Complete Workflow

1. ✅ Create workflow as shown above (all 8 steps)
2. ✅ Execute successfully
3. ✅ Screenshot showing all GREEN nodes
4. ✅ Save workflow

#### Task 2: Modify and Test

1. ✅ Change the IP address in "Set IP" node
2. ✅ Execute again
3. ✅ Verify data flows correctly

#### Task 3: Add Logging

1. ✅ Add a "Log" node at the end
2. ✅ Configure to log the result status
3. ✅ Execute and view logs

#### Task 4: Export Workflow

1. ✅ Click workflow name
2. ✅ Click "⋮" menu
3. ✅ Click "Download"
4. ✅ Save as `hello-security-world.json`

#### Task 5: Document

Write in your notes:
- [ ] What does each node do?
- [ ] How long did workflow take?
- [ ] What was the final output?
- [ ] How would you modify for real threat intel API?

---

## 💡 Real-World Modifications

### To Use Real Threat Intelligence:

**Replace "Query Threat Intel" HTTP node with:**

**Option 1: AbuseIPDB**
```
URL: https://api.abuseipdb.com/api/v2/check
Method: GET
Headers:
  Key: "Authorization"
  Value: "Bearer YOUR_API_KEY"
Parameters:
  ipAddress: {{ $node["Set IP"].json.ip_to_check }}
```

**Option 2: VirusTotal**
```
URL: https://www.virustotal.com/api/v3/ip_addresses/{{ $node["Set IP"].json.ip_to_check }}
Method: GET
Headers:
  Key: "x-apikey"
  Value: "YOUR_API_KEY"
```

**Option 3: AlienVault OTX**
```
URL: https://otx.alienvault.com/api/v1/indicators/IPv4/{{ $node["Set IP"].json.ip_to_check }}/general
Method: GET
```

Then modify the "Check Result" node to parse the real API response!

---

## ✅ Summary

### What You Built

✅ **Complete workflow** with trigger, actions, and logic  
✅ **Data mapping** between nodes  
✅ **Conditional routing** with If/Then  
✅ **Error handling** and debugging  
✅ **Execution monitoring**  

### Key Takeaways

> **Workflows are built incrementally, node by node.**  
> **Test as you build to catch issues early.**  
> **Debug using the execution panel.**  
> **Monitor execution for production reliability.**

---

## 🚀 Next Steps

1. ✅ Complete "Hello Security World" workflow
2. ✅ Export workflow JSON
3. ✅ Commit to GitHub
4. ⬜ Ready for **02-first-automation** (real security workflow)

---

## 📚 Resources

- [n8n HTTP Request Documentation](https://docs.n8n.io/nodes/n8n-nodes-base.httpRequest/)
- [n8n If Node Documentation](https://docs.n8n.io/nodes/n8n-nodes-base.if/)
- [n8n Code Node JavaScript](https://docs.n8n.io/nodes/n8n-nodes-base.code/)
- [Threat Intelligence APIs](https://docs.n8n.io/integrations/)

---

**Module Author:** Network Security Learning Team  
**Last Updated:** December 2025  
**License:** MIT
