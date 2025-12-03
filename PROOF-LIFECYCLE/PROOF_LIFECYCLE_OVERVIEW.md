# DGCP™ — Proof Lifecycle Overview  
Version: 1.0  
MMFARM-POL-2025 Licensed

This document explains how each Real-Work Data (RWD) proof moves through the DGCP pipeline while remaining immutable, human-origin, and globally auditable.

## Minimal Lifecycle
1. **Capture (Phone)**  
   - Worker performs real work.  
   - Takes photo/video.  
   - Writes short human description.  
   - Generates signature.

2. **Store (IPFS)**  
   - Media uploaded → CID v1 created.  
   - Immutable by design (content addressing).

3. **Commit (GitHub SHA256)**  
   - Metadata + CID stored in append-only repo.  
   - Git commit SHA256 becomes permanent history.

4. **Anchor (Minimal DLT Timestamp)**  
   - A single external timestamp (Bitcoin/OTS).  
   - Confirms the commit existed before time X.  
   - Zero IoT, Zero Surveillance, Zero ML scoring.

## Invariants (Unbreakable Rules)
- No edit, no overwrite.  
- No machine interpretation overrides human meaning.  
- No surveillance data.  
- No biometric data.  
- Human Audit > Machine Validation.  

This ensures DGCP preserves Real-Work Truth at planetary scale.
