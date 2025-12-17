# 01-Core Concepts: Understanding n8n Fundamentals

## 📚 Learning Path Overview

This module covers the foundational concepts you need to understand n8n before building workflows. By the end, you'll understand:

- What n8n is and how it fits in network security
- Internal architecture and how workflows execute
- Nodes, connections, and data flow
- Your first "Hello World" workflow

**Estimated Duration:** 2-3 days (Days 2-4)  
**Prerequisites:** Complete 00-platform-setup  
**Skill Level:** Beginner (no n8n experience needed)

---

## 📖 Learning Modules

### Module 1: What is n8n? (30 mins)
**File:** `what-is-n8n.md`

Learn:
- n8n definition and purpose
- Why network security engineers need n8n
- n8n vs competitors (Zapier, Power Automate, etc.)
- Real-world SOC automation examples

**Hands-on Task:**
- Navigate n8n UI
- Create a blank workflow
- Identify key UI components

---

### Module 2: Architecture Overview (45 mins)
**File:** `architecture-overview.md`

Learn:
- Execution models (Webhook, trigger, manual)
- How data flows through workflows
- Nodes and their lifecycle
- Error handling fundamentals

**Hands-on Task:**
- Create a simple 3-node workflow
- Trace data flow
- Understand node states

---

### Module 3: Nodes and Workflows (1 hour)
**File:** `nodes-and-workflows.md`

Learn:
- What are nodes?
- Core node types (Trigger, Action, Logic)
- Connections and data mapping
- Workflow execution rules

**Hands-on Task:**
- Build a multi-step workflow
- Use different node types
- Export and inspect workflow JSON

---

### Module 4: Hello World Workflow (30 mins)
**Workflow File:** `workflows/hello-world.json`

Learn:
- Building your first complete workflow
- Testing and debugging
- Workflow execution monitoring

**Hands-on Task:**
- Deploy hello-world workflow
- Execute and inspect output
- Modify and re-run

---

## 🎯 Learning Outcomes

By completing this module, you should be able to:

✅ Explain what n8n is and its role in security automation  
✅ Understand how workflows execute internally  
✅ Identify different node types  
✅ Create and execute a basic workflow  
✅ Read and modify workflow JSON  
✅ Debug workflow execution  

---

## 🔒 Security Perspective

Key security concepts throughout this module:

| Concept | Security Relevance |
|---------|-------------------|
| Workflow Isolation | Each execution is sandboxed |
| Credential Management | Secure API key storage |
| Audit Trail | All executions logged |
| Error Handling | Graceful failure vs. cascading breaches |

---

## 📋 Time Breakdown

| Section | Time | Hands-On |
|---------|------|----------|
| What is n8n? | 30 min | 10 min |
| Architecture | 45 min | 15 min |
| Nodes & Workflows | 60 min | 20 min |
| Hello World | 30 min | 20 min |
| **Total** | **165 min** | **65 min** |

---

## ✅ Completion Checklist

- [ ] Read all 4 modules
- [ ] Complete all hands-on tasks
- [ ] Created hello-world workflow in n8n
- [ ] Understood workflow JSON structure
- [ ] Executed and debugged a workflow
- [ ] Committed code to GitHub
- [ ] Ready for 02-first-automation

---

## 🚀 Next Steps

After completing this module:
1. Review all workflow JSON files
2. Test workflows in your n8n instance
3. Document any questions
4. Proceed to **02-first-automation** (building your first security workflow)

---

## 📚 Resources

- [n8n Official Docs](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- [n8n Workflows Gallery](https://n8n.io/workflows/)
- [Network Security Automation Best Practices](../README.md)

---

**Author:** Mohd Farees Azuan  
**Last Updated:** December 2025  
**License:** MIT (Open Source)
