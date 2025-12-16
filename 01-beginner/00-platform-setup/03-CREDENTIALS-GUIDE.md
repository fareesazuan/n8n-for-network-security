# Credentials Management: Secure Your API Keys

## How to Store & Use API Keys Safely in n8n

This guide teaches you the **right way** to handle credentials so your workflows are secure.

---

## ⚠️ The Critical Rule

### ❌ NEVER DO THIS:

```
❌ Hardcode API keys in workflows
❌ Put credentials in workflow JSON
❌ Share credentials in messages/Slack
❌ Store plain text passwords anywhere
❌ Use same key for multiple services
❌ Leave credentials in version control
```

### ✅ ALWAYS DO THIS:

```
✅ Use n8n Credentials system
✅ Store each credential once, reuse everywhere
✅ Rotate credentials regularly
✅ Use strong, unique passwords
✅ Enable 2FA on accounts with credentials
✅ Keep credentials database safe
```

---

## 🎯 What Are n8n Credentials?

**Credentials** are stored API keys, passwords, and tokens that n8n can use without you entering them every time.

Think of it like:
```
Your workflow says: "Use the Slack credential"
   ↓
n8n looks up: "Slack credential = xoxb-YOUR-REAL-TOKEN"
   ↓
n8n uses that token securely (never shown in workflow)
   ↓
Your workflow stays safe even if someone sees it
```

---

## 📋 Credential Types You'll Use

| Service | Credential Type | Where to Get |
|---------|-----------------|--------------|
| **Slack** | OAuth2 or Token | Slack App settings |
| **Google** | OAuth2 | Google Cloud Console |
| **Webhook** | HTTP Basic/Bearer | Your API docs |
| **Splunk** | API Token | Splunk settings |
| **ServiceNow** | OAuth2 | ServiceNow developer |
| **VirusTotal** | API Key | VirusTotal account |
| **Email** | SMTP credentials | Email provider |

---

## 🔐 Creating Your First Credential

### Step 1: Find Your API Key/Token

Example: Getting a Slack bot token

```
1. Go to https://api.slack.com/apps
2. Create new app or select existing
3. Go to "Bot Token Scopes"
4. Add permissions you need
5. Copy the Bot User OAuth Token (starts with xoxb-)
6. Keep it secret!
```

### Step 2: Add to n8n

**In n8n UI:**

```
1. Click "Credentials" (top left menu)
2. Click "+ New"
3. Select service (e.g., "Slack")
4. Enter credential details:
   - Name: "Slack - Security Team"
   - Token: (paste your token here)
5. Click "Create"
6. n8n encrypts and stores it
```

**Now you can use this credential in any workflow!**

### Step 3: Use in Workflow

```
1. Add Slack node to your workflow
2. Select "Credential" field
3. Choose "Slack - Security Team"
4. Node automatically uses that token
5. Your workflow never shows the token
```

---

## 📝 Best Practices by Service

### Slack
```
⚠️ Token starts with: xoxb- (bot) or xoxp- (user)
✅ Create separate bot for workflows
✅ Limit permissions to what's needed
✅ Regenerate if token is leaked
❌ Never paste token in messages
```

### Google
```
⚠️ Use OAuth2 (safer than API key)
✅ Create service account for automation
✅ Grant minimal permissions needed
✅ Review access logs monthly
❌ Don't use personal account
```

### API Keys (Generic)
```
⚠️ Store in n8n Credentials
✅ Use Bearer token if supported
✅ Rotate every 90 days
✅ Create separate key per service
❌ Don't reuse keys
```

### Webhooks
```
⚠️ Validate incoming data
✅ Use HTTPS for webhook URLs
✅ Add secret/token to URL if possible
✅ Log all webhook calls
❌ Trust external data blindly
```

---

## 🚨 Security Checklist

Before deploying any workflow:

- [ ] All credentials stored in n8n (not in workflow JSON)
- [ ] Each service has unique credential
- [ ] Credentials have descriptive names
- [ ] No hardcoded tokens/keys visible in workflow
- [ ] Webhook URLs are HTTPS (not HTTP)
- [ ] Input validation is configured
- [ ] Execution logs don't expose credentials
- [ ] Team members know not to share credentials

---

## 🔄 Managing Multiple Credentials

### Scenario: Multiple Slack Workspaces

```
Instead of:
❌ Slack token 1: xoxb-...
❌ Slack token 2: xoxb-...
❌ (mixed and confusing)

Do this:
✅ Create separate credentials:
   - "Slack - Security Team Bot"
   - "Slack - Engineering Ops Bot"
   - "Slack - Finance Team Bot"

Then in workflows:
✅ Each workflow uses right credential by name
✅ Easy to see which workspace is used
✅ Easy to rotate one credential without affecting others
```

---

## 🔄 Rotating Credentials (Important!)

When should you rotate?
- ✅ Regularly (every 90 days is good)
- ✅ After security incident
- ✅ When someone leaves team
- ✅ If token is accidentally exposed
- ✅ After major workflow changes

How to rotate safely:

```
Step 1: Generate new token in the service
        (e.g., Slack app settings)

Step 2: In n8n, update credential:
        - Click Credentials
        - Find the credential
        - Click "Edit"
        - Paste new token
        - Click "Save"

Step 3: Test workflows that use it
        - Create a test workflow
        - Execute and verify it works
        - Check results

Step 4: Retire old token
        - Go back to the service
        - Delete/revoke old token
        - Confirm in logs it's no longer used
```

---

## 🚨 If Credentials Are Exposed

**If a token/key is accidentally revealed:**

1. **Immediately revoke it**
   ```
   Go to the service, regenerate/delete the token
   Do this FIRST - don't wait!
   ```

2. **In n8n, update the credential**
   ```
   Paste the new token
   Save
   Test workflows
   ```

3. **Check logs for misuse**
   ```
   Did anyone use the old token?
   Check the service's activity logs
   ```

4. **Document the incident**
   ```
   When was it exposed?
   How was it exposed?
   Was it used maliciously?
   What did you do to fix it?
   ```

---

## 🔍 Viewing Credentials (Safely)

### See What You Have:
```
In n8n:
1. Click "Credentials" menu
2. See all your stored credentials
3. Click credential to edit
   (but can't see the token - encrypted!)
```

### Check What's Used Where:
```
1. Go to credential
2. Scroll down to "Used in workflows"
3. See which workflows use this credential
4. Helps find impact if credential needs rotating
```

---

## 💡 Example Workflow with Credentials

### Simple Alert → Slack Workflow:

```
[Webhook receives alert]
    ↓
[Extract alert details]
    ↓
[Slack node with "Slack - Security Team" credential]
    ↓
[Sends message to #security-alerts]

The workflow JSON looks like:
{
  "nodes": [
    {
      "type": "slack",
      "credential": "Slack - Security Team",
      ...
    }
  ]
}

Not:
{
  "token": "xoxb-REAL-TOKEN-HERE"  ❌ BAD!
}
```

---

## 🛡️ Advanced: Credential-only Workflows

Some workflows should only have one purpose: store credentials for reuse.

But in n8n, every workflow stores credentials separately. The right approach is:

```
✅ Store each credential once in "Credentials" section
✅ Reference in any workflow that needs it
✅ Credentials are encrypted at rest
✅ Credentials not visible in workflow code
```

---

## 🆘 Troubleshooting

### Issue: "Credential not found"
```
Solution:
1. In workflow node, check Credentials dropdown
2. Verify credential is listed
3. Try deleting and re-adding credential
4. Ensure you have permission to use it
```

### Issue: "Unauthorized" when running workflow
```
Solution:
1. Verify credential is correct
2. Check token hasn't expired
3. Verify account still has permissions
4. Try rotating the credential
5. Check service logs for blocks
```

### Issue: Cant remember what a credential is for
```
Solution:
1. Name credentials clearly:
   ✅ "Slack - Security Team Bot"
   ✅ "Splunk - Production API"
   ✅ "ServiceNow - Incident Creation"
   
   Not:
   ❌ "Slack 1"
   ❌ "api_token"
   ❌ "temp"
```

---

## 📋 Credential Template

When creating a new credential, fill this out first:

```
Service Name: [e.g., Slack]
Credential Name: [e.g., "Slack - Security Team"]
Purpose: [What workflows use this?]
Token/Key Location: [Where to get it]
Expiration Date: [When to rotate]
Created Date: [When created]
Last Rotated: [When last changed]
Used in Workflows: [List workflows]
```

---

## 🎓 Learning Outcomes

By end of this section, you should:

✅ Never put API keys in workflow JSON  
✅ Know how to create n8n credentials  
✅ Know how to use credentials in workflows  
✅ Understand credential rotation  
✅ Know what to do if credentials leak  
✅ Feel confident keeping n8n secure  

---

## 🔗 Resources

- [n8n Credentials Docs](https://docs.n8n.io/credentials/)
- [n8n Security Guide](https://docs.n8n.io/hosting/securing/)
- Service-specific guides:
  - [Slack API](https://api.slack.com/)
  - [Google Cloud](https://cloud.google.com/docs/)
  - [Splunk API](https://dev.splunk.com/)

---

## ✨ Next Steps

### Now That You Know Credentials:

1. ✅ Create your first credential (Slack or similar)
2. ✅ Test using it in a workflow
3. ✅ See how it's never shown in the workflow
4. ✅ Feel secure about your automations

### Coming Next:
- Learn core concepts (nodes, triggers)
- Create your first workflow
- Use credentials in real workflows
- Build your first automation!

---

**Last Updated:** December 2025  
**Status:** Credentials Guide Complete  
**Next:** Core Concepts & Your First Workflow

You're doing great! 🚀
