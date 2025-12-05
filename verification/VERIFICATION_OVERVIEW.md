# DGCP™ — Verification Layer Overview (Short Spec)
Version: 1.0  
License: MMFARM-POL-2025  

The DGCP™ Verification Layer checks that every Real-Work Data (RWD) proof  
is technically valid before it enters the Global Proof Registry.

Verification separates into:

- **Machine Validation** – fast, automatic checks on structure & cryptography  
- **Human Audit** – slower, context-aware checks on meaning & truth  

Machines protect **integrity**.  
Humans protect **truth**.

---

## 1. Machine Validation (What software can do)

- Validate JSON/YAML structure against DMS schema  
- Check required Machine-Critical fields are present  
- Validate formats (ISO 8601 timestamps, CID patterns, URLs)  
- Verify digital signature using `worker_id_public`  
- Ensure proof_id is unique within the repository  

Result:  
- `VALID_TECHNICAL` or `REJECTED_FORMAT`

---

## 2. Human Audit (What machines must not decide)

Human auditors review:

- `short_human_description`  
- `work_type`, `tags`, `location_label`  
- Media content via `ipfs_cid_primary`  
- Consistency with worker history, local weather, and context  

Result:  
- `ACCEPTED_RWD`, `NEEDS_REVIEW`, or `FLAGGED`  

Machines are **not** allowed to:

- Score workers  
- Classify honesty  
- Predict fraud via black-box models  

Final authority on truth always belongs to humans.

---

## 3. Minimal Verification Flow

1. Worker submits signed DMS metadata  
2. Machine Validator checks structure & signature  
3. If valid → commit to GitHub  
4. Later → batch SHA256 anchor to minimal DLT  
5. Human Audit groups review proofs and record decisions in a separate index  

---

License: **MMFARM-POL-2025**  
DGCP™ — Data Governance & Continuous Proof™
