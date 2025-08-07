# 🧼 How to Write Clean Git Commits (For Humans and Dumbasses Alike)

This guide teaches you how to write **clean**, **helpful**, and **conventional** commit messages that won’t make your future self cry. 👇

---

## 🤔 Why Bother?

Clean commit messages:
- Help others (and you) understand **why** something changed
- Make code reviews easier
- Are ✨ beautiful ✨ in changelogs and history

---

## 🧙‍♂️ The Conventional Commits Format

Write your commit messages like this:

```
<type>(optional-scope): short summary
```

Example:
```
feat(auth): add login with Google
```

### 🔧 Types You Should Use

| Type     | Use this when...                            | Example                                      |
|----------|---------------------------------------------|----------------------------------------------|
| `feat`   | You’re adding a **new feature**             | `feat(cart): add discount code functionality`|
| `fix`    | You’re fixing a **bug**                     | `fix(api): handle 500 error on GET /users`   |
| `docs`   | You're changing **documentation**           | `docs(readme): update setup instructions`    |
| `style`  | Code style change (no logic changes)        | `style(ui): fix indent in header CSS`        |
| `refactor`| Code change that isn't a bug or feature   | `refactor(api): simplify user validation`    |
| `test`   | Adding or fixing **tests**                  | `test(utils): add unit tests for date parser`|
| `chore`  | Boring stuff (build, deps, config)          | `chore(ci): update GitHub Actions node version` |

---

## ✍️ Writing Good Messages

Bad:
```
fix stuff
```

Better:
```
fix(auth): correctly store JWT after login
```

Tips:
- Use **present tense**: `add` not `added`
- Be specific: say *what* and *why*, not just "fix"
- Avoid committing 20 changes in one commit like a maniac

---

## 🔥 Bonus: Commit Like a Boss

### 1. One purpose per commit
> Don’t mix feature + bugfix + formatting = no one will understand what you did

### 2. Use `git add -p`
> Add hunks piece by piece to make logical commits

### 3. Use emoji if you want 😎 (but optional)
```
🎨 style: remove extra spaces
🐛 fix(api): null check user before saving
🚀 feat: deploy button for admin
```

---

## 🧪 Examples

```
feat(blog): add post pagination

fix(blog): correct typo in meta tags

docs(readme): add instructions to run locally

refactor(utils): move date helpers to separate file

test(blog): add tests for post rendering

chore(deps): upgrade to react 18.3.0
```

---

## 🛑 What NOT to Do

- ❌ `commit`
- ❌ `update`
- ❌ `changes`
- ❌ `stuff`
- ❌ `final final v2 actually working now`

---

## 💬 TL;DR Cheat Sheet

```
feat     = new feature
fix      = bug fix
docs     = documentation change
style    = formatting (no logic)
refactor = code cleanup (no behavior change)
test     = add or fix tests
chore    = other (build, config, deps)
```

---

## ✅ Final Tip

If you can’t explain your commit in a sentence, it’s probably too big. Break it up.

---

Made for people who forget how to do things. Like me. And maybe you.

🖤