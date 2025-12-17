# Module 1: What is n8n?

## 🎯 What You'll Learn (30 minutes)

- What n8n is and how it works
- How n8n fits into your network security workflow
- Why n8n beats manual processes
- Real-world SOC and network security examples

---

## 📖 What is n8n?

### Definition

**n8n** = **"No Code Integration & Automation Platform"**

Think of it as: **"A visual programming language for connecting tools and automating tasks without writing code."**

```
n8n = Node Connector 8 Nodes
    = Automation for everything
    = Your DevOps/Security Swiss Army Knife
```

### How Does n8n Work?

At its core, n8n:

1. **Connects Systems** - Links your security tools (SIEM, firewalls, endpoints, etc.)
2. **Moves Data** - Passes information between systems automatically
3. **Executes Logic** - Makes decisions based on data conditions
4. **Performs Actions** - Takes automated responses to events

**Simple Workflow Example:**
```
Alert from SIEM 
    ↓
(TRIGGER: Webhook receives alert)
    ↓
Check if IP is malicious
    ↓
(LOGIC: Query threat intelligence)
    ↓
Block IP on firewall
    ↓
(ACTION: API call to firewall)
    ↓
Send notification to SOC
    ↓
(ACTION: Send Slack message)
```

---

## 🔒 Why Network Security Engineers Need n8n

### The Problem: Manual SOC Work

**Current Reality (Manual Process):**
```
SOC Analyst Day:
09:00 - Alert comes in on SIEM
09:05 - Manually check firewall logs (boring!)
09:10 - Query threat intelligence database
09:15 - Check if IP is in watchlist
09:20 - If malicious: Create ticket, notify team
09:25 - Manually block IP on firewall
09:30 - Document in incident response system
Result: 30 minutes for ONE routine alert
```

**The Cost:**
- 💰 Expensive analyst time
- ⏰ Slow response time (30 min = dangerous in security!)
- 😴 Repetitive work = analyst burnout
- 🚨 Human errors in procedures

### The Solution: n8n Automation

**With n8n (Automated):**
```
Alert comes in → n8n executes workflow → Done in 2 seconds
Analyst never leaves the dashboard
```

**The Benefit:**
- ⚡ 900x faster (30 min → 2 sec)
- 🎯 Consistent, no human error
- 😊 Analysts do important work, not repetition
- 📊 Better response times = better security posture

---

## 🏆 n8n vs Competitors

### Comparison Table

| Feature | n8n | Zapier | Power Automate | IFTTT |
|---------|-----|--------|-----------------|-------|
| **Self-Hosted** | ✅ Yes | ❌ Cloud only | ❌ Cloud only | ❌ No |
| **Open Source** | ✅ Yes | ❌ No | ❌ No | ❌ No |
| **Cost** | 💰 Free | 💸💸💸 Expensive | 💸 Moderate | 💰 Free tier |
| **Complex Workflows** | ✅ Excellent | ⚠️ Limited | ⚠️ Limited | ❌ Very limited |
| **Security/Compliance** | ✅ Full control | ⚠️ Cloud dependent | ⚠️ Cloud dependent | ❌ Not for security |
| **Custom Nodes** | ✅ Build custom | ❌ No | ❌ Limited | ❌ No |
| **On-Premise Security Tools** | ✅ Easy | ❌ Hard | ⚠️ VPN needed | ❌ No |

### Why n8n Wins for Security

```
Network Security Requirements → n8n Answer
─────────────────────────────────────────
1. On-premise tools?          → Self-hosted deployment
2. Sensitive data?            → Full data control (no vendor access)
3. Custom integrations?       → Build custom nodes
4. Compliance audits?         → Open source = auditable
5. Cost at scale?             → One server = unlimited workflows
6. 24/7 reliability?          → Self-hosted = your control
```

---

## 💡 Real-World Security Examples

### Example 1: Automated Threat Response (SOC)

**Scenario:** Your SIEM detects suspicious login activity

**Manual Process:**
1. Analyst sees alert (5 min later)
2. Checks logs manually (15 min)
3. Queries AD for user info (10 min)
4. Blocks account (if suspicious) (5 min)
5. Notifies manager (2 min)
**Total: 37 minutes** ⏰

**n8n Automated:**
1. Alert triggers n8n workflow (instant)
2. Queries threat intel (2 sec)
3. Checks AD (1 sec)
4. If suspicious: blocks account + sends alert (1 sec)
5. Creates incident ticket (1 sec)
**Total: 5 seconds** ⚡

**Workflow:**
```
SIEM Alert (Trigger)
    ↓
Get User Info from AD (Action)
    ↓
Check Threat Intel (Action)
    ↓
Is Suspicious? (Decision)
    ├─ YES → Block Account, Send Alert, Create Ticket
    └─ NO → Log and Continue
```

### Example 2: Automated Vulnerability Management

**Scenario:** Patch Tuesday - new vulnerabilities released

**Manual Process:**
1. Download CVE list (10 min)
2. Check each asset manually (60 min)
3. Create remediation tickets (30 min)
4. Assign to teams (15 min)
5. Send notifications (10 min)
**Total: 2 hours** ⏰

**n8n Automated:**
```
CVE Feed (Trigger)
    ↓
Query Vulnerability Scanner (Action)
    ↓
Correlate with Assets (Logic)
    ↓
For each vulnerable asset:
    ├─ Create Ticket (Action)
    ├─ Assign to Team (Action)
    └─ Send Notification (Action)
```
**Total: 30 seconds** ⚡

### Example 3: Compliance Reporting

**Scenario:** Monthly compliance report for firewalls, access logs, etc.

**Manual:**
```
1. Export firewall logs (30 min)
2. Export access logs (30 min)
3. Manual analysis (2 hours)
4. Format for report (45 min)
5. Send to management (10 min)
Total: 4 hours every month
```

**n8n (Runs automatically at 2 AM):**
```
Trigger: Monthly Schedule
    ↓
Query Firewall API (1 sec)
    ↓
Query Access Logs (2 sec)
    ↓
Analyze & Correlate (5 sec)
    ↓
Generate PDF Report (3 sec)
    ↓
Email to Stakeholders (1 sec)
Total: 12 seconds, runs automatically
```

---

## 🔐 Security Perspective: What Makes n8n Safe?

### Key Security Features

| Feature | Why It Matters |
|---------|---|
| **Self-Hosted** | Your data never leaves your network |
| **Open Source** | You can audit the code |
| **Encryption** | Credentials stored encrypted |
| **Audit Logs** | Every workflow execution is logged |
| **Access Control** | Role-based permissions |
| **Air-Gapped** | Can run on isolated networks |

### Common Security Concerns & Answers

```
Q: "Is n8n safe for sensitive security tools?"
A: YES - self-hosted means full control. Data never leaves your network.

Q: "What about API keys and passwords?"
A: Encrypted at rest. n8n uses credential encryption.

Q: "Can I audit what n8n does?"
A: YES - open source code + audit logs of all executions.

Q: "What if a workflow has a bug?"
A: Caught in testing. Workflows are version controlled.

Q: "Can I isolate it from production systems?"
A: YES - run it on a separate server or even air-gapped network.
```

---

## 🎬 Hands-On Task 1: Explore n8n UI

### Step 1: Open n8n

1. Open your n8n instance (from Day 1 setup)
   - **Cloud:** https://app.n8n.cloud
   - **Self-Hosted:** https://your-server:5678
2. Log in with your credentials

### Step 2: Navigate the UI

Explore these sections:

```
n8n Dashboard
├── Workflows (left sidebar)
│   ├── My Workflows
│   ├── Templates
│   └── Create New
├── Credentials (settings)
├── Executions (logs)
├── Templates Gallery
└── Settings
```

**What to look for:**
- [ ] Find "Workflows" section
- [ ] Find "Credentials" section
- [ ] Find "Executions" log
- [ ] Click on a template workflow (to see an example)

### Step 3: Create Blank Workflow

1. Click **"New Workflow"** button
2. You'll see the editor with a blank canvas
3. Notice:
   - **Canvas** (center) - where you drag nodes
   - **Node Library** (left) - all available nodes
   - **Node Inspector** (right) - settings for selected node

### Step 4: Identify Key Components

Look for these in the editor:

| Component | Location | Purpose |
|-----------|----------|---------|
| **Add Node Button** | Bottom center | Drag to add nodes |
| **Play Button** | Top right | Execute workflow |
| **Save Button** | Top right | Save workflow |
| **Settings** | Top right | Workflow configuration |
| **Debug Panel** | Bottom | See execution output |

### Step 5: Screenshot & Document

Take a screenshot of:
- ✅ The main editor screen
- ✅ The node library
- ✅ A sample node's settings panel

Save screenshots to: `01-core-concepts/assets/ui-exploration/`

---

## 🎬 Hands-On Task 2: UI Component Identification Quiz

**Answer these questions (write answers in a note):**

1. **Where do you find available nodes to add?** (Hint: look left side)
2. **What button would you click to test your workflow?** (Hint: top right)
3. **Where can you see past workflow executions?** (Hint: sidebar or settings)
4. **What's the difference between "Save" and "Activate"?** (Hint: read the buttons)

**Expected Answers:**
```
1. Node Library (left sidebar)
2. Play/Execute button (top right, green button)
3. Executions tab (can see it after running a workflow)
4. Save = save locally, Activate = workflow runs on triggers
```

---

## ✅ Summary

### What You Learned

✅ **n8n is:** A visual automation platform connecting security tools  
✅ **Why it matters:** 900x faster than manual SOC work  
✅ **How it wins:** Self-hosted, open source, full control  
✅ **Real-world usage:** Threat response, vulnerability management, compliance  

### Key Takeaway

> **n8n lets SOC teams do what they're trained for: security analysis.**  
> **It handles repetitive tasks: collecting data, checking rules, running responses.**

---

## 🚀 Next Steps

1. ✅ Complete both hands-on tasks above
2. ✅ Document your findings
3. ⬜ Move to **Module 2: Architecture Overview**

---

## 📚 Resources

- [n8n Official Website](https://n8n.io/)
- [n8n Documentation](https://docs.n8n.io/)
- [n8n GitHub](https://github.com/n8n-io/n8n)
- [n8n Community Examples](https://n8n.io/workflows/)

---

**Module Author:** Network Security Learning Team  
**Last Updated:** December 2025  
**License:** MIT
