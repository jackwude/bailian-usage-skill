# bailian-usage Skill

让你的 OpenClaw 助手自动查询阿里云百炼 Coding Plan 的剩余额度。

再也不用手动登录控制台查用量了。问一句，它直接告诉你结果。

---

## 你能得到什么

- 套餐状态和剩余天数
- 用量明细：近 5 小时、近一周、近一月
- 套餐包含的可用模型列表

## 为什么做这个

我受够了每次想看剩余额度都要登录百炼控制台。数据明明就在页面上，为什么非得点进 dashboard 才能看到？

这个技能把麻烦的部分自动化。你问，它查，你继续干活。

## 安装

```bash
git clone https://github.com/jackwude/bailian-usage-skill.git
cp -r bailian-usage-skill/bailian-usage ~/.openclaw/workspace/skills/
```

然后在 `~/.openclaw/workspace/TOOLS.md` 里添加你的账号：

```markdown
## 🔐 阿里云百炼账号
- **账号**: your-email@example.com
- **密码**: your-password
```

## 使用方法

发以下任意命令给你的助手：

- "查百炼额度"
- "百炼用量"
- "看看阿里云还剩多少额度"
- "Check my Bailian quota"

它会返回类似这样的结果：

```
## 📊 百炼 Coding Plan 套餐详情

**套餐状态：** ✅ 生效中 | 剩余 **18 天**（2026-04-03 到期）
**自动续费：** ❌ 未开启

**用量消耗：**
- 近 5 小时：48%
- 近一周：42%
- 近一月：39%

**用量分析：** ✅ 用量充足
```

## 技术实现

这个技能用的是 OpenClaw 内置的 `browser` 工具 —— 不是 Playwright，不是 Selenium，没有任何外部依赖。

**为什么？** 因为我一开始试的是 Playwright。它一直被登录弹窗的 iframe 卡住（跨域限制）。browser tool 直接在页面上下文里执行 JavaScript，没这个问题。

说白了：能用，不折腾。

## 可能遇到的问题

- **滑块 / 短信验证：** 如果阿里风控触发了，你需要手动完成一次验证。之后就正常了。
- **需要浏览器环境：** 这个技能在真实浏览器里跑，所以需要图形界面（macOS、Linux with X11、Windows）。
- **数据延迟：** 用量数据来自百炼后端，可能有几分钟延迟 —— 不是 bug，人家系统就这样。

## 安全性

你的账号密码存在本地的 `TOOLS.md` 里，不会发给任何地方 —— 除了阿里云的登录页面（不然怎么登录呢）。

不保存 cookies。每次查询都是全新登录 —— 更简单，而且少一个可能出问题的环节。

## 许可证

MIT 协议。随便用，随便改，随便折腾。

---

**发现 bug？** 提个 issue。**改得更好了？** 发个 PR。我对这东西没啥执念，好用就行。
