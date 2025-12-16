# Contributing to n8n for Network Security

Thank you for your interest in contributing to this learning resource! We welcome contributions from security professionals, n8n enthusiasts, and learners at all levels.

---

## 📋 Table of Contents

- [How to Contribute](#how-to-contribute)
- [Contribution Guidelines](#contribution-guidelines)
- [Workflow Submission Requirements](#workflow-submission-requirements)
- [Documentation Standards](#documentation-standards)
- [Pull Request Process](#pull-request-process)
- [Code of Conduct](#code-of-conduct)

---

## How to Contribute

### Ways to Help

We're looking for contributions in many areas:

#### 1. **Add Workflows** ⭐ (Most Valuable)
- Create working n8n workflow examples
- Implement security use cases
- Share your own workflows
- Contribute workflow templates

#### 2. **Improve Documentation**
- Fix typos and clarity issues
- Add more detailed examples
- Create video tutorials
- Translate content to other languages

#### 3. **Report Issues & Bugs**
- Found an unclear section?
- Workflow not working for you?
- Missing information?
- Open an issue on GitHub

#### 4. **Share Knowledge**
- Write case studies of your implementations
- Document your learnings
- Share security automation best practices
- Contribute to the FAQ

#### 5. **Help Others**
- Answer questions in issues
- Review pull requests
- Test workflows and provide feedback
- Mentor other learners

---

## Contribution Guidelines

### Before You Start

1. **Check if it's needed**
   - Search existing issues and PRs
   - Check if workflow/doc already exists
   - Post an issue first for major changes

2. **Understand the scope**
   - Beginner-focused content (not advanced jargon)
   - Security-focused examples (relevant to use case)
   - Open-source friendly (reusable, shareable)
   - Well-documented (others can understand it)

3. **Respect existing structure**
   - Follow folder organization
   - Use naming conventions
   - Keep consistency with existing content

### General Rules

✅ **DO:**
- Keep content beginner-friendly
- Include security considerations
- Test everything before submitting
- Add comments to workflows
- Document your reasoning
- Be respectful and helpful
- Include examples and use cases

❌ **DON'T:**
- Promote specific commercial products
- Include proprietary code
- Create overly complex examples without explanation
- Submit untested workflows
- Use security vulnerabilities as examples (without mitigation)
- Copy content without attribution

---

## Workflow Submission Requirements

### When Submitting a Workflow

**Your workflow must include:**

1. **Working Workflow File** (`workflow-name.json`)
   - Exported from n8n
   - Tested and verified working
   - Includes comments explaining each node
   - Uses realistic example data

2. **Documentation File** (`workflow-name.md`)
   - Clear description of what it does
   - Use case explanation
   - Setup instructions
   - Expected inputs/outputs
   - Screenshot of successful run
   - Security considerations

3. **README** (if in subfolder)
   - Overview of workflows in folder
   - Prerequisites and setup
   - When to use each workflow
   - Links to related workflows

### Workflow File Format

```json
{
  "name": "Alert Triage Workflow",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "url": "=YOUR_SPLUNK_API_URL",
        "authentication": "headerAuth",
        "headerParameters": {
          "parameters": [
            {
              "name": "Authorization",
              "value": "Bearer {{ $credentials.splunk_api_key }}"
            }
          ]
        }
      },
      "name": "Receive Alert",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.1,
      "position": [
        250,
        300
      ],
      "description": "Receives alert from Splunk via webhook"
    }
  ],
  "connections": {},
  "active": true,
  "settings": {},
  "versionId": "123e4567-e89b-12d3-a456-426614174000",
  "meta": {
    "instanceId": "abc123"
  },
  "pinData": {}
}
```

### Documentation Template

Use this template for workflow documentation:

```markdown
# Workflow Name

## Overview
Brief description of what this workflow does.

## Use Case
When and why would you use this workflow?

## Prerequisites
- [ ] n8n instance running
- [ ] API key for [Service]
- [ ] Webhook URL accessible
- [ ] Other requirements

## Setup Instructions

### Step 1: Create Credentials
```bash
Instructions for setting up credentials
```

### Step 2: Import Workflow
1. Copy `workflow-name.json`
2. In n8n, click Import
3. Paste the JSON
4. Update credential references

### Step 3: Configure
1. Update webhook URL
2. Replace API keys
3. Modify field mappings if needed

## Inputs
- **Format:** JSON
- **Required Fields:**
  - `field1` (string): Description
  - `field2` (number): Description
- **Optional Fields:**
  - `field3` (boolean): Description

## Outputs
- **Format:** JSON
- **Fields:**
  - `status` (string): Success or error
  - `ticket_id` (string): Created ticket ID
  - `message` (string): Description

## Testing

### Test Data
```json
{
  "alert_id": "123",
  "severity": "high",
  "source": "splunk",
  "description": "Unusual login activity detected"
}
```

### Expected Result
```json
{
  "status": "success",
  "ticket_id": "INC0123456",
  "message": "Ticket created successfully"
}
```

## Security Considerations
- [ ] Credentials stored securely (use n8n credentials, not hardcoding)
- [ ] API calls use HTTPS/TLS
- [ ] Sensitive data not logged
- [ ] Rate limiting respected
- [ ] Input validation performed

## Troubleshooting
**Issue:** Workflow fails with authentication error
**Solution:** Verify API key has correct permissions

## Related Workflows
- [Alert Routing](../alert-routing.md)
- [Ticket Creation](../ticketing/ticket-creation.md)

## Author
Your name or GitHub handle

## Last Updated
December 2025
```

---

## Documentation Standards

### Writing Style
- **Be clear:** Explain concepts simply
- **Be specific:** Include actual examples
- **Be practical:** Focus on how-to, not theory
- **Be inclusive:** Assume beginner knowledge of n8n, advanced knowledge of security

### Code Examples
- Include actual code, not pseudo-code
- Test examples before submitting
- Add comments explaining complex lines
- Use realistic, sanitized data

### File Naming
- Use lowercase with hyphens: `my-workflow-name.md`
- Be descriptive: `alert-triage-system.md` ✅ vs `workflow.md` ❌
- Workflow files: `alert-triage-system.json`
- Folders: `01-platform-setup/`, `alert-ingestion/`

### Markdown Formatting
```markdown
# Main Heading (one per document)

## Section Heading

### Subsection Heading

**Bold for important terms**

`code` for inline code

\`\`\`json
code blocks with language
\`\`\`

- Bullet lists
- For multiple items

1. Numbered lists
2. For step-by-step

| Column 1 | Column 2 |
|----------|----------|
| Data     | Data     |

> Blockquotes for important notes
```

---

## Pull Request Process

### 1. Fork & Clone
```bash
git clone https://github.com/YOUR-USERNAME/n8n-for-network-security.git
cd n8n-for-network-security
```

### 2. Create Feature Branch
```bash
git checkout -b feature/your-feature-name
```

**Branch naming convention:**
- `feature/new-workflow-name`
- `fix/issue-description`
- `docs/documentation-improvement`
- `tutorial/topic-name`

### 3. Make Your Changes

Example folder structure for workflow contribution:
```
02-intermediate/01-security-integrations/workflows/
├── my-new-workflow.json
├── my-new-workflow.md
└── README.md (updated to list new workflow)
```

### 4. Commit with Clear Messages
```bash
git add .
git commit -m "Add alert triage workflow for SIEM integration

This workflow demonstrates how to automatically triage security
alerts from a SIEM system by enriching with threat intel and
routing to appropriate teams.

- Ingests alerts via webhook
- Enriches with VirusTotal data
- Routes based on severity
- Creates tickets for high-severity alerts

Fixes #42"
```

### 5. Push & Create Pull Request
```bash
git push origin feature/your-feature-name
```

Then on GitHub:
1. Click "Create Pull Request"
2. Fill out the PR template (see below)
3. Link related issues
4. Request review from maintainers

### PR Template

```markdown
## Description
Brief description of what this PR adds/fixes.

## Type of Change
- [ ] New workflow
- [ ] Documentation improvement
- [ ] Bug fix
- [ ] New feature
- [ ] Other: _____

## Related Issues
Fixes #123

## Testing
- [ ] Tested on n8n cloud
- [ ] Tested on self-hosted n8n
- [ ] Works with sample data provided
- [ ] Tested error scenarios

## Workflow Details (if applicable)
- **Nodes Used:** List here
- **Integrations:** Tools/APIs used
- **Data Format:** JSON/CSV/other
- **Execution Time:** ~X seconds

## Screenshots
Add screenshots of working workflow if helpful

## Checklist
- [ ] Documentation is clear and complete
- [ ] Workflow is tested and working
- [ ] Comments added to complex nodes
- [ ] No hardcoded credentials
- [ ] No proprietary code
- [ ] Follows existing style/standards
```

### 6. Address Feedback
- Reviewers may request changes
- Respond to comments
- Make requested changes
- Re-request review

### 7. Merge
Once approved, your contribution will be merged! 🎉

---

## Documentation Standards for Pull Requests

### Before Submitting

- [ ] Spell-checked (use spell-checker tool)
- [ ] Grammar reviewed
- [ ] Links tested and working
- [ ] Code examples tested
- [ ] Images/screenshots included (if helpful)
- [ ] Follows existing documentation style
- [ ] Beginner-friendly language
- [ ] No sensitive information (IPs, API keys, etc.)

### For Workflow Submissions

- [ ] Workflow file is valid JSON (can be imported)
- [ ] Documentation file included
- [ ] Security considerations documented
- [ ] At least 2 test cases provided
- [ ] Error handling shown
- [ ] Uses proper credential references (not hardcoded)
- [ ] Related workflows linked

---

## Code of Conduct

### Our Commitment
We are committed to providing a welcoming, inclusive, and safe community for everyone.

### Expected Behavior
- **Be Respectful:** Treat all people with respect and kindness
- **Be Helpful:** Share knowledge generously and help others learn
- **Be Patient:** Remember everyone is at different learning levels
- **Be Professional:** Keep discussions constructive and on-topic
- **Give Credit:** Acknowledge others' contributions and ideas

### Unacceptable Behavior
- Harassment, discrimination, or hostile language
- Spam or self-promotion
- Sharing of credentials or sensitive data
- Promoting illegal or unethical practices
- Spreading misinformation

### Reporting Issues
If you experience or witness unacceptable behavior:
1. Document what happened
2. Report to project maintainers
3. We'll investigate and take appropriate action

---

## Questions?

### Getting Help

1. **Check the FAQ:** `docs/faq.md`
2. **Search Issues:** GitHub Issues for similar questions
3. **Ask in Forum:** [n8n Community](https://community.n8n.io/)
4. **Open an Issue:** Create a discussion issue on GitHub

### Contact
- GitHub Issues: For bugs and features
- Discussions: For questions and ideas
- Email: Maintainers contact info (if available)

---

## Recognition

### Contributors
All contributors are recognized in:
- `README.md` contributors section
- Individual files where they contributed
- Special mention in release notes for major contributions

### Levels
- **Beginner:** First 2 contributions
- **Regular:** 5+ contributions
- **Expert:** 10+ contributions or subject matter expert

---

## Contributor License Agreement

By contributing, you agree that:
- Your contributions are your own work
- You grant the project a license to use your contributions
- Your contributions can be used under the MIT license
- You have permission to contribute the content

---

## What's Next?

1. **Pick something to contribute**
   - Check "Good First Issue" label
   - Look at open issues
   - Add a workflow you've created

2. **Get familiar with the repo**
   - Review existing structure
   - Read similar contributions
   - Check PR standards

3. **Create and test**
   - Work on your contribution
   - Test thoroughly
   - Document clearly

4. **Submit & engage**
   - Create PR with clear description
   - Respond to feedback
   - Help refine the content

5. **Celebrate!** 🎉
   - Your contribution helps hundreds of people
   - Join our community of contributors

---

## Thank You! 🙏

Your contributions make this learning resource better for everyone. Whether it's a small documentation fix or a complete workflow, we appreciate your effort!

**Happy contributing!**

---

**Last Updated:** December 2025  
**Questions?** Open an issue on GitHub!
