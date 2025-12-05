# DGCP™ — Machine Validation Rules (Minimal Set)
Version: 1.0  
License: MMFARM-POL-2025  

This document defines the minimal rules that any DGCP™ Metadata Validator  
must implement. The goal is **technical correctness only**, not judging  
the meaning of the work.

---

## 1. Input

- One DMS metadata object (JSON or YAML)  
- Optionally: raw signature payload if stored separately  

---

## 2. Required Checks

1. **Schema Check**
   - `dms_version` must be `"1.0.0"`  
   - All Machine-Critical fields must be present  
   - No unknown required fields

2. **Type & Format Check**
   - `timestamp_utc` is valid ISO 8601 (UTC)  
   - `ipfs_cid_primary` matches CID pattern  
   - `git_commit_sha256` matches hex pattern  
   - `proof_id` format is UUID or approved pattern

3. **Signature Check**
   - Rebuild canonical hash of metadata (excluding `signature`)  
   - Verify digital signature using `worker_id_public`  
   - Reject if verification fails

4. **Uniqueness Check**
   - `proof_id` not previously used in this repository  
   - (If duplicate → reject and log error)

5. **No Machine Judgement**
   - Validator must **not** score, rank, or classify workers  
   - Validator must **not** infer “honesty” or “quality of work”  

---

## 3. Output States

- `VALID_TECHNICAL` – all checks passed  
- `REJECTED_FORMAT` – structural or format error  
- `REJECTED_SIGNATURE` – cryptographic verification failed  

All results should be logged in an append-only validation log.

---

License: **MMFARM-POL-2025**  
DGCP™ — Data Governance & Continuous Proof™
