# DGCP™ — Proof Versioning (Short Spec)
Version: 1.0  
License: MMFARM-POL-2025  

This document defines how DGCP™ manages proof versioning while preserving
100% historical integrity in an append-only system.

Versioning extends truth; it never replaces previous proofs.

---

## 1. Core Concept

DGCP does not modify or overwrite proofs.  
Instead, updates use **version chains**:

```
root_proof  →  v2  →  v3  →  v4  → ...
```

Each new version is a new proof with:
- New timestamp  
- New signature  
- Link to the original proof  

---

## 2. When to Create a New Version

A new version is required when:
- Adding more context  
- Adding extra media (new angles, extra proof)  
- Updating tags or non-critical fields  
- Extending information about the same event  

Versioning = extending truth  
Correction = fixing errors (handled separately)

---

## 3. Version Metadata Format

```json
{
  "version_of": "<original_proof_id>",
  "version_number": "v2",
  "reason": "added_additional_context"
}
```

Rules:
- `v1` = original  
- Numbers increase sequentially  
- Must reference original root proof  

---

## 4. Version Chain Rules

- Linear only (no branching)  
- Original proof stays frozen  
- Every version links back to the root  
- Timestamps must always increase  
- All versions remain visible and auditable  

---

## 5. Purpose of Versioning

- Enables multi-step story of the same event  
- Supports richer research and AI training  
- Preserves every state of truth  
- Works naturally with minimal DGCP pipeline (Phone → IPFS → GitHub → SHA256)

---

License: MMFARM-POL-2025  
DGCP™ — Data Governance & Continuous Proof™
