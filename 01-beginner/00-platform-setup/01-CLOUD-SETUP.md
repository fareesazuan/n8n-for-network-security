# Cloud Setup Guide: n8n Cloud in 5 Minutes

## Get Started Instantly (No Installation Required)

This is the **fastest way to get n8n running**. Perfect for learning and testing.

---

## ✅ What You'll Get

- ✅ Free n8n account
- ✅ Instant access to web editor
- ✅ Built-in example workflows
- ✅ No installation needed
- ✅ 10 active workflows free tier
- ✅ Ready to build in 5 minutes

---

## ⏱️ 5-Minute Setup

### Step 1: Visit n8n Cloud (2 min)
1. Go to **[n8n.cloud](https://n8n.cloud)**
2. Click **"Start Free"** button
3. Sign up with:
   - Email address
   - Strong password
   - Accept terms

### Step 2: Verify Email (1 min)
1. Check your email inbox
2. Click verification link
3. Wait for redirect (may take 30 seconds)

### Step 3: First Login (2 min)
1. You'll see the n8n editor
2. Click **"+ New"** to create first workflow
3. Name it: "Hello World"
4. You're ready to build!

---

## 🎯 Verify Your Setup Works

### Quick Test Workflow:
1. Add **Manual Trigger** node
   - Click **"+"** on canvas
   - Search "Manual Trigger"
   - Click to add

2. Add **Debug** node
   - Search "Debug"
   - Connect to Manual Trigger

3. Click **"Execute Workflow"**
   - You should see "Execution succeeded"
   - Check Debug output

**Success! You have working n8n.** 🎉

---

## 🔐 Security: First Steps

### Step 1: Enable 2FA (Recommended)
1. Click your profile icon (top right)
2. Select **"Settings"**
3. Go to **"Account"**
4. Enable **Two-Factor Authentication**

### Step 2: Create Your First Credential
1. Click **"Credentials"** (top left dropdown)
2. Click **"+ New"**
3. Choose **"Slack"** (or any service)
4. Add your credential
5. Test connection

**Remember:** Credentials are encrypted in n8n. Never paste raw tokens.

---

## 📊 Cloud Tier Limits

### Free Tier (Perfect for Learning):
- ✅ 10 active workflows
- ✅ 1,000 executions/month
- ✅ Unlimited workflow size
- ✅ Basic support
- ❌ No custom domains
- ❌ No advanced features

### Pro Tier ($50/month, if you want):
- ✅ Unlimited active workflows
- ✅ Unlimited executions
- ✅ Priority support
- ✅ Custom domain

**For learning: Free tier is perfect!**

---

## 🌐 URL Pattern for Webhooks

When you create a webhook trigger in n8n Cloud, your URL will be:

```
https://your-instance.n8n.cloud/webhook/your-webhook-name
```

**Example:**
```
https://myinstance.n8n.cloud/webhook/security-alerts
```

You'll use this URL to receive data from external services.

---

## 📱 Accessing Your Instance

### After Setup, You Can:
1. ✅ **Access from anywhere** - Just log in to n8n.cloud
2. ✅ **Use mobile browser** - Responsive design works on phones
3. ✅ **Share workflows** - Export/import JSON
4. ✅ **View execution history** - See all runs and results

---

## ✨ Your First Workflow (10 minutes)

Let's build something useful:

### Alert Notifier Workflow:
1. **Add nodes:**
   - Webhook Trigger (receives alert)
   - Set Node (extract data)
   - Slack Node (send message)

2. **Configure webhook:**
   - Set path: "security-alert"
   - Copy the webhook URL

3. **Configure Slack node:**
   - Add Slack credential
   - Select channel
   - Build message

4. **Test with curl:**
   ```bash
   curl -X POST https://your-instance.n8n.cloud/webhook/security-alert \
     -H "Content-Type: application/json" \
     -d '{"severity": "high", "alert": "Suspicious login"}'
   ```

5. **Check Slack** - Message should appear! 🎉

---

## 🆘 Troubleshooting

### Issue: Can't log in
**Solution:**
- Check email spelling
- Reset password
- Check spam folder for verification email

### Issue: Webhook not triggering
**Solution:**
- Check webhook path is exact
- Make sure workflow is active (toggle switch)
- Check execution history for errors

### Issue: Slow performance
**Solution:**
- Refresh browser
- Check internet connection
- Try incognito mode
- Cloud might be busy (try later)

### Issue: Credential not working
**Solution:**
- Double-check token/key
- Verify permissions in original service
- Test connection before saving
- Use correct credential type

---

## 🚀 Next Steps

### Today:
- ✅ Set up account
- ✅ Create hello world workflow
- ✅ Enable 2FA

### This Week:
- ✅ Build notification workflow
- ✅ Create webhook endpoint
- ✅ Connect to Slack or email

### Next Week:
- ✅ Build more complex workflows
- ✅ Integrate with security tools
- ✅ Move to Phase 2

---

## 💡 Cloud Workflow Best Practices

### Do:
✅ Test with sample data first  
✅ Use credentials (never hardcode)  
✅ Enable error handling  
✅ Monitor execution history  
✅ Document your workflows  

### Don't:
❌ Hardcode API keys  
❌ Store sensitive data in workflow  
❌ Skip error handling  
❌ Expose raw data in logs  
❌ Share credentials  

---

## 🔗 Useful Links

- [n8n Cloud Home](https://n8n.cloud)
- [Documentation](https://docs.n8n.io/)
- [Community Forum](https://community.n8n.io/)
- [Status Page](https://status.n8n.io/)

---

## 🎓 Ready to Learn?

You have n8n up and running! 🎉

### Next:
👉 Read `01-core-concepts/architecture-overview.md` to understand how n8n works

Or start building:
👉 Follow `02-first-workflow/manual-trigger-workflow.md`

---

**Congratulations on setting up n8n Cloud!**

You're now ready to build workflows. Let's create something awesome! 🚀

---

**Last Updated:** December 2025  
**Status:** Cloud Setup Complete  
**Next:** Learn Core Concepts

Happy Automating! 🤖
