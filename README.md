# personal-os

> A second brain for the builder, the learner, and the practitioner — all in one place.

Four pillars. One system. Every piece of information here knows where it came from and where it can go.

---

## Pillars

| Repo | Purpose | Cadence |
|---|---|---|
| [daily-journal](./daily-journal/) | Inner practice — Sadhana, intentions, evening reflection | Daily |
| [daily-learnings](./daily-learnings/) | Published learnings — AI, fintech, leadership | When you learn something worth sharing |
| [domain-notes](./domain-notes/) | Deep knowledge base — MF, Demat, LAS, Insurance, G-Sec | When domain understanding deepens |
| [learning-labs](./learning-labs/) | Course work and experiments — one folder per course | Per course/module |

---

## How the pillars connect

```
daily-journal  ──links──►  daily-learnings  ──domain_ref──►  domain-notes
     │                            │
     └──youtube_idea──►  (future content ideas)
     
learning-labs  ──applies──►  daily-journal (focus_tag: lab)
                      └──►  daily-learnings (publish what you built)
```

Every journal entry has a `links:` block that bridges the four pillars:
- `learning_post` — did you publish something today? link it.
- `domain_ref` — did you deepen a domain note? say which one.
- `youtube_idea` — did you have a content idea? seed it here.

---

## Daily rhythm

| Time | Action | Tool |
|---|---|---|
| Morning | Create today's entry | `daily-journal/scripts/today.sh` |
| Anytime | Publish a learning | create `_posts/YYYY-MM-DD-title.md` in daily-learnings |
| Evening | Reflect + fill links block | same entry file |
| Commit | Push the day | `daily-journal/scripts/commit.sh` |
| Sunday | Weekly synthesis | `daily-journal/scripts/weekly.py` |
| Anytime | Check streak + stats | `python3 daily-journal/scripts/streak.py` |

---

## Repo remotes

Each sub-folder is its own independent git repo. Remotes are configured inside each `.git/config`.

```bash
# Check where each repo pushes to
git -C daily-journal remote -v
git -C daily-learnings remote -v
git -C domain-notes remote -v
git -C learning-labs remote -v
```
