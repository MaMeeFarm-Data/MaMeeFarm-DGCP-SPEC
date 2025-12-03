# DGCP™ — Metadata Standard (DMS) Overview  
Version: 1.0.0  
MMFARM-POL-2025 Licensed

The DGCP Metadata Standard (DMS) defines the minimal, verifiable contract required to record Real-Work Data (RWD) using the smallest possible technology stack:  
**Phone → IPFS → GitHub SHA256 → Minimal DLT Timestamp.**

## Core Purpose
DMS ensures that every proof:
- originates from a human  
- is cryptographically signed  
- is contextually interpretable by humans  
- is structurally verifiable by machines  
- remains immutable once committed  

## DMS Structure
The standard contains four layers:
1. Core & Signature (machine-critical)  
2. Context & Time (hybrid)  
3. Activity & Media (hybrid)  
4. Registry & Audit (machine-critical)

This folder contains:
- **DMS_SPEC.md** (canonical human spec)  
- **dms-v1.0.0.json** (machine schema)  
- **DMS_VERSIONING.md** (future evolution rules)  
- **EXAMPLES/** (sample DMS files)
