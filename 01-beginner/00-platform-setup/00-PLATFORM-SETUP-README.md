# 00 Platform Setup: Choose Your Path

## Getting n8n Running - Free Options Only

Welcome to Platform Setup! This section helps you choose between **n8n Cloud (free tier)** or **self-hosted (free, open-source)** and get running quickly.

---

## 📋 This Section Covers

- ✅ What are your setup options?
- ✅ Cloud setup (5 minutes, free)
- ✅ Self-hosted setup (15 minutes, free)
- ✅ Credentials management (security first)
- ✅ Verification that everything works
- ✅ Troubleshooting if something breaks

**Time to complete:** 30-45 minutes total  
**Cost:** $0 (completely free)  
**Prerequisites:** None!

---

## 🎯 Quick Comparison: Cloud vs Self-Hosted

| Feature | n8n Cloud (Free) | Self-Hosted (Free) |
|---------|------------------|-------------------|
| **Setup time** | 5 min | 15 min |
| **Cost** | $0 | $0 |
| **Data location** | n8n servers | Your server/VPS |
| **Technical knowledge** | Beginner | Intermediate |
| **Internet required** | Always | Always |
| **Best for** | Learning first | Production later |
| **Workflows limit** | 10 active | Unlimited |
| **Executions/month** | 1,000 free | Unlimited |
| **Scalability** | Pay to upgrade | Add resources |

---

## 🚀 Choose Your Path

### Path A: Cloud Setup (Fastest - 5 minutes)
**Perfect if:**
- ✅ You want to start immediately
- ✅ You're learning and don't have a VPS
- ✅ You want zero setup complexity
- ✅ You're comfortable with cloud services

👉 **Next:** Go to `cloud-setup.md`

---

### Path B: Self-Hosted Setup (More Control - 15 minutes)
**Perfect if:**
- ✅ You have a Linux VPS (DigitalOcean, Linode, AWS, etc.)
- ✅ You want data on your own server
- ✅ You're learning DevOps concepts
- ✅ You plan to use this for production

👉 **Next:** Go to `self-hosted-setup.md`

---

## 💡 Decision Guide

### Use Cloud If:
1. You don't have a VPS
2. You're on Windows/Mac without Docker
3. You want the absolute fastest start
4. You want n8n to handle all infrastructure
5. You prefer someone else managing updates

### Use Self-Hosted If:
1. You have a VPS (even $5/month)
2. You want data on your own hardware
3. You're learning Docker/Linux
4. You need unlimited workflows/executions
5. You want complete control

---

## 🔐 Security First: What You Need to Know

### Cloud (n8n Cloud):
✅ **Good security by default**
- Credentials stored encrypted
- HTTPS/TLS included
- n8n manages backups
- Regular security updates

⚠️ **Your responsibility:**
- Use strong password
- Enable 2FA
- Don't share credentials
- Review execution history

### Self-Hosted:
✅ **Maximum control**
- You own all infrastructure
- Data stays on your server
- No data sent to n8n servers

⚠️ **Your responsibility:**
- Keep OS/Docker updated
- Use HTTPS/TLS
- Manage backups
- Monitor security logs

---

## 📁 What's in This Section

```
00-platform-setup/
├── README.md                    ← You are here
├── cloud-setup.md               ← 5-minute cloud guide
├── self-hosted-setup.md         ← 15-minute self-hosted guide
└── credentials-guide.md         ← Managing credentials safely
```

---

## ✅ After This Section, You'll Have:

- [ ] Chosen your platform (cloud or self-hosted)
- [ ] n8n running and accessible
- [ ] First login successful
- [ ] Understanding of credentials
- [ ] Ready to create your first workflow

---

## 🎓 Learning Outcomes

### By End of This Section:
✅ Know the difference between cloud and self-hosted  
✅ Have n8n installed and working  
✅ Can log in to n8n  
✅ Understand where to find your URL/endpoint  
✅ Know how credentials work  
✅ Ready for Week 1 Day 2  

---

## 📊 Time Breakdown

| Task | Time | Notes |
|------|------|-------|
| Read this overview | 5 min | You're doing it now |
| Setup (choose one path) | 5-15 min | Cloud is faster |
| Verify it works | 5-10 min | Test login |
| Read credentials guide | 5-10 min | Security important |
| **Total** | **20-40 min** | You decide the pace |

---

## 🆘 Troubleshooting This Section

### "I don't have a VPS"
→ Use **Cloud Setup** (Path A)

### "I have a VPS but no Docker"
→ Use **Cloud Setup** temporarily, then install Docker on VPS later

### "What VPS should I use?"
→ Popular free/cheap options:
- DigitalOcean ($5/month basic droplet)
- Linode ($5/month)
- AWS EC2 (free tier 1 year)
- Hetzner (€4/month)
- Vultr ($6/month)

### "Can I switch between cloud and self-hosted?"
→ Yes! Start with cloud, move to self-hosted later (workflows can be exported/imported)

---

## 🔗 Quick Links in This Section

1. **Cloud Setup Guide** → `cloud-setup.md`
   - 5-minute quick start
   - No installation needed
   - Best for beginners

2. **Self-Hosted Setup Guide** → `self-hosted-setup.md`
   - 15-minute Docker setup
   - For VPS users
   - More control and scalability

3. **Credentials Guide** → `credentials-guide.md`
   - How to safely store API keys
   - Best practices
   - Security considerations

---

## 📝 Next Steps (Choose One)

### If using Cloud (Recommended for now):
```
1. Open cloud-setup.md
2. Follow the 5-minute guide
3. Create your first n8n account
4. Come back and read credentials-guide.md
5. You're done with setup! 🎉
```

### If using Self-Hosted:
```
1. Ensure you have VPS access
2. Open self-hosted-setup.md
3. Follow the Docker setup
4. Wait 1-2 minutes for startup
5. Come back and read credentials-guide.md
6. You're done with setup! 🎉
```

---

## 💡 Pro Tips

**Tip 1: Start Simple**
- Use cloud first to learn n8n
- Switch to self-hosted when comfortable

**Tip 2: Test Everything**
- After setup, create a test workflow
- Make sure you can execute it
- Verify you see results

**Tip 3: Document Your Setup**
- Write down your n8n URL
- Save your login details (use password manager!)
- Note any custom configuration

**Tip 4: Security Mindset**
- Enable 2FA if available
- Use strong, unique passwords
- Never hardcode API keys in workflows

---

## ⏱️ Time Estimate for Phase 1

```
Week 1 Timeline:
├─ Today: Platform Setup (30-45 min)
├─ Tomorrow: Create first workflow (1 hour)
├─ Day 3: Understand triggers (1 hour)
└─ Days 4-7: Practice & Day 1-3 review

Total Week 1: 4-5 hours
```

---

## 🎯 What Comes Next

Once you complete this section:

**Day 2:** Learn core concepts
- What is a node?
- What is a trigger?
- How does data flow?

**Days 3-4:** Create first workflows
- Manual trigger
- Webhook trigger
- Scheduled trigger

**Days 5-7:** Practice and projects
- Build notification workflow
- Build alert router
- Complete Week 1 project

---

## 🤝 Getting Help

### If Setup Fails:
1. Check the troubleshooting section in the specific guide
2. Read the official n8n docs
3. Ask in n8n community forum
4. Open an issue on GitHub (our learning repo)

### Resources:
- 📖 [n8n Official Docs](https://docs.n8n.io/)
- 💬 [n8n Community Forum](https://community.n8n.io/)
- 🎥 [n8n YouTube](https://www.youtube.com/@n8nio)
- 📚 [This Learning Repository](https://github.com/yourusername/n8n-for-network-security)

---

## ✨ You're Ready!

You've chosen your path. Now:

**Cloud Users:** 👉 Open `cloud-setup.md` (5 minutes to running n8n)

**Self-Hosted Users:** 👉 Open `self-hosted-setup.md` (15 minutes to running n8n)

**Then all:** 👉 Read `credentials-guide.md` (understand security)

---

## 📋 Section Checklist

Before moving to next section, confirm:
- [ ] You've read this overview
- [ ] You've chosen cloud or self-hosted
- [ ] You've followed the setup guide for your choice
- [ ] n8n is running and you can log in
- [ ] You've read the credentials guide
- [ ] You understand how to store API keys safely
- [ ] You're ready to create your first workflow

---

**Once everything above is checked, you're done with platform setup!** 🎉

**Next stop:** `01-core-concepts/` to learn what workflows actually are.

---

**Last Updated:** December 2025  
**Status:** Complete  
**Next Section:** Core Concepts (what is n8n, nodes, triggers)

Good luck with setup! 🚀
