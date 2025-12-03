# DGCP™ — Proof Error Handling (Short Spec)
Version: 1.0  
License: MMFARM-POL-2025  

This document defines the minimal error-handling rules for Real-Work Data proofs within DGCP™.  
All corrections follow append-only principles: no deletion, no overwriting.

---

## 1. Error Categories

### 1.1 Metadata Errors
Examples: missing fields, wrong formats, invalid CID, invalid signature.

Handling:
- Validator rejects proof  
- Worker submits new proof  
- Original proof remains unchanged  

---

### 1.2 Human Description Errors

```json
{
  "correction_of": "<proof_id>",
  "reason": "description_fix"
}
```

---

### 1.3 Media Errors

```json
{
  "correction_of": "<proof_id>",
  "reason": "wrong_media"
}
```

---

### 1.4 Audit-Flag Errors
Triggered by human auditors, federation reviewers, or community reports.

Handling:
- Mark proof as FLAGGED  
- Add append-only flag record  
- Original proof stays  
- Worker may submit explanation proof  

---

## 2. Minimal Rules

- No overwriting  
- No deletion  
- All corrections create new proofs  
- Every correction must link via "correction_of"  
- Machines validate structure; humans validate truth  

---

License: MMFARM-POL-2025  
DGCP™ — Data Governance & Continuous Proof™
