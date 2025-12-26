# ROCEF Base — Decisions (v1.0)

Purpose: This file records architectural and workflow decisions that are considered
“locked” for ROCEF Base. These decisions define the boundaries of this repository
and prevent accidental scope creep.

---

## D001 — ROCEF Base is a UI contract, not the production system
**Decision:**  
ROCEF Base exists as the canonical UI style guide and shell reference for the ROCEF system.

**Implications:**  
- No backend integration belongs in this repository  
- No authentication, APIs, databases, or AWS services  
- Production functionality lives in a separate repo (e.g., `rocef-app`)

---

## D002 — Three shells are first-class and must remain distinct
**Decision:**  
ROCEF is structured around three primary shells:
- Pilot
- Admin
- Executive

**Implications:**  
- Shells should not be merged “for convenience”  
- Shell-specific layout and styling is intentional  
- Navigation between shells should be explicit

---

## D003 — Static-only implementation
**Decision:**  
ROCEF Base must remain a static site composed of HTML, CSS, and assets.

**Implications:**  
- No build step required  
- Must run locally via file server or GitHub Pages  
- Avoid frameworks or tooling that require compilation

---

## D004 — GitHub Pages is the deployment target
**Decision:**  
ROCEF Base is deployed via GitHub Pages to provide a stable, shareable reference URL.

**Implications:**  
- The Pages site represents the current UI contract  
- Any consumer of ROCEF UI should reference this site

---

## D005 — Stable filenames and public paths
**Decision:**  
Public-facing filenames and asset paths should remain stable.

**Implications:**  
- Avoid renaming files unless there is a strong reason  
- Treat URLs and paths as part of the contract

---

## D006 — No sensitive data
**Decision:**  
This repository is treated as public documentation.

**Implications:**  
- No credentials, tokens, secrets, or customer data  
- No environment-specific configuration

---

## D007 — Small, intentional changes
**Decision:**  
Changes should be incremental and reviewable.

**Implications:**  
- Prefer small commits and PRs  
- Meaningful UI changes should include a short explanation
