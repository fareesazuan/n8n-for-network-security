# n8n Learning Roadmap: 30–60–90 Day Master Plan

## Overview

This is a detailed, day-by-day learning roadmap designed to take you from zero n8n experience to building enterprise-grade security automation workflows in **90 days**.

**Time Commitment:** 5–10 hours per week  
**Difficulty Progression:** Beginner → Intermediate → Advanced  
**Focus:** Network Security & SOC Automation  
**By Day 90:** You'll have built multiple production-ready security workflows

---

## 🎯 Success Criteria

By the end of each phase, you should be able to complete these milestones:

### Phase 1 (Day 30): Beginner Fundamentals ✅
- [ ] Set up n8n environment (cloud or self-hosted)
- [ ] Create workflows using triggers and nodes
- [ ] Debug workflows and understand data flow
- [ ] Build 3 simple workflows (notification, schedule, webhook)
- [ ] Deploy a working schedule-based automation

### Phase 2 (Day 60): Security Integration Master ✅
- [ ] Integrate with 5+ security tools
- [ ] Build alert ingestion from SIEM
- [ ] Create ticket automation workflow
- [ ] Implement alert triage system
- [ ] Handle complex data transformations

### Phase 3 (Day 90): Enterprise Architecture ✅
- [ ] Design multi-step security workflows
- [ ] Deploy n8n in production (self-hosted)
- [ ] Implement security best practices
- [ ] Build SOAR-like orchestration system
- [ ] Mentor others and contribute workflows

---

# PHASE 1: BEGINNER FUNDAMENTALS (Days 1–30)

## Focus: Master the Basics

**Goal:** Understand how n8n works and build your first workflows

**Weekly Time:** 5–7 hours  
**Format:** Learning → Examples → Hands-on Tasks

---

## WEEK 1: Platform Setup & Core Concepts (Days 1–7)

### Day 1-2: Platform Understanding
**Topics:**
- What is n8n and why use it for security?
- n8n vs traditional automation (Zapier, IFTTT, custom scripts)
- Cloud vs. self-hosted comparison
- Architecture overview (frontend, backend, database, scheduler)

**Learning Material:**
- Read: `01-beginner/00-platform-setup/README.md`
- Read: `01-beginner/01-core-concepts/what-is-n8n.md`
- Read: `01-beginner/01-core-concepts/architecture-overview.md`
- Watch: [n8n Introduction](https://www.youtube.com/watch?v=Gjv_x80a0zE) (15 min)

**Hands-On Task:**
- [ ] Create an n8n account (cloud) or install Docker locally
- [ ] Access n8n UI and explore the interface
- [ ] Take a screenshot of your setup (proof for learning log)

---

### Day 3-4: Credentials & Authentication
**Topics:**
- Credential types (API key, OAuth, Basic Auth)
- Storing credentials securely
- Testing connections
- Common authentication patterns

**Learning Material:**
- Read: `01-beginner/00-platform-setup/credentials-guide.md`
- Read: `reference/security-tools-reference.md` (authentication section)

**Hands-On Task:**
- [ ] Create at least 2 test credentials:
  - Option 1: GitHub API key (easiest to test)
  - Option 2: Slack webhook (also simple)
- [ ] Test each credential to confirm it works
- [ ] Document your credentials setup in a local notes file

---

### Day 5-6: Nodes & Workflow Basics
**Topics:**
- What are nodes?
- Common node types (trigger, action, helper)
- Node configuration and data flow
- First workflow: "Hello World"

**Learning Material:**
- Read: `01-beginner/01-core-concepts/nodes-and-workflows.md`
- Watch: [Understanding Nodes](https://www.youtube.com/watch?v=...) (20 min)
- Study: `01-beginner/01-core-concepts/workflows/hello-world.json`

**Hands-On Task:**
- [ ] Create "Hello World" workflow:
  1. Add Manual Trigger node
  2. Add Debug node
  3. Run and observe output
- [ ] Modify workflow to output "Hello, [Your Name]!"
- [ ] Screenshot your working workflow

---

### Day 7: Weekly Review & Practice
**Topics:**
- Data types in n8n
- Basic expressions
- Simple data manipulation

**Learning Material:**
- Read: `01-beginner/03-working-with-data/data-types-in-n8n.md`
- Review all Week 1 materials

**Hands-On Task:**
- [ ] Complete 3 simple workflows from samples
- [ ] Create learning journal documenting:
  - What you learned
  - What confused you
  - Questions for next week

---

## WEEK 2: Triggers & First Real Workflows (Days 8–14)

### Day 8-9: Manual & Webhook Triggers
**Topics:**
- Manual trigger (testing)
- Webhook trigger (receiving external data)
- Webhook URL and how to use it
- Testing webhooks with tools (curl, Postman)

**Learning Material:**
- Read: `01-beginner/02-first-workflow/webhook-trigger.md`
- Study: `01-beginner/02-first-workflow/workflows/first-webhook.json`

**Hands-On Task:**
- [ ] Create a webhook-triggered workflow:
  1. Add Webhook Trigger node
  2. Configure to receive POST data
  3. Log incoming data with Debug node
  4. Test with curl or Postman
- [ ] Capture test results

**Curl Example:**
```bash
curl -X POST http://localhost:5678/webhook/test-webhook \
  -H "Content-Type: application/json" \
  -d '{"alert_id": "123", "severity": "high"}'
```

---

### Day 10-11: Scheduled Triggers
**Topics:**
- Cron expressions
- Scheduled workflows
- Common scheduling patterns
- Timezone considerations

**Learning Material:**
- Read: `01-beginner/02-first-workflow/scheduled-workflow.md`
- Study: `01-beginner/02-first-workflow/workflows/first-schedule.json`
- Reference: `reference/expression-cheatsheet.md` (cron section)

**Hands-On Task:**
- [ ] Create a scheduled workflow:
  1. Add "Schedule Trigger" node
  2. Set to run every day at 9 AM
  3. Add "Debug" node to see when it runs
  4. Keep running for 3 days and verify execution
- [ ] Document the cron expressions learned

**Common Cron Patterns:**
```
Every day at 9 AM: 0 9 * * *
Every Monday 8 AM: 0 8 * * 1
Every 30 minutes: */30 * * * *
Every hour: 0 * * * *
```

---

### Day 12-13: Basic Data Transformation
**Topics:**
- Data types (string, number, array, object)
- Expressions and field mapping
- Simple filtering
- Using the "Set" node

**Learning Material:**
- Read: `01-beginner/03-working-with-data/data-types-in-n8n.md`
- Read: `01-beginner/03-working-with-data/expressions-and-filtering.md`
- Study: `01-beginner/03-working-with-data/workflows/data-transformation.json`

**Hands-On Task:**
- [ ] Create data transformation workflow:
  1. Use webhook to receive JSON data
  2. Use "Set" node to extract and reformat fields
  3. Output to Debug node
  4. Test with sample security alert data
- [ ] Examples:
  - Extract alert severity and convert to priority number
  - Create a formatted string from multiple fields

---

### Day 14: Week 2 Project - Simple Alert Notifier
**Project:** Create a workflow that receives alerts and sends Slack notification

**Steps:**
1. Create webhook trigger
2. Extract important fields from alert JSON
3. Format a readable Slack message
4. Send to Slack using Slack node
5. Test with sample alert data

**Workflow:**
```
Webhook Trigger
    ↓
Set Node (extract fields)
    ↓
Slack Node (send message)
    ↓
Debug (log success)
```

**Hands-On Task:**
- [ ] Build complete working workflow
- [ ] Test with at least 3 different alert samples
- [ ] Screenshot the Slack message output
- [ ] Document any issues encountered

---

## WEEK 3: Error Handling & Debugging (Days 15–21)

### Day 15-16: Error Handling Basics
**Topics:**
- Try-catch patterns
- Error messages and logs
- Node-level error handling
- Workflow-level error handling

**Learning Material:**
- Read: `01-beginner/04-basic-error-handling/error-handling-basics.md`
- Read: `01-beginner/04-basic-error-handling/try-catch-patterns.md`
- Study: `01-beginner/04-basic-error-handling/workflows/error-handling-basic.json`

**Hands-On Task:**
- [ ] Create error-handling workflow:
  1. Create workflow with potential error (e.g., API call)
  2. Add error handling path
  3. Send error notification to Slack
  4. Test by triggering an error intentionally

---

### Day 17-18: Debugging Techniques
**Topics:**
- Using Debug node effectively
- Reading execution history
- Common errors and solutions
- Logging best practices

**Learning Material:**
- Reference: `reference/troubleshooting-guide.md`

**Hands-On Task:**
- [ ] Debug sample workflows with intentional errors
- [ ] Use execution history to trace issues
- [ ] Create debugging checklist for future workflows

**Debugging Checklist:**
- [ ] Check input data (use Debug node)
- [ ] Verify credentials are correct
- [ ] Check field mappings match actual data
- [ ] Verify data types match node requirements
- [ ] Check error messages in execution history
- [ ] Test with minimal data first

---

### Day 19-20: Working with APIs
**Topics:**
- REST API basics
- HTTP node configuration
- Request/response patterns
- Status codes and error responses

**Learning Material:**
- Read: `02-intermediate/02-api-integration/http-node-guide.md` (start of intermediate, but valuable now)

**Hands-On Task:**
- [ ] Create workflow making HTTP request:
  1. Use HTTP node to call public API (e.g., jsonplaceholder.typicode.com)
  2. Parse response
  3. Extract specific data
  4. Output to Debug node

**Example API Call:**
```
GET https://jsonplaceholder.typicode.com/posts/1
Parse response and extract title
```

---

### Day 21: Week 3 Project - Smart Alert Router
**Project:** Create workflow that routes alerts based on severity

**Workflow Logic:**
```
Webhook (receive alert)
    ↓
Extract severity field
    ↓
Route based on severity:
  - CRITICAL → Page on-call + Slack + Email
  - HIGH → Slack + Ticket
  - MEDIUM → Slack only
  - LOW → Log only
```

**Hands-On Task:**
- [ ] Build complete routing workflow
- [ ] Test all 4 severity levels
- [ ] Verify correct routing behavior
- [ ] Document the workflow logic

---

## WEEK 4: Practical Security Workflows (Days 22–30)

### Day 22-23: First Security Integration
**Topics:**
- How security tools expose data
- Common APIs (SIEM, ticketing, endpoints)
- Mapping security data to n8n workflows

**Learning Material:**
- Read: `02-intermediate/01-security-integrations/README.md` (preview)
- Watch: Security tool API examples

**Hands-On Task:**
- [ ] Choose one security tool you have access to:
  - Option 1: Free tier (e.g., VirusTotal, Shodan)
  - Option 2: API documentation (e.g., Splunk, ServiceNow)
- [ ] Create workflow to query that tool's API
- [ ] Parse and display results

---

### Day 24-25: Building Notification Workflows
**Topics:**
- Multi-channel notifications (Slack, email, Teams, webhook)
- Message formatting
- Conditional notifications

**Learning Material:**
- Study templates in `templates/notification-template.json`

**Hands-On Task:**
- [ ] Create multi-channel notification workflow:
  1. Receive alert
  2. Send to 3 different channels
  3. Customize message for each channel

---

### Day 26-27: Data Persistence
**Topics:**
- Storing workflow data (Google Sheets, databases)
- Creating audit logs
- Data archival

**Learning Material:**
- Study templates in `templates/`

**Hands-On Task:**
- [ ] Create workflow that logs all alerts to Google Sheets:
  1. Receive alert
  2. Send to Slack
  3. Log to Google Sheets
  4. Verify data in spreadsheet

---

### Day 28-30: Phase 1 Capstone Project
**Project:** Complete Alert Management Workflow

**Build a workflow that:**
1. ✅ Receives security alerts via webhook
2. ✅ Validates and parses alert data
3. ✅ Routes based on severity
4. ✅ Creates tickets (or logs to spreadsheet)
5. ✅ Sends notifications
6. ✅ Handles errors gracefully
7. ✅ Logs all activity for audit

**Submission:**
- [ ] Working workflow JSON
- [ ] Screenshots of test runs
- [ ] Documentation explaining each step
- [ ] List of tools/APIs used
- [ ] Common errors you handled

**Evaluation Criteria:**
- ✅ Workflow runs without errors
- ✅ Properly handles different alert types
- ✅ Error handling implemented
- ✅ Code is readable with comments
- ✅ Documentation is clear

---

## Phase 1 Summary: What You've Learned

By Day 30, you should understand:

✅ **Platform Knowledge**
- How n8n works internally
- Cloud vs. self-hosted differences
- Core UI and navigation

✅ **Workflow Fundamentals**
- Creating workflows from scratch
- Understanding data flow
- Using triggers (manual, webhook, schedule)
- Using basic nodes (Debug, Set)

✅ **Data Handling**
- Working with JSON data
- Basic expressions and filtering
- Field mapping and transformation

✅ **Error Handling**
- Understanding common errors
- Debugging workflows
- Error handling patterns

✅ **First Workflows**
- Simple notification workflows
- Data ingestion from APIs
- Alert routing logic
- Basic logging/persistence

**You are now ready for Phase 2!**

---

---

# PHASE 2: INTERMEDIATE - SECURITY INTEGRATION (Days 31–60)

## Focus: Apply to Real Security Operations

**Goal:** Build production-like security workflows with real tool integrations

**Weekly Time:** 6–8 hours  
**Format:** Deeper dives into security use cases

---

## WEEK 5-6: Security Tool Integrations (Days 31–42)

### Goals for This Period:
- Integrate with major security platforms
- Handle real alert data
- Build triage workflows
- Create ticket automation

### Topics to Cover:

**SIEM Integration** (Days 31-35)
- Splunk webhook integration
- Azure Sentinel integration
- Alert forwarding
- Real-time data ingestion

**Hands-On:**
- [ ] Create workflow to ingest SIEM alerts
- [ ] Parse SIEM alert format
- [ ] Extract key fields (timestamp, severity, source)
- [ ] Test with sample SIEM data

**Ticketing System** (Days 36-40)
- ServiceNow integration
- Jira integration
- Ticket enrichment
- Update existing tickets

**Hands-On:**
- [ ] Create workflow that auto-creates ServiceNow tickets
- [ ] Auto-update tickets when alerts change
- [ ] Enrich tickets with context

**Threat Intelligence** (Days 41-42)
- VirusTotal integration
- Shodan integration
- IP/Domain reputation lookup
- Alert enrichment with TI data

**Hands-On:**
- [ ] Create enrichment workflow
- [ ] Query TI feeds for IOCs
- [ ] Combine alert with enrichment data

---

## WEEK 7-8: Advanced Data Operations (Days 43–56)

### Topics:

**JavaScript Expressions** (Days 43-47)
- Writing custom expressions
- String manipulation
- Array/object operations
- Conditional logic

**Hands-On:**
- [ ] Write 5 different JavaScript expressions
- [ ] Practice with security data (IP extraction, domain parsing)
- [ ] Build regex patterns for IOC extraction

**Example Expressions:**
```javascript
// Extract IP from log line
$('Webhook.body.log_line').match(/\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}/)[0]

// Check if severity is critical
$('Alert.severity') === 'CRITICAL' ? true : false

// Count occurrences
$('raw_data').split('error').length - 1

// Parse timestamp
new Date($('Alert.timestamp')).toISOString()
```

**Subworkflows** (Days 48-50)
- Creating reusable subworkflows
- Passing data between workflows
- Modular workflow design

**Hands-On:**
- [ ] Extract alert enrichment as subworkflow
- [ ] Extract ticket creation as subworkflow
- [ ] Create main workflow using subworkflows

**Complex Workflows** (Days 51-56)
- Multi-step alert triage
- Conditional branching
- Parallel processing
- Error paths

---

## WEEK 9: Intermediate Projects (Days 57–63)

### Project 1: Alert Triage System (Days 57-59)

**Requirements:**
1. Ingest alerts from multiple sources
2. Deduplicate alerts
3. Enrich with threat intelligence
4. Calculate risk score
5. Route to appropriate team

**Workflow:**
```
Multiple Alert Sources
    ↓
Deduplication Node
    ↓
Enrich with TI (parallel)
    ↓
Calculate Risk Score
    ↓
Route by Priority
```

**Hands-On:**
- [ ] Complete working workflow
- [ ] Test with 10+ sample alerts
- [ ] Verify deduplication works
- [ ] Test routing logic

### Project 2: Automated Ticket Creation (Days 60-63)

**Requirements:**
1. Receive alerts
2. Check if ticket exists
3. Create new ticket or update existing
4. Add context/attachments
5. Notify ticket owner

**Workflow:**
```
Alert → Check ticket exists → 
  If yes: Update ticket
  If no: Create new ticket
→ Add context/comments
→ Notify
```

**Hands-On:**
- [ ] Complete working workflow
- [ ] Test all paths (new vs. existing)
- [ ] Verify ticket creation in system
- [ ] Test notifications

---

## Phase 2 Summary

By Day 60, you can:

✅ **Integrate with Security Tools**
- Connect to SIEM, EDR, ticketing systems
- Handle tool-specific data formats
- Query security APIs
- Enrich data from multiple sources

✅ **Build Complex Workflows**
- Multi-step alert processing
- Conditional routing
- Error handling at scale
- Parallel processing

✅ **Real-World Automation**
- Alert triage automation
- Ticket lifecycle automation
- Threat intelligence enrichment
- Automated reporting

✅ **Security Best Practices**
- Secure credential handling
- Audit logging
- Error recovery
- Monitoring

**You are halfway to expert level!**

---

---

# PHASE 3: ADVANCED - ENTERPRISE ARCHITECTURE (Days 61–90)

## Focus: Production-Grade Systems

**Goal:** Deploy enterprise-class security automation

**Weekly Time:** 8–10 hours

---

## WEEK 10-11: Production Deployment (Days 61–77)

### Topics:

**Self-Hosted Deployment** (Days 61-69)
- Docker setup
- Docker Compose configuration
- Database configuration
- Reverse proxy (nginx)
- SSL/TLS setup
- Performance tuning

**Hands-On:**
- [ ] Deploy n8n with Docker Compose
- [ ] Configure PostgreSQL database
- [ ] Setup nginx reverse proxy
- [ ] Enable SSL certificates
- [ ] Test full deployment

**Security Hardening** (Days 70-77)
- Credential encryption
- RBAC implementation
- Audit logging
- API security
- Network segmentation
- Secret management

**Hands-On:**
- [ ] Implement all security controls
- [ ] Test encryption at rest
- [ ] Verify audit logs work
- [ ] Setup RBAC for team access

---

## WEEK 12: Advanced Architecture (Days 78–84)

### Topics:

**Workflow Architecture** (Days 78-80)
- Design patterns for scale
- Event-driven architecture
- Queue-based processing
- Monitoring and alerting

**Hands-On:**
- [ ] Design SOAR-like system
- [ ] Implement event queues
- [ ] Setup monitoring

**Custom Nodes** (Days 81-82)
- Creating custom nodes
- Packaging nodes
- Sharing with team

**Hands-On:**
- [ ] Build one custom node for proprietary tool

**Multi-Environment** (Days 83-84)
- Dev/staging/prod setup
- Workflow versioning
- Safe deployment

---

## WEEK 13: Final Capstone (Days 85–90)

### Capstone Project: Complete SOAR System

**Build End-to-End Security Orchestration:**

**Requirements:**
1. ✅ Multi-source alert ingestion
2. ✅ Intelligent deduplication
3. ✅ Threat intelligence enrichment
4. ✅ Automated risk scoring
5. ✅ Multi-level routing & escalation
6. ✅ Ticket creation & tracking
7. ✅ Automated response actions
8. ✅ Comprehensive logging & audit
9. ✅ Performance & error monitoring
10. ✅ Team notifications

**Architecture:**
```
[Alert Sources] → [Ingestion] → [Dedup] → [Enrich]
                                              ↓
                                    [Risk Score]
                                              ↓
                      ┌─────────────────────┼─────────────────────┐
                      ↓                     ↓                     ↓
                  [Low Route]         [Medium Route]        [High Route]
                      ↓                     ↓                     ↓
              [Log & Monitor]      [Auto Ticket]          [Escalate]
                                      ↓                     ↓
                               [Notify Team]          [Executive Alert]
                                                       [Auto Response]
```

**Submission (Days 85-90):**

1. **Complete Working System**
   - [ ] All workflows documented
   - [ ] All integrations tested
   - [ ] Error handling verified
   - [ ] Deployed in secure environment

2. **Documentation**
   - [ ] Architecture diagram
   - [ ] Workflow documentation
   - [ ] Integration guide
   - [ ] Troubleshooting guide
   - [ ] SOP for team

3. **Testing**
   - [ ] Test plan and results
   - [ ] Load testing results
   - [ ] Failure scenario testing
   - [ ] Security assessment

4. **Team Handoff**
   - [ ] Training materials
   - [ ] Knowledge transfer
   - [ ] Monitoring dashboard
   - [ ] Escalation procedures

---

## Phase 3 Summary

By Day 90, you can:

✅ **Deploy & Maintain**
- Production n8n infrastructure
- Security hardening
- Monitoring and observability
- Disaster recovery

✅ **Design Enterprise Systems**
- Complex workflow orchestration
- Event-driven architecture
- Integration of 10+ security tools
- Scalable automation

✅ **Advanced Skills**
- Custom node development
- Performance optimization
- Security best practices
- Team training/mentoring

✅ **Real SOAR Capabilities**
- Alert ingestion from multiple sources
- Automated enrichment & correlation
- Intelligent routing & prioritization
- Automated response actions
- Complete audit trail

---

## 🎓 Continuing Education (Beyond Day 90)

The learning doesn't stop at Day 90. Here's how to continue:

### Keep Learning:
- [ ] Contribute your workflows to the repository
- [ ] Build custom nodes for specialized tools
- [ ] Join n8n community forum
- [ ] Attend webinars and training
- [ ] Read n8n blog and documentation
- [ ] Experiment with new integrations

### Share Knowledge:
- [ ] Document your implementations
- [ ] Create case studies
- [ ] Mentor junior team members
- [ ] Speak at security conferences
- [ ] Write blog posts
- [ ] Contribute to this repository

### Level Up:
- [ ] Get n8n certified
- [ ] Build AI-powered workflows
- [ ] Explore advanced queuing
- [ ] Implement advanced scaling
- [ ] Multi-cloud automation

---

## 📊 Progress Tracking Template

Use this to track your learning:

```
WEEK 1-4 (BEGINNER):
Day 1: ✅ Platform setup
Day 2: ✅ Core concepts
...
Day 30: ✅ Phase 1 project complete

WEEK 5-8 (INTERMEDIATE):
Day 31: ✅ SIEM integration
...
Day 60: ✅ Phase 2 project complete

WEEK 9-13 (ADVANCED):
Day 61: ✅ Production deployment
...
Day 90: ✅ SOAR system deployed

LESSONS LEARNED:
- Key insight 1
- Key insight 2
- What I'd do differently
```

---

## 🚀 Success Factors

### Time Management:
- Schedule specific learning times
- Treat learning like work commitments
- 5-10 hours per week is sustainable
- Block out distractions

### Hands-On Practice:
- Don't just read—build every example
- Modify examples to understand them
- Test error scenarios
- Break workflows intentionally to learn

### Community Support:
- Join n8n community forum
- Ask questions when stuck
- Help others (reinforces learning)
- Share your progress

### Real-World Application:
- Apply to your actual security stack
- Start small, grow bigger
- Document your use cases
- Measure impact and improvement

---

## 📚 Key Resources

**During Learning Path:**
- `01-beginner/` - Phase 1 materials
- `02-intermediate/` - Phase 2 materials
- `03-advanced/` - Phase 3 materials
- `reference/` - Quick lookup
- `templates/` - Reusable starting points

**Official Resources:**
- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- [n8n Blog](https://blog.n8n.io/)
- [n8n YouTube](https://www.youtube.com/@n8nio)

**Security-Specific:**
- MITRE ATT&CK Framework
- NIST Cybersecurity Framework
- CIS Controls
- OWASP Guidelines

---

## 🎯 Final Thoughts

This 90-day journey will fundamentally change how you approach security operations:

**From Manual To Automated:**
- Manual alert triage → Automated, intelligent triage
- Manual ticketing → Automated with enrichment
- Manual logging → Comprehensive audit trails
- Manual escalation → Intelligent escalation

**From Reactive To Proactive:**
- Respond faster to incidents
- Prevent issues before they escalate
- Detect patterns humans miss
- Make data-driven decisions

**From Individual to Team:**
- Share knowledge with team
- Build repeatable processes
- Document everything
- Create organizational memory

**Keep going, keep learning, and happy automating! 🚀**

---

**Last Updated:** December 2025  
**Version:** 1.0  
**Status:** Production-Ready Learning Path

Need clarification? Open an issue on GitHub!
