# Contributing to ROCEF Base (v1.0)

ROCEF Base is a reference implementation and UI contract. Contributions should
prioritize clarity, stability, and intent over speed.

## Core rules
1. **No backend logic**
   - No APIs, auth, databases, or service integrations

2. **Keep it static**
   - HTML, CSS, and assets only
   - No build systems or compiled frameworks

3. **Respect shell boundaries**
   - Pilot, Admin, and Executive shells must remain distinct

4. **No sensitive information**
   - Treat this repo as public documentation

5. **Prefer small, intentional changes**
   - Each change should have a clear purpose
   - UI changes should include context or screenshots when possible

## Workflow
- Create a feature branch when making non-trivial changes
- Merge into `master` when ready
- GitHub Pages will update automatically after merge
