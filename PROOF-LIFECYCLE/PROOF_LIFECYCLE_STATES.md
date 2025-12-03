# DGCP™ — Proof Lifecycle States & Transitions  
Version: 1.0  
License: MMFARM-POL-2025  

This document defines the **official state machine** for every Real-Work Data (RWD) proof inside the DGCP protocol.  
No proof is ever deleted; states only move forward in an append-only way.

---

## 1. Core States

DGCP defines six canonical states:

1. **CAPTURED**
2. **IPFS_STORED**
3. **GITHUB_COMMITTED**
4. **DLT_ANCHORED**
5. **AUDITED**
6. **FLAGGED**

Each proof must follow this order.  
No backward transitions are allowed.

---

### 1.1 CAPTURED

- Human performs real work.  
- Photo / video captured on phone.  
- Short human description written.  
- Local metadata draft exists but not yet published.

**Source of truth:**  
- Phone storage only.

---

### 1.2 IPFS_STORED

- Media uploaded to IPFS.  
- `ipfs_cid_primary` generated (CIDv1).  
- Optional `ipfs_cid_additional` created.

**Invariants:**

- If media changes → CID changes → new proof required.  
- Old CID is never overwritten.

---

### 1.3 GITHUB_COMMITTED

- DMS metadata file created (JSON/YAML).  
- Signed with `worker_id_public` private key.  
- Stored in append-only GitHub repo.  
- `git_commit_sha256` recorded.

**Invariants:**

- No force-push allowed.  
- No history rewrite.  
- Corrections must be new commits, never edits.

---

### 1.4 DLT_ANCHORED

- Daily or batched SHA256 root committed to minimal DLT  
  (e.g., Bitcoin OTS / timestamp service).  
- `ots_timestamp_ref` filled in metadata.

**Guarantee:**

- Proof existed before DLT block time.  
- External, neutral clock added to history.

---

### 1.5 AUDITED

- Human audit group has reviewed the proof.  
- Checks consistency: description, tags, location, season, etc.  
- Marks proof as **valid RWD** in audit index.

**Important:**  
- This is a *social* decision, not a machine decision.  
- Stored in separate audit index, not in the original metadata file.

---

### 1.6 FLAGGED

- Proof is suspected of error, misuse, or fraud.  
- Proof itself is **not deleted**.  
- A separate FLAG record is created and linked by `proof_id`.

Examples:

- Wrong description vs. media.  
- Suspicion of non-human origin.  
- Policy or license violations.

**Append-Only Rule:**  
Flagging = adding more data, never removing history.

---

## 2. Allowed Transitions

The valid state transitions are:

- `CAPTURED → IPFS_STORED`  
- `IPFS_STORED → GITHUB_COMMITTED`  
- `GITHUB_COMMITTED → DLT_ANCHORED`  
- `DLT_ANCHORED → AUDITED`  
- `DLT_ANCHORED → FLAGGED`  
- `AUDITED → FLAGGED` (if later evidence appears)

**Disallowed Transitions:**

- Any backward move (e.g., `GITHUB_COMMITTED → CAPTURED`).  
- Any direct jump skipping core steps.

---

## 3. Why States Matter

The lifecycle state model enables:

- Clear reasoning about where each proof is.  
- Safe scaling to 10,000+ workers.  
- External audit by NGOs, universities, regulators.  
- Strong guarantees without complex infrastructure.

Machines track **state**.  
Humans interpret **truth**.

---

**License: MMFARM-POL-2025**  
DGCP™ — Data Governance & Continuous Proof™
