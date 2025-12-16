# Quick Start Guide: Begin Your n8n Learning Journey

Welcome! This guide helps you get started in the next 30 minutes.

---

## 🚀 5-Minute Setup

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/n8n-for-network-security.git
cd n8n-for-network-security
```

### Step 2: Choose Your Path

#### Option A: Cloud (Easiest for Beginners)
1. Visit [n8n Cloud](https://n8n.cloud)
2. Sign up for free account
3. You get instant access to n8n editor
4. ⏱️ **Setup time:** 2 minutes

#### Option B: Local Docker (Recommended for Production Learning)
```bash
# Install Docker Desktop if not already installed
# Then:
cd lab-environment
docker-compose up -d

# Access n8n at http://localhost:5678
# ⏱️ Setup time:** 10 minutes
```

#### Option C: Local Installation
```bash
npm install n8n -g
n8n start

# Access at http://localhost:5678
# ⏱️ Setup time:** 15 minutes (requires Node.js)
```

---

## 📚 Your First 30 Minutes

### Minute 1-5: Understand the Big Picture
```
Read: README.md (this file gives you the overview)
```

### Minute 6-15: Tour the Repository
```
Explore: Repository structure
- Notice the 3 phases (Beginner, Intermediate, Advanced)
- Check out 01-beginner/00-platform-setup/README.md
- Skim through ROADMAP.md to see the full journey
```

### Minute 16-25: Create Your First Workflow
```
Do: Follow 01-beginner/01-core-concepts/
1. Open n8n (cloud or local)
2. Create new workflow
3. Add "Manual Trigger" node
4. Add "Debug" node
5. Click "Execute Workflow"
6. See the output in Debug node
```

### Minute 26-30: Join the Community
```
Do:
1. Star this repository (top right of GitHub)
2. Watch for updates (so you're notified)
3. Open an issue if you have questions
4. Schedule your learning time this week
```

---

## 📅 This Week's Homework

### Pick ONE task from Phase 1, Week 1:

**Option A: Platform Exploration (30 min)**
- Set up n8n in your preferred environment
- Explore the UI and nodes available
- Take a screenshot showing your setup

**Option B: First Webhook (45 min)**
- Create a webhook-triggered workflow
- Test it with curl or Postman
- Screenshot the successful test

**Option C: Scheduled Workflow (45 min)**
- Create a workflow that runs on a schedule
- Use "Schedule Trigger" node
- Wait to see it execute (or use a 1-minute schedule)

---

## 🎯 30-Day Learning Schedule

### Week 1 (Days 1-7)
```
Mon: Read platform setup guide
Tue: Create hello world workflow
Wed: Explore webhook triggers
Thu: Learn scheduled workflows
Fri: Build alert notifier
Sat-Sun: Review & practice
```

### Week 2 (Days 8-14)
```
Mon: Webhook deep dive
Tue: Create test workflow
Wed: Learn data transformation
Thu: Error handling basics
Fri: Build routing workflow
Sat-Sun: Week 2 project
```

### Week 3 (Days 15-21)
```
Mon-Tue: Error handling patterns
Wed-Thu: API integration basics
Fri: First API call
Sat-Sun: Week 3 project
```

### Week 4 (Days 22-30)
```
Mon-Wed: Integration with security tools
Thu-Fri: Multi-channel notifications
Sat-Sun: Phase 1 capstone project
```

---

## 📖 Recommended Learning Path

### If You Have 1 Hour This Week:
1. **5 min:** Read README.md
2. **15 min:** Set up n8n
3. **30 min:** Create your first workflow
4. **10 min:** Explore sample workflows

### If You Have 3 Hours This Week:
1. **1 hour:** Complete Week 1 materials
2. **1 hour:** Build "Hello World" workflow
3. **1 hour:** Explore triggers (manual, webhook, schedule)

### If You Have 5+ Hours This Week:
1. **1-2 hours:** Week 1 setup and concepts
2. **1-2 hours:** Build first 3 workflows
3. **1-2 hours:** Explore security integrations
4. **Time to practice:** Build Week 1 project

---

## 🛠️ Tools You'll Need

### Required
- ✅ n8n account (cloud or self-hosted)
- ✅ Git (to clone repository)
- ✅ Text editor (VS Code recommended)

### Recommended
- 🔧 Postman (test API calls)
- 🐳 Docker (for self-hosted)
- 📝 Notion or similar (keep learning notes)

### Optional
- 🔍 curl command line
- 💻 Local Node.js environment
- 📊 Sample data sources

---

## 🔗 Quick Links by Learning Phase

### Phase 1: Beginner (Days 1-30)
- [Platform Setup](01-beginner/00-platform-setup/README.md)
- [Core Concepts](01-beginner/01-core-concepts/)
- [First Workflows](01-beginner/02-first-workflow/)
- [Projects](01-beginner/05-beginner-projects/)

### Phase 2: Intermediate (Days 31-60)
- [Security Integrations](02-intermediate/01-security-integrations/)
- [API Integration](02-intermediate/02-api-integration/)
- [Data Transformation](02-intermediate/03-advanced-data-transformation/)
- [Projects](02-intermediate/06-intermediate-projects/)

### Phase 3: Advanced (Days 61-90)
- [Architecture Patterns](03-advanced/01-architecture-patterns/)
- [Production Deployment](03-advanced/02-production-deployment/)
- [Security Best Practices](03-advanced/03-security-best-practices/)
- [Projects](03-advanced/06-advanced-projects/)

---

## ❓ Common Questions

### Q: Do I need programming experience?
**A:** No! This is designed for network security engineers new to automation.

### Q: Can I use n8n Cloud or do I need self-hosted?
**A:** Start with Cloud for learning. Move to self-hosted for production/advanced topics.

### Q: How long will this take?
**A:** ~300 hours total (5-10 hours/week for 30-90 days). You can adjust pace.

### Q: What if I get stuck?
**A:** 
1. Check the troubleshooting guide
2. Review similar workflows
3. Open an issue on GitHub
4. Join n8n community forum

### Q: Can I skip to advanced topics?
**A:** Not recommended. Each phase builds on previous knowledge.

### Q: How do I practice with my own security tools?
**A:** Start with free tiers or test environments. Phase 2 covers tool integration.

### Q: Is this security best practices?
**A:** Yes! Every workflow includes security considerations.

---

## 📞 Getting Help

### If You're Stuck:

1. **Check docs first**
   - Review related section in phase materials
   - Check reference/ folder
   - Read troubleshooting guide

2. **Search existing issues**
   - Someone may have asked before
   - Solution might already exist

3. **Ask the community**
   - Open an issue on GitHub
   - Ask in n8n community forum
   - Describe the problem clearly:
     - What you're trying to do
     - What error you see
     - Screenshot if helpful
     - Steps to reproduce

4. **Review examples**
   - Look at similar workflows
   - Study how they work
   - Modify for your use case

---

## ✅ Checklist: Ready to Start?

Before you begin, confirm:

- [ ] GitHub account created
- [ ] Repository cloned or bookmarked
- [ ] n8n setup (cloud or local)
- [ ] First workflow created (Hello World)
- [ ] Able to access learning materials
- [ ] Time blocked on calendar for learning
- [ ] Community connections made (starred repo, etc.)
- [ ] Backup plan if you get stuck (know how to ask for help)

---

## 🎓 Expected Timeline

```
Week 1-2:  Platform basics & simple workflows (5-7 hrs/week)
Week 3-4:  Data handling & error management (6-8 hrs/week)
Week 5-8:  Security integrations & advanced workflows (6-8 hrs/week)
Week 9-13: Production deployment & SOAR system (8-10 hrs/week)

Total: ~300 hours for complete mastery
Or ~8 hours/week for 6 months
```

---

## 🚀 Next Steps

### Do This RIGHT NOW:
1. ✅ Set up n8n account
2. ✅ Clone this repository
3. ✅ Create your first workflow
4. ✅ Screenshot and celebrate! 🎉

### This Week:
- [ ] Complete Week 1 materials
- [ ] Build 3 simple workflows
- [ ] Take learning notes
- [ ] Ask if anything is unclear

### This Month:
- [ ] Complete all Phase 1 materials
- [ ] Build Phase 1 capstone project
- [ ] Document your learnings
- [ ] Help others in the community

---

## 💡 Pro Tips

### 1. **Build Constantly**
Don't just read—create workflows as you learn. Hands-on experience is essential.

### 2. **Test Thoroughly**
Always test error scenarios, not just happy paths. Real workflows must handle failures.

### 3. **Document Your Work**
Keep notes on what you learned. It helps retention and helps others.

### 4. **Use Real Data**
Practice with actual alert formats and tool responses (sanitized for privacy).

### 5. **Join the Community**
Share your progress, ask questions, help others. Learning together is more fun!

### 6. **Start Small**
Build simple workflows first. Add complexity gradually.

### 7. **Review Others' Code**
Study how others built their workflows. Learn different approaches.

### 8. **Practice Regularly**
Even 30 minutes daily beats 5 hours once a week.

---

## 📊 Your Learning Dashboard

Track your progress with this simple template:

```markdown
## My n8n Learning Progress

**Current Date:** [Date]
**Phase:** [1/2/3]
**Week:** [Week number]

### This Week's Goals
- [ ] Goal 1
- [ ] Goal 2
- [ ] Goal 3

### What I've Built
- Workflow 1: [Name]
- Workflow 2: [Name]

### Key Learnings
- Learning 1
- Learning 2

### Questions/Blockers
- Issue 1
- Issue 2

### Next Week's Focus
- Next topic
```

---

## 🎉 Welcome Aboard!

You're about to start an exciting journey in security automation. Welcome to the community!

**Remember:** Every expert was once a beginner. You've got this! 💪

---

## 📞 Need Help Before You Start?

Open an issue on GitHub with:
- What setup option you chose
- Any error messages
- What you've tried already
- Screenshot if possible

**We're here to help!** 🤝

---

**Ready? Let's go!** 🚀

👉 **Next Step:** Head to `01-beginner/00-platform-setup/README.md`

Good luck, and happy automating! 🔧✨
