# DGCP™ — Trust Model Overview
Version: 1.0  
License: MMFARM-POL-2025  

The DGCP™ Trust Model explains **who** is trusted for **what** at each layer  
of the Real-Work Data pipeline.

Trust is not centralised in one institution.  
It is distributed across four layers:

1. Worker  
2. Local Audit  
3. Federation  
4. Public Anchor

---

## 1. Layer 0 — Worker (Origin of Truth)

- Performs the real work  
- Captures media on phone  
- Writes short human description  
- Signs metadata with `worker_id_public`  

DGCP assumption:  
> The worker is the only entity who knows the full context of the work.

---

## 2. Layer 1 — Local Human Audit

- Small group (co-op, community, NGO)  
- Checks consistency of proofs with local reality  
- May mark proofs as `ACCEPTED_RWD`, `NEEDS_REVIEW`, or `FLAGGED`  

They **do not** edit original proofs.  
They add audit records on top of them.

---

## 3. Layer 2 — Federation Trust

- Regional or sector-level alliances of auditors  
- Share methods, red flags, and cross-region checks  
- Help detect systemic fraud without punishing honest workers  

Federation exists to **share knowledge**, not to control workers.

---

## 4. Layer 3 — Public Anchor

- GitHub commit history + minimal DLT timestamp  
- Anyone (researchers, regulators, buyers) can verify that:
  - a proof existed before a certain time  
  - history has not been edited  

This layer is **trust-minimising**:  
even if organisations fail, the public anchor remains.

---

License: **MMFARM-POL-2025**  
DGCP™ — Data Governance & Continuous Proof™
