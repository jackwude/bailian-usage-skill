# bailian-usage Skill

Your OpenClaw agent can now check your Alibaba Cloud Bailian Coding Plan quota — automatically.

No more manual dashboard logins. Just ask, and it tells you exactly where you stand.

---

## What You Get

- Subscription status and days remaining
- Usage breakdown: last 5 hours, 1 week, 1 month
- Which models your plan includes

## Why I Built This

I got tired of logging into the Bailian console every time I wanted to check my quota. The data's right there on the page — why should I have to click through a dashboard to see it?

This skill automates the boring part. You ask, it checks, you move on.

## Installation

```bash
git clone https://github.com/jackwude/bailian-usage-skill.git
cp -r bailian-usage-skill/bailian-usage ~/.openclaw/workspace/skills/
```

Then add your credentials to `~/.openclaw/workspace/TOOLS.md`:

```markdown
## 🔐 Alibaba Cloud Bailian Account
- **Email**: your-email@example.com
- **Password**: your-password
```

## Usage

Ask your agent any of these:

- "查百炼额度"
- "百炼用量"
- "看看阿里云还剩多少额度"
- "Check my Bailian quota"

It'll respond with something like:

```
## 📊 Bailian Coding Plan Details

**Status:** ✅ Active | **18 days remaining** (expires 2026-04-03)
**Auto-renewal:** ❌ Disabled

**Usage:**
- Last 5 hours: 48%
- Last 1 week: 42%
- Last 1 month: 39%

**Verdict:** ✅ Plenty of quota left
```

## Under the Hood

This skill uses OpenClaw's built-in `browser` tool — not Playwright, not Selenium, nothing external.

**Why?** Because I tried Playwright first. It kept choking on the login iframe (cross-origin restrictions). The browser tool evaluates JavaScript directly in the page context, so none of that applies.

Translation: it just works.

## What Could Go Wrong

- **CAPTCHA / SMS verification:** If Alibaba's fraud detection kicks in, you'll need to complete it manually once. After that, you're good.
- **Browser required:** This runs in a real browser, so you need a graphical environment (macOS, Linux with X11, or Windows).
- **Data lag:** The usage numbers come from Bailian's backend. They might be a few minutes behind — not a bug, just how their system works.

## Security

Your credentials stay in `TOOLS.md` on your machine. They're never sent anywhere except directly to Alibaba's login page (which is... kind of the point).

No cookies are saved. Every query does a fresh login — simpler, and one less thing to debug when it breaks.

## License

MIT. Use it, break it, fix it, whatever.

---

**Found a bug?** Open an issue. **Made it better?** Send a PR. I'm not precious about this thing.
