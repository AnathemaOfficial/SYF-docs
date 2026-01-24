---
status: canonical
version: 1.0
author: AnathemaOfficial
last_updated: 2026-01-24
tags: [education, communication, anathema]
---

# Anathema Soft — Human Explanation Cheatsheet

This file exists to explain Anathema Soft to humans
(CTOs, engineers, decision-makers) without losing them.

---

## Core Idea (Simple)

Anathema Soft controls **how much a system can act**,  
not **who is allowed to act**.

---

## What to Say First (Safe Entry)

- "Anathema Soft is an action control system."
- "It limits action capacity, not access."
- "It assumes breach and limits impact."

---

## Key One-Liners (Use These)

| Situation | Line |
|-----------|------|
| Opening | "Assume breach. Limit impact." |
| Technical | "It's not about preventing access, it's about preventing irreversible damage." |
| Comparison | "Firewalls try to stop attacks. We limit how much damage is possible." |
| Skeptic | "Even with a stolen key, the system can't do much." |
| AI context | "Intelligence never grants unlimited action." |

---

## What It Is (Human Version)

- A system that enforces **hard limits on action**
- Independent of identity, roles, or permissions
- Based on time, budget, and exhaustion
- Automatically self-closing

---

## What It Is NOT (Important)

| Not This | Why |
|----------|-----|
| Firewall | Doesn't block entry |
| IAM | Doesn't care about identity |
| Policy engine | No rules to configure |
| Monitoring | Doesn't watch behavior |
| Trust-based | Assumes no trust |
| Alignment-based | No intent analysis |

---

## The Honest Line (After They're Hooked)

> "So technically, it's not a protection layer.
> It's a system that removes unsafe actions from the set of things that can happen."

---

## Example That Always Works

> "If a production key is stolen,
> the attacker can't drain the system.
> The system physically can't do more than a small, predefined amount of action."

---

## The Mental Model

| Permissions say: | Anathema says: |
|------------------|----------------|
| "You may act." | "You may act a little, for a short time, and then it stops." |

---

## Visual Comparison

```
Traditional Security:
┌─────────────────────────────────────┐
│  WHO can do WHAT?                   │
│  → Check identity                   │
│  → Check permissions                │
│  → Allow or deny                    │
└─────────────────────────────────────┘

Anathema:
┌─────────────────────────────────────┐
│  HOW MUCH can happen RIGHT NOW?     │
│  → Read system capacity (R)         │
│  → Derive action budget             │
│  → Gate at point of effect          │
└─────────────────────────────────────┘
```

---

## For the Security-Minded

| Classic Question | Anathema Answer |
|------------------|-----------------|
| "Who is attacking?" | "Doesn't matter." |
| "What's their intent?" | "Doesn't matter." |
| "How did they get in?" | "Doesn't matter." |
| "What can they do?" | "Very little, for a short time." |

---

## For the Engineering-Minded

```
// Traditional
if (user.hasPermission(action)) {
    execute(action);
}

// Anathema
let budget = derive_budget(read_R());
if (action.cost <= budget) {
    execute(action);
} else {
    deny();
}
```

---

## FAQ for Humans

**Q: So anyone can do anything?**  
A: Anyone can *try*. But actions are capped by physics, not policy.

**Q: What if they're patient?**  
A: Patience doesn't accumulate budget. Each moment is independent.

**Q: What's the worst case?**  
A: System goes inert. No catastrophic damage possible.

**Q: Do we still need auth?**  
A: Yes, for accountability. Not for safety.

---

## Final Line (If You Want to Land It)

> "It's not about keeping bad things out.
> It's about making sure nothing can do too much damage, even if it's already inside."

---

## Closing

Use this document to introduce Anathema Soft without triggering confusion or skepticism.

Start simple. Add depth only when asked.

The concept is radical. The explanation doesn't have to be.
