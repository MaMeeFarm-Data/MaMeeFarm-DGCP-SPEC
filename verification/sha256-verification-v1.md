# DGCP™ SHA-256 Verification Layer  
**Version 1.0**  
Duck Governance & Continuous Proof Protocol  
MaMeeFarm™ — Real-Work Data Integrity System

This specification defines the **SHA-256 cryptographic verification layer** for DGCP™.  
It ensures that every proof, metadata entry, and log file remains tamper-evident,  
platform-independent, and auditable over time.

This is a required layer for DGCP™ Version 1.0.

---

# 1. Purpose of the SHA-256 Layer

DGCP™ uses multiple independent verification layers.  
But IPFS and GitHub alone are not enough, because:

- IPFS prevents file modification  
- GitHub prevents commit rewriting  

However, **neither prevents post-upload editing of proof files** unless hashing is added.

SHA-256 provides:

- independent verification  
- byte-level content freezing  
- cryptographic fingerprinting  
- AI/auditor-friendly integrity checking  

If a file changes → its SHA-256 hash changes → proof invalid.

---

# 2. What Must Be Hashed

The following files **must** have SHA-256 fingerprints:

### **1. Proof files**
proof/proof_0xx.md

### **2. CID metadata**
cid/proof_0xx_cid.json

### **3. Daily logs**
daily/YYYY-MM-DD-daily-log.md

### **4. Operational documents (optional but recommended)**
- DGCP.md  
- DGCP-OPERATIONAL-FLOW.md  
- LEGAL-SPEC.md  

This strengthens audit capability.

---

# 3. Hash Storage Standard

All hashes are stored under:

verification/hashes/

## Example files:

sha256-proofs.txt
sha256-cids.txt
sha256-daily-logs.txt

---

# 4. SHA-256 Entry Format

Each line must follow:

<SHA256_HASH> <RELATIVE_FILE_PATH>

Example:

e3f1c9a12d... proof/proof_018.md
4a7b92dd3e... cid/proof_018_cid.json
18bb3effd2... daily/2025-11-20-daily-log.md

No extra text.  
No markdown.  
Plain machine-readable format.

---

# 5. Hashing Rules

1. Hash only **final version** of the file.  
2. Write hash to the correct `.txt` file.  
3. Always **append** — never delete old entries.  
4. If file changes → treat as *new proof*, not overwrite.  
5. Hash files must be tracked in GitHub.  
6. Auditors must be able to re-hash at any time.

---

# 6. How Verification Works

To verify a proof:

### Step 1 — Recalculate SHA-256 of file  
### Step 2 — Compare with stored hash in `verification/hashes/*.txt`  
### Step 3:

| Result | Meaning |
|--------|---------|
| **Match** | File is 100% original and untampered |
| **Mismatch** | File changed → proof invalid |

---

# 7. Interaction with DGCP Layers

SHA-256 cross-checks:

- **IPFS CID** (matches content)  
- **GitHub commit** (matches history)  
- **Google Sheet metadata** (time and filename)  
- **Blogger** (timeline consistency)  
- **NFT metadata** (OpenSea)  

Even if any layer is compromised, SHA-256 catches manipulation.

---

# 8. Security Model

The SHA-256 layer prevents:

- editing proof files after commit  
- replacing image but keeping same CID  
- backdating metadata  
- tampering or corruption  
- GitHub manipulation  
- silent reuploads  
- AI-generated fake files  

It is the “last line of defense” against data forgery.

---

# 9. Versioning

This is **DGCP™ SHA-256 Verification Layer — Version 1.0**.  
Future enhancements may include:

- PGP-signed hashes  
- multi-node hashing  
- validator signatures  
- zkHash mechanism  

---

**© 2025 MaMeeFarm™ — DGCP™ Protocol**  
Licensed under CC BY-NC 4.0 + MMFARM-POL-2025

