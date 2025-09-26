
---

## 🌱 Git Workflow & Branching

We follow a standard **Git branching strategy**:

- **main** → Stable production-ready branch.  
- **dev** → Development branch for integration.  
- **feature/build** → Feature branch for Build stage.  
- **feature/deploy** → Feature branch for Deploy stage.  

### Workflow:
1. Developers create **feature branches** from `dev`.  
2. Changes are pushed → Pull Requests (PRs) are created.  
3. PRs are reviewed & merged into `dev`.  
4. Once stable, `dev` is merged into `main`.  

---

## 🏷️ Git Tags

We use **tags** for versioning:

- `v1.0` → Initial Build pipeline completed.  
- `v2.0` → Deploy stage added.  

```bash
# Create tag
git tag v1.0

# Push tag to remote
git push origin v1.0

