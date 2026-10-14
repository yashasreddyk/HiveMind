# HiveMind — Git & Release Workflow Instructions

## 1. Repository Details

* **Repository Name**: `HiveMind`
* **Owner / User**: `yashasreddyk`
* **User Email**: `yashasreddyk@gmail.com`
* **Default Branch**: `main`
* **HTTPS Clone / Remote URL**: `https://github.com/yashasreddyk/HiveMind.git`
* **SSH Clone / Remote URL**: `git@github.com:yashasreddyk/HiveMind.git`
* **License**: MIT (Permissive Open Source)

---

## 2. Remote Configuration

If the remote origin is not yet set up on a new clone or environment, configure it with:
```bash
git remote add origin https://github.com/yashasreddyk/HiveMind.git
git branch -M main
```

To verify the remote configuration:
```bash
git remote -v
```

---

## 3. Commit Message Standards

HiveMind strictly follows the **Conventional Commits** specification:

```
<type>(<scope>): <short description in present tense>

[optional body explaining motivation and context]

[optional footer(s) for breaking changes or issue closes]
```

### Allowed Types:
* `feat`: A new feature or user-facing functionality (e.g., `feat(synapse): add entity extraction pipeline`)
* `fix`: A bug fix (e.g., `fix(canvas): prevent message re-render loop on stream end`)
* `docs`: Documentation changes only (e.g., `docs(readme): update quickstart and architecture links`)
* `refactor`: A code change that neither fixes a bug nor adds a feature
* `perf`: A code change that improves performance (e.g., `perf(graph): optimize pgvector cosine distance query`)
* `test`: Adding missing tests or correcting existing tests
* `chore`: Maintenance tasks, dependency updates, build scripts, configs

---

## 4. Git Tagging & Release Scheme

HiveMind uses a **decimal increment tagging scheme** (or SemVer tag with `v` prefix):
* Baseline tag: `v0.01`
* Increments: `v0.02`, `v0.03`, … `v0.10`, `v0.11`, … `v1.00`
* For every release milestone or major feature commit requested by the user with a tag increment:
  1. Inspect existing tags: `git tag -l --sort=-v:refname`
  2. Compute the next `+0.01` decimal increment over the previous git tag.
  3. Create an annotated git tag: `git tag -a vX.XX -m "Release vX.XX: <summary>"`

---

## 5. Pre-Commit Quality Gate Checklist

BEFORE committing or pushing any code to GitHub:
1. **Type Checking**: Run TypeScript validation:
   ```bash
   npm run typecheck # or npx tsc --noEmit
   ```
   Must pass with zero errors.
2. **Linting**: Ensure code complies with ESLint and Prettier rules:
   ```bash
   npm run lint
   ```
3. **Secret Audit**:
   * Verify that **NO `.env`**, `.env.local`, API keys, private keys, database connection strings with passwords, or credentials are staged.
   * Verify that `git status` only lists intended application code and assets.
4. **Build Verification**:
   ```bash
   npm run build
   ```

---

## 6. Commit & Push Instructions

Execute commits and pushes using this standard sequence:

```bash
# 1. Review status and diffs
git status
git diff

# 2. Stage specific intended files (avoid blind git add . if untracked junk exists)
git add <files>

# 3. Commit with conventional message
git commit -m "feat(<scope>): <description>"

# 4. Tag (when cutting a release or requested by user)
git tag -a v0.01 -m "Release v0.01: Initial product specification and agent instructions"

# 5. Push to GitHub main branch with tags
git push origin main --tags
```

---

## 7. Protected Rules & Safety Guardrails

1. **Never Force Push to Main**:
   * Blind `git push -f origin main` is strictly FORBIDDEN.
   * If rebase is required, only use `git push --force-with-lease origin <branch>` on feature branches after verifying.
2. **Never Commit Secrets**:
   * All LLM endpoints, database URLs, and session secrets belong in `.env.local` (which is in `.gitignore`).
   * Provide dummy templates in `.env.example` only.
3. **Keep CoffeeChat and HiveMind Decoupled**:
   * HiveMind lives in `C:\Yashas\Antigravity workspace\HiveMind`.
   * CoffeeChat lives in `C:\Yashas\Antigravity workspace\CoffeeChat`.
   * Never commit CoffeeChat files to HiveMind or vice-versa.
